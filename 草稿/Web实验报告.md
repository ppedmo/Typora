**实验目标**

- 以最小可运行骨架搭建个人博客站点的前后端，验证页面路由、主题切换、留言模块（提交/分页/实时滚动）、基础 SEO 与跨端通信
- 评估 Express + React + Ant Design + Vite 的组合在开发体验、性能与可维护性方面的可行性

**实验内容**

- 项目结构梳理与代码走读，定位关键模块与数据流
- 前后端本地启动与端口代理联调，验证接口与跨源访问
- 留言列表分页获取与表单提交，验证校验、限流、持久化
- 实时消息：跑马灯展示，验证事件广播与 UI 更新
- 路由导航与滚动行为、主题切换持久化
- 站点文件与健康检查接口验证：`/robots.txt`、`/sitemap.xml`、`/api/health`

**实验工具和开发平台**
- 开发平台：Windows 10， VS Code
- 后端：Node.js
- 前端：React 18、Vite 5、Ant Design 5、React Router 6
- 浏览器：Edge
- 包管理：`npm`
- 本地运行命令：
  - 前端：`cd frontend && npm install && npm run dev`（默认端口 `5173`）
  - 后端：`cd backend && npm install && npm run start`（默认端口 `3000`）

**系统需求**
- 环境与端口：Node.js v18+；前端 `5173`，后端 `3000`
- 文件系统权限：后端需要写入 `backend/data/messages.json`
- 网络：前端开发服务器到后端的本机访问与代理能力
- 磁盘与内存：本项目数据量小，常规开发机即可

**系统架构**
- 前端（SPA）
  - 技术：React + Ant Design + Vite
  - 路由：`/`、`/about`、`/projects`、`/blog`、`/contact`
  - 主题：亮/暗模式，`localStorage` 持久化
  - 代理：将 `/api` 代理到 `http://localhost:3000`
- 后端（API + SSE）
  - 技术：Express + CORS
  - 数据持久化：JSON 文件
  - 限流与输入清洗：IP 限流与脚本标签移除

**核心模块/关键问题和解决方法**
- 输入校验与安全
  - 问题：防止 XSS 与无效输入
  - 方案：后端清洗 `<script>` 标签与长度裁剪 500 字
- 提交限流
  - 问题：频繁提交导致刷屏或资源消耗
  - 方案：基于 IP 的 30 秒限流
- 分页与全量获取
  - 问题：列表展示与性能平衡
  - 方案：分页接口与可选全量模式，页大小限制 1000
- 前端跨源联调
  - 问题：开发环境跨端访问
  - 方案：Vite 代理 `/api` 指向后端；后端启用 CORS
- 数据持久化与上限
  - 问题：文件持久化易膨胀
  - 方案：只保留最近 1000 条

**重要代码**
- 后端
  - 文件初始化与读写：`backend/server.js`
  
    ```js
    function ensureDataFile() {
      const dir = path.dirname(DATA_FILE)
      if (!fs.existsSync(dir)) fs.mkdirSync(dir, { recursive: true })
      if (!fs.existsSync(DATA_FILE)) fs.writeFileSync(DATA_FILE, '[]', 'utf-8')
    }
    
    function readMessages() {
      ensureDataFile()
      try {
        const raw = fs.readFileSync(DATA_FILE, 'utf-8')
        const arr = JSON.parse(raw)
        if (!Array.isArray(arr)) return []
        return arr
          .map((it) => (typeof it === 'string' ? it : (it && typeof it === 'object' ? (it.content || '') : '')))
          .map((s) => (typeof s === 'string' ? s : ''))
          .map((s) => s.trim())
          .filter((s) => s.length > 0)
      } catch {
        return []
      }
    }
    
    function writeMessages(list) {
      fs.writeFileSync(DATA_FILE, JSON.stringify(list, null, 2), 'utf-8')
    }
    ```
  
  - 留言获取（分页/全量）：`backend/server.js`
  
    ```js
    app.get('/api/messages', (req, res) => {
      const list = readMessages().slice().reverse()
      const allParam = String(req.query.all || '').toLowerCase()
      const isAll = allParam === '1' || allParam === 'true' || allParam === 'yes'
      if (isAll) {
        const data = list
        return res.json({ page: 1, pageSize: data.length, total: list.length, data })
      }
      const page = Math.max(1, parseInt(req.query.page || '1', 10) || 1)
      const rawPageSize = parseInt(req.query.pageSize || '20', 10) || 20
      const pageSize = Math.max(1, Math.min(1000, rawPageSize))
      const start = (page - 1) * pageSize
      const data = list.slice(start, start + pageSize)
      res.json({ page, pageSize, total: list.length, data })
    })
    ```
  
    
  
- 前端服务层
  - API 基址与获取留言：`frontend/src/services/messages.js`
  
    ```js
    const DEV_BASE = typeof window !== 'undefined' && window.location.port === '5173' ? 'http://localhost:3000' : ''
    const api = (path) => `${DEV_BASE}${path}`
    
    export async function getMessages({ page = 1, pageSize = 20, all = false } = {}) {
      const qs = all ? 'all=1' : `page=${page}&pageSize=${pageSize}`
      const res = await fetch(api(`/api/messages?${qs}`))
      if (!res.ok) throw new Error('获取留言失败')
      return res.json()
    }
    ```
  
  - 提交留言与错误信息提取：`frontend/src/services/messages.js`
  
    ```js
    export async function postMessage(payload) {
      const body = { content: (payload?.content || '').trim() }
      const res = await fetch(api('/api/messages'), {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(body)
      })
      if (!res.ok) {
        // 尝试拿到更具体的错误信息
        let text = ''
        try {
          const data = await res.json()
          text = data?.message || ''
        } catch {
          try {
            text = await res.text()
          } catch {}
        }
        throw new Error(text || '提交留言失败')
      }
      return res.json()
    }
    ```
  
    
  
- 前端组件与页面
  - 分页列表展示：`frontend/src/components/MessageList.jsx`
  
    ```js
    useEffect(() => {
        ;(async () => {
          try {
            const res = await getMessages({ page, pageSize })
            setData(res.data || [])
            setTotal(res.total || 0)
          } catch {}
        })()
      }, [page])
    ```
  
    ```js
    <Card className="card">
          <List
            itemLayout="horizontal"
            dataSource={data}
            pagination={{ current: page, pageSize, total, onChange: setPage }}
            renderItem={(it) => (
              <List.Item>
                <List.Item.Meta description={typeof it === 'string' ? it : it?.content} />
              </List.Item>
            )}
          />
        </Card>
    ```
  
    
  
  - 跑马灯（实时消息 + 上滚动画）：`frontend/src/components/MessageTicker.jsx`
  
    ```js
    <Card className="card">
          <div className="ticker" ref={stopRef} style={{ overflow: 'hidden', height: 120 }}>
            <div
              className="track"
              style={{
                display: 'flex',
                flexDirection: 'column',
                gap: 12,
                animation: `scrollUp ${durationSec}s linear infinite`,
              }}
            >
              {items.map((it, idx) => (
                <div key={idx} style={{ whiteSpace: 'nowrap', textOverflow: 'ellipsis', overflow: 'hidden' }}>
                  <span>{typeof it === 'string' ? it : it?.content}</span>
                </div>
              ))}
            </div>
          </div>
          <style>
            {`
            @keyframes scrollUp {
              0% { transform: translateY(0); }
              100% { transform: translateY(-100%); }
            }
            `}
          </style>
        </Card>
    ```
  
    ```js
    useEffect(() => {
        let unsub = () => {}
        ;(async () => {
          try {
            const res = await getMessages({ all: true })
            setItems(res.data || [])
          } catch {}
          unsub = subscribeMessages((msg) => {
            setItems((prev) => [msg, ...prev].slice(0, 50))
          })
        })()
        return () => unsub()
      }, [])
    ```
  
    
  
  - 联系页组合布局：`frontend/src/pages/Contact.jsx`
  
    ```js
    <SectionTitle>联系我</SectionTitle>
    <ContactList />
    <SectionTitle>留言</SectionTitle>
    <Row gutter={[16, 16]}>
      <Col xs={24} md={12}><MessageForm /></Col>
      <Col xs={24} md={12}><MessageList /></Col>
    </Row>
    ```
  
    
  
  - 全局路由与主题切换：`frontend/src/App.jsx`
  
    ```js
    export default function App() {
      const [mode, setMode] = useState(() => localStorage.getItem('theme') || 'light')
      useEffect(() => {
        localStorage.setItem('theme', mode)
        document.documentElement.setAttribute('data-theme', mode)
      }, [mode])
      const algorithm = useMemo(() => (mode === 'dark' ? theme.darkAlgorithm : theme.defaultAlgorithm), [mode])
      return (
        <ConfigProvider theme={{ algorithm, token: { fontSize: 16 } }}>
          <BrowserRouter>
            <Layout style={{ minHeight: '100vh' }}>
              <Header style={{ position: 'sticky', top: 0, zIndex: 100, width: '100%' }}>
                <div style={{ display: 'flex', alignItems: 'center', justifyContent: 'space-between' }}>
                  <Link to="/" aria-label="主页">
                    <Avatar size={40} src={AVATAR_URL} alt="****" icon={<UserOutlined />} style={{ backgroundColor: '#1677ff' }} />
                  </Link>
                  <div style={{ display: 'flex', gap: 12, alignItems: 'center' }}>
                    <NavBar />
                    <ThemeToggle mode={mode} onChange={setMode} />
                  </div>
                </div>
              </Header>
              <Content style={{ padding: '24px', maxWidth: 1200, margin: '0 auto', width: '100%' }}>
                <ScrollToTop />
                <Routes>
                  <Route path="/" element={<Home />} />
                  <Route path="/about" element={<About />} />
                  <Route path="/projects" element={<Projects />} />
                  <Route path="/blog" element={<Blog />} />
                  <Route path="/contact" element={<Contact />} />
                </Routes>
              </Content>
              <FooterBar />
            </Layout>
          </BrowserRouter>
        </ConfigProvider>
      )
    }
    ```
  
    

**实验总结**
- 此次实验我把前后端完整串起来，真正理解了从页面到接口、再到数据持久化的闭环
- 最有成就感的是留言模块：提交、分页和 SSE 实时推送跑通后，看到页面自己“动起来”的那一刻很开心
- 同时我也意识到 JSON 文件持久化的局限，未来应该接数据库、做索引和审计日志
- 整体来说，这次实践让我从“写页面/写接口”走向“设计系统”，也更明确了我所欠缺的能力，以便后续能补足自己的实践能力