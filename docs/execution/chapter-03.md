---
title: 执行程序概述
description: Abaqus 执行指南章节
---

# 执行程序概述

## 关于执行程序

### 概述

Abaqus 通过 Abaqus 执行程序来运行。在下述讨论中，运行执行程序的命令假定为 abaqus。但是，您可以使用任何您选择的别名自定义执行程序来运行 Abaqus。（有关详细信息，请参阅 Abaqus Configuration Guide。）

abaqus 命令在执行程序中有详细描述。以下部分包含有关运行 Abaqus 作业的更多信息：

- 环境文件设置
- 内存和磁盘资源管理
- 并行执行
- 文件扩展名定义
- Fortran 单元号

### 约定

以下约定在这些部分中使用：

- 每个讨论都包含一个"命令摘要"部分，在左列提供命令语法，在右列提供其选项的语法。完整命令必须首先出现，然后是选项。在某些情况下，命令有多个单词，例如 abaqus fetch；您必须在发出任何选项语句之前输入命令的所有单词。
- 选项以粗体显示。它们可以以任何顺序出现，可以缩写。
- 默认选项带下划线 ( __ )。
- 方括号 ([ ]) 中的项目是可选的。
- 用竖线 ( | ) 分隔的列表中出现的项目是互斥的。
- 必须从大括号 ({ }) 中包含的值列表中选择一个值。
- 您必须以斜体提供值。
- 空格用作选项之间的分隔符，不能在等号之前或之后出现。
- 可以使用替代语法 -optionvalue 而不是 option=value 格式。

如果 abaqus 命令行上未提供所需信息，abaqus 程序将提示您输入。如果 abaqus 未带选项输入，则会提示输入所有选项。

### 环境设置

Abaqus 执行程序使用环境参数来自定义作业的执行。这些设置可以使用 Abaqus 环境文件之一进行更改：custom_v6.env 或 abaqus_v6.env。

如果同一作业参数在多个环境文件中定义，或在同一环境文件中多次定义，则将使用遇到的最后一个定义。此规则的一些例外情况在环境文件设置中注明。这些环境文件可用于自定义 Abaqus 的行为，包括修改默认选项。

### 选择 TCP/UDP 端口号

多个执行程序命令行选项（如 port 和 listenerport）需要您指定端口号。TCP/UDP 端口号范围从 0 到 65535。

端口 0 到 1023 是系统进程使用的知名端口（如 FTP、SSH、SMTP 等），不应使用。端口 1024 到 49151 是已注册端口，由软件供应商在 IANA 注册。这些端口可以使用，但您应小心不要与可能使用此端口的系统上安装的任何软件冲突。端口 49152 到 65535 是未保留的，只要没有其他应用程序使用它们，就可以自由使用。

端口可能被防火墙阻止。请联系您的系统管理员以确保您要指定的端口未被阻止。

您可以使用 netstat 命令获取有关 TCP/UDP 网络连接的信息。

## 执行程序

本节介绍使用 abaqus 命令运行 Abaqus。

本节包含以下子部分：

- Abaqus 执行
- Abaqus 协同仿真
- Abaqus 实用程序
- 将其他求解器输入翻译为 Abaqus 输入
- 将 Abaqus 输出翻译为另一种格式

### Abaqus 执行

本节介绍使用 abaqus 命令运行 Abaqus 以及使用 abaqus doc 命令运行 Abaqus 文档。

本节包含以下子部分：

- 获取信息
- Abaqus/Standard 和 Abaqus/Explicit 执行
- Abaqus 作业执行控制
- Abaqus/CAE 执行
- Abaqus/Viewer 执行
- 创建用户定义的可执行文件和子程序
- 优化执行
- 参数化研究
- Abaqus 文档

## 获取信息

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

Abaqus 执行程序可用于获取有关命令语法或有关安装和计算环境的信息。

### 命令摘要

```
abaqus {help | information = {environment | local | memory | release | support | system | all} [job = job-name] | whereami}
```

### 命令行选项

**help**：此选项打印 abaqus 命令语法摘要。

**information**：此选项将有关安装和生效环境的信息写入屏幕。所有信息请求都输出以下信息：当前版本、Abaqus 所在目录以及信息文件所在目录。

- 如果 information=environment，则显示环境文件选项的当前设置。
- 如果 information=local，则输出本地安装说明。
- 如果 information=memory，则输出有关为分析作业设置内存参数的一些建议。
- 如果 information=release，则提供有关在哪里找到当前版本说明的信息。
- 如果 information=support，则提供有关诊断硬件相关问题的信息。请在请求帮助时将此信息发送给系统支持人员。
- 如果 information=system，则提供有关系统软件和硬件资源的信息（操作系统级别、编译器级别、处理器类型、图形板、内存等）。
- 如果 information=all，则输出所有上述信息主题的信息。

**job**：如果指定了 job-name，则信息文本将写入 job-name.log 文件。

**whereami**：此选项打印 Abaqus 版本目录的位置。

### 示例

使用以下命令显示本地安装说明：

```
abaqus information=local
```

以下命令将本地安装说明写入文件 support.log：

```
abaqus information=local job=support
```

---

*原文来源：Abaqus 2025 FD02 Execution Guide*
