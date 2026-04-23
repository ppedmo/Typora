# 零、参考文章

[postman接口测试工具详解【全】_postman工具-CSDN博客](https://blog.csdn.net/2301_80864686/article/details/135936366)

# 一、简介--接口测试

API：给程序使用的接口

我们通常说的接口测试（或者API接口测试），其实就是对软件系统消息交互接口的测试--软件系统和其他软件系统交互的那部分

接口测试分类：

#### （1）测试外部接口

是被测系统和外部系统之间的接口（一般只需要<u>正常调</u>用即可）

#### （2）测试内部接口

是被测系统内部各个模块之间的接口

- 内部接口提供给内部系统使用（一般只需要正常调用即可）
- ==内部接口提供给外部系统使用==（测试必须非常全面）

接口测试步骤：

1. 发送请求（api接口文档）
2. 接收响应
3. 断言响应

接口测试，通常是对服务端做的比较多

接口测试工作，主要包括

- 获取接口文档，评审文档，了解接口的实现细节
- 根据接口文档，写出测试用例，
- 等产品发布后，根据测试用例，使用软件工具，直接通过消息接口 对 被测系统 进行消息收发，验证被测系统行为是否正确

# 二、postman

![image-20250717123641541](C:/Users/honor/AppData/Roaming/Typora/typora-user-images/image-20250717123641541.png)

1. 工程目录workspace--项目名
2. 创建集合collection--模块
3. 创建接口请求request

**GET**通常作用于从数据库中读取数据；而**POST**则是将数据提交/更新于数据库中。

## 01请求

**请求方式、请求路径、请求头、请求参数**

==Params：get请求传参==

Authorization：鉴权

Headers：请求头

==Body：post请求传参==

Pre-request Script：请求之前的脚本

Tests：请求之后的脚本

Settings：设置

Cookies：Postman用于自动管理Cookie的功能

## 02响应

**响应码、响应信息、响应头、响应数据（返）**

Body：返回的值

Cookies：响应的Cookie

Headers：响应头

Test Results：断言的结果

## 03调试

Console：控制台，用于调试，位于界面左下角

# 三、使用

## 0.也可以创建新的工作空间

## 1.建项目--collections

![image-20250717102942476](C:/Users/honor/AppData/Roaming/Typora/typora-user-images/image-20250717102942476.png)

Overview：概述，可更改项目名

Authorization：鉴权（可对项目整个鉴权）

Script：脚本--项目请求前后

Variables：变量

Runs：运行

## 2.Add request--创建接口请求

### 请求

**请求四要素：请求方式、请求路径、请求头、请求参数**

**第一种传参方式Params**--会显示在url中

**第二种传参方式Body**--不会显示在url中，相对安全

![image-20250717104519436](C:/Users/honor/AppData/Roaming/Typora/typora-user-images/image-20250717104519436.png)

none：没有参数

from-data：文件上传以及键值对（两种请求，可选）

x-www-form-urlencoded：表单请求（键值对）

raw：JSON、XML、HTML、Text、JavaScript

binary：二进制文件上传

GraphQL：不怎么使用，可忽略
![image-20250717105356019](C:/Users/honor/AppData/Roaming/Typora/typora-user-images/image-20250717105356019.png)

Cookies：请求的Cookie--请求头--Postman用于自动管理Cookie的功能

### 响应

**响应四要素：响应码、响应信息、响应头、响应数据（返）**

![image-20250717105818881](C:/Users/honor/AppData/Roaming/Typora/typora-user-images/image-20250717105818881.png)

200 OK：响应码 响应信息

Body：响应数据

Cookies：响应的Cookie--响应头

Test Results：断言的结果

# 四、实例--在postman中

- {
      "errcode": 0,
      "errmsg": "ok"
  }
- 这是对的

- 添加动态时间戳--*{{$timestamp}}*

# 五、接口关联

### 1.接口关联：在接口中上一个接口的返回值需要作为下一个接口的参数

### 2.如何实现：

- 获取上一个接口返回值中的指定数据

  - 使用json对象取值，保存到全局变量中

  - 使用正则提取，保存在全居变量

- 使用全局变量，通过{{变量名}}引用

全局变量：**Postman 中全局生效**的变量，无论当前选择哪个环境，全局变量都可以被访问和使用，适合存储跨环境通用的数据（如固定的基础 URL、通用 Token 等）。

环境变量：**基于 “环境” 隔离的变量**，需要先创建环境（如 “开发环境”“测试环境”“生产环境”），变量仅在当前选中的环境中生效，适合存储不同环境的差异化数据（如不同环境的接口域名、端口等）。

1. 变量名区分大小写（如 `token` 和 `Token` 是两个不同变量）。
2. 若全局变量与环境变量同名，**环境变量会覆盖全局变量**（优先使用环境变量）。
3. 可通过 Postman 的 “Collection Runner” 或 “Newman”（命令行工具）批量运行时，动态传入变量值。

### 3.json--提取

```javascript
// 从响应数据中提取Json数据
var response = pm.response.json();
console.log("response",response);// 在Console面板查看输出
console.log("access_token",response.access_token);
console.log("expires_in",response.expires_in);
// 保存到全局变量中
pm.globals.set("access_token", response.access_token); // 将access_token字段的值保存到环境变量中
```

- `let` 是 ES6（ES2015）引入的**变量声明关键字**，用于声明块级作用域的变量，类似于 `var`，但有更严格的作用域规则。
- `pm` 是 **Postman 提供的全局对象**，用于访问和操作 Postman 运行时环境，包含请求、响应、变量等功能
- `response`：是通过 pm.response.json() 解析后得到的 完整 JSON 对象，代表整个接口响应的内容（对应上面的整个 JSON 结构）。
- `response.access_token`这个是根据Json格式来的，指要提取的对象access_token
- Json：复杂的层级关系`response.result.orders[0].items[0].access_token`
- 注意要跟获取到的响应（Json）对应上
- 要形成**数据闭环，避免脏数据**

### 4.正则表达式

```javascript
var responseText = pm.response.text(); // 获取响应文本
console.log(responseText);
var match = responseText.match(/"id":(.*?),"name"/);// 匹配
console.log("tag_id",match);
pm.globals.set("tag_id", match[1]);// 保存到全局变量
```

- 正则表达式如何匹配--网上查或者AI

- match到的有两个--match[1]

  ```xiasanjiao
  "tag_id" ⬇(2) [""id":20696,"name"", "20696"]
  0: ""id":20696,"name""
  1: "20696"
  ```

- 在调试JavaScript代码的时候注意避免脏数据，创建出来了记得删一下

# 六、全局变量、环境变量、动态参数

全局变量：在所有的接口里面都可以访问的变量

环境变量：在当前环境里面可以访问的变量

## 1.全局变量

![image-20250718102633286](https://gitee.com/ppedmo/pic-go/raw/master/img/202507181026365.png)

![image-20250718102658584](https://gitee.com/ppedmo/pic-go/raw/master/img/202507181026649.png)

- 【Environments】中的Globals即为全局变量统称

- 按照接口关联中的方法来创建使用

- 使用：{{变量名}}

## 2.环境变量

- 在实际工作中，一套脚本希望能够在开发环境，测试环境，生产环境都能测试。

- 它的作用域比全局变量小，只能在单一环境中使用。
- 多种环境的区别在于：IP或者域名不一样

**使用：**

- 创建--设置环境变量的值
- ![QQ_1752806363699](https://gitee.com/ppedmo/pic-go/raw/master/img/202507181039530.png)

- 要创建不同环境的环境变量--同一个名字，切换环境的时候可以直接变
- 比如：开发环境--ip，测试环境--ip**即所有环境变量名一致**

## 3.动态参数

**系统自带的动态参数**

> 1. {{$timestamp}}     //动态时间戳
> 2. {{$randomInt}}     //动态0-100的整型
> 3. {{$guid}}        //动态的guid字符串





# 七、批量运行（接口测试+性能测试）

![QQ_1752809973419](https://gitee.com/ppedmo/pic-go/raw/master/img/202507181139704.png)

## 1.功能测试--接口自动化

### 手动运行

![QQ_1752808486617](https://gitee.com/ppedmo/pic-go/raw/master/img/202507181137987.png)

![QQ_1752809802418](https://gitee.com/ppedmo/pic-go/raw/master/img/202507181136022.png)

- Iterations：运行多少次
- Delay：延时多久

### 定期运行



### 通过CLI运行

**1.安装PostmanCLI工具--命令安装：**

```shell
powershell.exe -NoProfile -InputFormat None -ExecutionPolicy AllSigned -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://dl-cli.pstmn.io/install/win64.ps1'))"
```

**2.配置PATH路径：**

"C:\Users\honor\AppData\Local\Microsoft\WindowsApps\postman.exe"

**3.通过CLI命令**

```shell
#登录

#运行

```



## 2.性能测试--performance

免费版：受限制

![QQ_1753413242081](https://gitee.com/ppedmo/pic-go/raw/master/img/202507251114813.png)

fixed：固定

Ramp up：逐步增强

Spike：尖刺

Peak：尖峰（峰值稳定一段时间）

批量运行的时候图片附件是有问题的--上传至云端

# 八、postman接口自动化测试结果断言

状态断言和业务断言

常见断言：

- Get anenvironment variable:获取环境变量
- Get a global variable:获取全局变量
- Get a variable:获取变量
- Get a collection variable:获取集合变量
- Set an environment variable:设置环境变量
- Set a globalvariable：设置全局变量
- Set a collection variable：设置集合变量
- Clear an environment variable:清除环境变量
- Clear a globalvariable:清除全局变量
- Clear a collection variable：清除集合变量
- Send a request:发送一个请求
- Status code: Code is 200:断言返回码为2db(常用)
- Response body:Contains string:断言返回数据包含字符串（常用）
- Response body:JSON value check:断言JSON的值(常用)
- Responsebody:lsequal toastring:断言返回数据等于字符串（常用）
- Response headers: Content-Type header check:断言响应头包含Content-Type
- Responsetimeisless than 200ms:断言响应时间少于200Ms(常用）
- Status code:SuccessfulPOSTrequest:断言Post请求成功，即响应码在201-202之间
- Statuscode:Codenamehasstring：断言状态码的名字包括字符串，如OK
- Response body:Convert XML body to aJSON Object:将XML正文转换为JSON对象
- Use Tiny Validator for JSON data：对JSON数据使用微型验证器

例子：

```JS
//断言
//状态断言
pm.test("断言状态码是200", function () {
    pm.response.to.have.status(200);
});
//业务断言
pm.test("断言返回值包含access_token", function () {
    pm.expect(pm.response.text()).to.include("access_token");
});
```

如何精准断言带有动态参数的接口

1. 不能用系统时间戳

2. 请求之前创建自己的时间戳

```JS
//Pre-request
var dn = Date.now();
pm.globals.set("times", dn);
```

3. 把参数改为自定义的参数

```json
{
    "tag": {
        "name": "浙江{{times}}"
    }
}
```



4. 断言不能用双大括号取值

```JS
//Post-request
/*
错误
//业务断言
pm.test("断言标签", function () {
    pm.expect(pm.response.text()).to.include("浙江{{times}}");
});
*/
//业务断言
pm.test("断言标签", function () {
    pm.expect(pm.response.text()).to.include("浙江" +pm.globals.get("times"));
});
```

全局断言--公共断言

把断言放在集合中

# 九、Postman的参数化（CSV、JSON）--数据驱动

**推荐使用：**

![QQ_1753928662956](https://gitee.com/ppedmo/pic-go/raw/master/img/202507311024186.png)

**适用场景**：接口需要测试多个场景用例：正向用例、反向异常用例，可以使用数据驱动的形式实现

设计接口用例：

**单接口测试**

- 正向测试：

  - 必填参数组合--P0

  - 必填+非必填组合
    - 全部参数组合--P1
    - 与单个非必填参数组合--P2/P3

- 反向测试：
  - 功能异常：错误信息、数据库中没有的数据--P1
  - 数据异常：空、类型不符、长度不符--P2
  - 参数异常：多参、少参、空参--P3

**data.csv文件设置**

![QQ_1753776475058](https://gitee.com/ppedmo/pic-go/raw/master/img/202507291607369.png)

**data.json文件设置**

![QQ_1753776540974](https://gitee.com/ppedmo/pic-go/raw/master/img/202507291609183.png)

上面二选一

**接口参数设置：**变量名与文件中的变量名一致，变量值直接调用全局变量（文件中的变量都默认为全局变量）

**缺点：**所有共享一个测试用例

# 十、Postman接口自动化加密接口测试实战

加密使用的网站：[在线JSON校验格式化工具（Be JSON）](https://www.bejson.com/)

## 1.加密方式

单向加密：只能加密，不能解密

- MD5（哈希）、SHA、HMacSHA

双向加密：可以加密，也可以解密

- 对称（相同的密钥）：AES、DES、Base64（没有密钥）
- 不对称（密钥不同、公钥--加密和私钥--解密）：RSA（Postman不支持）

**测试只需要加密不必解密**

## 2.Postman加密实现

测试之前进行加密

```JS
//MD5加密--先加密，再添加为全局变量
var md5_username = CryptoJS.MD5("admin");
var md5_password = CryptoJS.MD5("123");
pm.globals.set("md5_username",md5_username);
pm.globals.set("md5_password",md5_password);
//Base64加密--先加密，再添加为全局变量
var bs_username = btoa("admin");
var bs_password = btoa("123");
pm.globals.set("bs_username",bs_username);
pm.globals.set("bs_password",bs_password);
```





# 十一、Cookie鉴权

**Cookie** 是服务器发送给客户端（浏览器/Postman）的一小段数据，客户端后续请求时自动附带回服务器，用于**身份验证和状态保持**

- ### cookie定义

  存储在客户端的一小段文本信息，格式为键值对的形式

- ### cookie查找

  控制台--Application(应用程序)--Cookie

- ### cookie分类

  （1）会话Cookie
  保存在内存，当浏览器关闭之后会自动删除cookie

  （2）持久Cookie
  保存在磁盘，当浏览器关闭之后不会清除，只有在失效时间到了之后才会清除

  注意：Cookie的值是在服务端设置，在客户端存储，可以设置Cookie的失效时间

- ### Cookie的鉴权原理

  （1）当客户端第一次访问服务器的时候，服务器就会生成Cookie信息，并且通过响应里的Set-Cookie将Cookie值传输给客户端，**客户端**接收并自动存储Cookie值。

  （2）当客户端第二次访问服务器的时候，客户端就会自动读取本地的cookie，然后根据主机IP或者域名添加对应的cookie，从而实现鉴权

- ### Postman实现Cookie鉴权

  Postman**会自动完成cookie鉴权**，无需手动完成。

  获取cookie以后，postman发请求不用自己手动添加cookie，他会自动帮我们填写cookie在请求头上

# 十二、Mock测试

## 1.定义/作用

模拟接口（我要测的接口A依赖他B，但他B还没开发好/调用第三方接口--状态不稳定或需要付费/模拟异常场景）,用 ==Mock== 技术 “模拟” B 接口的返回，让 A 接口的测试能正常进行

- 前后端联调
- 调用第三方接口测试错误场景
- demo演示

Mock不是一个真实的服务，仅是一个被伪装成真实服务的假服务，通过Mock，可以测试我们API并检验结果是否正确。

## 2.如何实现--postman创建

本地搭建

linux服务器搭建

还可以模拟不同协议

## 3.如何实现--代码实现



# 十三、自动化持续集成

**Postman+CLI+Jenkins自动化持续集成**

环境变量-改-集合变量

## 1.环境变量改为集成变量

不用导出全局变量和环境变量

## 2.持续集成

- 安装Jenkins

- 配置Jenkins：

  不使用自定义空间、Build Steps输入命令、不要Allure报告

- 一步到位：

  ```shell
  postman collection run 46570498-ef6f1682-c7a2-4e76-afbb-0c4058d6cb8c -e 46570498-8f11cb5c-1f8a-4c10-bb8f-e384cd54a035
  ```
  


## 3.优点

不用导入数据、非常适合适合敏捷开发中的快速迭代、可配置定时执行
