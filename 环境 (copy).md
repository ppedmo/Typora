照着readme来：[HEU-Database-course-design/HEU-Database-course-design/Readme.md at master · wfloveiu/HEU-Database-course-design (github.com)](https://github.com/wfloveiu/HEU-Database-course-design/blob/master/HEU-Database-course-design/Readme.md)

# vue

[好细的Vue安装与配置_vue配置-CSDN博客](https://blog.csdn.net/m0_57545353/article/details/124366678?ops_request_misc=%7B%22request%5Fid%22%3A%22171673183816800182786160%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=171673183816800182786160&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-124366678-null-null.142^v100^pc_search_result_base5&utm_term=Vue安装&spm=1018.2226.3001.4187)

换了一个镜像[registry.npmmirror.com](https://registry.npmmirror.com/)

`npm config set registry https://registry.npmmirror.com/`



# VScode

[VScode运行错误：【npm : 无法将“npm”项识别为 cmdlet、函数、脚本文件或可运行程序的名称。请检查名称的拼写，如果包括路径，请确保路径正确，然后 再试一次。】_vscode无法将npm项识别为-CSDN博客](https://blog.csdn.net/qq_51463650/article/details/131548673)

[解决VSCODE"因为在此系统上禁止运行脚本"报错-CSDN博客](https://blog.csdn.net/larpland/article/details/101349586)

# 后端文件

使用他给的虚拟环境

删掉了原来的虚拟环境给它重新配了，按照那个require的那个文本下载

先删除掉venu全部文件



[【Python基础】PyCharm配置Python虚拟环境详解_pycharm虚拟环境设置-CSDN博客](https://blog.csdn.net/didi_ya/article/details/120664678?ops_request_misc=%7B%22request%5Fid%22%3A%22171757234116800182719937%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fall.%22%7D&request_id=171757234116800182719937&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-120664678-null-null.142^v100^pc_search_result_base5&utm_term=pycharm用别人的虚拟环境打开别人的项目&spm=1018.2226.3001.4187)

# 连接数据库sql server

sql server host查看

![image-20240527210503257](C:\Users\honor\AppData\Roaming\Typora\typora-user-images\image-20240527210503257.png)

1.2步

[Python连接SQL SEVER数据库全流程_python连接sql server-CSDN博客](https://blog.csdn.net/qq_33909788/article/details/133980334?ops_request_misc=&request_id=&biz_id=102&utm_term=Python连接SQL server&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-133980334.142^v100^pc_search_result_base5&spm=1018.2226.3001.4187)

```SQL Sever
class BaseConfig:

    # 数据库的配置
    DIALCT = "mssql"
    DRITVER = "pyodbc"
    HOST = 'LAPTOP-8S7TJ1RU'
    PORT = "1433"  # 默认 SQL Server 端口号
    USERNAME = "sa"
    PASSWORD = "2022214317"
    DBNAME = 'zhangsan'

    REDIS_HOST = 'your_redis_host'
    REDIS_PORT = 6379


    SQLALCHEMY_DATABASE_URI = f"{DIALCT}+{DRITVER}://{USERNAME}:{PASSWORD}@{HOST}/{DBNAME}?driver=ODBC+Driver+17+for+SQL+Server"
    SQLALCHEMY_TRACK_MODIFICATIONS = True
```

# 连接openGauss数据库

[openGauss数据库之Python驱动快速入门_python orm连接华为gauss db 数据库-CSDN博客](https://blog.csdn.net/GaussDB/article/details/121330008)

# mysql

mysql安装：[MySQL的下载安装与Navicat配置（超详细）_navicat安装教程及环境配置方法-CSDN博客](https://blog.csdn.net/qq_39715000/article/details/118942579)

navicat破解:[Navicat安装破解和激活详细讲解（全网最简单且靠谱）-CSDN博客](https://blog.csdn.net/jyyzhongwjg/article/details/139410232?ops_request_misc=&request_id=&biz_id=102&utm_term=navicat破解教程&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-2-139410232.142^v100^pc_search_result_base5&spm=1018.2226.3001.4187)

[MySQL导入sql文件的三种方法-CSDN博客](https://blog.csdn.net/Elliseaon/article/details/118275142)

出现如图所示：![image-20240530153015853](C:\Users\honor\AppData\Roaming\Typora\typora-user-images\image-20240530153015853.png)



[安装 MySQL 服务时提示 Install/Remove of the Service Denied-CSDN博客](https://blog.csdn.net/weixin_43960383/article/details/124376546)

（管理员运行命令提示符）

**修改密码**  ：mysql@123

打咩好像这个密码不太行

换mysql（密码别带@）

改密码：[mysql设置密码报错:mysqladmin: connect to server at 'localhost' failed的解决方法-CSDN博客](https://blog.csdn.net/weixin_42709849/article/details/103782061)

连接数据库之前先启动一下mysql：命令行（管理员）net start mysql

导入数据库：照着这个导入https://blog.csdn.net/Elliseaon/article/details/118275142

结果展示：![image-20240604192904663](C:\Users\honor\AppData\Roaming\Typora\typora-user-images\image-20240604192904663.png)


