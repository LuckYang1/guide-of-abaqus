---
title: Abaqus 执行（下）
description: Abaqus 执行指南章节
---

# Abaqus 执行（下）

## Abaqus 作业执行控制

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

作业执行控制的执行程序包括 abaqus suspend、abaqus resume 和 abaqus terminate。这些实用程序用于暂停、恢复和终止 Abaqus 分析作业。暂停分析作业将停止其执行并将许可证令牌释放到空闲令牌池。恢复分析将重新激活暂停的作业，并在可用时检出该作业的许可证令牌。如果许可证令牌不可用，作业将被放置在许可证队列中。终止分析作业将停止分析的可执行文件并释放其许可证令牌。终止的分析作业无法恢复。

您可以远程执行这些命令；不需要在与运行分析的同一台机器上执行这些命令。

### 命令摘要

```
abaqus {suspend | resume | terminate} {job = job-name | host = hostname port = port-number}
```

### 命令行选项

**job**：此选项用于指定要暂停、恢复或终止的分析作业的名称。使用此选项时，命令必须从作业的工作目录执行。命令读取 job-name.cid 文件以获取用于向作业发出信号的 hostname 和 port-number。

**host**：此选项用于指定运行分析作业的连接的 hostname。此选项必须与 port 选项一起使用。hostname 可以通过读取 job-name.cid 文件的最后一行来识别，其中列出了 hostname:port-number。

**port**：此选项用于指定运行分析作业的连接的 port-number。此选项必须与 host 选项一起使用。port-number 可以通过读取 job-name.cid 文件的最后一行来识别，其中列出了 hostname:port-number。

## Abaqus/CAE 执行

**产品**：Abaqus/CAE

### 参考文献

- 关于执行程序

### 概述

Abaqus/CAE 是用于创建、提交、监控和评估 Abaqus 仿真结果的交互式环境，通过运行 Abaqus 执行程序并指定 cae 参数来执行。

### 命令摘要

```
abaqus cae
[database = database-file]
[replay = replay-file]
[recover = journal-file]
[startup = startup-file]
[script = script-file]
[noGUI [ = noGUI-file ]]
[noenvstartup]
[noSavedOptions]
[noSavedGuiPrefs]
[noStartupDialog]
[custom = script-file]
[guiTester [ = GUI-script ]]
[guiRecord]
[guiNoRecord]
```

### 命令行选项

**database**：此选项指定要打开的模型数据库文件或输出数据库文件的名称。

**replay**：此选项指定要从中重放 Abaqus/CAE 命令的文件名。

**recover**：此选项指定要从中重新构建模型数据库的文件名。

**startup**：此选项指定包含要在应用程序启动时运行的 Python 配置命令的文件名。

**script**：与 startup 相同。

**noGUI**：此选项指定在不使用图形用户界面 (GUI) 的情况下运行 Abaqus/CAE。如果未指定文件名，则检出 Abaqus/CAE 许可证并初始化 Python 解释器以允许交互式输入 Python 或 Abaqus 脚本界面命令。如果指定了文件名，Abaqus/CAE 在文件中的命令完成时运行命令并退出。

**noenvstartup**：此选项指定在应用程序启动时不运行环境文件中的所有配置命令。

**noSavedOptions**：此选项指定 Abaqus/CAE 不应应用存储在 abaqus_2025.gpr 中的显示选项设置。

**noSavedGuiPrefs**：此选项指定 Abaqus/CAE 不应应用存储在 abaqus_2025.gpr 中的 GUI 设置。

**noStartupDialog**：此选项指定不显示 Abaqus/CAE 的"开始会话"对话框。

**custom**：此选项指定包含 Abaqus GUI Toolkit 命令的文件名。

**guiTester**：此选项启动包含 Abaqus Python 开发环境的单独用户界面以及 Abaqus/CAE。

**guiRecord**：此选项使您能够在 Abaqus/CAE 用户界面中记录您的操作。

**guiNoRecord**：此选项使您能够在设置环境变量 ABQ_CAE_GUIRECORD 时禁用用户界面录制。

### 示例

**打开模型数据库**：

```
abaqus cae database=beam
```

**传递参数给脚本**：

```
abaqus cae script=try.py -- argument1
```

**无 GUI 运行 Abaqus/CAE**：

```
abaqus cae noGui=checkPartValidity.py -- test.cae Model-1 Part-1
```

## Abaqus/Viewer 执行

**产品**：Abaqus/Viewer

### 参考文献

- 关于执行程序

### 概述

Abaqus/Viewer 是 Abaqus/CAE 的一个子集，仅包含 Visualization 模块的后处理功能，通过运行 Abaqus 执行程序并指定 viewer 参数来执行。

### 命令摘要

```
abaqus viewer
[database = database-file]
[replay = replay-file]
[startup = startup-file]
[script = script-file]
[noGUI [ = noGUI-file ]]
[noenvstartup]
[noSavedOptions]
[noSavedGuiPrefs]
[noStartupDialog]
[custom = script-file]
[guiTester [ = GUI-script ]]
[guiRecord]
[guiNoRecord]
```

### 命令行选项

**database**：此选项指定要使用的输出数据库文件的名称。

**replay**：此选项指定要从中读取 Abaqus/Viewer 命令的文件名。

**startup**：此选项指定包含要在应用程序启动时运行的 Python 配置命令的文件名。

**script**：与 startup 相同。

**noGUI**：此选项指定在不使用图形用户界面 (GUI) 的情况下运行 Abaqus/Viewer。

**guiTester**：此选项启动包含 Python 开发环境的单独用户界面以及 Abaqus/Viewer。

**guiRecord**：此选项使您能够在 Abaqus/Viewer 用户界面中记录您的操作。

**guiNoRecord**：此选项使您能够在设置环境变量 ABQ_CAE_GUIRECORD 时禁用用户界面录制。

## 创建用户定义的可执行文件和子程序

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus make 实用程序用于创建用户后处理可执行文件和 Abaqus 用户子程序的用户定义库。用于编译和链接用户提供的程序或用户子程序源文件的命令可以使用适当的环境文件参数进行更改。

### 命令摘要

```
abaqus make {job = job-name | library = source-file}
[user = {source-file | object-file}]
[directory = library-dir]
[object_type = {fortran | c | cpp}]
[uniquelibs]
```

### 命令行选项

**job**：此选项用于创建用户提供的后处理程序。

**library**：此选项用于创建用户子程序对象文件和共享库。

**user**：此选项仅在与 job 选项一起使用时有效。

**directory**：此选项仅在与 library 选项一起使用时有效。

**object_type**：此选项仅在与 job 选项一起使用时有效。

**uniquelibs**：此选项仅在与 library 选项一起使用时有效。

### 示例

```
abaqus make job=pprocess
```

## 优化执行

**产品**：Abaqus/CAE

### 参考文献

- 关于执行程序

### 概述

使用 TOSCA 进行优化的 Abaqus 通过运行 Abaqus 执行程序并提供参数文件的名称来执行，而参数文件又引用 Abaqus 输入文件。

### 命令摘要

```
abaqus optimization task = parameter file
job = results folder
[cpus = total number-of-cpus]
[gpus = total number-of-gpgpus]
[memory = memory-size]
[interactive]
[globalmodel = {results file-name | ODB output database file-name | SIM database file-name}]
[scratch = scratch-dir]
```

### 命令行选项

**task**：此选项用于指定包含用于执行优化的参数的文件。

**job**：此选项用于指定存储优化结果的文件夹名称。

**cpus**：此选项指定在分析运行期间要使用的处理器总数。

**gpus**：此选项指定 Abaqus/Standard 直接求解器的加速。

**memory**：此选项指定最大内存量或可在分析期间分配的最大物理内存百分比。

**interactive**：此选项将导致作业交互运行。

**globalmodel**：此选项指定全局模型的结果文件、ODB 输出数据库文件或 SIM 数据库文件的名称。

**scratch**：此选项用于指定用于临时文件的目录名称。

### 示例

```
abaqus optimization task=WeightReduction job=WeightReductionResults
```

## 参数化研究

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序
- Abaqus/Standard 和 Abaqus/Explicit 执行

### 概述

abaqus script 工具表示要执行参数化研究。设计中涉及的每个分析都可以使用 execute 命令执行。

### 命令摘要

```
abaqus script [=script-file]
[startup = startup file-name]
[noenvstartup]
```

### 命令行选项

**script-file**：指定脚本文件名时，参数化研究模块被导入并执行参数化研究脚本文件中的指令。

**startup**：此选项指定包含要在应用程序启动时运行的 Python 配置命令的文件名。

**noenvstartup**：此选项指定在应用程序启动时不运行环境文件中的所有配置命令。

### 示例

```
abaqus script=parstudy
```

## Abaqus 文档

**产品**：Abaqus/Standard、Abaqus/Explicit、Abaqus/CAE

### 参考文献

- 关于执行程序
- 获取帮助

### 概述

Abaqus 文档与产品分开安装，通过 Web 浏览器查看。

### 使用 Abaqus 文档

文档包含以下指南：

- Abaqus/CAE User's Guide
- Abaqus Analysis Guide
- Abaqus Benchmarks Guide
- Abaqus Constraints Guide
- Abaqus Elements Guide
- Abaqus Example Problems Guide
- Abaqus Execution Guide
- Getting Started with Abaqus/CAE
- Abaqus GUI Toolkit User's Guide
- Abaqus GUI Toolkit Reference Guide
- Abaqus Interactions Guide
- Abaqus Introduction & Spatial Modeling Guide
- Abaqus Keywords Guide
- Abaqus Materials Guide
- Abaqus Output Guide
- Abaqus Prescribed Conditions Guide
- Abaqus Release Notes
- Abaqus Scripting User's Guide
- Abaqus Scripting Reference Guide
- Abaqus Theory Guide
- Abaqus User Subroutines Guide
- Abaqus Verification Guide
- Abaqus Configuration Guide

### 查看文档

1. 输入 `abaqus doc`。文档在 Web 浏览器中打开。
2. 单击书的标题以显示它。
3. 展开目录中的主题标题。

### 命令摘要

```
abaqus doc
```

---

*原文来源：Abaqus 2025 FD02 Execution Guide*
