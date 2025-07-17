# 展示

![image-20250518193557927](https://gitee.com/ppedmo/pic-go/raw/master/img/202505181935985.png)

# 编译问题：

1.未将小狼毫依赖的两个子仓库加入

![image-20250518113450019](https://gitee.com/ppedmo/pic-go/raw/master/img/202505181134116.png)

复制问题给AI，发现是缺少东西，检查librime和plum发现未添加，最后添加上了

2.执行`build.bat`前未执行`build.bat all`

在添加子仓库后依然没有成功，再一遍文档时发现命令输错了

3.不支持ARM64

![image-20250518114236676](https://gitee.com/ppedmo/pic-go/raw/master/img/202505181142767.png)

vs加载数据

(开始没找到，后面在单个组件中找到的)

4.添加之后仍显示冲突

![image-20250518115934057](https://gitee.com/ppedmo/pic-go/raw/master/img/202505181159127.png)

![image-20250518140458284](https://gitee.com/ppedmo/pic-go/raw/master/img/202505181405418.png)

选错了



5.还是不行

![3e12c7dd7b51df56eb61b9b25df0c960](https://gitee.com/ppedmo/pic-go/raw/master/img/202505181636864.png)

查看帮助文档解决

缺少mfc组件

改成以下几个

![image-20250518163928620](https://gitee.com/ppedmo/pic-go/raw/master/img/202505181639677.png)

6.一直有弹窗，提示找不到rime.dll
![de2b068456693b8d0c39f79c78b3a3e7](https://gitee.com/ppedmo/pic-go/raw/master/img/202505181724502.png)

把64位的rime.dll放进output

# 调试问题：

1.重启算法还是不能输入中文

![image-20250518173746843](https://gitee.com/ppedmo/pic-go/raw/master/img/202505181737928.png)

2.在生成解决方案时，包内部编译错误

![image-20250518182116033](https://gitee.com/ppedmo/pic-go/raw/master/img/202505181821130.png)

关闭启用最小重新生成
