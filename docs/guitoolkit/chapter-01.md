# 第一章：简介

## 本章概述

本章提供 Abaqus GUI Toolkit 的概述。

Abaqus GUI Toolkit 是 Abaqus Process Automation 工具之一，允许您修改和扩展 Abaqus/CAE 图形用户界面（GUI）的功能，使更广泛的用户能够生成更高效的 Abaqus 解决方案。

## 本章内容

- [我能用 Abaqus GUI Toolkit 做什么？](#我能用-abaqus-gui-toolkit-做什么)
- [使用 Abaqus GUI Toolkit 的先决条件](#使用-abaqus-gui-toolkit-的先决条件)
- [Abaqus GUI Toolkit 基础](#abaqus-gui-toolkit-基础)
- [Abaqus GUI Toolkit 用户指南的组织结构](#abaqus-gui-toolkit-用户指南的组织结构)

---

## 我能用 Abaqus GUI Toolkit 做什么？

您可以使用 Abaqus GUI Toolkit 定制 Abaqus 产品。

定制 Abaqus 产品有多种方式：

- **User subroutines（用户子程序）** 允许您更改 Abaqus/Standard 和 Abaqus/Explicit 计算分析结果的方式。用户子程序的信息请参阅 Abaqus User Subroutines Guide。

- **Environment files（环境文件）** 允许您更改各种默认设置。环境文件的信息请参阅 Abaqus Execution Guide。

- **Kernel scripts（内核脚本）** 允许您创建新的函数来执行建模或后处理任务。内核脚本的信息请参阅 Abaqus Scripting User's Guide。

- **GUI scripts（GUI 脚本）** 允许您创建新的图形用户界面。GUI 脚本在本指南中描述。

Abaqus GUI Toolkit 提供了编程例程，允许您创建或修改 GUI 的组件。工具包允许您执行以下操作：

### 创建新的 GUI 模块（GUI module）

GUI 模块是类似功能的分组，例如 Abaqus/CAE 中的 Part 模块。

### 创建新的 GUI 工具集（GUI toolset）

GUI 工具集类似于 GUI 模块，因为它将类似功能分组在一起，但通常包含更具体的功能，可被一个或多个 GUI 模块使用。Abaqus/CAE 中的 Datum 工具就是 GUI 工具集的一个例子。

### 创建新的对话框（Dialog boxes）

Abaqus GUI Toolkit 提供了完整的控件（widget）库，您可以用它来构建自己的对话框。但是，Abaqus GUI Toolkit 不允许您修改现有的 Abaqus/CAE 对话框。

### 移除 Abaqus/CAE GUI 模块和工具集

您可以选择在应用程序中包含哪些 GUI 模块和省略哪些 GUI 模块。例如，Abaqus/Viewer 应用程序不包含建模相关的 GUI 模块；它只包含 Visualization 模块。

### 移除某些顶级菜单或这些菜单中的某些项目

例如，您可以移除整个顶级 Viewport 菜单以防止用户操作视口，或者您可以移除 File 菜单中的 Import 和 Export 菜单项。

### 对 Abaqus/CAE GUI 模块和工具集进行有限的更改

有关更多信息，请参阅修改和访问 Abaqus/CAE GUI 模块和工具集。

> **重要**：Abaqus GUI Toolkit 不能在 Abaqus/CAE 外部运行；它必须与 Abaqus/CAE 一起使用，以便基础设施能够正常工作。

---

## 使用 Abaqus GUI Toolkit 的先决条件

要使用 Abaqus GUI Toolkit 编写应用程序，您需要具备以下方面的经验：

### Python 编程

在编写 Abaqus/CAE 内核脚本之前，您应该具备 Python 语言的一些经验。在编写 GUI 应用程序时，您应该具有类似的经验。

### Abaqus 内核命令（Kernel commands）

GUI 的最终目标是向内核发送命令以执行；因此，您应该了解内核命令的工作原理。

### 面向对象编程（Object-oriented programming）

Python 是一种面向对象的语言，编写应用程序通常包括派生您自己的新类、为它们编写方法以及操作它们的数据。您应该理解面向对象编程的概念。

### GUI 设计

根据应用程序的复杂性，用户界面设计和可用性测试方面的培训可能会有所帮助。这将帮助您创建一个既直观又易于使用的应用程序。

Abaqus 提供涵盖 Python、内核脚本和 GUI 设计的培训课程。有关更多信息，请联系您当地的销售办公室。GUI 设计培训也可从许多独立的培训组织获得。

---

## Abaqus GUI Toolkit 基础

Abaqus GUI Toolkit 是 FOX GUI Toolkit 的扩展，就像 Abaqus Scripting Interface 是 Python 编程语言的扩展一样。

FOX（Free Objects for X 的缩写）是一个现代的、面向对象的、平台无关的 GUI 工具包。由于 Abaqus GUI Toolkit 是平台无关的，一旦您为某个平台编写了应用程序，您就可以在所有支持的平台上运行该应用程序——您不需要更改源代码。

Abaqus GUI Toolkit 生成的用户界面在所有平台上看起来都相似。这是由于工具包的架构。虽然应用程序编程接口（API）在所有平台上都是相同的，但调用操作系统 GUI 库的方式不同——在 Linux 系统上调用 Xt 库，而在 Windows 系统上调用 Win32 库。这些差异对应用程序开发人员是隐藏的。

由于 FOX GUI Toolkit 是面向对象的，它允许开发人员通过从基础工具包派生新类来轻松扩展其功能。Abaqus GUI Toolkit 利用这一特性，添加了 Abaqus GUI 所需的特殊功能。以 FX 开头的类名是标准 FOX 库的一部分；例如，FXButton。以 AFX 开头的类名是 Abaqus 对 FOX 库的扩展的一部分；例如，AFXDialog。当相同的类同时存在 FX 和 AFX 前缀时（例如 FXTable 和 AFXTable），您应该使用 AFX 版本，因为它为使用 Abaqus 构建应用程序提供了增强的功能。

---

## Abaqus GUI Toolkit 用户指南的组织结构

本指南按功能组织，旨在通过解释如何使用工具包的组件并提供示例代码片段来指导开发人员完成编写应用程序的过程。提供了单独的 Abaqus GUI Toolkit Reference Guide，其中包含所有工具包调用的字母顺序列表。

Abaqus GUI Toolkit 基于 FOX GUI 工具包。虽然本指南解释了 FOX 工具包的一些基本概念，但没有提供 FOX 工具包许多其他方面的详细信息。有关 FOX GUI 工具包的更多详细信息，请参阅 FOX 网站（http://www.fox-toolkit.org）。

本指南由以下部分组成：

### Widgets（控件）

本节描述 Abaqus GUI Toolkit 中一些最常用的控件。

### Layout managers（布局管理器）

本节描述如何使用 Abaqus GUI Toolkit 中的各种布局管理器在对话框中排列控件。

### Dialog boxes（对话框）

本节描述您可以使用 Abaqus GUI Toolkit 创建的对话框。

### Commands（命令）

在采用图形用户界面的应用程序中，界面必须收集用户的输入并将该输入传达给应用程序。此外，图形用户界面必须根据应用程序的状态保持其状态最新。本节描述如何使用 Abaqus GUI Toolkit 和 Abaqus/CAE 中的两种命令（内核命令和 GUI 命令）完成这些任务。

### Modes（模式）

模式是一种收集用户输入、处理该输入，然后向内核发出命令的机制。本节描述 Abaqus GUI Toolkit 中可用的模式。

### Creating a GUI module（创建 GUI 模块）

本节描述如何创建 GUI 模块。

### Creating a GUI toolset（创建 GUI 工具集）

本节描述如何创建 GUI 工具集。

### Customizing an existing module or toolset（自定义现有模块或工具集）

前面的章节描述了如何创建新的模块或工具集。或者，Abaqus GUI Toolkit 允许您从现有模块或工具集派生新模块或工具集，并从中添加或删除功能。

### Creating an application（创建应用程序）

本节解释如何创建应用程序，例如 Abaqus/CAE。它还描述了负责运行应用程序的高级基础设施。

### The application object（应用程序对象）

本节描述 Abaqus 应用程序对象。应用程序对象管理消息队列、计时器、任务、GUI 更新和其他系统设施。

### The main window（主窗口）

本节描述 Abaqus 主窗口的布局、组件和行为。

### Customizing the main window（自定义主窗口）

主窗口基类提供 GUI 基础设施以允许用户交互、模块操作和在视口中显示对象。本节描述如何通过从主窗口基类派生然后注册模块和工具集来向应用程序添加功能。
