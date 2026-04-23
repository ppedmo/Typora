

https://www.runoob.com/java

https://www.w3school.com.cn/java

java复习

## java基础

> javac Hello.java
>
> java Hello
>
> Java 编译器在编译`.java`文件时，会为每个类生成一个独立的`.class`字节码文件

### 注释

单一功能：

```java
/**
 * 计算两个整数的和
 *
 * @param a 第一个加数，必须为整数
 * @param b 第二个加数，必须为整数
 * @return 两个整数的和，类型为int
 * @throws IllegalArgumentException 当输入参数为null时抛出
 */
public int add(int a, int b) {
    return a + b;
}


```

复杂流程：

```java
/**
 * 处理用户开户业务流程
 * 功能：引导用户输入开户信息（姓名、性别、密码等），生成唯一卡号，
 * 并将新账户信息保存到系统中
 */
```



### **异常处理：**

- 如果不捕捉异常，程序在遇到除以零的情况时会直接终止运行，抛出异常并显示错误信息。这会导致程序无法继续执行后续的逻辑，用户体验会非常差。通过捕捉异常，可以**避免程序直接崩溃**，从而让程序有机会处理错误情况。

- 可以避免程序崩溃，提供友好的错误提示，记录日志，提供备用逻辑，并遵循良好的编程实践

### **方法重载和方法重写：**

- **“方法重载”**是指在一个类中，允许有多个同名方法，但这些方法的参数类型、参数个数或者参数顺序不同。

- **“方法重写”**是指在子类中重新定义父类中的方法。

### **抽象类、抽象方法、接口：**

- **抽象类**：适合定义具有共同属性和行为的类，提供部分实现。
- **抽象方法**：定义在抽象类中的没有具体实现的方法，子类必须实现。--有抽象方法的类一定是抽象类
- **接口**：适合定义一组行为规范，一个类可以实现多个接口，提供更高的灵活性。--单继承，接口多实现

### 一些**源文件的规则**：

- 一个源文件中只能有一个 public 类

- 一个源文件可以有多个非 public 类

- 源文件的名称应该和 public 类的类名保持一致

- package 语句应该在源文件的首行

### **基本类**：

```
基本类型：char 二进制位数：16
包装类：java.lang.Character
最小值：Character.MIN_VALUE=0
最大值：Character.MAX_VALUE=65535
char 的默认值是 \u0000（空字符）
引用类型（类、接口、数组）的默认值是 `null`
```

- 如果不明确初始化，实例变量会被赋予**默认值**（数值类型为0，boolean类型为false，对象引用类型为null）

### **注意**

- 请记住，Java 中的 String 是对象（不是原始类型）

### **重写**

- ```java
  @Override
  public int hashCode() {
      return name.hashCode() + age;
  }
  ```

- 在Java中，所有类都默认继承自Object类，而Object类中定义了hashCode()方法。如果你的类没有显式地继承其他类，那么它会隐式地继承Object类。

### **命名**：

```java
public class MyClass {
    // 类的成员和方法
    private int myVariable;
    public static final int MAX_SIZE = 100;//蛇形下划线连接
    public void myMethod(int myParameter) {
    // 方法体
        int myLocalVariable;
}
}
```

### 概念区分--成员变量、静态变量、静态方法

- 成员变量（实例变量）：对象的

- 静态变量（类变量）：属于类的，通过类名访问，也可以通过对象名访问。（**static**--局部变量不能被声明为 static 变量）

- 静态方法：也是属于类的，通过类名访问，也可以通过对象名访问，只能使用静态变量，不能使用实例变量

### **参数变量**

> - 值传递：传递的是实际参数的值的副本
> - 引用传递：传递的是地址

总结--**值传递**：==Java 中所有参数传递都是值传递。==

> - 效果不同：
>   - 基本数据类型：传递的是变量的值，方法中对参数的修改不会影响原始变量。
>   - 引用数据类型：传递的是对象引用的值（即内存地址），方法中对对象的修改会直接影响原始对象。

## 关键字

### **访问修饰符**

- **default** (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
- **private** : 在同一类内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**
- **protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。
  - 若子类与基类不在同一包中，那么在子类中，子类实例可以访问其从基类继承而来的protected方法，而不能访问基类实例的protected方法
- **public** : 对所有类可见。使用对象：类、接口、变量、方法

- 继承中访问权限不能变小。

### **final**

- final变量--变量一旦赋值后，不能被重新赋值。被 final 修饰的实例变量必须显式指定初始值--定义的时候就要给**初始值**
- final方法--可以被子类继承，但是不能被子类重写
- final类--不能被继承
- `public static final`：存储全局配置信息，或者实现其他需要全局共享的数据

### **super**

- 当需要在子类中调用父类的被重写方法时，要使用 super 关键字
- `super.move();//你已经重写了父类的move()方法`

### **abstract**

- 抽象类：
  - 抽象类不能用来实例化对象
  - 如果一个类包含抽象方法，那么该类一定要声明为抽象类
  - 一个类不能同时被 abstract 和 final 修饰
  - 抽象类可以包含抽象方法和非抽象方法
- 抽象方法
  - 抽象方法不能被声明成 final 和 static。
  - 如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。
  - 抽象类可以不包含抽象方法--抽象类提供一个通用的框架，供子类扩展和重写
  - 抽象方法的声明以分号结尾，例如：**public abstract sample();**。

## 运算

### **自增自减**：

- **前缀自增自减法(++a,--a):** 先自增或者自减，再运算

- **后缀自增自减法(a++,a--):** 先运算，再自增或者自减

- ```java
  int a=1;
  //a++这个表达式的值为1,a = 2
  //++a这个表达式的值为2,a = 2
  ```

### **位运算**：[Java 运算符 | 菜鸟教程](https://www.runoob.com/java/java-operators.html)

- ^：异或运算
- `<<`：左移
- `>>`：右移，算术右移，补符号位，符号位0补0，符号位1补1
- `>>>`：右移，0填充
- `()?:`：**条件运算符**本身不能直接包含赋值语句，它只能返回值。`(a == 1) ? 20 : 30`这是一个表达式，条件成立，表达式的值为前一个20；条件不成立，表达式的值为后一个30

- `instanceof`：左边是对象，右边是类名或接口名，判断左边对象是否为右边类（子类，实现类），是返回true

## **Java数组**

- 「动态创建」：声明时只是定义变量，不分配内存，大小需要在创建时确定
- 可以是「不规则数组」（每行长度不同）

### **增强型 for 循环**：遍历数组

- for (元素类型 变量名 : 数组/集合) { ... }
- **依次取出数组 / 集合中的每个元素**

[Java Number & Math 类 | 菜鸟教程](https://www.runoob.com/java/java-number.html)

只要参数的数量和/或类型不同，多个方法就可以拥有相同的名称

## java类

### **各种类：**

- [All Classes](https://www.runoob.com/manual/jdk11api/allclasses.html)

### **包**：

- 多个类在同一个`.java`文件里（默认包）
- 开头都写了相同的`package`语句 
- 包名会对应实际的文件夹结构--同一个「文件夹」也就是同一个「包」
- 有层级关系也不算「同一个包」
- 层级包的一大作用是避免类名重复。比如：
  - `com.a` 里可以有一个 `User` 类
  - `com.a.b` 里也可以有一个 `User` 类
    因为包不同，它们是两个完全独立的类，不会冲突。

### **内部类**

- 嵌套类（类中的类）
- 可以访问外部类的属性和方法

### **接口：**

- 当类实现接口的时候，类要实现接口中所有的方法。否则，类必须声明为抽象的类。

**枚举**

- 每个枚举常量都有一个默认的「序号」，从 `0` 开始依次递增
- 有属性方法
- 实例放在最前面
- 构造方法--私有private
- 手动指定数字属性
- **`Season.values()`**：**返回该枚举中所有常量的数组**

### **用户输入 (Scanner)**

- [Java 用户输入 (Scanner)](https://www.w3school.com.cn/java/java_user_input.asp)
- [Java Scanner 方法](https://www.w3school.com.cn/java/java_ref_scanner.asp)

- ```java
  import java.util.Scanner;  // 导入 Scanner 类
  ```

- nextLine() 方法
- nextByte()

### **时间日期：**

- [Java 日期和时间](https://www.w3school.com.cn/java/java_date.asp)

- ```java
  import java.time.LocalDate; // 导入 LocalDate 类
  
  public class Main {
    public static void main(String[] args) {
      LocalDate myObj = LocalDate.now(); // 创建日期对象
      System.out.println(myObj); // 显示当前日期
    }
  }
  ```

- 使用`now()`方法返回

## **数据结构**

- [Java 数据结构 | 菜鸟教程](https://www.runoob.com/java/java-data-structures.html)

### **ArrayList：**

- [Java ArrayList 方法](https://www.w3school.com.cn/java/java_ref_arraylist.asp)

- 可调整大小的数组

- ```java
  import java.util.ArrayList; // 导入 ArrayList 类
  ArrayList<String> cars = new ArrayList<String>(); // 创建 ArrayList 对象
  ```

- add()
- 访问--`get(索引)`
- 修改--`set()` 方法并引用索引号

- 删除-- `remove()` 方法并引用索引号

- ArrayList 中的元素实际上是对象--int应该使用包装类Integer

- 排序

  ```java
  import java.util.Collections;  // 导入 Collections 类
  Collections.sort(cars);  // 对 cars 排序
  ```

### **LinkedList:**

- [Java LinkedList 方法](https://www.w3school.com.cn/java/java_ref_linkedlist.asp)

- **ArrayList 的工作原理**

  `ArrayList` 类内部有一个常规数组。添加元素时，将其放入数组中。如果数组不够大，则会创建一个新的更大的数组来替换旧数组，然后删除旧数组。

- **LinkedList 的工作原理**

  `LinkedList` 将其项目存储在“容器”中。该列表有一个指向第一个容器的链接，每个容器都有一个指向列表中下一个容器的链接。要将元素添加到列表中，需要将该元素放入一个新容器中，并将该容器链接到列表中的其他容器之一。

### **HashMap：**

- [Java HashMap 方法](https://www.w3school.com.cn/java/java_ref_hashmap.asp)

- 映射类

- 用于存储**键值对**，适合快速根据键查找值。

- ```java
  import java.util.HashMap; // 导入 HashMap 类
  ```

- 键在HashMap中是唯一的，而值可以重复

- `put()`添加键值对

- 当需要快速查找、插入和删除数据时使用

- get(键)会返回他对应的值

### **HashSet：**

- 集合

- 用于存储一组**不重复**的元素，适合快速检查元素是否存在。

- ```java
  import java.util.HashSet; // 导入 HashSet 类
  ```

- `add()`添加元素
- ==！！！==内部是由HashMap实现的

### **迭代器**

- ```java
  import java.util.Iterator; // 引入 Iterator 类
  ```

- ```java
  // 创建集合
  ArrayList<String> sites = new ArrayList<String>();
  sites.add("Google");
  sites.add("Runoob");
  sites.add("Taobao");
  sites.add("Zhihu");
  
  // 获取迭代器
  Iterator<String> it = sites.iterator();
  
  // 输出集合中的第一个元素
  System.out.println(it.next());
  ```

- **next()** - 返回迭代器的下一个元素，并将迭代器的指针移到下一个位置

- **hasNext()** - 用于判断集合中是否还有下一个元素可以访问

- **remove()** - 从集合中删除迭代器最后访问的元素（可选操作）

### **String**

- 不用导包--Java.long下
- 不可变的
- 直接赋值--在常量池中，相同字符串的话同一引用
- 直接new出来的，它是对象，在堆中
- 字符串拼接其实是将str1和str2拼起来给str3
- 常用方法：
  - `length()`：返回字符串长度
  - `charAt(int index)`：获取指定位置的字符
  - `equals(Object obj)`：比较字符串内容（区分大小写）
  - `equalsIgnoreCase(String anotherString)`：忽略大小写比较
  - `indexOf(String str)`：查找子串首次出现的位置
  - `substring(int beginIndex, int endIndex)`：截取子串（左闭右开）
  - `trim()`：去除首尾空格
  - `toUpperCase()`/`toLowerCase()`：转换大小写
  - `split(String regex)`：按正则分割字符串为数组
- 补充：
  - ==：
    - 基本数据类型：比较值
    - 引用对象：比较引用地址
  - equals()：比的是值，区分大小写的
- `String` 类的底层是 `final` 修饰的字符数组

### **StringBuffer**

- 线程安全的**可变**字符串
- 修改的是自身，返回修改后的当前对象引用
- 加了锁，多线程环境下安全，但性能较低
- 常用方法：
  - `append(...)`：拼接字符串（支持各种数据类型）
  - `insert(int offset, ...)`：在指定位置插入内容
  - `delete(int start, int end)`：删除指定范围的字符（左闭右开）
  - `reverse()`：反转字符串

### **StringBuilder**

- 与**StringBuffer**类似
- 非线程安全的，可变字符串
- 性能好

### **总结：**

- **优先用 `String`**：
  字符串内容固定不变（如常量、配置项），或修改操作极少的场景。
  例：`String name = "张三";`、`String url = "https://example.com";`
- **优先用 `StringBuffer`**：
  多线程环境下，需要频繁修改字符串（如多线程日志拼接）。
  （注：实际开发中多线程场景较少，`StringBuilder` 更常用）
- **优先用 `StringBuilder`**：
  单线程环境下，需要频繁修改字符串（如拼接、插入）。
  例：循环中拼接日志、动态生成 SQL 语句。

## java文件处理



## java高级

### **Java异常**

- try{尝试代码块}catch{处理错误的代码块}

- try--可能会出错的代码块

- catch--根据不同的错误类型,捕获错误

- ```java
  try {
      // 可能发生异常的代码
  } catch (异常类型1 e) {
      // 处理异常类型1
  } catch (异常类型2 e) {
      // 处理异常类型2（子类异常需放在父类前）
  }
  ```

  

- **`throw`主动抛出错误**

- **`throws`声明方法可能抛的异常**

- ```java
  // 1. 自定义异常：成绩超出范围
  class ScoreOutOfRangeException extends Exception {
      public ScoreOutOfRangeException(String message) {
          super(message);
      }
  }
  ```

- **`finally`：必执行的代码块**

  ```java
  try { ... } 
  catch (Exception e) { ... }
  finally {
      // 无论是否异常，必执行（用于释放资源：关闭流、连接等）
  }
  ```


### **正则表达式**

- [Java 正则表达式 | 菜鸟教程](https://www.runoob.com/java/java-regular-expressions.html)

- [正则表达式 – 教程 | 菜鸟教程](https://www.runoob.com/regexp/regexp-tutorial.html)

- 导入 `java.util.regex` 包

  - `Pattern` 类 - 定义模式（用于搜索）
  - `Matcher` 类 - 用于搜索模式
  - `PatternSyntaxException` 类 - 指示正则表达式模式中的语法错误

- ```java
  import java.util.regex.Matcher;
  import java.util.regex.Pattern;
   
  public class RegexMatches
  {
      public static void main( String[] args ){
   
        // 按指定模式在字符串查找
        String line = "This order was placed for QT3000! OK?";
        String pattern = "(\\D*)(\\d+)(.*)";
   
        // 创建 Pattern 对象
        Pattern r = Pattern.compile(pattern);
   
        // 现在创建 matcher 对象
        Matcher m = r.matcher(line);
        if (m.find( )) {
           System.out.println("Found value: " + m.group(0) );
           System.out.println("Found value: " + m.group(1) );
           System.out.println("Found value: " + m.group(2) );
           System.out.println("Found value: " + m.group(3) ); 
        } else {
           System.out.println("NO MATCH");
        }
     }
  }
  ```

- `m.find();`找下一个匹配的，返回是否找到了

- `m.group();`返回当前匹配到的字符串

### **Java 泛型**

- 提高了代码的复用性、类型安全性和可维护性

- **java 中泛型标记符：**
  - **E** - Element (在集合中使用，因为集合中存放的是元素)
  - **T** - Type（Java 类）
  - **K** - Key（键）
  - **V** - Value（值）
  - **N** - Number（数值类型）
  - **？** - 表示不确定的 java 类型


### **线程**

- 线程<进程（线程开销小）

- 特点：轻量级、并发执行、共享资源

- **并发：**多个任务在同一时间段内**交错执行**，但不一定同时运行

  任务的执行顺序和时间上是重叠的，但具体哪个任务在哪个时刻运行是由操作系统调度决定的

- **并行：**多个任务在**同一时刻**同时运行

  任务的执行是同时进行的，需要多核处理器或多个处理器来支持

- ![QQ_1755499854243](https://gitee.com/ppedmo/pic-go/raw/master/img/202508181451394.png)

- 并发运行--start()方法之后，在循环语句执行过程中，执行run()方法

- 创建线程

- 运行线程

- ```java
  public class Main extends Thread {
      //public static int var = 0;静态变量
    public static void main(String[] args) {
      Main thread = new Main();
      thread.start();
      System.out.println("这段代码在线程之外");
    }
    public void run() {
      System.out.println("这段代码在一个线程中运行");
        //可以用一些静态变量
        //注意并发问题
    }
  }
  ```

- ```java
  public class Main implements Runnable {
    public static void main(String[] args) {
      Main obj = new Main();
      Thread thread = new Thread(obj);
      thread.start();
      System.out.println("这段代码在线程之外");
    }
    public void run() {
      System.out.println("这段代码在一个线程中运行");
    }
  }
  ```

- `isAlive();`解决并发的方法之一：检查线程是否已完成运行

### **Lambda表达式**

- 用于简化函数式接口（**只有一个抽象方法的接口**）的实现

- Lambda 表达式通常作为参数传递给函数

- `(参数列表) -> { 方法体 }`

- ```java
  //完整形式
  (参数类型 参数1, 参数类型 参数2, ...) -> {
      // 方法体（可多行）
      return 结果; // 若有返回值
  }
  ```

- 表达式形式：Lambda体只包含一个表达式

- ```java
  x -> x * 2
  (x) -> return x*2;
  ```

- `compare(a, b)` 方法的返回值是一个整数，规则如下：
  - 若返回 **负数**：表示 `a` 应该排在 `b` 前面
  - 若返回 **0**：表示 `a` 和 `b` 位置相等
  - 若返回 **正数**：表示 `a` 应该排在 `b` 后面
  - 所以a-b是升序，b-a是降序

### **高级排序--Comparator（比较器）**

- `Comparator` 接口允许你创建一个包含 `compare()` 方法的类，该方法比较两个对象以决定哪个在列表中应排在前面

- `compare()` 方法应返回一个数字，该数字：
  - 为负数时，表示第一个对象应在列表中排在前面。
  - 为正数时，表示第二个对象应在列表中排在前面。
  - 为零时，表示顺序无关紧要。

- ```java
  myCars.sort((a, b) -> a.year - b.year);
  ```

- 这是一个比较简便的使用方法，任何类都可以比较，只要指定比较规则

- a-b升序：a >b， a-b为正数，a在b后面，即后面的大--升序

- b-a降序：a >b， a-b为负数，a在b前面，即前面的大--降序

- 还可以制定复杂的规则

- ```java
  import java.util.ArrayList;
  import java.util.Collections;
  import java.util.Comparator;
  
  // 定义一个比较器类 SortEvenFirst，实现 Comparator 接口
  class SortEvenFirst implements Comparator {
    // 实现 compare 方法，用于比较两个对象
    public int compare(Object obj1, Object obj2) {
      // 确保传入的对象是 Integer 类型
      Integer a = (Integer) obj1;
      Integer b = (Integer) obj2;
      
      // 检查每个数字是否为偶数
      // 一个数字如果除以 2 的余数为 0，则为偶数
      boolean aIsEven = (a % 2) == 0;
      boolean bIsEven = (b % 2) == 0;
      
      // 如果两个数字同为偶数或同为奇数，则按正常排序规则比较
      if (aIsEven == bIsEven) {
        if (a < b) return -1; // a小于b，返回-1
        if (a > b) return 1;  // a大于b，返回1
        return 0;             // a等于b，返回0
      } else {
        // 如果 a 是偶数，则 a 排在前面，否则 b 排在前面
        if (aIsEven) {
          return -1; // a 是偶数，返回 -1，表示 a 排在前面
        } else {
          return 1;  // b 是偶数，返回 1，表示 b 排在前面
        }
      }
    }
  }
  
  public class Main {
    public static void main(String[] args) {
      // 创建一个 Integer 类型的 ArrayList
      ArrayList<Integer> myNumbers = new ArrayList<Integer>();
      // 向列表中添加一些整数
      myNumbers.add(33);
      myNumbers.add(15);
      myNumbers.add(20);
      myNumbers.add(34);
      myNumbers.add(8);
      myNumbers.add(12);
  
      // 创建一个 SortEvenFirst 比较器实例
      Comparator myComparator = new SortEvenFirst();
      // 使用该比较器对列表进行排序
      Collections.sort(myNumbers, myComparator);
  
      // 遍历并打印排序后的列表
      for (int i : myNumbers) {
        System.out.println(i);
      }
    }
  }
  ```

  

### **高级排序--Comparable 接口**

- `Comparable` 接口允许对象通过 `compareTo()` 方法指定其自身的排序规则

- `compareTo()` 方法返回一个数字，该数字：

  - 为负数时，表示可比较对象应在列表中排在前面。
  - 为正数时，表示另一个对象应在列表中排在前面。
  - 为零时，表示顺序无关紧要。

- 许多原生 Java 类（如 `String` 和 `Integer`）都实现了 `Comparable` 接口。

  这就是为什么字符串和数字不需要比较器就可以进行排序的原因。

### **反射--不是很懂**

- [Java 反射（Reflection） | 菜鸟教程](https://www.runoob.com/java/java-reflection.html)

- 多是框架用的多

### Java Object 类--没记



### Java序列化

- 序列化是将对象的状态转换为字节流的过程

- **对象的内存地址是本地的**：对象在内存中的存储位置是通过内存地址来标识的。这些地址是运行时环境（如JVM）分配的，是本地的、临时的。当程序结束时，这些地址会失效。

  **跨环境无效**：如果直接传输对象的内存地址，接收方无法解析这些地址，因为它们是发送方环境中的地址。例如，一个对象在发送方的地址可能是0x12345678，但在接收方的环境中，这个地址可能没有任何意义。

- 保存到磁盘（持久化）、传输到网络

- 反序列化，将字节流重新转换为对象

-  **java.io.Serializable** 接口：该接口没有任何方法，只是一个标记接口，用于标识类可以被序列化

- 实现 `java.io.Serializable` 接口，告诉 Java 编译器这个类可以被序列化

### 网络编程

- 服务器和客户端建立联系的过程：
  - 首先服务器段先创建SeverSocket对象监听端口，并调用accept()方法等待连接；客户端创建 Socket 指定服务器 IP 和端口发起连接请求（即第一次握手）；服务器收到请求后响应同意连接（即第二次握手）；客户端确认收到响应（即第三次握手），此时连接建立，双方可通过各自的 Socket 通道收发数据
- 本质是基于 TCP 协议的 “三次握手” 连接建立过程，配合 Socket 编程接口的具体操作
- **三次握手**：
  - 核心原因是**它能确保通信双方都确认 “对方具备收发能力”**
  - 第一次握手（客户端→服务器）：客户端告诉服务器 “我能发”；
  - 第二次握手（服务器→客户端）：服务器告诉客户端 “我能收，且我能发”；
  - 第三次握手（客户端→服务器）：客户端告诉服务器 “我能收”。
- 
