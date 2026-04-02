# 第十四章：自定义主窗口

## 本章概述

主窗口基类提供 GUI 基础设施以允许用户交互、模块操作和在视口中显示对象。本节描述如何通过从主窗口基类派生然后注册模块和工具集来向应用程序添加功能。

## 本章内容

- [模块和工具集](#模块和工具集)
- [Abaqus/CAE 主窗口示例](#abaqus-cae-主窗口示例)
- [图标](#图标)
- [颜色和 RGB 值](#颜色和-rgb-值)

---

## 模块和工具集

模块是交互式 Abaqus 应用程序的基本概念之一。模块将功能分组为逻辑单元；例如，创建部件的单元或网格划分装配的单元。

工具集类似于模块，因为它们将功能分组为逻辑单元。但是，工具集通常比模块包含更少的功能，因为工具集专注于一项特定任务；例如，分区。工具集可用于多个模块。

### 注册模块

注册模块将模块名称放入上下文栏中的模块组合框中。

```python
self.registerModule(displayedName='My Module',
    moduleImportName='myModuleGui')
```

### 注册工具集

工具集在主窗口注册后，在应用程序首次启动时可用。

```python
self.registerToolset(FileToolsetGui(),
    GUI_IN_MENUBAR|GUI_IN_TOOLBAR)
```

---

## Abaqus/CAE 主窗口示例

```python
from abaqusGui import *

class CaeMainWindow(AFXMainWindow):
    def __init__(self, app, windowTitle=''):
        # Construct the GUI infrastructure
        AFXMainWindow.__init__(self, app, windowTitle)
        
        # Register the "persistent" toolsets
        self.registerToolset(FileToolsetGui(),
            GUI_IN_MENUBAR|GUI_IN_TOOLBAR)
        self.registerToolset(ModelToolsetGui(),
            GUI_IN_MENUBAR)
        
        # Register modules
        self.registerModule('Part', 'Part')
        self.registerModule('Property', 'Property')
        self.registerModule('Assembly', 'Assembly')
```

---

## 图标

Abaqus GUI Toolkit 支持以下图标格式：XPM、BMP、GIF 和 PNG。

### 创建图标

```python
icon = afxCreatePNGIcon('myIcon.png')
FXLabel(self, 'A label with an icon', icon)
```

### XPM 图标

XPM 图像数据可以定义为 Python 字符串列表：

```python
blueIconData = [
    "12 12 2 1",
    "  c None s None",
    ". c #0000FF",
    "            ",
    "   ......   ",
    "  ........  ",
    " .......... ",
    "............",
    "............",
    "  ........  ",
    "   ......   ",
    "            "
]
blueIcon = FXXPMIcon(getAFXApp(), blueIconData)
```

---

## 颜色和 RGB 值

Abaqus GUI Toolkit 提供预定义的颜色和 RGB 值支持。

### 预定义颜色

- `FX_RED` - 红色
- `FX_GREEN` - 绿色
- `FX_BLUE` - 蓝色
- `FX_BLACK` - 黑色
- `FX_WHITE` - 白色

### RGB 值

您可以使用 RGB 值指定自定义颜色：

```python
# RGB values are specified as hex strings
color = "#FF0000"  # Red
```
