# 模块划分

#### 1. 主函数模块 (main.cpp)

- 负责初始化 Qt 应用程序，加载翻译文件，创建并显示绘图板窗口。

#### 2. 绘图板窗口模块 (DrawingBoardWidget.h 和 DrawingBoardWidget.cpp)

- 包含各种绘图工具按钮，如矩形、椭圆、三角形等，以及旋转按钮。
- 处理按钮点击事件，根据用户选择的按钮设置绘图类型。
- 加载样式表文件，设置窗口的样式。

#### 3. 绘图区域模块 (DrawWidget.h 和 DrawWidget.cpp)

- 继承自 `QOpenGLWidget`，负责处理绘图操作。
- 处理鼠标事件（按下、移动、释放），根据用户的操作绘制相应的图形。
- 支持图形的旋转操作，可旋转 0°、90°、180° 和 270°。

#### 4. 图形数据模块

- 定义了各种图形的数据类，如 `CRectangleData`、`CEllipseData`、`CTriangleData` 等。
- 每个数据类包含图形的起始位置、尺寸等信息，并提供相应的访问和设置方法。

#### 5. 系统数据模块 (SystemData.h 和 SystemData.cpp)

- 管理所有图形数据的集合，提供单例模式获取系统数据实例。
- 在析构函数中负责释放所有图形数据的内存。

### 构建和依赖

- 使用 CMake 进行项目构建，要求 CMake 版本为 3.10 或更高。
- 依赖 Qt5 库，包括 Core、Widgets、Gui、Network、Svg 和 LinguistTools 模块。





# 主要类及功能

#### 1. `CDrawingBoardWidget`

- **功能**：作为主界面类，负责创建和管理绘图板界面，包含各种绘图工具按钮（如矩形、椭圆、三角形等），并处理按钮点击事件。
- **相关文件**：DrawingBoardWidget.h、DrawingBoardWidget.cpp

#### 2. `CDrawWidget`

- **功能**：继承自`QOpenGLWidget`，负责实际的绘图操作，处理鼠标事件（如按下、移动、释放）以绘制图形，支持图形旋转。
- **相关文件**：DrawWidget.h、DrawWidget.cpp

#### 3. 图形数据类

- **功能**：用于存储各种图形的相关数据，如起始位置、尺寸、半径等。
- 相关类及文件：
  - `CRectangleData`：矩形数据类，RectangleData.h、RectangleData.cpp
  - `CEllipseData`：椭圆数据类，EllipseData.h、EllipseData.cpp
  - `CTriangleData`：三角形数据类，TriangleData.h、TriangleData.cpp
  - `CLineData`：直线数据类，LineData.h、LineData.cpp
  - `CTextData`：文本数据类，TextData.h、TextData.cpp
  - `CPentagonData`：五边形数据类，PentagonData.h、PentagonData.cpp
  - `CHexagonData`：六边形数据类，HexagonData.h、HexagonData.cpp
  - `CFreehandData`：自由手绘数据类，FreehandData.h、FreehandDat.cpp

#### 4. `CSystemData`

- **功能**：作为单例类，负责管理所有图形数据，提供获取系统数据的静态方法。
- **相关文件**：SystemData.h、SystemData.cpp

#### 5. `CContentEdit`

- **功能**：继承自`QLineEdit`，用于输入文本内容，处理键盘事件，当按下回车键时发射信号传递文本内容。
- **相关文件**：ContentEdit.h、ContentEdit.cpp

# 主要功能实现

#### 1. 绘图功能

在`CDrawWidget`的`paintEvent`方法中，根据`CSystemData`中存储的图形数据，使用`QPainter`绘制各种图形。同时，在鼠标事件处理方法中（如`mousePressEvent`、`mouseMoveEvent`、`mouseReleaseEvent`），根据当前选择的图形类型，动态绘制图形。

#### 2. 图形旋转功能

`CDrawWidget`支持图形旋转，通过`RotateLeft`和`RotateRight`方法改变旋转角度，在`paintEvent`中根据旋转角度对绘图坐标系进行变换。

#### 3. 文本输入功能

通过`CContentEdit`类实现文本输入，当用户输入文本并按下回车键时，将文本内容传递给`CDrawWidget`进行绘制。

# 项目概况

图形旋转：具备图形旋转功能，支持向左和向右旋转，旋转角度有 90 度、180 度和 270 度。

界面交互：界面采用布局管理器进行设计，左侧为功能按钮区域，右侧为绘图区域。按钮有正常和选中两种样式，方便用户区分当前选择的功能。