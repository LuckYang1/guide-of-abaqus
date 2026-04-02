---
title: 文件转换工具（二）
description: Abaqus 执行指南章节
---

# 文件转换工具（二）

## 翻译其他求解器输入为 Abaqus 输入

本节介绍将其他求解器输入翻译为 Abaqus 输入的命令。

### 本节包含：

- 将 Nastran 数据翻译为 Abaqus 文件
- 将 ANSYS 输入文件翻译为部分 Abaqus 输入文件
- 将 PAM-CRASH 输入文件翻译为部分 Abaqus 输入文件
- 将 RADIOSS 输入文件翻译为部分 Abaqus 输入文件
- 将 LS-DYNA 数据文件翻译为 Abaqus 输入文件
- 与 ZAERO 交换 Abaqus 数据
- 将 Simpack 柔性体翻译为 Abaqus 矩阵数据
- 将 Moldflow 数据翻译为 Abaqus 输入文件

## 将 Nastran 数据翻译为 Abaqus 文件

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus fromNastran 实用程序将 Nastran Bulk Data 文件翻译为 Abaqus 输入文件。

### 命令摘要

```
abaqus fromNastran job = job-name input = input-file
[wtmass_fixup] [loadcases] [pbar_zero_reset]
[surface_based_coupling] [beam_offset_coupling]
```

### 命令行选项

**job**：此选项指定作业名称。

**input**：此选项指定输入文件。

**wtmass_fixup**：此选项修复质量权重。

**loadcases**：此选项翻译负载情况。

**pbar_zero_reset**：此选项重置 pbar 为零。

**surface_based_coupling**：此选项启用基于表面的耦合。

**beam_offset_coupling**：此选项启用梁偏移耦合。

## 将 ANSYS 输入文件翻译为部分 Abaqus 输入文件

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus fromANSYS 实用程序将 ANSYS 输入文件翻译为部分 Abaqus 输入文件。

### 命令摘要

```
abaqus fromANSYS job = job-name input = input-file
```

### 命令行选项

**job**：此选项指定作业名称。

**input**：此选项指定输入文件。

## 将 PAM-CRASH 输入文件翻译为部分 Abaqus 输入文件

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus fromPAMCrash 实用程序将 PAM-CRASH 输入文件翻译为部分 Abaqus 输入文件。

### 单元编号和分组

所有单元必须具有唯一的单元编号。分配了相同 PART 标识号的单元被分组到一个单元集中。

除了由 SPRING 和 KJOIN 翻译产生的连接器单元外，截面属性需要在 PART 部分输入，而不是在单元部分单独输入。

### 材料模型

翻译器仅支持有限材料模型。所有不支持的材料模型都被翻译为双线性弹塑性。

### 命令摘要

```
abaqus fromPAMCrash job = job-name input = input-file
[pLinkConnectors] [splitAirbagElements] [autoKJoinStops]
```

### 命令行选项

**job**：此选项指定作业名称。

**input**：此选项指定输入文件。

**pLinkConnectors**：此选项处理 pLink 连接器。

**splitAirbagElements**：此选项分割气囊单元。

**autoKJoinStops**：此选项自动 KJoin 停止。

## 将 RADIOSS 输入文件翻译为部分 Abaqus 输入文件

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus fromRADIOSS 实用程序将 RADIOSS 输入文件翻译为部分 Abaqus 输入文件。

### 单元编号和分组

所有单元必须具有唯一的单元编号。

### 材料模型

翻译器支持有限材料模型。

### 包含文件

RADIOSS 使用包含文件。

### 命令摘要

```
abaqus fromRADIOSS job = job-name input = input-file
[splitAirbagElements] [readAbaqusDat]
[userDefaultMass] [userDefaultInertia] [userHistoryTime]
```

### 命令行选项

**job**：此选项指定作业名称。

**input**：此选项指定输入文件。

**splitAirbagElements**：此选项分割气囊单元。

**readAbaqusDat**：此选项读取 Abaqus .dat 文件。

**userDefaultMass**：此选项使用用户默认质量。

**userDefaultInertia**：此选项使用用户默认惯性。

**userHistoryTime**：此选项使用用户历史时间。

## 将 LS-DYNA 数据文件翻译为 Abaqus 输入文件

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus fromDyna 实用程序将 LS-DYNA 数据文件翻译为 Abaqus 输入文件。

### 命令摘要

```
abaqus fromDyna job = job-name input = input-file
[splitFile] [i10]
```

### 命令行选项

**job**：此选项指定作业名称。

**input**：此选项指定输入文件。

**splitFile**：此选项分割文件。

**i10**：此选项使用 i10 格式读取整数数据。

## 与 ZAERO 交换 Abaqus 数据

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus zaero 实用程序在 Abaqus 和 ZAERO 之间交换数据。

### 命令摘要

```
abaqus zaero job = job-name unvfile = unv-file odbname = odb-name
mtxfile = mtx-file [mode = {aeroelastic | stress}]
```

### 命令行选项

**job**：此选项指定作业名称。

**unvfile**：此选项指定 Universal File 文件。

**odbname**：此选项指定 ODB 文件名。

**mtxfile**：此选项指定矩阵文件。

**mode**：此选项指定模式（aeroelastic 或 stress）。

## 将 Simpack 柔性体翻译为 Abaqus 矩阵数据

**产品**：Abaqus/Standard

### 参考文献

- 关于执行程序

### 概述

abaqus fromSimpack 实用程序将 Simpack 柔性体翻译为 Abaqus 矩阵数据。

### 命令摘要

```
abaqus fromSimpack job = job-name
```

## 将 Moldflow 数据翻译为 Abaqus 输入文件

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus fromMoldflow 实用程序将 Moldflow 数据翻译为 Abaqus 输入文件。

### 命令摘要

```
abaqus fromMoldflow job = job-name input = input-file
[midplane] [3D] [element_order] [initial_stress]
[material] [orientation]
```

### 命令行选项

**job**：此选项指定作业名称。

**input**：此选项指定输入文件。

**midplane**：此选项指定中面网格。

**3D**：此选项指定 3D 网格。

**element_order**：此选项指定单元阶次。

**initial_stress**：此选项包含初始应力。

**material**：此选项包含材料数据。

**orientation**：此选项包含方向数据。

---

*原文来源：Abaqus 2025 FD02 Execution Guide*
