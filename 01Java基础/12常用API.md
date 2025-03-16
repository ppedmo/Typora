# API

- 只记类名和作用
- 直接在API帮助文档中查找

### 1.Math

![image-20241112081619984](https://gitee.com/ppedmo/pic-go/raw/master/img/202411120816173.png)

### 2.system

```java
public static long currentTimeMillis()			// 获取当前时间所对应的毫秒值（当前时间为0时区所对应的时间即就是英国格林尼治天文台旧址所在位置）
public static void exit(int status)				// 终止当前正在运行的Java虚拟机，0表示正常退出，非零表示异常退出
public static native void arraycopy(Object src,  int  srcPos, Object dest, int destPos, int length); // 进行数值元素copy
```

- arraycopy(arr1,0,arr2,1,3)
- arr1 数组从索引 0 开始拷贝到 arr2 数组中的 1 索引，长度为3

### 3.Runtime

```java
public static Runtime getRuntime()		//当前系统的运行环境对象
public void exit(int status)			//停止虚拟机
public int availableProcessors()		//获得CPU的线程数
public long maxMemory()				    //JVM能从系统中获取总内存大小（单位byte）
public long totalMemory()				//JVM已经从系统中获取总内存大小（单位byte）
public long freeMemory()				//JVM剩余内存大小（单位byte）
public Process exec(String command) 	//运行cmd命令
```

### 4.Object

```java
public String toString()				//返回该对象的字符串表示形式(可以看做是对象的内存地址值)
    //包名加类名@地址值
public boolean equals(Object obj)		//比较两个对象地址值是否相等；true表示相同，false表示不相同
protected Object clone()    			//对象克隆
```

### 5.Objects

```java
public static String toString(Object o) 					// 获取对象的字符串表现形式
public static boolean equals(Object a, Object b)			// 比较两个对象是否相等
public static boolean isNull(Object obj)					// 判断对象是否为null
public static boolean nonNull(Object obj)					// 判断对象是否不为null
```



### 6.BigIntege

```java
//构造方法
public BigInteger(int num, Random rnd) 		//获取随机大整数，范围：[0 ~ 2的num次方-1]
public BigInteger(String val) 				//获取指定的大整数
public BigInteger(String val, int radix) 	//获取指定进制的大整数
    
//下面这个不是构造，而是一个静态方法获取BigInteger对象
public static BigInteger valueOf(long val) 	//静态方法获取BigInteger的对象，内部有优化，长度long类型的

//对象一旦创建不能改变
//add()是新创建了一个对象

//如果BigInteger表示的数字没有超出long的范围，可以用静态方法获取，
//如果BigInteger表示的超出long的范围，可以用构造方法获取，
//对象一旦创建，BigInteger内部记录的值不能发生改变
//只要进行计算都会产生一个新的BigInteger对象    
```

###  7.BigDecimal类

```java
BigDecimal(string val)								//精准的

public BigDecimal add(BigDecimal value)				// 加法运算
public BigDecimal subtract(BigDecimal value)		// 减法运算
public BigDecimal multiply(BigDecimal value)		// 乘法运算
public BigDecimal divide(BigDecimal value)			// 触发运算
```

