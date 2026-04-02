---
title: 数据库工具
description: Abaqus 执行指南章节
---

# 数据库工具

## SIM 数据库工具

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序
- Abaqus/Standard 和 Abaqus/Explicit 执行

### 概述

sim_version 实用程序将 SIM 数据库文件从一个版本转换到另一个版本，查询 SIM 数据库文件的 SIM 发布级别，或确定您正在使用的代码的 SIM 发布级别。

### 命令摘要

```
abaqus sim_version {convert = old-sim-file-name | query = sim-file-name | -current}
[out = new-sim-file-name] [level = release-level] [help]
```

### 命令行选项

**convert**：此选项用于指定要转换的 SIM 数据库文件的名称。

**query**：此选项用于指定要查询的 SIM 数据库文件的名称。

**current**：此选项用于确定当前代码的 SIM 发布级别。

**out**：此选项用于指定输出文件的名称。

**level**：此选项用于指定发布级别名称。

### 示例

```
abaqus sim_version query=sim-file-name
```

## 将 ODB 输出数据库文件转换为 SIM 格式

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序
- 输出数据库

### 概述

翻译器将包含模型和结果信息的输出数据库 (.odb) 文件转换为 SIM 数据库 (.sim) 文件，允许您在 3DEXPERIENCE 平台上使用 Physics Results Explorer 应用进行高性能后处理。

### 命令摘要

```
abaqus odb2sim odb = odb-file-name sim = SIM-database-file-name
[log = log-file-name] [o2sdebug]
```

### 限制

以下输出变量的场和历史结果不会被转换：MMIXDME、MMIXDMI、NFORC、SSPEEQ、SSSPRD、SSTORQ、SSFORC、TIME

以下单元的数据不会被转换：ELBOW31C、缓冲单元、弹簧单元、子结构单元、用户单元

## 生成输出数据库报告

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序
- 输出数据库的对象模型

### 概述

输出数据库报告实用程序将 Abaqus 输出数据库 (.odb) 文件中的信息打印到格式化报告中。默认情况下，报告以纯文本格式打印；您也可以 HTML 和 CSV（逗号分隔值）格式创建报告。

### 输出数据库结构

每个输出数据库包含两个主要部分：模型数据和结果数据。数据库进一步分解为容器的层次结构。

### 命令摘要

```
abaqus odbreport [job = job-name] [odb = output-database-file]
[mode = {HTML | CSV}]
[all] [mesh] [sets] [results]
[step = {step-name | _LAST_}]
[frame = {number | load-case-name | description | _LAST_}]
[framevalue = {time | mode | frequency}]
[field [ = field-variable ]]
[components] [invariants] [orientation]
[histregion = region-name]
[history [ = history-variable ]]
[instance = {instance-name | _NONE_}]
[blocked] [extrema]
```

### 命令行选项

**job**：此选项用于指定生成报告的文件名。

**odb**：此选项用于指定要从中生成报告的输出数据库 (.odb) 文件。

**mode**：此选项指定生成报告的文件格式。mode=HTML 生成 HTML 格式，mode=CSV 生成逗号分隔值格式。

**all**：此选项用于报告所有可用的模型信息和结果信息。

**mesh**：此选项用于报告与模型网格相关的节点坐标和单元连接信息。

**sets**：此选项用于报告与模型相关的所有集合和表面的名称和内容。

**results**：此选项用于报告输出数据库中的所有场和历史输出变量值。

**step**：此选项用于报告指定步骤的场和历史输出变量值。

**frame**：此选项用于报告指定帧的场输出变量值。

**field**：此选项用于报告指定的场输出变量值。

### 示例

```
abaqus odbreport job=beam
```

## 连接来自重启分析的输出数据库 (.odb) 文件

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序
- 继续输出重启

### 概述

abaqus restartjoin 实用程序将模型重启分析生成的输出数据库 (.odb) 文件追加到该模型原始分析生成的输出数据库。

### 命令摘要

```
abaqus restartjoin originalodb = odb-file-name restartodb = odb-file-name
[copyoriginal] [history] [compressresult]
```

### 命令行选项

**originalodb**：此选项指定原始分析生成的输出数据库文件。

**restartodb**：此选项指定重启分析生成的输出数据库文件。

**copyoriginal**：如果指定此选项，Abaqus 创建原始输出数据库文件的副本并追加内容到副本。

**history**：如果指定此选项，Abaqus 从重启输出数据库复制历史数据。

### 示例

```
abaqus restartjoin originalodb=Job-1.odb restartodb=Job-1_res.odb
```

## 合并来自子结构的结果

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序
- 获取子结构内的结果输出
- 合并多个输出数据库的数据

### 概述

abaqus substructurecombine 实用程序将模型的两个子结构生成的模型和结果数据合并到单个输出数据库 (.odb) 文件中。

### 命令摘要

```
abaqus substructurecombine baseodb = odb-file-name copyodb = odb-file-name
[all] [step = step-name] [frame = frame-number] [variable = variable-key]
```

### 命令行选项

**baseodb**：此选项指定基础输出数据库的名称。

**copyodb**：此选项指定副本输出数据库的名称。

**all**：此选项指示应复制所有步骤和帧中的所有变量的数据。

**step**：此选项指示步骤名称。

**frame**：此选项指示帧号。

**variable**：此选项指示变量键。

## 从子结构恢复结果

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus substructurerecover 实用程序从子结构分析中恢复结果。

### 命令摘要

```
abaqus substructurerecover job = job-name substructure = substructure-job-name
input = input-file [format = {abaqus | simpack}] [eigenproblem]
[minframevalue = value] [maxframevalue = value]
[resultsformat = {odb | fil | both}] [output = path]
[nset = set-name] [elset = set-name]
```

### 命令行选项

**job**：此选项指定恢复作业的名称。

**substructure**：此选项指定子结构作业的名称。

**input**：此选项指定输入文件。

**format**：此选项指定格式（abaqus 或 simpack）。

**eigenproblem**：此选项用于特征问题。

**resultsformat**：此选项指定结果格式（odb、fil 或 both）。

## 合并来自多个输出数据库的数据

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus odbcombine 实用程序将来自多个输出数据库的数据组合成单个输出数据库。

### 命令摘要

```
abaqus odbcombine job = job-name input = input-file [verbose]
[frequencyrange = frequency-range]
```

### 命令行选项

**job**：此选项指定组合输出数据库的名称。

**input**：此选项指定输入文件。

**verbose**：此选项启用详细输出。

**frequencyrange**：此选项指定频率范围。

## 网络输出数据库文件连接器

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus odbnetconnect 实用程序允许通过网络连接访问远程输出数据库。

### 命令摘要

```
abaqus odbnetconnect [port = port-number] [timeout = timeout]
[stop]
```

### 命令行选项

**port**：此选项指定端口号。

**timeout**：此选项指定超时值。

**stop**：此选项停止连接器。

## 映射热和磁载荷

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

abaqus mapoutput 实用程序映射热和磁载荷。

### 命令摘要

```
abaqus mapoutput job = job-name input = input-file
```

## 单元矩阵组装实用程序

**产品**：Abaqus/Standard

### 参考文献

- 关于执行程序

### 概述

abaqus matrix 实用程序生成单元矩阵。

### 命令摘要

```
abaqus matrix job = job-name oldjob = oldjob-name [text]
```

### 命令行选项

**job**：此选项指定作业名称。

**oldjob**：此选项指定旧作业名称。

**text**：此选项以文本格式输出。

---

*原文来源：Abaqus 2025 FD02 Execution Guide*
