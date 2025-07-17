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