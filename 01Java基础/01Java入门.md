### CMD

常见的CMD命令如下：

| 操作               | 说明                              |
| ------------------ | --------------------------------- |
| 盘符名称:          | 盘符切换。E:回车，表示切换到E盘。 |
| dir                | 查看当前路径下的内容。            |
| cd 目录            | 进入单级目录。cd itheima          |
| cd ..              | 回退到上一级目录。                |
| cd 目录1\目录2\... | 进入多级目录。cd itheima\JavaSE   |
| cd \               | 回退到盘符目录。                  |
| cls                | 清屏。                            |
| exit               | 退出命令提示符窗口。              |

###  环境变量

作用：

​	如果我想要在CMD的任意目录下，都可以启动某一个软件，那么就可以把这个软件的路径配置到环境变量中的PATH里面。

​	在启动软件的时候，操作系统会先在当前路径下找，如果在当前录课没有再到环境变量的路径中去找。如果都找不到就提示无法启动。

### java基础学习

- 运行：

  - 先转到书写代码的文件夹下

  - javac XXXX.java（编译）

  - java XXXX（运行）

    ![image-20241022192723390](https://gitee.com/ppedmo/pic-go/raw/master/img/202410221927489.png)

- Java的三大平台
  - JavaSE：桌面应用的开发（c c++做的好些），是其他两个版本的基础。
  - JavaME：Java语言的小型版，用于嵌入式消费类电子设备或者小型移动设备的开发。
  - JavaEE：用于Web方向的网站开发。（主要从事后台服务器的开发）在服务器领域，Java是当之无愧的龙头老大。

- 主要特性：面向对象，安全性，多线程，简单易用，开源，跨平台
- 跨平台：
  - 编译型：整体翻译（c/c++）
  - 解释型：按行翻译（python）
  - 混合型：![image-20241022201901409](https://gitee.com/ppedmo/pic-go/raw/master/img/202410222019561.png)
  - java：先编译成字节码文件，再按行翻译交由虚拟机（JVM）运行

- JRE 和 JDK

  - JRE：java运行环境

    ![image-20241022202925309](https://gitee.com/ppedmo/pic-go/raw/master/img/202410222029414.png)

  - JDK：java开发工具包

  ![image-20241022202607408](https://gitee.com/ppedmo/pic-go/raw/master/img/202410222026504.png)

  - 