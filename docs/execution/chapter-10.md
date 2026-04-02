---
title: 环境文件设置
description: Abaqus 执行指南章节
---

# 环境文件设置

## 概述

Abaqus 执行程序使用环境参数来自定义作业的执行。这些设置可以使用 Abaqus 环境文件之一进行更改：custom_v6.env 或 abaqus_v6.env。

如果同一作业参数在多个环境文件中定义，或在同一环境文件中多次定义，则将使用遇到的最后一个定义。

## 环境设置层次结构

Abaqus 环境设置具有以下层次结构（从最低优先级到最高优先级）：

1. **abaqus_v6.env**：Abaqus 安装时创建的默认环境文件
2. **custom_v6.env**：用户自定义环境文件
3. **命令行参数**：直接在命令行上指定的参数

## 语法

环境文件是包含一系列环境变量赋值的文本文件。每行格式为：

```
variable_name = value
```

### 变量类型

- **整数变量**：如 `cpus = 4`
- **浮点变量**：如 `memory = 80%`
- **字符串变量**：如 `scratch = /tmp/abaqus`
- **布尔变量**：如 `standard_parallel = all`

## 故障排除

### 检查环境设置

使用以下命令显示当前环境设置：

```
abaqus information=environment
```

### 常见问题

- 如果作业行为异常，请检查环境文件语法
- 确保没有在同一文件中重复定义变量
- 使用 `abaqus information=system` 检查系统配置

## 命令行默认参数

### cpus

指定用于分析的 CPU 数量。默认值通常为 1。

```
cpus = 4
```

### domains

指定 Abaqus/Explicit 中的并行域数量。

```
domains = 4
```

### double_precision

指定双精度执行。

```
double_precision = explicit
```

### parallel

指定并行方法（domain 或 loop）。

```
parallel = domain
```

### run_mode

指定运行模式（interactive 或 background）。

```
run_mode = background
```

### scratch

指定临时目录。

```
scratch = /tmp/abaqus
```

### standard_parallel

指定标准并行选项（all 或 solver）。

```
standard_parallel = all
```

### gpus

指定 GPU 数量。

```
gpus = 2
```

### unconnected_regions

指定是否为未连接区域创建集合。

```
unconnected_regions = yes
```

## 系统资源参数

### memory

**语法**：`memory = memory_specification`

**说明**：指定 Abaqus 可以在分析期间使用的最大内存量或物理内存的百分比。

**示例**：
```
memory = 80%
memory = 4GB
```

## 系统自定义参数

### ask_delete

指定在覆盖现有文件之前是否提示确认。

```
ask_delete = off
```

### auto_calculate

启用自动计算。

```
auto_calculate = on
```

### auto_convert

指定自动转换选项。

```
auto_convert = all
```

### average_by_section

按截面平均输出。

```
average_by_section = on
```

### mp_host_list

指定 MPI 主机列表。

```
mp_host_list = [['host1', 4], ['host2', 4]]
```

### odb_output_by_default

默认启用 ODB 输出。

```
odb_output_by_default = on
```

### output_warnings_level

指定警告级别。

```
output_warnings_level = 1
```

### onCaeStartup

指定启动时运行的脚本。

```
onCaeStartup = ['script1.py', 'script2.py']
```

## 并行执行期间的环境变量导出

在并行执行期间，某些环境变量会被导出到子进程。

## 协同仿真参数

### cosimulation_port

指定协同仿真端口号。

```
cosimulation_port = 48000
```

### cosimulation_timeout

指定协同仿真超时值（秒）。

```
cosimulation_timeout = 3600
```

### cpus_weight_std

指定 Abaqus/Standard 的 CPU 权重。

```
cpus_weight_std = 2
```

### cpus_weight_xpl

指定 Abaqus/Explicit 的 CPU 权重。

```
cpus_weight_xpl = 1
```

### portpool

指定端口池范围。

```
portpool = [51000, 52000]
```

## 环境文件示例

### Linux 环境文件

```bash
# Linux 环境文件示例
cpus = 4
memory = 80%
scratch = /tmp/abaqus
standard_parallel = all
```

### Windows 环境文件

```batch
@REM Windows 环境文件示例
set cpus=4
set memory=80%
set scratch=C:\TEMP\abaqus
set standard_parallel=all
```

---

*原文来源：Abaqus 2025 FD02 Execution Guide*
