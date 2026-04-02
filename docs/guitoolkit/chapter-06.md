# 第六章：命令

## 本章概述

本部分描述对话框如何向 Abaqus/CAE 内核发出命令。

## 本章内容

- [命令概述](#命令概述)
- [内核和 GUI 进程](#内核和-gui-进程)
- [执行命令](#执行命令)
- [内核命令](#内核命令)
- [GUI 命令](#gui-命令)
- [AFXTargets](#afxtargets)
- [从 GUI 访问内核数据](#从-gui-访问内核数据)
- [接收内核数据更改通知](#接收内核数据更改通知)

---

## 命令概述

在 Abaqus/CAE 中有两类命令：内核命令（Kernel commands）和 GUI 命令（GUI commands）。

### Kernel commands（内核命令）

内核命令用于构建、分析和后处理有限元模型。内核命令记录在 Abaqus Scripting Reference Guide 中。

### GUI commands（GUI 命令）

GUI 命令被用户界面用来处理从用户那里收集的输入，并构建发送到内核执行的内核命令字符串。GUI 命令记录在 Abaqus GUI Toolkit Reference Guide 中。

---

## 内核和 GUI 进程

Abaqus/CAE 以两个进程执行：内核进程和 GUI 进程。

### Kernel process（内核进程）

内核进程保存 Abaqus/CAE 用于执行建模操作的所有数据和方法；例如，创建部件和网格划分装配。内核进程可以独立于 GUI 进程运行。

### GUI process（GUI 进程）

GUI 是用户指定 Abaqus/CAE 输入的便捷方式。内核命令字符串通过进程间通信（IPC）协议从 GUI 进程发送到内核进程。内核进程解释并执行内核命令字符串。如果内核命令抛出异常，异常会被传播回 GUI 进程，在那里应该被正确捕获和处理，通常是通过显示错误对话框。

---

## 执行命令

所有命令最终在内核进程中执行，但有几种方式可以完成此操作：

- 您可以使用命令行上的 `-start` 或 `-replay` 选项从文件执行内核命令。
- 您可以使用 File->Run Script 从文件执行内核命令。
- 您可以在 Abaqus/CAE CLI 中键入内核命令。
- GUI 模式基础设施可以将命令字符串从 GUI 发送到内核进程以执行。
- 您可以使用 `sendCommand` 函数直接从 GUI 发出内核命令。

### sendCommand 函数

`sendCommand` 函数接受三个参数：

- 一个必需的字符串参数，指定要在内核中执行的命令。
- 两个可选的布尔参数 `writeToReplay` 和 `writeToJournal`。

通常，您应该将 `sendCommand` 函数包装在 try 块中以捕获内核命令可能抛出的任何异常。

```python
from abaqusGui import sendCommand
try:
    sendCommand("mdb.customData.myCommand('Cmd-1', 50, 200)")
except ValueError as x:
    print('an exception was raised: ValueError: %s' % (x))
except:
    exc_type, exc_value = sys.exc_info()[:2]
    print('error. %s.%s'%(exc_type.__name__, exc_value))
```

---

## 内核命令

内核命令可以包括方法、对象和参数。

内核命令可以由以下部分组成：

```
object + method + arguments (keywords)
```

命令并不总是有对象甚至参数，但它们总是有方法。

---

## GUI 命令

GUI 命令设计为与模式协同工作。

模式执行命令处理并将命令发送到内核。本节描述如何构造和使用 GUI 命令。

### 构造 GUI 命令

使用 `AFXGuiCommand` 类来构造 GUI 命令。

`AFXGuiCommand` 类接受以下参数：

- **mode**：模式通过 GUI 中的控件激活，通常是菜单按钮。
- **method**：指定内核命令方法的字符串。
- **objectName**：指定内核命令对象的字符串。
- **registerQuery**：一个布尔值，指定是否在对象上注册查询。

### GUI 命令和当前对象

大多数 Abaqus/CAE 命令对当前对象进行操作；例如，当前视口或当前部件。

模式在解释 GUI 命令中指定的对象时识别一种特殊语法。如果您在某些存储库后面的方括号之间放置 `%s`，模式会用当前名称替换 `%s`。

支持的当前对象：

| 对象规格 | 模式解释 |
|---------|---------|
| `mdb.models[%s]` | 当前模型 |
| `mdb.models[%s].parts[%s]` | 当前部件 |
| `mdb.models[%s].sketches[%s]` | 当前草图 |
| `session.odbs[%s]` | 当前输出数据库 |
| `session.viewports[%s]` | 当前视口 |

### 目标和消息

Abaqus GUI Toolkit 采用目标/消息系统来实现 GUI 进程内的通信。

消息由两部分组成：

- **消息类型**：指示发生了什么类型的事件。
- **消息 ID**：标识消息的发送者。

两个最常见的消息类型是 SEL_COMMAND 和 SEL_UPDATE。

---

## AFXTargets

AFXTargets 用于在 GUI 和内核之间进行通信。
