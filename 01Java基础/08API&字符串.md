### 1.API

学会如何使用

### 2.String类

- tring 类代表字符串，Java 程序中的所有字符串文字（例如“abc”）都被实现为此类的实例。也就是说，Java 程序中所有的双引号字符串，都是 String 类的对象。String 类在 java.lang 包下，所以使用的时候不需要导包！
- 直接赋值出来的字符串，在字符串常量池中，若有则复用
- 特点
  - 字符串不可变，它们的值在创建后不能被更改
  - 虽然 String 的值是不可变的，但是它们可以被共享
  - 字符串效果上相当于字符数组( char[] )，但是底层原理是字节数组( byte[] 

- **string类的构造方法**

  - 后两种方式也要会，之后蛮常用的

  - 常用的构造方法

    | 方法名                      | 说明                                      |
    | --------------------------- | ----------------------------------------- |
    | public   String()           | 创建一个空白字符串对象，不含有任何内容    |
    | public   String(char[] chs) | 根据字符数组的内容，来创建字符串对象      |
    | public   String(byte[] bys) | 根据字节数组的内容，来创建字符串对象      |
    | String s =   “abc”;         | 直接赋值的方式创建字符串对象，内容就是abc |

  - 示例代码

    ```java
    public class StringDemo01 {
        public static void main(String[] args) {
            //public String()：创建一个空白字符串对象，不含有任何内容
            String s1 = new String();
            System.out.println("s1:" + s1);
    
            //public String(char[] chs)：根据字符数组的内容，来创建字符串对象
            char[] chs = {'a', 'b', 'c'};
            String s2 = new String(chs);
            System.out.println("s2:" + s2);
    
            //public String(byte[] bys)：根据字节数组的内容，来创建字符串对象
            byte[] bys = {97, 98, 99};
            String s3 = new String(bys);
            System.out.println("s3:" + s3);
    
            //String s = “abc”;	直接赋值的方式创建字符串对象，内容就是abc
            String s4 = "abc";
            System.out.println("s4:" + s4);
        }
    }
    ```

- 两种创建方式：

  - 通过构造方法创建

    ​	通过 new 创建的字符串对象，每一次 new 都会申请一个内存空间，虽然内容相同，但是地址值不同

    ​	即new出来的都是不同的，即使内容一样，但仍占有内存空间

  - 直接赋值方式创建

    ​	以“”方式给出的字符串，只要字符序列相同(顺序和大小写)，无论在程序代码中出现几次，JVM 都只会建立一个 String 对象，并在字符串池中维护

- 字符串的比较
  - ==号的作用
    - 基本数据类型：比较的是具体的值
    - 引用数据类型：比较的是对象地址值
  - equals比较区分大小写
  - 

- 遍历字符串

  - cahrAt(i)----索引

  - ```java
    //2.遍历
            for (int i = 0; i < str.length(); i++) {
                //i 依次表示字符串的每一个索引
                //索引的范围：0 ~  长度-1
    
                //根据索引获取字符串里面的每一个字符
                //ctrl + alt + V 自动生成左边的接受变量
                char c = str.charAt(i);
                System.out.println(c);
            }
    ```

- 拼接字符串

- **空字符串“”和null**

  空串是指没有长度，但是有内存的空间

  null则是空引用，没有内存

- substring()
  - ![image-20241029184951702](https://gitee.com/ppedmo/pic-go/raw/master/img/202410291849807.png)

- ![image-20241029185724004](https://gitee.com/ppedmo/pic-go/raw/master/img/202410291857044.png)
- replace:
  - replace("vsdf","***")

### 3.StringBuilder

- StringBuilder 可以看成是一个容器，创建之后里面的内容是**可变**的。

  ![image-20241029190806844](https://gitee.com/ppedmo/pic-go/raw/master/img/202410291908904.png)

  ![image-20241029192406304](https://gitee.com/ppedmo/pic-go/raw/master/img/202410291924348.png)

- 链式编程：依赖前一个函数的结果

### 4. StringJoiner

* StringJoiner跟StringBuilder一样，也可以看成是一个容器，创建之后里面的内容是可变的。
* 作用：提高字符串的操作效率，而且代码编写特别简洁，但是目前市场上很少有人用。 
* JDK8出现的

基本使用：![image-20241029193258600](https://gitee.com/ppedmo/pic-go/raw/master/img/202410291932673.png)

![image-20241029193335135](https://gitee.com/ppedmo/pic-go/raw/master/img/202410291933193.png)

### 5.底层原理

- 有变量参与---new出来的东西

![image-20241029194718449](https://gitee.com/ppedmo/pic-go/raw/master/img/202410291947516.png)

![image-20241029194855533](https://gitee.com/ppedmo/pic-go/raw/master/img/202410291948586.png)

![image-20241029195044012](https://gitee.com/ppedmo/pic-go/raw/master/img/202410291950062.png)

![image-20241029195000394](https://gitee.com/ppedmo/pic-go/raw/master/img/202410291950450.png)

### 6.关于字符串的小扩展：

1. 字符串存储的内存原理

   String s = “abc”；直接赋值

   特点：

   ​	此时字符串abc是存在字符串常量池中的。

   ​	先检查字符串常量池中有没有字符串abc，如果有，不会创建新的，而是直接复用。如果没有abc，才会创建一个新的。

   所以，直接赋值的方式，代码简单，而且节约内存。

2. new出来的字符串

   看到new关键字，一定是在堆里面开辟了一个小空间。

   String s1 = new String（“abc”）；

   String s2 = “abc”；

   s1记录的是new出来的，在堆里面的地址值。

   s2是直接赋值的，所以记录的是字符串常量池中的地址值。

3. ==号比较的到底是什么？

   如果比较的是基本数据类型：比的是具体的数值是否相等。

   如果比较的是引用数据类型：比的是地址值是否相等。

   结论：==只能用于比较基本数据类型。不能比较引用数据类型。