# 第三章：构建对话框

## 本章概述

本部分描述对话框的组件以及如何使用 Abaqus GUI Toolkit 创建这些组件。

## 本章内容

- [Widgets（控件）](#widgets-控件)
- [Layout managers（布局管理器）](#layout-managers-布局管理器)
- [Dialog boxes（对话框）](#dialog-boxes-对话框)

---

## Widgets（控件）

本节描述如何在应用程序中创建控件。

Abaqus GUI Toolkit 中有很多控件；但是，这里只描述最常用的控件。您应该参阅 Abaqus GUI Toolkit Reference Guide 以获取控件类的完整列表。

### 标签和按钮

本节描述 Abaqus GUI Toolkit 中使用标签和按钮的控件。

#### 关于标签和按钮

Abaqus GUI Toolkit 中的多个控件支持标签。

例如，如果您想在文本字段前放置标签，应该使用 AFXTextField，而不是创建水平框架并添加标签控件和文本字段控件。以下部分描述支持标签的特定控件。

标签和按钮构造函数都接受文本字符串参数。此文本字符串可以由三部分组成，每部分用 `\t` 分隔。文本字符串的三部分是：

**Text（文本）**：控件显示的文本。

**Tip text（提示文本）**：将鼠标指针悬停在控件上一小段时间时显示的文本。如果控件只有一个关联的图标，则必须提供提示文本。

**Help text（帮助文本）**：在应用程序状态栏中显示的文本（假设应用程序有状态栏）。

此外，您可以通过在文本中的一个字符前加 & 符号来为控件定义键盘加速器。例如，如果为按钮指定字符串 `&Calculate`，按钮标签将如图 1 所示。您可以按 Alt 键和 C 键来使用加速器调用按钮。

#### Labels（标签）

FXLabel 控件显示只读字符串。FXLabel 还可以显示可选图标。

```python
FXLabel(parent, 'This is an FXLabel.\tThis is\nthe tooltip')
```

#### Push buttons（按钮）

FXButton 控件提供用户可以单击以触发操作的按钮。

#### Check buttons（复选按钮）

FXCheckButton 控件提供用户可以单击以切换选项开关状态的小框。

#### Radio buttons（单选按钮）

FXRadioButton 控件提供一组中只能选择一个的选项。

#### Menu buttons（菜单按钮）

AFXMenuButton 控件在按下时显示菜单窗格。

#### Popup menus（弹出菜单）

您可以创建弹出菜单，当用户在控件上单击鼠标右键 3 时显示。

#### Toolbar and toolbox buttons（工具栏和工具箱按钮）

AFXToolButton 控件在按钮中不显示文本，但按钮通常有工具提示。

#### Flyout buttons（飞出按钮）

AFXFlyoutButton 控件显示飞出弹出窗口。

#### Color buttons（颜色按钮）

AFXColorButton 控件显示一个按钮，单击该按钮会显示颜色选择对话框。

### 文本控件

本节描述 Abaqus GUI Toolkit 中允许用户输入文本的控件。

#### Single line text field widget（单行文本字段控件）

AFXTextField 控件提供单行文本字段。

#### Multi-line text widget（多行文本控件）

FXText 控件提供多行文本区域。

### Lists and combo boxes（列表和组合框）

本节描述 Abaqus GUI Toolkit 中允许您从列表中选择一个或多个项目的控件。

当 GUI 中有足够空间并且同时显示所有或大部分选择时，您使用列表控件。

当您想节省 GUI 中的空间并且只显示当前选择时，您使用组合框。

#### Lists（列表）

AFXList 允许从其项目中进行一个或多个选择。

AFXList 支持以下选择策略：

- **LIST_SINGLESELECT**：用户可以选择零个或一个项目。
- **LIST_BROWSESELECT**：始终选择一个项目。
- **LIST_MULTIPLESELECT**：用户可以选择零个或多个项目。
- **LIST_EXTENDEDSELECT**：用户可以选择零个或多个项目；允许拖动、Shift 选择和 Ctrl 选择。

#### List boxes（列表框）

AFXListBox 是下拉列表框，允许用户从列表中选择一个项目。

#### Combo boxes（组合框）

AFXComboBox 允许用户从列表中选择或输入自己的值。

### Range widgets（范围控件）

本节描述 Abaqus GUI Toolkit 中允许用户选择一系列值的控件。

#### Spinners（微调框）

AFXSpinner 控件允许用户通过单击控件的箭头来选择一系列值中的一个。

### Tree widgets（树形控件）

本节描述 Abaqus GUI Toolkit 中的树形控件。

#### Tree list（树形列表）

FXTreeList 控件以分层树结构显示项目。

### Table widget（表格控件）

AFXTable 控件以类似电子表格的方式排列项目。

#### Table widget layout（表格控件布局）

AFXTable 控件布局的表格可以有作为标题的前导行和前导列。

#### Table constructor（表格构造函数）

AFXTable 构造函数定义如下：

```python
AFXTable(p, numVisRows, numVisColumns, numRows, numColumns,
tgt=None, sel=0, opts=AFXTABLE_NORMAL,
x=0, y=0, w=0, h=0,
pl=DEFAULT_MARGIN, pr=DEFAULT_MARGIN,
pt=DEFAULT_MARGIN, pb=DEFAULT_MARGIN)
```

#### Rows and columns（行和列）

表格支持前导行和前导列。前导行显示在表格顶部，前导列显示在表格左侧。

#### Spanning（跨距）

您可以使标题行或列中的项目跨越多行或多列。

#### Justification（对齐）

默认情况下，表格显示左对齐的条目。您可以使用以下表格方法更改项目的对齐方式：

- `setColumnJustify(column, justify)`
- `setItemJustify(row, column, justify)`

#### Editing（编辑）

默认情况下，表格中的所有项目都不可编辑。要使表格中的所有项目可编辑，您必须在表格构造函数中指定 AFXTABLE_EDITABLE。

#### Types（类型）

默认情况下，表格中的所有项目都是文本项目。但是，表格控件还支持 BOOL、COLOR、FLOAT、ICON、INT、LIST 和 TEXT 项目。

### Miscellaneous widgets（其他控件）

#### Progress bar（进度条）

AFXProgressBar 控件显示操作进度的视觉指示。

### The create method（create 方法）

大多数控件在创建后需要调用 create() 方法来初始化底层数据结构。

### Widgets and fonts（控件和字体）

Abaqus GUI Toolkit 提供以下字体选项：

- FONT_TIMESROMAN
- FONT_HELVETICA
- FONT_COURIER
- FONT_SERIF
- FONT_SANSSERIF
- FONT_MONOSPACE
