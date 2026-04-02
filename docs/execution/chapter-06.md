---
title: 协同仿真
description: Abaqus 执行指南章节
---

# 协同仿真

## SIMULIA 协同仿真引擎 Director 执行

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

Abaqus/Standard 和 Abaqus/Explicit 之间的协同仿真由一个额外的进程（SIMULIA Co-Simulation Engine，CSE director）控制。通常，您不需要调用 CSE director 进程；当您运行 Abaqus 协同仿真程序时，或如果您从 Abaqus/CAE 提交协同仿真，它会自动调用。

如果您无法使用 Abaqus 协同仿真程序或 Abaqus/CAE，并且需要使用 Abaqus 执行程序分别提交协同仿真分析，则必须按照本节所述调用 CSE director。

### 命令摘要

```
abaqus cse job = cosim-job-name
configure = configuration file-name
listenerport = listener port-number
[datacheck]
[interactive]
[license_type = {token | credit}]
```

### 命令行选项

**job**：此选项指定运行期间生成的协同仿真摘要日志文件的名称。

**configure**：此选项指定governing协同仿真的 SIMULIA Co-Simulation Engine 配置文件的名称。

**listenerport**：此选项用于指定协同仿真入站消息到 director 的 TCP/UDP 端口号。

**datacheck**：此选项仅使 director 检查配置文件的正确性。

**interactive**：此选项使 director 交互运行。

**license_type**：此选项用于控制 Abaqus 用于 SimUnit 许可证模型的许可证类型。可能的值是 token 和 credit。默认值是 token。

### 示例

**运行 Abaqus/Standard 到 Abaqus/Explicit 协同仿真**：

使用以下命令让第一个 Abaqus 分析（在机器"earth"上运行）连接到协同仿真 director（在机器"mercury"上运行并在端口 44444 上监听）：

```
abaqus job=explicit csedirector=mercury:44444
```

使用以下命令让第二个 Abaqus 分析（在机器"venus"上运行）连接到协同仿真 director：

```
abaqus job=standard csedirector=mercury:44444
```

使用以下命令让协同仿真 director（在机器"mercury"上运行）根据文件 explicit_standard_config.xml 中定义的协同仿真配置操作，并通过端口 44444 接收通信：

```
abaqus cse job=cosim listenerport=44444 configure=explicit_standard_config.xml
```

## Abaqus/Standard、Abaqus/Explicit 和 FMU 协同仿真执行

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

Abaqus/Standard 和 Abaqus/Explicit 之间的协同仿真以及协同仿真格式 Functional Mockup Unit (FMU) 文件可以通过运行 Abaqus 协同仿真程序来执行。有几个参数可以在命令行设置，也可以在环境文件中设置。

协同仿真分析执行指定的"子"分析，并根据协同仿真配置文件规范 directs 进程的通信。

### 命令行参数组成

您可以使用逗号分隔的选项列表来指定参与子分析的命令行参数。命令行参数分为：

- 全局选项，采用单个参数
- 适用于 Abaqus 子分析的选项，采用逗号分隔的列表
- 适用于 FMU 的选项，采用逗号分隔的列表

### 为 Abaqus 作业分配 CPU 进行并行处理

您的 CPU 分配规范适用于 Abaqus/Standard 和 Abaqus/Explicit 子作业。Functional Mockup Units (FMU) 不支持多 CPU 使用。有三种方法可用于为并行处理分配 CPU：指定每个作业的 CPU 数量、在分析作业之间分配 CPU、在分析产品之间分配 CPU。

**指定每个作业的 CPU 数量**：最直接的方法是使用 cpus 参数指定每个子分析使用的 CPU 数量。

**在分析作业之间分配 CPU**：您可以指定用于协同仿真分析的 CPU 总数，以及确定 CPU 在子分析之间分布的权重因子。

**在分析产品之间分配 CPU**：您可以指定用于协同仿真分析的 CPU 总数，以及在参与协同仿真的分析产品之间分配 CPU 的权重因子。

### 限制

以下限制适用于协同仿真执行程序：

- 分析只能在一台机器上运行，也可以在头节点可由两个子分析作业共享的计算集群上运行。
- 此执行程序不支持与第三方应用程序的协同仿真。

### 命令摘要

```
abaqus cosimulation cosimjob = cosim-job-name
configure = co-simulation configuration file name
job = comma-separated list of Abaqus job names
[cpus = {number-of-cpus | comma-separated list}]
[cpuratio = comma-separated list of weight factors]
[interactive] | [background] | [queue [ = queue-name ][after = time]]
[timeout = co-simulation timeout value in seconds]
[listenerport = port number]
[portpool = colon-separated pair of socket port numbers]
[license_type = {token | credit}]
[input = comma-separated list of input-file names]
[user = comma-separated list of {source-file | object-file} names]
[globalmodel = comma-separated list of results file names]
[memory = comma-separated list of memory-sizes]
[oldjob = comma-separated list of oldjob-names]
[double = comma-separated list of double precision settings]
[scratch = comma-separated list of scratch-dir names]
[output_precision = comma-separated list of {single | full}]
[fmu = comma-separated list of FMU files]
[fmuinstance = comma-separated list of instance names]
```

### 示例

**交互运行 Abaqus/Standard 到 FMU 协同仿真**：

```
abaqus cosimulation cosimjob=cosim_controls job=plant configure=cosim_controls fmu=controller interactive
```

**提交 Abaqus/Standard 到 Abaqus/Explicit 协同仿真到批处理队列**：

```
abaqus cosimulation cosimjob=beam job=beam,beam2 configure=beam_config cpus=8,4 queue=long
```

## SIMULIA 协同仿真引擎 FMU 执行

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序
- SIMULIA Co-Simulation Engine Director 执行

### 概述

任意数量的 Functional Mockup Unit (FMU) 文件可用于与 Abaqus/Standard 或 Abaqus/Explicit 的信号/执行器协同仿真。FMU 文件符合 Modelisar 组织定义的 Functional Mockup Interface (FMI) 标准。

### 警告

仅在更通用的协同仿真执行程序不支持您的 FMU 协同仿真使用的情况下，才建议使用此程序。

### 命令摘要

```
abaqus fmu csedirector = CSE director hosts:port-number
fmu = fmu-file-name
instance = co-simulation-instance-name
[interactive]
[timeout = timeout value in seconds]
```

### 命令行选项

**csedirector**：此选项用于指定 CSE director 与 FMU 执行之间协同仿真消息的连接。

**fmu**：此选项指定要用于协同仿真的 FMU 文件名。

**instance**：此选项指定 FMU 的实例名称。

**interactive**：此选项使 director 交互运行。

**timeout**：此选项用于指定协同仿真 director 连接的超时值（以秒为单位）。

### 示例

**运行协同仿真 Director**：

```
abaqus cse job=cosim listenerport=44444 configure=cosim_config.xml
```

**运行第一个基于 FMU 的仿真**：

```
abaqus fmu fmu=controller.fmu instance=controller1 csedirector=mercury:44444
```

**运行第二个基于 FMU 的仿真**：

```
abaqus fmu fmu=controller.fmu instance=controller2 csedirector=mercury:44444
```

**运行 Abaqus/Standard 仿真**：

```
abaqus job=standard csedirector=mercury:44444
```

---

*原文来源：Abaqus 2025 FD02 Execution Guide*
