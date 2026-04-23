# 旧版IO

### File类

- `import java.io.File`

- **File 类**的对象可以表示一个**文件** 或者 **目录**

- `File file = new File("cc.txt");` 这行代码**不会直接创建文件**，它只是在内存中创建了一个 “文件路径的抽象表示”（类似一个路径标签），并不会在磁盘上实际生成文件。

- File 类的对象 还不能直接对文件进行读写操作，只能修改文件的属性

- 检查文件是否存在、创建文件、获取文件信息

- 操作：

- ```java
  		System.out.println("文件已经存在:"+f1.exists());
  		System.out.println("文件的名字:"+f1.getName());
  		System.out.println("文件的路径:"+f1.getPath());
  		System.out.println("文件的绝对路径:"+f1.getAbsolutePath());
  		System.out.println("是目录吗:"+f1.isDirectory());
  		System.out.println("文件大小:"+f1.length());
  
  ```

- `f1.createNewFile()`是必要的，因为它<u>确保了文件的存在</u>。如果没有这一步，后续对文件的操作（如写入内容）可能会失败，因为文件可能不存在。

### FileInputStream类

- 将文件中的数据输入到内存中，我们可以用它来读文件操作
- 以程序为视角

写法：

```java
File file = new File("src\\aa.txt");
FileInputStream f1 = new FileInputStream(file);
```

简洁一点：

```java
FileInputStream f1 = new FileInputStream(new File("src\\aa.txt"));
```

例子：

```java
import java.io.*;

public class FileStreamDemo {
    public static void main(String[] args) {
        try {
            File file=new File("aa.txt");
            // 检查文件是否存在
            if (!file.exists()) {
                System.out.println("错误：文件不存在！");
                file.createNewFile();
            }
            FileInputStream f1=new FileInputStream(file);//这里需要进行抛出异常处理
            long length = file.length();
//            for (int i = 0; i < length; i++) {
//                char ch=(char)(f1.read());//循环读取字符
//                System.out.print(ch+" ");
//            }
            int ch = 0;
            while ((ch = f1.read()) != -1) { // 使用while循环，直到读取到-1（文件末尾）
                System.out.print((char) ch + " "); // 将读取到的字节值转换为字符并输出
            }
            System.out.println();//换行操作
            f1.close();//关闭文件
        } catch (Exception e) {
            // TODO: handle exception
            System.out.println("文件打开失败");
        }

    }
}
```

- 解释：`(ch = f1.read()) != -1`可以作为条件，`ch !=  -1`

### FileOutputStream类

- 将内存中的数据输出到文件中，所以我们可以用这个类来进行写文件的操作

- 先打开-把要写入的字符串转为字符数组（可以写编码方式）-tyr...catch把字符数组写入文件-finally关闭文件

- ```java
  import java.io.*;
  
  public class FileOuputDemo {
  	public static void main(String[] args) throws FileNotFoundException {
  		File file=new File("src\\aa.txt");
  		FileOutputStream f1=new FileOutputStream(file);//(file,true)，这里有true的话，代表可以在文件后面追加内容
  		String str="I love coding";
  		byte[] buff=str.getBytes();//将字符串转换为字节数组
  		try {
  			f1.write(buff);//把字节数组的内容写进去文件
  		} catch (Exception e) {
  			// TODO: handle exception
  		}finally {
  			try {
  				f1.close();
  			} catch (IOException e) {
  				// TODO Auto-generated catch block
  				e.printStackTrace();
  			}
  		}
  	}
  }
  ```

### FileWriter类 与 BufferedWriter类

- 文件写入对象f->字符流写入对象f1->f1.write()写入数据

```java
import java.io.*;

public class FileWriterDemo {
	public static void main(String[] args) {
		String[] str= {"春眠不觉晓,","处处闻啼鸟,","夜来风雨声,","花落知多少,"};
		File file=new File("src\\cc.txt");//我们在该类的位置创建一个新文件
		FileWriter f=null;//创建文件写入对象
		BufferedWriter f1=null;//创建字符流写入对象
	
		try {
			//这里把文件写入对象和字符流写入对象分开写了
			f=new FileWriter("src\\cc.txt");//创建一个名为cc.txt的文件
			f1=new BufferedWriter(f);
			//通过循环遍历上面的String 数组中的元素
			for (int i = 0; i < str.length; i++) {
				f1.write(str[i]);//把String中的字符写入文件
				f1.newLine();//换行操作
				}
		} catch (Exception e) {
			// TODO: handle exception
		}finally {//如果没有catch 异常，程序最终会执行到这里
			try {
				f1.close();
				f.close();//关闭文件
			} catch (Exception e2) {
				// TODO: handle exception
			}
		}
	}
}
```

- 解释：try块外面创建

```java
FileWriter f=null;//创建文件写入对象
BufferedWriter f1=null;//创建字符流写入对象
```

finally中就可以关闭文件

也可写在里面--`try-with-resources`自动关闭

- 注意文件关闭顺序：先BufferedWriter后FileWriter

- `try-with-resources`自动关闭

```java
import java.io.BufferedWriter;
import java.io.FileWriter;

public class FileWriterDemo {
    public static void main(String[] args) {
        String[] str = {"春眠不觉晓,", "处处闻啼鸟,", "夜来风雨声,", "花落知多少,"};
        // 目标文件路径
        String filePath = "src\\cc.txt";
        
        // 使用 try-with-resources 自动关闭流（无需手动close）
        // 格式：try (流对象创建) { ... }
        try (
            FileWriter f = new FileWriter(filePath);
            BufferedWriter f1 = new BufferedWriter(f);
        ) {
            // 遍历数组，逐行写入
            for (String line : str) {  // 增强for循环更简洁
                f1.write(line);
                f1.newLine();  // 换行
            }
            System.out.println("文件写入成功！");
        } catch (Exception e) {
            // 打印异常信息，方便排查问题
            e.printStackTrace();
        }
        // 无需finally块，try-with-resources会自动关闭流
    }
}

```

### FileReader类 与 BufferedReader类

- 创建文件读取对象->创建字符流对象->循环打印->异常捕获，关闭文件

```java
import java.io.*;

public class FileReaderDemo {
	public static void main(String[] args) {
		File file=new File("src\\cc.txt");
		FileReader f=null;//文件读取对象
		BufferedReader f1=null;//字符流对象
		try {
			f=new FileReader(file);
			f1=new BufferedReader(f);
			//循环打印cc文件中的每行数据
			String str=null;
			while((str=f1.readLine())!=null) {
				System.out.println(str);
			}
				
		} catch (Exception e) {
			// TODO: handle exception
		}finally {
			try {
				f1.close();
				f.close();
			} catch (Exception e2) {
				// TODO: handle exception
			}
		}
	}
}

```

# NIO（New I/O）

- [Java NIO Files 类 | 菜鸟教程](https://www.runoob.com/java/java-nio-file.html)

- `import java.nio.file.Files`
- 主要特点：
  - **静态方法**：所有方法都是静态的，无需创建实例
  - **功能丰富**：提供文件读写、属性操作、目录遍历等多种功能
  - **异常处理**：统一使用 `IOException` 处理文件操作异常
  - **与 Path 配合**：主要与 `java.nio.file.Path` 接口一起使用
- `import java.nio.file.Path`

## 1、文件操作

### 文件读写

- `Files.readAllLines()`读取所有行
- 备注：path指的是Path类的对象，通过Path.get(filePath)获取
- `content`：字符串，通过`content.getBytes()`转为字符数组

```java
// 读取文件所有行--不用循环读取了
List<String> lines = Files.readAllLines(path);

// 写入文件
Files.write(path, content.getBytes());
//备注：path指的是Path类的对象，通过Path.get(filePath)获取

// 追加写入
Files.write(path, content.getBytes(), StandardOpenOption.APPEND);
```



### 文件复制/移动/删除

```java
*// 复制文件*
Files.copy(sourcePath, targetPath);

*// 移动/重命名文件*
Files.move(sourcePath, targetPath);

*// 删除文件*
Files.delete(path);
```



## 2、目录操作

### 创建目录

```java
*// 创建单级目录*
Files.createDirectory(path);

*// 创建多级目录*
Files.createDirectories(path);
```



### 目录遍历

```java
*// 遍历目录*
**try** (Stream<Path> paths = Files.list(directoryPath)) {
  paths.**forEach**(System.out::println);
}

*// 递归遍历目录*
**try** (Stream<Path> paths = Files.walk(directoryPath)) {
  paths.**forEach**(System.out::println);
}
```



## 3、文件属性操作

### 获取文件属性

```java
*// 检查文件是否存在*
**boolean** exists = Files.exists(path);

*// 获取文件大小*
**long** size = Files.size(path);

*// 获取文件最后修改时间*
FileTime lastModifiedTime = Files.getLastModifiedTime(path);
```



### 设置文件属性

```java
*// 设置文件最后修改时间*
Files.setLastModifiedTime(path, FileTime.fromMillis(System.currentTimeMillis()));

*// 设置文件权限*
Set<PosixFilePermission> perms = PosixFilePermissions.fromString("rwxr-x---");
Files.setPosixFilePermissions(path, perms);
```



------

## 4、高级功能

### 1、文件查找

```java
*// 查找特定扩展名的文件*
**try** (Stream<Path> paths = Files.find(
    directoryPath,
    Integer.MAX_VALUE,
    (path, attrs) -> path.toString().endsWith(".txt"))) {
  paths.**forEach**(System.out::println);
}
```



### 2、临时文件操作

```java
*// 创建临时文件*
Path tempFile = Files.createTempFile("prefix", ".suffix");

*// 创建临时目录*
Path tempDir = Files.createTempDirectory("tempDir");
```



### 3、文件属性视图

```java
*// 获取文件所有者*
UserPrincipal owner = Files.getOwner(path);

*// 获取文件存储信息*
FileStore store = Files.getFileStore(path);
```



------

## 5、最佳实践

### 1、异常处理

```java
**try** {
  Files.copy(sourcePath, targetPath, StandardCopyOption.REPLACE_EXISTING);
} **catch** (IOException e) {
  System.err.println("文件操作失败: " + e.getMessage());
}

```

### 2、资源清理

```java
**try** (Stream<String> lines = Files.lines(path)) {
  lines.**forEach**(System.out::println);
} *// 自动关闭流*
```



### 3、性能考虑

- 对于大文件，使用缓冲流 (`Files.newBufferedReader`/`Files.newBufferedWriter`)
- 批量操作时考虑使用 `Files.walk` 而非递归调用
- 频繁访问的属性可以缓存
