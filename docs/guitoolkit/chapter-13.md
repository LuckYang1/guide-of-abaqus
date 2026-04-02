# 第十三章：主窗口

## 本章概述

本节描述 Abaqus 主窗口的布局、组件和行为。

## 主窗口组件

### 标题栏

标题栏显示应用程序名称和版本。

### 菜单栏

菜单栏提供对应用程序功能的访问。

### 工具栏

工具栏提供对常用命令的快速访问。

### 上下文栏

上下文栏包含模块组合框和其他上下文相关控件。

### 模块工具箱

模块工具箱包含当前模块常用工具的图标。

### 绘图区域和画布

画布提供无限空间来创建和操作视口。绘图区域是画布可见部分的窗口。

### 提示区域

提示区域显示提示以引导用户，以及进行中的工作（WIP）消息。

### 消息区域

应用程序使用消息区域显示信息和警告消息。

```python
mainWindow = getAFXApp().getAFXMainWindow()
mainWindow.writeToMessageArea('Warning: Some items failed!')
```

### 命令行界面

命令行界面（CLI）提供到内核侧 Python 命令解释器的接口。

用户可以在 CLI 中输入 Abaqus 脚本接口命令，然后发送到内核处理。

```python
# Hide the CLI
mainWindow = getAFXApp().getAFXMainWindow()
mainWindow.hideCli()
```
