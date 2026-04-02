# 第五章：对话框

## 本章概述

本节描述您可以使用 Abaqus GUI Toolkit 创建的对话框。

## 本章内容

- [关于对话框](#关于对话框)
- [Modal versus modeless（模态与非模态）](#modal-versus-modeless-模态与非模态)
- [Showing and hiding dialog boxes（显示和隐藏对话框）](#showing-and-hiding-dialog-boxes-显示和隐藏对话框)
- [Message dialog boxes（消息对话框）](#message-dialog-boxes-消息对话框)
- [Custom dialog boxes（自定义对话框）](#custom-dialog-boxes-自定义对话框)
- [Data dialog boxes（数据对话框）](#data-dialog-boxes-数据对话框)
- [Common dialog boxes（通用对话框）](#common-dialog-boxes-通用对话框)

---

## 关于对话框

Abaqus GUI Toolkit 中提供以下常用类型的对话框：消息对话框、自定义对话框、数据对话框和通用对话框。

### Message dialog boxes（消息对话框）

消息对话框允许您发布错误、警告或信息消息。

### Custom dialog boxes（自定义对话框）

自定义对话框允许您构建任何自定义界面。但是，您必须提供使对话框按要求运行所需的基础设施。

### Data dialog boxes（数据对话框）

数据对话框为用户输入数据的对话框提供支持。数据对话框设计用于向表单提供用户输入，表单会自动发出命令。

### Common dialog boxes（通用对话框）

通用对话框是提供在许多应用程序中常见的标准功能的对话框。文件选择对话框是典型的通用对话框。

---

## Modal versus modeless（模态与非模态）

对话框可以是模态的或非模态的。

### Modal（模态）

模态对话框阻止与应用程序其余部分的交互，直到用户关闭对话框。

### Modeless（非模态）

非模态对话框允许用户在对话框显示时与 GUI 的其他部分交互。在 Abaqus/CAE 中，除了提示外的所有辅助对话框都应该是模态对话框。

对话框本身不定义为模态或非模态——该行为是从用于显示对话框的方法获得的。

---

## Showing and hiding dialog boxes（显示和隐藏对话框）

对话框有 show 和 hide 方法，用于从屏幕上显示或隐藏对话框。

在大多数情况下，您不需要调用这些方法，因为模式基础设施会为您调用它们。但是，您可能想编写自己的 show 和 hide 方法来执行一些特殊处理，这些处理将在应用程序显示或隐藏对话框之前执行。

```python
def show(self):
    # Do some special processing here.
    ...
    # Call base class method.
    AFXDataDialog.show(self)

def hide(self):
    # Do some special processing here.
    ...
    # Call base class method.
    AFXDataDialog.hide(self)
```

---

## Message dialog boxes（消息对话框）

AFXMessageDialog 类通过强制执行对话框的某些特性（例如窗口标题和消息符号）来扩展 FXMessageDialog 类。

### 消息对话框类型

#### Error dialog boxes（错误对话框）

错误对话框显示错误消息。

#### Warning dialog boxes（警告对话框）

警告对话框显示警告消息。

#### Information dialog boxes（信息对话框）

信息对话框显示信息性消息。

#### Specialized message dialog boxes（专用消息对话框）

专用消息对话框提供特定功能。

---

## Custom dialog boxes（自定义对话框）

自定义对话框允许您构建任何自定义界面。

### 关于自定义对话框

#### 构造函数

AFXDialog 构造函数定义对话框的父级、标题和选项。

```python
AFXDialog(parent, title, opts=0, x=0, y=0, w=0, h=0)
```

#### Sizing and location（大小和位置）

对话框构造函数中指定的大小和位置是初始建议大小和位置。实际大小可能会有所不同，具体取决于对话框内容。

#### Action area（操作区域）

操作区域通常包含确定、取消、应用等按钮。

#### Custom action area button names（自定义操作区域按钮名称）

您可以自定义操作区域中按钮的名称。

#### Action button handling（操作按钮处理）

对话框通常有确定、取消、应用等按钮。这些按钮的处理方式由 AFXDialog 类管理。

---

## Data dialog boxes（数据对话框）

数据对话框为用户输入数据的对话框提供支持。

### 关于数据对话框

AFXDataDialog 类扩展了 AFXDialog 类，为数据输入对话框提供支持。

#### 构造函数

AFXDataDialog 构造函数比 AFXDialog 构造函数更复杂，因为它需要与表单和模式交互。

#### Bailout

Bailout 是用户取消操作时执行的清理操作。

#### Constructor contents（构造函数内容）

数据对话框构造函数通常包含控件创建、布局设置和消息处理程序设置。

#### Transitions

数据对话框可以有过渡状态，例如步骤之间的转换。

#### Updating your GUI（更新 GUI）

当数据更改时，您可能需要更新 GUI。

#### Action area（操作区域）

数据对话框的操作区域与自定义对话框类似。

---

## Common dialog boxes（通用对话框）

通用对话框是提供标准功能的对话框。

### File/Directory selector（文件/目录选择器）

AFXFileSelector 提供文件选择功能。

### Print dialog box（打印对话框）

AFXPrintDialog 提供打印功能。

### Color selector dialog box（颜色选择对话框）

AFXColorSelector 提供颜色选择功能。
