# 第十一章：创建应用程序

## 本章概述

本节解释如何创建应用程序，例如 Abaqus/CAE。它还描述负责运行应用程序的高级基础设施。

## 本章内容

- [关于 GUI 代码](#关于-gui-代码)
- [启动脚本](#启动脚本)
- [许可和执行](#许可和执行)
- [应用程序对象](#应用程序对象)
- [主窗口](#主窗口)

---

## 关于 GUI 代码

创建自定义应用程序时，您需要创建以下组件：

1. **应用程序对象** - 管理应用程序的生命周期
2. **主窗口** - 提供用户界面的容器
3. **模块和工具集** - 提供具体功能
4. **模式** - 处理用户交互

### GUI 代码文件

典型的 GUI 应用程序包含以下文件：

- `application.py` - 应用程序入口点
- `mainWindow.py` - 主窗口实现
- `moduleGui.py` - GUI 模块定义
- `toolsetGui.py` - GUI 工具集定义
- `modes.py` - 模式定义

---

## 启动脚本

启动脚本初始化应用程序并启动事件循环。

```python
from abaqusGui import *

# Create the application object
app = AFXApp()

# Create the main window
mainWindow = MyMainWindow(app)

# Initialize and run
app.init(sys.argv)
app.run()
```

### 启动参数

启动脚本可以接受参数来控制应用程序的行为。

---

## 许可和执行

### 许可证配置

应用程序启动时检出的许可证由应用程序配置控制。

### 执行方式

```bash
abaqus cae -custom myApplication -noStartup
```

---

## 应用程序对象

AFXApp 类是应用程序对象。

### 应用程序对象的方法

- `init(sys.argv)` - 初始化应用程序
- `run()` - 启动事件循环
- `exit()` - 退出应用程序

---

## 主窗口

AFXMainWindow 类提供主窗口。

### 主窗口组件

- 标题栏
- 菜单栏
- 工具栏
- 上下文栏
- 模块工具箱
- 绘图区域和画布
- 提示区域
- 消息区域
- 命令行界面
