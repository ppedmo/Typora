# 0.Web概述

**前后端分离模式**

![image-20250313210120851](https://gitee.com/ppedmo/pic-go/raw/master/img/202503132101983.png)

![image-20250317161538194](https://gitee.com/ppedmo/pic-go/raw/master/img/202503171615297.png)

[HTML 系列教程](https://www.w3school.com.cn/h.asp)

[JavaScript 教程](https://www.w3school.com.cn/js/index.asp)

查看

# 1.HTML、CSS

HTML:网页的结构（元素与内容）

CSS:网页的表现（外观，颜色大小）

W3Cschool

## 1.1HTML快速入门

```html
<html>
	<head>
		<title>HTML快速入门</title>
	</head>
	<body>
		<h1>Hello HTML</h1>
		<img src = "1.jpg"/>
	</body>
</html>
```

特点：不区分大小写，属性可以使用该双引号也可以使用单引号，语法不严格

## 1.2 VS Code开发工具

前端程序应用广泛

建议以后安装所有与开发相关的软件，尽量安装在一个没有中文不带空格的目录下

## 1.3 基础标签&样式

**以新浪新闻为例**

### 1.3.1 新浪新闻--实现标题

- 图片标签:<img>

  - src：指定图像url(资源路径)

  - width：宽（px，像素；%相对于父元素的百分比）

  - height：高

  - 绝对路径（磁盘路径和网络路径）

  - 相对路径

    ./:当前目录（可省略）， ../上级目录

- 标题标签:<h1>-<h6>
- 水平标签：<hr>

- css控制字体样式：

  ![image-20250317183134563](https://gitee.com/ppedmo/pic-go/raw/master/img/202503171831635.png)

  - 行内样式
  - 内嵌样式
  - 外联样式

- CSS选择器：

  ![image-20250317190019015](https://gitee.com/ppedmo/pic-go/raw/master/img/202503171900057.png)

  - 元素选择器：在head中写的，h1 span之类的东西
  - 类选择器：根据标签中class的名字注意是：.cls(点+名字)
  - id选择器：不可以重复的标签中id="time" #time
  - 优先级：id选择器>类选择器>元素选择器

- ==超链接==
  - 标签: <a href="..." target="...">央视网
  -  href: 指定资源访问的url
     target: 指定在何处打开资源链接
    _self: 默认值，在当前页面打开
    _blank: 在空白页面打开

- CSS属性
  - text-decoration: none;/*设置文本为标准文本*/

### 1.3.2 新浪新闻--实现正文

- 视频标签：<video>
  - src: 规定视频的url
  - controls: 显示播放控件
  - width: 播放器的宽度
  - height: 播放器的高度

- 音频标签:  <audio>
  - src: 规定音频的url 
  - controls: 显示播放控件

- 段落标签: <p>

- 加粗标签：<b>或者<strong>

- ```html
  text-indent: 35px;/*首行缩进*/
  
  line-height: 28px;/*设置段落行高*/
  
  text-align: right;/*设置水平对齐方式*/
  ```

- 在html中无论你打多少个空格，都会合并成一个空格，如果要的话可以使用空格占位符:&nbsp

- 要实现页面布局--==盒子模型==

  ![image-20250317203552877](https://gitee.com/ppedmo/pic-go/raw/master/img/202503172035955.png)

  - 都是没有语义的布局标签
  - div标签：一行只显示一个（独占）；宽度默认是父元素的宽度，高度由内容撑开；可设置宽高
  - span标签：一行可显示多个；宽度和高度默认由内容撑开；不可以设置宽高

## 1.4 表格、表单标签

### 1.4.1表格标签

![image-20250317223901954](https://gitee.com/ppedmo/pic-go/raw/master/img/202503172239017.png)

- table：定义整个表
- tr：表格的行，可以包裹多个
- tb：表格单元格(普通)，可以包裹内容，如果为表头的话可用 th 替换
- 各部件间用空格隔开，不用“ ， ”逗号
- ```html
  <table border="1px" cellspacing="0"  width="600px">
          <tr>
              <th>序号</th>
              <th>品牌Logo</th>
              <th>品牌名称</th>
              <th>企业名称</th>
          </tr>
          <tr>
              <td></td>
              <td></td>
              <td></td>
              <td></td>
          </tr>
          <tr>
              <td></td>
              <td></td>
              <td></td>
              <td></td>
          </tr>
      </table>
  ```

  cellspacing="1"是这种情况

  ![image-20250319164901995](https://gitee.com/ppedmo/pic-go/raw/master/img/202503191649138.png)

### 1.4.2表单标签

如注册登录等**数据采集**

- **form**

  - 表单项：input 、下来列表、文本域
    - input :  定义表单项，通过type属性控制输入形式
    - select :  定义下拉列表
    - textarea :  定义文本域
  - 属性：
    - action：规定表单提交时向何处发送数据，URL，不写默认提交到当前页面
    - method：表单提交方式（GET、POST）

  - ```html
    <!--
    默认是在提交到当前页面
    表单项中必须要有name
    get方式提交，在url后面拼接表单数据，如：?username=Tom&age=23
    get是默认提交方式，url长度有限，不能提交大量表单数据
    -->
    <form action="" method="get">
            用户名：<input type="text" name="username">
            年龄：<input type="text" name="age">
            <input type="submit" value="提交">
    </form>
    
    <!--
    post方式提交，f12网络请求栏payload(负载中可查看数据)可看到
    view sorce（查看源）：可看到原始数据也是这样的username=Tom&age=23
    在消息体（请求体）中传递的，参数大小无限制
    -->
    <form action="" method="post">
            用户名：<input type="text" name="username">
            年龄：<input type="text" name="age">
            <input type="submit" value="提交">
    </form>
    ```

    ![image-20250319171251084](https://gitee.com/ppedmo/pic-go/raw/master/img/202503191712226.png)

    ![image-20250319171338207](https://gitee.com/ppedmo/pic-go/raw/master/img/202503191713344.png)

### 1.4.3表单项标签

- input：表单项，通过type属性控制输入形式

  - `<br><br>`换行

  - `label`包含在label中的点到文字也可以选中

  - | type取值                 | **描述**                             |
    | ------------------------ | ------------------------------------ |
    | text                     | 默认值，定义单行的输入字段           |
    | password                 | 定义密码字段                         |
    | radio                    | 定义单选按钮                         |
    | checkbox                 | 定义复选框                           |
    | file                     | 定义文件上传按钮                     |
    | date/time/datetime-local | 定义日期/时间/日期时间               |
    | number                   | 定义数字输入框                       |
    | email                    | 定义邮件输入框                       |
    | hidden                   | 定义隐藏域                           |
    | submit / reset / button  | 定义提交按钮 / 重置按钮 / 可点击按钮 |

- select：下拉列表，option定义列表项

  - ```html
    学历: <select name="degree">
                   <option value="">----------- 请选择 -----------</option>
                   <option value="1">大专</option>
                   <option value="2">本科</option>
                   <option value="3">硕士</option>
                   <option value="4">博士</option>
          </select>  <br><br>
    ```

- textarea：文本域

# 2. JavaScript

## 2.1介绍

JavaScript（简称：JS），是一门跨平台、面向对象的脚本语言（脚本语言：不需要编译，直接由浏览器的解释就可以运行了）。是用来控制网页行为的，使网页能交互。

## 2.2 JS引入方式

- 内部脚本：一般把<script></script>放在body元素的底部，其实放在哪都可以的

- 外部脚本：JS文件中，通过script标签及src属性

- ```html
  <!-- 内部脚本 -->
  <script>
      alert("Hello JS!");
  </script>
  <!-- 外部脚本 -->
  <script src="./js/demo.js"></script>
  ```

  

## 2.3 JS基础语法

- 书写语法

  - 基础语法和java类似
  - 区分大小写，结尾的分号可以不写
  - 单引号和双引号都可以
  - 注释`  // 或者 /**/  `
  - {}表示代码块的作用范围

- 输出语句

  - `alert(“Hello JS！”)`弹出警告框

  - `write()`写入HTML，在浏览器中展示

  - log()写入浏览器控制台

  - ```js
    window.alert("Hello JS!");
    document.write("Hello JS!");
    console.log("Hello JS!");
    ```

- 变量

  - 用**var**关键字声明变量

    - 作用域大，是一个全局变量
    - 可以重复声明

  - JavaScript 是一门弱类型语言，==变量可以存放不同类型的值== 。

  - 变量名需要遵循如下规则：

    - 组成字符可以是任何字母、数字、下划线（_）或美元符号（$）
    - 数字不能开头
    - 建议使用驼峰命名

  - | 关键字 | 解释                                                         |
    | ------ | ------------------------------------------------------------ |
    | var    | 早期ECMAScript5中用于变量声明的关键字                        |
    | let    | ECMAScript6中新增的用于变量声明的关键字，相比较var，let只在代码块内生效，不可以重复声明 |
    | const  | 声明常量的，常量一旦声明，不能修改                           |

- 数据类型

  - 原始类型和引用类型-对象

  - `typeof`可直接获取数据类型 ，如：`typeof 3 -->number`

  - | 数据类型  | 描述                                               |
    | --------- | -------------------------------------------------- |
    | number    | 数字（整数、小数、NaN(Not a Number)）              |
    | string    | 字符串，单双引皆可                                 |
    | boolean   | 布尔。true，false                                  |
    | null      | 对象为空                                           |
    | undefined | 当声明的变量未初始化时，该变量的默认值是 undefined |

- 运算符

  - ==：只比较值（先进行类型转换：类型不一样会先转换为同一类型）
  
  - ===：比较类型和值
  
  - ```javascript
     var age = 20;
     var _age = "20";
     var $age = 20;
      
     alert(age == _age);//true ，只比较值
     alert(age === _age);//false ，类型不一样
     alert(age === $age);//true ，类型一样，值一样
    ```
  
  - 类型转换
  
    - js中可以通过`parseInt()`函数来进行将其他类型转换成数值类型
  
    - ```javascript
      // 类型转换 - 其他类型转为数字
      alert(parseInt("12")); //12
      alert(parseInt("12A45")); //12
      alert(parseInt("A45"));//NaN (not a number)
      ```
  
    - js中，0,null,undefined,"",NaN理解成false,反之理解成true

## 2.4 JS函数

- 用来执行特定任务的代码块

- 通过关键字function来定义

- 注意：

  - 形式参数不需要声明类型，并且JavaScript中不管什么类型都是let或者var去声明，加上也没有意义。
  - 返回值也不需要声明类型，直接return即可

- ```javascript
  //定义函数-1
  // function add(a,b){
  //    return  a + b;
  // }
  
  //定义函数-2
  //用var关键字来定义一个变量
  var add = function(a,b){
      return  a + b;
  }
  
  
  //函数调用
  //可以传递任意各参数，但是接受只会接受前两个
  var result = add(10,20);
  alert(result);
  ```

  

## 2.5 JS对象

### Array数组

> 

- 定义

- ```js
  //方式1：
  var 变量名 = new Array(元素列表); 
  var arr = new Array(1,2,3,4); //1,2,3,4 是存储在数组中的数据（元素）
  
  //方式2：
  var 变量名 = [ 元素列表 ]; 
  var arr = [1,2,3,4]; //1,2,3,4 是存储在数组中的数据（元素）
  ```

- 特点：JavaScript中数组相当于java中的集合，数组的长度是可以变化的。而且JavaScript是弱数据类型的语言，所以数组中可以存储任意数据类型的值。

  - ```JS
    //特点: 长度可变 类型可变
    var arr = [1,2,3,4];
    arr[10] = 50;
    
    // console.log(arr[10]);
    // console.log(arr[9]);
    // console.log(arr[8]);
    
    arr[9] = "A";
    arr[8] = true;
    
    console.log(arr);
    ```

    


### String字符串

### JSON

### BOM浏览器对象模型

### DOM文档对象模型

## 2.6 JS事件监听