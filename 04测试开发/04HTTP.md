[HTTP协议 - 白月黑羽](https://www.byhy.net/auto/apitest/01/)

# 一、HTTP简介

- HTTP 协议 全称是 超文本传输协议， 英文是 Hypertext Transfer Protocol 。

- HTTP 协议最大的特点是 通讯双方 分为 `客户端` 和 `服务端` 。
- HTTP 双方的信息交互的方式
  - 客户端 先发送 **http请求（request）**给 服务端
  - 然后服务端 发送 **http响应（response）**给 客户端

- 注意：HTTP协议中，服务端不能主动先发送信息给 客户端

# 二、HTTP请求消息

示例：

```http
GET /mgr/login.html HTTP/1.1
Host: www.baiyueheiyu.com
User-Agent: Mozilla/6.0 (compatible; MSIE5.01; Windows NT)
Accept-Language: zh-cn
Accept-Encoding: gzip, deflate
```

```http
POST /api/medicine HTTP/1.1
Host: www.baiyueheiyu.com
User-Agent: Mozilla/6.0 (compatible; MSIE5.01; Windows NT)
Content-Type: application/x-www-form-urlencoded
Content-Length: 51
Accept-Language: zh-cn
Accept-Encoding: gzip, deflate

name=qingmeisu&sn=099877883837&desc=qingmeisuyaopin
```



## 请求行 request line

- http请求的第一行的内容，表示要操作什么资源，使用的 http协议版本是什么。
- ==请求的方法，操作资源的地址， 协议的版本号==

- `GET /mgr/login.html HTTP/1.1`

### 常见的HTTP 请求方式：

#### 1.GET--获取

- 从服务器**读取数据**（查询、检索）
- Http协议规范没有对**GET请求的URL**长度进行限制，目前说的**get长度有限制**，是特定的浏览器及服务器对它的限制。

####  2.POST--添加

-  创建资源
- 向服务器**提交数据**（新增、复杂操作）
- 参数在请求体中传递（支持JSON/XML）
- 无长度限制

#### 3.PUT--完整更新资源

- **替换**服务器上的整个资源
- 需提供资源全部字段（未传字段可能被置空）

#### 4.DELETE--删除

- 从服务器**删除指定资源**

- **测试要点**：
  - 权限控制（如禁止未授权删除）
  - 级联删除（如关联评论是否同步删除）

#### 5. PATCH - 部分更新资源

- **局部修改**资源（与PUT的区别）
- **测试要点**：
  - 部分字段更新后，其他字段是否保持不变

#### 6. HEAD - 获取资源元数据

- 仅获取响应头（不返回Body）

- **用途**：
  - 检查资源是否存在（状态码200/404）
  - 验证缓存有效性（Last-Modified头）
- 状态码：200表示资源存在，404表示不存在

#### 7. OPTIONS - 查询支持的方法

- 获取服务器支持的HTTP方法
- **用途**：
  - 跨域请求预检（CORS）

#### 8.测试时的核心验证点

1. **状态码**：
   - 成功：GET(200)、POST(201)、PUT(200)、DELETE(204)
   - 错误：400（参数错误）、405（方法不允许）
2. **数据一致性**：
   - POST后检查数据库记录
   - PATCH后验证未传字段是否保留原值
3. **幂等性**：
   - PUT/DELETE多次调用结果应一致
   - POST重复调用可能产生重复数据
4. **安全性**：
   - GET/HEAD不应修改数据
   - 敏感操作（如DELETE）需权限校验

### url

- url表示要获取资源的具体路径

`https://www.baidu.com/s?wd=iphone&rsv_spt=1`

- `https://www.baidu.com/s`：资源路径

- `wd=iphone&rsv_spt=1`：参数--?问号后面

- 两个参数 wd 和 rsv_spt， 他们的值分别为 iphone 和 1 

- 每个参数之间是用 `&` 隔开的。

## 请求头 request headers

- http请求行下面的内容，里面存放一些信息
- 请求发送的服务端域名是什么， 希望接收的响应消息使用什么语言，请求消息体的长度等等。
- 通常请求头 都有好多个，一个请求头 占据一行
- 单个请求头的 格式是： `名字: 值`
- HTTP协议规定了一些标准的请求头，[点击查看MDN的描述](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)

## 消息体 message body

- 请求的url、请求头中可以存放 一些数据信息， 但是有些数据信息，往往需要存放在消息体中。

- 特别是 **POST、PUT**等请求，添加、修改的数据信息通常都是存放在 请求消息体中的。
- 如果 HTTP 请求有消息体，需要在请求头和消息体之间插入一个空行， 隔开它们。

# 三、HTTP响应消息

示例：

```http
HTTP/1.1 200 OK
Date: Thu, 19 Sep 2019 08:08:27 GMT
Server: WSGIServer/0.2 CPython/3.7.3
Content-Type: application/json
Content-Length: 37
X-Frame-Options: SAMEORIGIN
Vary: Cookie

{"ret": 0, "retlist": [], "total": 0}
```

## 状态行 status line

`HTTP/1.1 200 OK`：版本协议 状态码 描述状态的短语

- 协议版本

上面的示例中，就是 `HTTP/1.1`

- 状态码

上面的示例中，就是 `200`

- 描述状态的短语

上面的示例中，就是 `OK`

### 状态码

- 状态码，它表示了 服务端对客户端请求的处理结果 
- 状态码用3位的数字来表示，第一位数字代表处理结果的大体类型
  - 2xx
    - 通常表示请求消息没有问题，而且服务器也正确处理了
    - 最常见的就是 200
  - 3xx
    - 重定向响应
    - 常见的值是 301，302， 表示客户端的这个请求的url地址已经改变了， 需要 客户端 重新发起一个 请求 到另外的一个url
  - 4xx
    - `400 Bad Request` 表示客户端请求不符合接口要求，比如格式完全错误
    - `401 Unauthorized` 表示客户端需要先认证才能发送次请求
    - `403 Forbidden` 表示客户端没有权限要求服务器处理这样的请求， 比如普通用户请求删除别人账号等
    - `404 Not Found` 表示客户端请求的url 不存在
  - 5xx
    - 表示服务端在处理请求中，发生了未知的错误
    - 通常是服务端的代码设计问题，或者是服务端子系统出了故障（比如数据库服务宕机了）

## 响应头 response headers

- 响应头 是响应状态行下面的内容，里面存放一些信息。 作用和格式与请求头类似。

## 消息体 message body

- 响应头和消息体 之间 插入一个空行

# 四、状态码

[HTTP 响应状态码总结_常见的响应状态码-CSDN博客](https://blog.csdn.net/qq_52964132/article/details/147869097?ops_request_misc=&request_id=&biz_id=102&utm_term=常见的http响应状态码&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-147869097.142^v102^pc_search_result_base9&spm=1018.2226.3001.4187)