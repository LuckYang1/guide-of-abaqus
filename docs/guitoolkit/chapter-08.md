# 第八章：创建 GUI 模块

## 本章概述

本节描述如何创建 GUI 模块。

## 创建 GUI 模块的步骤

要创建新的 GUI 模块，您必须遵循以下步骤：

1. 从模块基类派生一个新类。
2. 在菜单栏中创建菜单。
3. 在工具栏中创建图标（可选）。
4. 在工具箱中创建图标（可选）。
5. 创建模式以从用户收集输入并发出命令。模式包括过程和对话框。
6. 创建处理模块模式未处理的任何特殊行为的方法（可选）。

## 本章内容

- [检查 GUI 模块示例](#检查-gui-模块示例)
- [注册 GUI 模块](#注册-gui-模块)
- [切换到 GUI 模块](#切换到-gui-模块)

---

## 检查 GUI 模块示例

本节显示如何创建模块 GUI。

AFXModuleGui 基类提供各种模块基础设施支持功能。例如，AFXModuleGui 基类跟踪模块的菜单及其工具栏和工具箱图标。

### 派生新模块类

要创建您自己的模块 GUI，首先从 AFXModuleGui 基类派生一个新类。

```python
from abaqusGui import *

class MyModuleGui(AFXModuleGui):
    def __init__(self):
        mw = getAFXApp().getAFXMainWindow()
        AFXModuleGui.__init__(self, moduleName='My Module',
            displayTypes=AFXModuleGui.PART)
        # Menu items
        menu = AFXMenuPane(self)
        AFXMenuTitle(self, '&Menu1', None, menu)
        AFXMenuCommand(self, menu, '&Item 1', None, mode_1,
            AFXMode.ID_ACTIVATE)
```

### 树选项卡

默认情况下，当用户切换到自定义模块时，TreeToolsetGui 中的选项卡不可见。

### 菜单栏项目

菜单栏项目由控制菜单窗格的菜单标题组成。

### 工具栏项目

工具栏项目显示在菜单栏下方的主窗口顶部，由包含图标的按钮组成。

### 工具箱项目

工具箱项目显示在主窗口左边缘，由包含图标的按钮组成。

### 注册工具集

模块可以通过简单注册来包含工具集。

### 内核模块初始化

GUI 模块被设计为向内核模块提供接口。

当 GUI 从用户收集输入后，它构建一个命令字符串并发送到内核进行处理。

```python
def getKernelInitializationCommand(self):
    return 'import myModule'
```

### 实例化 GUI 模块

模块 GUI 代码的最后一步是构造模块：

```python
MyModuleGui()
```

---

## 注册 GUI 模块

要使 GUI 模块对 GUI 基础设施可访问，必须在主窗口代码中注册模块：

```python
self.registerModule(displayedName='My Module',
    moduleImportName='myModuleGui')
```

---

## 切换到 GUI 模块

当用户从上下文栏中的模块列表中选择模块时，GUI 基础设施调用当前 GUI 模块的 deactivate 方法，并调用用户选择的 GUI 模块的 activate 方法。

```python
switchModule('My Module')
```
