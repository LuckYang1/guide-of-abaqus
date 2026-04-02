# 第四章：布局管理器

## 本章概述

本节描述如何使用 Abaqus GUI Toolkit 中的各种布局管理器在对话框中排列控件。

## 本章内容

- [关于布局管理器](#关于布局管理器)
- [Padding and spacing（内边距和间距）](#padding-and-spacing-内边距和间距)
- [Horizontal and vertical frames（水平和垂直框架）](#horizontal-and-vertical-frames-水平和垂直框架)
- [Vertical alignment for composite children（复合子项的垂直对齐）](#vertical-alignment-for-composite-children-复合子项的垂直对齐)
- [General-purpose layout managers（通用布局管理器）](#general-purpose-layout-managers-通用布局管理器)
- [Row and column layout manager（行和列布局管理器）](#row-and-column-layout-manager-行和列布局管理器)
- [Resizable regions（可调整大小的区域）](#resizable-regions-可调整大小的区域)
- [Rotating regions（旋转区域）](#rotating-regions-旋转区域)
- [Tab books（选项卡簿）](#tab-books-选项卡簿)
- [Layout hints（布局提示）](#layout-hints-布局提示)
- [Layout examples（布局示例）](#layout-examples-布局示例)
- [Tips for specifying layout hints（布局提示规格技巧）](#tips-for-specifying-layout-hints-布局提示规格技巧)

---

## 关于布局管理器

布局管理器将其子项放置在其内部的某种排列中。

布局管理器使用布局提示和打包样式的组合来确定如何放置和调整其子项的大小。Abaqus GUI Toolkit 中的布局管理器计算相对大小和相对位置，而不是绝对坐标。这种相对方法会自动处理诸如不同字体大小和窗口调整大小等更改。

Abaqus GUI Toolkit 中提供以下布局管理器：

### FXHorizontalFrame

水平排列控件。有关更多信息，请参阅水平和垂直框架。

### FXVerticalFrame

垂直排列控件。有关更多信息，请参阅水平和垂直框架。

### AFXVerticalAligner

垂直对齐其子项的第一个子项。有关更多信息，请参阅复合子项的垂直对齐。

### FXPacker

以一般方式排列控件。有关更多信息，请参阅通用布局管理器。

### AFXDialog

提供与 FXPacker 相同的功能。有关更多信息，请参阅通用布局管理器。

### FXGroupBox

提供与 FXPacker 相同的功能，但允许有标题边框。有关更多信息，请参阅通用布局管理器。

### FXMatrix

以行和列排列控件。有关更多信息，请参阅行和列布局管理器。

### FXSplitter

垂直或水平分割区域，并允许您调整区域大小。有关更多信息，请参阅可调整大小的区域。

### FXSwitcher

管理堆叠在一起的子项（旋转区域）。有关更多信息，请参阅旋转区域。

### FXTabBook

一次显示一个选项卡或一页控件。用户通过单击选项卡按钮来选择要查看的选项卡。有关更多信息，请参阅选项卡簿。

---

## Padding and spacing（内边距和间距）

布局管理器（和大多数控件）提供一些默认内边距，以便控件彼此分开。

这些值通常位于控件参数列表的末尾。例如：

```python
FXPacker(…, pl, pr, pt, pb, …)
```

通常，您应该接受内边距的默认值。但是，如果您有嵌套的布局管理器，应将内边距值设置为零。

布局管理器还提供其子项之间的间距。这些值通常位于控件参数列表的末尾。例如：

```python
FXPacker(…, hs, vs)
```

通常，您应该接受间距的默认值。

---

## Horizontal and vertical frames（水平和垂直框架）

FXHorizontalFrame 和 FXVerticalFrame 是简单的布局管理器，分别在行或列中排列控件。

---

## Vertical alignment for composite children（复合子项的垂直对齐）

AFXVerticalAligner 控件垂直对齐其子项。

---

## General-purpose layout managers（通用布局管理器）

Abaqus GUI Toolkit 包括三个具有相似布局功能的通用布局管理器。

### FXPacker

FXPacker 是一个通用布局管理器。

### AFXDialog

AFXDialog 提供与 FXPacker 相似的功能。因此，您不需要在对话框中提供顶层布局管理器作为第一个子项；您可以改用对话框的布局功能。

### FXGroupBox

FXGroupBox 提供与 FXPacker 相同的功能。此外，FXGroupBox 可以显示围绕其子项的标签边框。Abaqus/CAE 使用 FRAME_GROOVE 标志在组框的子项周围产生细边框。

---

## Row and column layout manager（行和列布局管理器）

FXMatrix 以行和列排列控件。

---

## Resizable regions（可调整大小的区域）

FXSplitter 控件垂直或水平分割区域。用户可以拖动区域之间的光标并调整区域大小。

---

## Rotating regions（旋转区域）

FXSwitcher 控件管理堆叠在一起的子项。

FXSwitcher 允许您通过发送消息或调用其 setCurrent 方法来选择应显示的子项。

---

## Tab books（选项卡簿）

FXTabBook 控件使用"选项卡项"一次控制一个"页面"的显示。

FXTabBook 期望其奇数子项是 FXTabItems，偶数子项是某种布局管理器。布局管理器包含要显示在该页面中的所有控件。单击选项卡项将显示与该选项卡关联的布局管理器（及其所有子项），同时隐藏所有其他布局管理器。

您可以嵌套选项卡簿以在选项卡内提供选项卡。

---

## Layout hints（布局提示）

FXPacker、FXTopWindow 和 FXGroupBox 控件在其子项中接受布局提示。

### 布局提示详解

支持以下布局提示：

#### LAYOUT_SIDE_TOP

将控件附加到腔体的顶侧。LAYOUT_SIDE_TOP 是默认布局提示。

#### LAYOUT_SIDE_BOTTOM

将控件附加到腔体的底侧。

#### LAYOUT_SIDE_LEFT

将控件附加到腔体的左侧。

#### LAYOUT_SIDE_RIGHT

将控件附加到腔体的右侧。

所有布局管理器支持以下布局提示：

- **LAYOUT_LEFT（默认）和 LAYOUT_RIGHT**：布局管理器将控件放置在容器中剩余空间的左侧或右侧。
- **LAYOUT_TOP（默认）和 LAYOUT_BOTTOM**：布局管理器将控件放置在容器中剩余空间的顶部或底部。
- **LAYOUT_CENTER_X 和 LAYOUT_CENTER_Y**：布局管理器在父项的 X 或 Y 方向上将控件居中。
- **LAYOUT_FILL_X 和 LAYOUT_FILL_Y**：这些布局提示使布局管理器可以拉伸或收缩控件以适应可用空间。
- **LAYOUT_FIX_WIDTH 和 LAYOUT_FIX_HEIGHT**：这些选项将控件的宽度或高度修复为构造函数中指定的值。

---

## Layout examples（布局示例）

以下示例使用默认布局提示一次创建三个按钮。

### 示例 1

第一个示例首先在腔体左侧创建单个按钮。

### 示例 2

第二个示例说明如何使用非默认布局提示。

---

## Tips for specifying layout hints（布局提示规格技巧）

- 不要过度指定布局提示。在很多情况下，默认值就是您需要的，您不需要指定提示。
- 用简单的行和列来思考，尽可能使用水平或垂直框架。
- 为避免累积过多的内边距，请在嵌套布局管理器中将内边距设置为零。
