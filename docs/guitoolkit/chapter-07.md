# 第七章：模式（Modes）

## 本章概述

模式是一种收集用户输入、处理输入，然后向内核发出命令的机制。本节描述 Abaqus GUI Toolkit 中可用的模式。

## 本章内容

- [关于模式](#关于模式)
- [模式处理](#模式处理)
- [表单模式](#表单模式)
- [过程模式](#过程模式)
- [过程模式中的拾取](#过程模式中的拾取)

---

## 关于模式

模式通过 GUI 中的控件激活，通常是菜单按钮。一旦模式被激活，它负责：

1. 收集用户输入
2. 处理输入
3. 发送命令
4. 执行与模式或其发送的命令相关的任何错误处理

Abaqus GUI Toolkit 提供两种模式：

### Form modes（表单模式）

表单模式提供对话框接口。表单模式使用一个或多个对话框收集用户输入。

### Procedure modes（过程模式）

过程模式提供一种接口，通过在应用程序的提示区域中提示输入来引导用户完成一系列步骤。

---

## 模式处理

模式执行命令处理并将命令发送到内核。

当用户与 GUI 交互时，模式：

1. 从对话框收集用户输入
2. 将输入构建为内核命令字符串
3. 通过 IPC 协议将命令发送到内核进程
4. 接收并处理内核的响应

---

## 表单模式

表单模式提供对话框接口。

表单模式使用 AFXForm 类来管理对话框和数据输入。

### 表单示例

表单模式通常与 AFXDataDialog 结合使用来创建数据输入对话框。

---

## 过程模式

过程模式提供一种接口，通过在应用程序的提示区域中提示输入来引导用户完成一系列步骤。

过程模式使用 AFXProcedure 类作为基类。

### 过程模式示例

```python
class MyProcedure(AFXProcedure):
    def __init__(self, command):
        AFXProcedure.__init__(self, command)
        
    def getFirstStep(self):
        # Return the first step
        pass
        
    def getNextStep(self, currentStep):
        # Return the next step
        pass
```

---

## 过程模式中的拾取

过程模式通常需要用户通过在图形区域中拾取对象来输入。

### 拾取类型

- **点拾取（Point picking）**：用户单击以选择点。
- **对象拾取（Object picking）**：用户选择对象。
- **坐标拾取（Coordinate picking）**：用户输入坐标值。

### 拾取模式

Abaqus/CAE 使用 AFXPickMode 来管理拾取操作。
