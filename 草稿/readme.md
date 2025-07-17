根据提示分为三个子项目

- **kdemo**（exe）：主程序，通过按钮点击弹出对话框
- **klogin**（dll）：提供登录对话框
- **kpurchase**（lib）：提供购买会员对话框

关键实现：

- 阴影效果通过 `QGraphicsDropShadowEffect` 实现
- 对话框通过动态链接库（klogin）和静态链接库（kpurchase）提供
- 主程序通过按钮点击事件调用库中的对话框接口