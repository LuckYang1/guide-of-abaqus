---
title: 文件转换工具（一）
description: Abaqus 执行指南章节
---

# 文件转换工具（一）

## 加密和解密 Abaqus 输入数据

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus encrypt 实用程序加密 Abaqus 输入数据，abaqus decrypt 实用程序解密加密的 Abaqus 输入数据。

当您加密文件时，Abaqus 会在文件开头添加以下未加密的注释行：

"Do not modify or delete this header comment. You can, however, insert additional comment lines between this header comment and the first line of encrypted data."

您可以在此加密后注释行之后插入其他注释行，但不能在加密数据行内添加注释。

### 安全和支持注意事项

加密文件受密码保护。如果您丢失密码，Dassault Systèmes 无法恢复。

### 命令摘要

```
abaqus encrypt input = input-file output = output-file
[password = password] [license = license-type]
[siteid = site-id] [include_only = {encrypt | decrypt | all}]
```

```
abaqus decrypt input = input-file output = output-file
[password = password]
```

### 命令行选项

**input**：此选项指定要加密或解密的数据文件的名称。

**output**：此选项指定加密或解密后的数据文件的名称。

**password**：此选项指定此加密或解密的密码。密码区分大小写。

**license**：此选项仅适用于文件加密。此选项指定最终用户必须获得许可的 Abaqus 功能。

**siteid**：此选项仅适用于文件加密。此选项指定最终用户可以包含或解密此加密数据文件的 Abaqus 站点 ID。

**include_only**：此选项指定加密的输入数据不能使用 abaqus decrypt 执行程序解密。

### 示例

```
abaqus encrypt input=model.inp output=model_encrypted.inp password=secret
```

## ASCII 翻译结果 (.fil) 文件

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus ascfil 实用程序将 Abaqus 结果 (.fil) 文件从二进制格式转换为 ASCII 格式。

### 命令摘要

```
abaqus ascfil job = job-name
```

### 命令行选项

**job**：此选项指定作业名称。

## 连接结果 (.fil) 文件

**产品**：Abaqus/Standard

### 参考文献

- 关于执行程序

### 概述

abaqus append 实用程序将结果文件连接在一起。

### 命令摘要

```
abaqus append job = job-name oldjob = oldjob-name
```

### 命令行选项

**job**：此选项指定新作业名称。

**oldjob**：此选项指定旧作业名称。

### 示例

```
abaqus append job=combined oldjob=run1
```

## 将 Abaqus 文件翻译为 Nastran Bulk Data 文件

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus toNastran 实用程序将 Abaqus 输入文件翻译为 Nastran Bulk Data 文件。

### 命令摘要

```
abaqus toNastran job = job-name input = input-file
[bdf_format = {standard | crash}]
```

### 命令行选项

**job**：此选项指定作业名称。

**input**：此选项指定输入文件。

**bdf_format**：此选项指定 Bulk Data 格式。

## 将 Abaqus 输出数据库文件翻译为 Nastran Output2 结果文件

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus toNastranOdb 实用程序将 Abaqus 输出数据库文件翻译为 Nastran Output2 结果文件。

### 命令摘要

```
abaqus toNastranOdb job = job-name odb = odb-file-name
[step = step-number] [increment = increment-number]
[slim] [quad4corner] [quad4stress_bisector]
```

### 命令行选项

**job**：此选项指定作业名称。

**odb**：此选项指定输出数据库文件。

**step**：此选项指定步骤号。

**increment**：此选项指定增量号。

**slim**：此选项启用 slim 格式。

**quad4corner**：此选项用于 quad4 角点应力。

**quad4stress_bisector**：此选项用于 quad4 应力平分线。

## 将 Abaqus 子结构翻译为 MSC.Adams 柔性体

**产品**：Abaqus/Standard

### 参考文献

- 关于执行程序

### 概述

abaqus toAdams 实用程序将 Abaqus 子结构翻译为 MSC.Adams 柔性体。

### 命令摘要

```
abaqus toAdams job = job-name substructure_sim = sim-file-name
[adams_mnf_block_16]
```

### 命令行选项

**job**：此选项指定作业名称。

**substructure_sim**：此选项指定 SIM 文件名。

**adams_mnf_block_16**：此选项使用 16 位 MNF 块格式。

## 将 Abaqus 子结构翻译为 Simpack 柔性体

**产品**：Abaqus/Standard

### 参考文献

- 关于执行程序

### 概述

abaqus toSimpack 实用程序将 Abaqus 子结构翻译为 Simpack 柔性体。

### 命令摘要

```
abaqus toSimpack job = job-name substructure_sim = sim-file-name
```

### 命令行选项

**job**：此选项指定作业名称。

**substructure_sim**：此选项指定 SIM 文件名。

## 将 Abaqus 子结构翻译为 EXCITE 柔性体

**产品**：Abaqus/Standard

### 参考文献

- 关于执行程序

### 概述

abaqus toExcite 实用程序将 Abaqus 子结构翻译为 EXCITE 柔性体。

### 命令摘要

```
abaqus toExcite job = job-name substructure_sim = sim-file-name
[hide_mesh] [recovery_matrix]
```

### 命令行选项

**job**：此选项指定作业名称。

**substructure_sim**：此选项指定 SIM 文件名。

**hide_mesh**：此选项隐藏网格。

**recovery_matrix**：此选项包含恢复矩阵。

---

*原文来源：Abaqus 2025 FD02 Execution Guide*
