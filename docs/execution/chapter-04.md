---
title: Abaqus 执行（上）
description: Abaqus 执行指南章节
---

# Abaqus 执行（上）

## Abaqus/Standard 和 Abaqus/Explicit 执行

**产品**：Abaqus/Standard、Abaqus/Explicit

### 参考文献

- 关于执行程序

### 概述

Abaqus/Standard 和 Abaqus/Explicit 通过运行 Abaqus 执行程序来执行。几个参数可以在命令行设置，也可以在环境文件中设置（请参阅"环境文件设置"）。或者，您可以使用方便的 Abaqus/CAE 用户界面从输入文件提交 Abaqus 分析并设置分析参数；请参阅"了解分析作业"。

Abaqus 对文件名强制实施字符限制。对于任何命令行文件引用，文件名（包括路径描述）的总长度不能超过 256 个字符。

### 命令摘要

```
abaqus job = job-name
[analysis] | [datacheck] | [parametercheck] | [continue] | [convert = {select | odb | state | all}] | [recover] | [syntaxcheck]
[information = {environment | local | memory | release | support | system | all}]
[input = input-file]
[user = {source-file | object-file}]
[uniquelibs]
[oldjob = oldjob-name]
[fil = {append | new}]
[globalmodel = {results file-name | ODB output database file-name | SIM database file-name}]
[cpus = total number-of-cpus]
[parallel = {domain | loop}]
[domains = number-of-domains]
[dynamic_load_balancing = {on | off}]
[threads_per_mpi_process = number of threads per mpi process]
[standard_parallel = {all | solver}]
[gpus = total number-of-gpgpus]
[memory = memory-size]
[interactive] | [background] | [queue [ = queue-name ][after = time]]
[double = {explicit | both | off | constraint}]
[scratch = scratch-dir]
[output_precision = {single | full}]
[resultsformat = {odb | sim | both}]
[port = co-simulation port-number]
[host = co-simulation hostname]
[csedirector = Co-Simulation Engine director host:port-number]
[timeout = co-simulation timeout value in seconds]
[unconnected_regions = {yes | no}]
[noFlexBody]
[license_type = {token | credit}]
[ssd_split = number-of-frequency-partitions]
[ssd_partition = frequency-partition-number]
```

### 命令行选项

#### 必需选项

**job**：此选项的值指定在运行期间生成的所有文件的名称，以及在 continue、convert 和 recover 阶段读取的文件的名称。

如果此选项从命令行省略，系统将提示您输入其值（除非仅使用"获取信息"中描述的信息选项）。如果未提供 input 选项，程序将在当前目录中查找名为 job-name.inp 的输入文件。

#### 互斥选项（确定执行分析的哪些阶段）

所有选项都是顺序无关的。如果不存在任何这些选项，则假定为 analysis 选项。convert 选项是互斥规则的例外：convert 可以与任何选项一起出现，除了 datacheck、parametercheck、syntaxcheck 和 information。

**analysis**：此选项表示将执行完整的 Abaqus 分析（或重新启动 Abaqus 分析）。

**datacheck**：此选项表示运行仅用于数据检查。将不执行分析。如果使用此选项，将保存继续分析所需的所有文件。

**parametercheck**：此选项表示运行仅用于输入参数检查（必须使用参数定义；请参阅"参数化建模"）。将不执行分析或数据检查。

**continue**：此选项表示运行将从之前的数据检查运行结束的点开始。

**convert**：此参数的值指示哪些文件将进行后处理。结果可以按照以下方式转换：紧接在分析运行之后、作为分析运行之后的单独运行，或在分析运行时进行转换：

1. 要运行包括后续结果转换的分析，请将 convert 选项与 job 和 analysis 选项一起使用。
2. 要转换先前运行的分析结果，请将 convert 选项与 job 选项一起使用。
3. 要转换当前正在运行的作业的结果，请将 convert 选项与 oldjob 选项（用于命名正在运行的作业）和 job 选项（用于为 convert 选项生成的文件提供新名称）一起使用。

如果 convert=select，Abaqus/Explicit 选择的结果文件（job-name.sel）将被转换为标准的 Abaqus 结果文件（job-name.fil）。如果使用 parallel=domain 并行运行分析，单独的选择结果文件（job-name.sel.n）将在转换为标准的 Abaqus 结果文件之前被合并为一个选择的结果文件（job-name.sel）。

如果 convert=odb，输出数据库（job-name.odb）将使用后处理计算器进行转换（请参阅"后处理计算器"）。仅当请求"后处理计算器"中列出的输出类型时，才需要进行此转换。

如果 convert=state，如果使用 parallel=domain 并行运行分析，单独的 Abaqus/Explicit 状态文件（job-name.abq.n）将被合并为一个 Abaqus/Explicit 状态文件（job-name.abq）。

如果 convert=all，将执行所有适用的转换选项。

**recover**：此选项仅适用于 Abaqus/Explicit。它表示分析将在状态文件中最后一个可用的步骤和增量处重新启动。此功能可用于在灾难性故障后重新启动，例如超出 CPU 限制或磁盘配额（请参阅"重新启动分析"）。如果原始分析使用 parallel=domain 并行运行，则必须使用 parallel=domain 和相同的处理器数量重新启动。

**syntaxcheck**：此选项表示运行仅用于检查输入文件的语法。此选项不使用任何许可证令牌。将不执行分析，continue 选项不能用于继续进行分析。仅生成数据（.dat）和输出数据库（.odb）文件用于查看。在 Abaqus/Explicit 分析中，输出数据库中的模型数据可能不完整。

**information**：此选项将有关安装和生效环境的信息写入屏幕或 job-name.log 文件。

#### 分析模块的其他选项

**input**：此选项用于指定输入文件名，可以带或不带 .inp 扩展名（如果未提供扩展名，Abaqus 将自动附加）。如果未提供此选项，程序将在当前目录中查找名为 job-name.inp 的输入文件。如果找不到 job-name.inp，程序将提示输入输入文件名。

**user**：此选项指定包含要用于分析的用户子程序的源文件或对象文件的名称。用户例程的名称可以包含路径名，可以带或不带文件扩展名。Abaqus/Standard 和 Abaqus/Explicit 接受用 C、C++ 或 Fortran 编写的用户子程序。

如果提供了扩展名，程序将根据文件类型采取适当的操作。如果文件名没有扩展名，程序将搜索 C、C++ 或 Fortran 源文件。如果源文件不存在，则改为搜索对象文件。执行程序使用用户子程序文件创建一个共享库，分析期间使用该共享库。

如果经常需要相同的用户子程序，请考虑设置 usub_lib_dir 环境文件参数，并使用 abaqus make 执行程序创建一个包含用户子程序的共享库。这样可以避免每次需要时重新编译和/或重新链接用户子程序。如果分析调用的用户子程序包含在用户库中，则不需要 user 选项。如果指定了 user 选项，则不会使用 usub_lib_dir 环境文件参数指定的目录中的用户库。

当使用 double 选项运行 Abaqus/Explicit 分析时，user 选项不能用于指定对象文件，因为 Abaqus/Explicit 双精度运行需要单精度和双精度对象。在这种情况下，您必须设置 usub_lib_dir 环境文件参数，并将单精度和双精度对象文件放在指定目录中；或者，您可以提供用户子程序源。

**uniquelibs**：此选项表示输入文件执行将使用 abaqus make 执行程序中的 uniquelibs 选项创建的库。

**oldjob**：此选项标识先前运行的文件，从中将启动导入、重启或后处理运行（仅限 Abaqus/Standard；请参阅"在 Abaqus/Standard 中从重启数据恢复其他结果输出"），或从中导入结果。您指定 oldjob-name（不带文件扩展名）。对于导入或重启分析，您可以包含完整或相对路径。oldjob-name 必须与当前 job-name 不同。当重启、后处理或对称模型生成分析从重启或结果文件读取数据时，需要此选项。

**fil**：此选项指定是否将重启运行中指定的旧结果文件的数据包含在新结果文件的开始处（默认）。如果使用 fil=new，新结果文件将仅包含从分析发生重启的点开始的数据。此功能用于 Abaqus/Standard 运行，以将重启分析的输出连接到一个连续的结果文件中。非重启作业不能使用此功能将结果文件输出附加到旧结果文件；必须使用 abaqus append 执行程序来完成此目的。对于 Abaqus/Explicit 运行，不允许设置 fil=new。

**globalmodel**：此选项指定全局模型的结果文件、ODB 输出数据库文件或 SIM 数据库文件的名称，从中插值结果以驱动子模型分析。每当子模型分析或子模型边界条件从全局模型的结果读取数据时，需要此选项。

文件扩展名是可选的。如果您省略文件扩展名，Abaqus 使用结果文件。如果结果文件不存在，Abaqus 使用 SIM 输出数据库文件。如果结果文件和 SIM 输出数据库文件都不存在，Abaqus 使用 ODB 数据库文件。

**cpus**：此选项指定在分析运行期间要使用的处理器总数（如果并行处理可用）。此参数的默认值为 1，可以在环境文件中更改（请参阅"环境文件设置"）。

**parallel**：此选项指定用于 Abaqus/Explicit 中基于线程的并行处理的方法。可能的值是 domain 和 loop。默认值是 domain，可以在环境文件中更改（请参阅"环境文件设置"）。

如果 parallel=domain，则使用域级方法将模型分解为几何域。如果 parallel=loop，则使用循环级方法来并行化低级循环。

**domains**：此选项指定 Abaqus/Explicit 中的并行域数量。如果值大于 1，则无论 parallel 和 cpus 选项的值如何，都将执行域分解。但是，如果 parallel=domain，cpus 的值必须能整除 domains 的值。

**dynamic_load_balancing**：对于 Abaqus/Explicit 中的域并行执行（parallel=domain），其中域数量大于 CPU 数量，此选项激活/停用动态负载平衡方案。默认值是 on。Abaqus/Explicit 将尝试通过定期重新分配域到处理器来提高计算效率，从而最小化负载不平衡。

**threads_per_mpi_process**：此参数用于从以下选项中选择并行执行模式：纯 MPI 模式、纯线程模式或混合模式。线程执行模式要求所有核心限制在单个计算节点上，而其他两种模式的核心可以跨越多个计算节点。

值为 1 会产生纯 MPI 模式。纯 MPI 模式在 Abaqus/Explicit 中默认处于活动状态（请参阅"Abaqus/Explicit 中的并行执行"）。等于 cpus 参数的值会产生纯线程模式。介于 1 和 cpus 参数之间的值（可被 cpus 参数值整除）会产生混合模式。混合模式在 Abaqus/Standard 中默认处于活动状态，threads_per_mpi_process 值自动选择（请参阅"Abaqus/Standard 中的并行执行"）。

**standard_parallel**：此选项在 Abaqus/Standard 中指定并行执行模式。可能的值是 all 和 solver。如果 standard_parallel=all，元素操作和求解器都将并行运行。如果 standard_parallel=solver，只有求解器将并行运行。默认值是 standard_parallel=all。

**gpus**：此选项指定 Abaqus/Standard 直接求解器的加速。此选项仅在配备适当 GPGPU 硬件的计算机上才有意义。默认情况下，GPGPU 求解器加速未激活。此参数的值是要在 Abaqus/Standard 分析中使用的 GPGPU 总数。在基于 MPI 的分析中，此参数是所有主机上的 GPGPU 数量。

**memory**：输入文件预处理和 Abaqus/Standard 分析阶段期间可分配的最大内存量或物理内存的最大百分比（请参阅"管理内存和磁盘资源"）。默认值可以在环境文件中更改。

**interactive**：此选项将导致作业交互运行。对于 Abaqus/Standard，日志文件将输出到屏幕；对于 Abaqus/Explicit，状态文件和日志文件将输出到屏幕。默认 run_mode 可以在环境文件中设置。

**background**：此选项将提交作业在后台运行，这是默认设置。日志文件输出将保存在当前目录中的 job-name.log 文件中。

**queue**：此选项将提交作业到批处理队列。如果选项没有值，作业将提交到系统默认队列。允许使用带引号的字符串。可用队列是特定于站点的。

**after**：此选项与 queue 选项一起使用，用于指定作业将在所选批处理队列中开始的时间。

**double**：此选项用于指定 Abaqus/Explicit 使用双精度可执行文件。可能的值是 both、constraint、explicit 和 off。

如果 double=both，Abaqus/Explicit 打包器和分析都将以双精度运行。如果 double=constraint，Abaqus/Explicit 中的约束打包和约束求解器将以双精度运行，而 Abaqus/Explicit 打包器和 Abaqus/Explicit 分析继续以单精度运行。如果 double=explicit，Abaqus/Explicit 分析将以双精度运行，而打包器仍以单精度运行。默认值是 explicit。如果 double=off，则在必要时覆盖环境文件设置，以单精度调用 Abaqus/Explicit 打包器和 Abaqus/Explicit 分析。

**scratch**：此选项用于指定用于临时文件的目录名称。

**output_precision**：此选项指定写入输出数据库文件（job-name.odb）的场输出精度。使用 output_precision=full 会为 Abaqus/Standard 分析产生双精度节点和单元场输出。

**resultsformat**：此选项指定结果的输出格式。如果 resultsformat=odb，输出仅以 ODB 格式写入。如果 resultsformat=sim，输出仅以 SIM 格式写入。如果 resultsformat=both，输出以 ODB 和 SIM 两种格式写入。默认值是 odb。

**port**：此选项用于指定使用直接耦合接口的求解器之间协同仿真的 TCP/UDP 端口号。默认值是 48000。

**host**：此选项与 port 选项一起使用。

**csedirector**：此选项用于指定 SIMULIA Co-Simulation Engine director 进程的连接（例如 host:port）。

**timeout**：此选项用于指定建立协同仿真连接的超时值（以秒为单位）。默认值是 3600 秒。

**noFlexBody**：此选项用于指示不进行生成柔性体的翻译。

**license_type**：此选项用于控制 Abaqus 用于 SimUnit 许可证模型的许可证类型。可能的值是 token 和 credit。默认值是 token。

**ssd_split**：此选项指定将频率分割成分区以通过运行多个 Abaqus 作业来执行稳态动态分析的值。

**ssd_partition**：此选项与 ssd_split 选项指定的频率分割结合使用，指定特定的频率分区号。

#### 数据检查模块的其他选项

**unconnected_regions**：此选项用于请求 Abaqus/Standard 在分析输出数据库中为未连接区域创建单元和节点集。

### 示例

#### 在 Abaqus/Standard 中运行分析

使用以下命令在后台运行名为"c8"的热传导分析：

```
abaqus analysis job=c8 background
```

以下命令在后台运行作业 c8，并将当前环境设置输出到日志文件：

```
abaqus analysis job=c8 information=environment background
```

热传导分析 c8 的后续分析是"c10"，这是一个静态分析，使用 c8 的温度数据作为输入。温度数据从 c8 结果文件作为预定义场读取。执行程序扫描 Abaqus/Standard 输入文件以查找此类文件依赖关系。

使用以下命令在"long"队列中运行作业 c10：

```
abaqus analysis job=c10 queue=long
```

此作业接下来以"c11"重启，使用 c10 的最终结果作为蠕变分析的起点。使用以下命令在默认队列中运行此作业：

```
abaqus analysis job=c11 oldjob=c10 queue=
```

使用以下命令运行名为"draw_imp"的 Abaqus/Standard 分析，该分析从先前运行的名为"draw_exp"的 Abaqus/Explicit 分析导入结果：

```
abaqus analysis job=draw_imp oldjob=draw_exp
```

#### 在 Abaqus/Explicit 中运行分析

使用以下命令将名为"beam"的 Abaqus/Explicit 分析提交到默认队列：

```
abaqus analysis job=beam convert=all queue=
```

等价的结果可以通过以下系列命令获得：

```
abaqus datacheck job=beam interactive
abaqus continue job=beam queue=
abaqus convert=all job=beam interactive
```

CPU 密集型分析选项以批处理模式运行，而其他选项以交互方式运行。

#### 运行分析的不同阶段

使用以下命令对名为"parmodel"的输入文件执行参数检查运行：

```
abaqus job=parmodel parametercheck
```

使用以下命令对名为"parmodel"的输入文件执行数据检查运行：

```
abaqus job=parmodel datacheck
```

以下命令继续之前的 datacheck 作业来执行分析：

```
abaqus job=parmodel continue
```

---

*原文来源：Abaqus 2025 FD02 Execution Guide*
