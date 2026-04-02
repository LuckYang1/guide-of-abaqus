# 第四章：自定义 Abaqus 环境

本章介绍如何使用环境文件参数自定义 Abaqus 执行过程，包括如何定义分析批处理队列。示例文件在章节末尾提供。

## 4.1 使用 Abaqus 环境文件

Abaqus 执行过程读取环境文件以确定用于运行作业的各种参数（请参阅 Abaqus Execution Guide）。

当 Abaqus 启动时，它按以下顺序在三个目录中搜索主环境文件 `abaqus_v6.env`：

1. **安装目录** (`install_dir/os/SMA/site/`)

   安装的 `install_dir/os/SMA/site/` 子目录。此目录中必须存在 `abaqus_v6.env` 文件。
   
   当作业提交到远程队列时，此文件中的参数设置会被忽略；在这种情况下，将使用远程计算机上的 `install_dir/os/SMA/site/abaqus_v6.env` 中的设置。

   从 Abaqus 2016 开始，`abaqus_v6.env` 文件导入并使用以下辅助环境文件中的任何参数定义：
   
   - `custom_v6.env` - 应包含您的站点特定设置，如许可证和文档参数
   - `basic_v6.env` - 包含所有平台通用的参数
   - `win86_64.env` 或 `lnx86_64.env` - 包含特定于平台的参数，如编译器和 MPI 设置
   - `graphicsConfig.env` - 包含 `onCaeGraphicsStartup()` 函数，用于为 Abaqus/CAE 和 Abaqus/Viewer 配置特定于图形卡的设置

   您可以直接在 `install_dir/os/SMA/site/abaqus_v6.env` 文件中添加参数设置；但最佳实践是将您的站点特定设置放在 `install_dir/os/SMA/site/custom_v6.env` 文件中。

2. **用户主目录中的 `abaqus_v6.env` 文件**

   此环境文件是可选的，将影响从用户账户提交的所有作业。每个用户应仅在此文件中包含他们专门想要更改的参数。此文件不应是 `install_dir/os/SMA/site/abaqus_v6.env` 文件的完整副本。

   在 Windows 平台上，要使 Abaqus 找到用户主目录中的环境文件，必须使用 HOME 环境变量或 HOMEDRIVE 和 HOMEPATH 环境变量的组合来指定用户主目录的完整路径。

3. **当前工作目录中的 `abaqus_v6.env` 文件**

   此环境文件是可选的，将影响从当前工作目录提交的所有作业。每个用户应仅在此文件中包含他们专门想要更改的参数。此文件不应是 `install_dir/os/SMA/site/abaqus_v6.env` 文件的完整副本。

如果同一参数在多个环境文件中定义，或在文件内多次定义，则使用最后遇到的定义。

个人用户可以通过在主目录或当前工作目录中创建名为 `abaqus_v6.env` 的新文件来覆盖 `install_dir/os/SMA/site/custom_v6.env` 和 `install_dir/os/SMA/site/abaqus_v6.env` 文件中的站点范围参数设置。这些文件中设置的任何参数将由 Abaqus 最后读取（如上所述），从而覆盖站点范围的值。

如果您是从早期版本升级，请不要简单地将早期版本中 `abaqus_v6.env` 文件中的参数包含进来，而应先检查它们是否必要。

## 4.2 环境文件语法

Abaqus 的环境文件使用 Python 语法。有关 Python 语法的更多详细信息，请参阅 Abaqus Scripting User's Guide。

环境文件条目具有以下语法：

```python
parameter=value
```

所有参数都必须有一个值。以下语法规则也适用：

- 所有参数都区分大小写。
- 字符串值必须用一对双引号或单引号括起来。
- 注释以井号 (#) 开头。该行中井号后的所有字符都会被忽略。引号内的井号是字符串的一部分，不是注释的开头。
- 空行会被忽略。
- 列表必须用方括号 ([ ]) 括起来。列表中的各个项用逗号分隔。条目格式为：

```python
parameter=[value1, value2, value3]
```

- 元组必须用括号 (( )) 括起来。元组中的各个项用逗号分隔。如果元组用括号括起来且只包含一个值，则必须在值后面加逗号。条目格式为：

```python
parameter=(value1, value2)
```

- 如果单引号嵌入在双引号字符串中，则不需要特殊处理。例如，`"my value's"` 被翻译为 `my value's`。同样适用于嵌入在单引号字符串中的双引号。可以用反斜杠 (`\`) 字符作为前缀来嵌入与封闭引号相同类型的引号。列表或元组中的字符串必须用引号括起来。

- 三引号字符串 (`"""`) 可以跨越多行，字符串内的引号不需要特殊处理。条目格式为：

```python
parameter="""multi-line value"""
```

## 4.3 内存和磁盘管理参数

Abaqus/Standard 和 Abaqus/Explicit 的内存和磁盘资源管理在管理内存和磁盘资源中有详细讨论。相关参数在此列出，以及一个用于管理 Abaqus/CAE 和 Abaqus/Viewer 内存的单一参数 `abq_ker_memory`。

内存大小的可用单位是 mb（兆字节）和 gb（吉字节）。如果未指定单位，则假定大小以兆字节为单位。

### abq_ker_memory

Abaqus/CAE 和 Abaqus/Viewer 内核可以分配的最大内存量，以 MB（兆字节）为单位。如果超过限制，Abaqus/CAE 会显示错误消息。

如果内核内存大小达到 `abq_ker_memory` 值或机器的虚拟内存限制，将显示以下消息：由于内存分配失败，操作未能完成。

为获得最佳性能，内存限制应设置为小于机器上的物理内存量。允许的最小设置是 256 MB。

### scratch

要用作临时文件的目录的完整路径名。Linux 上的默认值是 `$TMPDIR` 环境变量的值；如果未定义 `$TMPDIR`，则为 `/tmp`。在 Windows 上，默认值是 `%TEMP%` 环境变量的值；如果未定义 `%TEMP%`，则为 `\TEMP`。在分析期间，将在此目录下创建一个子目录来存放分析临时文件。子目录的名称由用户的用户名、作业 ID 和作业的进程号构成。分析完成后，删除该子目录及其内容。

### memory

在输入文件预处理期间和 Abaqus/Standard 分析阶段可以分配的最大内存量或物理内存的最大百分比。默认值是机器物理内存的 80%。

## 4.4 并行化参数

您可以设置参数来自定义 Abaqus 中的并行执行。

Abaqus 中的并行化在以下章节中有详细讨论：

- Abaqus/Standard 中的并行执行
- Abaqus/Explicit 中的并行执行

相关参数在此列出。

### auto_convert

如果此参数设置为 ON，并且使用 `parallel=domain` 并行运行 Abaqus/Explicit 分析，则在分析需要时，将在分析结束时自动运行 `convert=select`、`convert=state` 和 `convert=odb` 选项。默认值是 ON。

### cpus

如果并行处理可用，则在分析运行期间使用的处理器总数。此参数的默认值是 1。

### direct_solver

将此变量设置为 DMP 以明确选择混合直接稀疏求解器。将其设置为 SMP 以明确选择纯线程的直接稀疏求解器。如果未设置此参数，默认是使用纯线程直接稀疏求解器。

### domains

Abaqus/Explicit 中的并行域数量。如果值大于 1，无论 `parallel` 和 `cpus` 变量的值如何，都将执行域分解。但是，如果 `parallel=DOMAIN`，则 `cpus` 的值必须能被 `domains` 的值整除。如果未设置此参数，如果 `parallel=DOMAIN`，则域数默认设置为分析运行期间使用的处理器数；如果 `parallel=LOOP`，则为 1。

### gpus

在 Abaqus/Standard 中激活使用 GPGPU 硬件的直接求解器加速。此参数的值应该是用于分析的 GPGPU 数量。在基于 MPI 的并行 Abaqus/Standard 分析中，这是跨所有主机使用的 GPGPU 总数。

### max_cpus

如果并行处理可用，则允许的最大处理器数。如果未设置此参数，则允许的处理器数等于系统上可用处理器的数量。

### mp_file_system

基于 MPI 的并行 Abaqus 分析可用的文件系统类型。必须将此参数设置为一个元组；例如：

```python
mp_file_system=(SHARED,LOCAL)
```

元组中的第一项指的是提交作业的目录，第二项指的是作业的临时目录。如果托管目录的文件系统是 LOCAL，Abaqus 会将所需的分析文件复制到远程主机，并在运行结束时将输出文件复制回来。在这种情况下，必须能够在 `mp_host_list` 中的所有主机上创建作业的目录结构。SHARED 文件系统意味着主机共享相同的文件系统，不需要文件传输。使用推荐的默认设置 (DETECT, DETECT)，Abaqus 将确定存在的文件系统类型。基于 MPI 的并行 Abaqus/Explicit 分析仅在使用用户子程序时才会使用临时目录，而 Abaqus/Standard 通常在此目录中写入大型临时文件。在本地文件系统上运行通常会提高性能。

### mp_host_list

要用作并行 Abaqus 分析的主机名列表，以及每台机器上要使用的处理器数量；例如：

```python
mp_host_list=[['maple',1],['pine',1],['oak',2]]
```

这表示，如果为分析指定的 CPU 数量为 4，则分析将在一台名为 maple 的机器上使用一个处理器，在一台名为 pine 的机器上使用一个处理器，在一台名为 oak 的机器上使用两个处理器。主机列表中定义的总处理器数必须大于或等于为分析指定的 CPU 数量。`mp_host_list` 会根据需要进行调整以考虑 `threads_per_mpi_process` 值。如果未定义主机列表，Abaqus 将在本地系统上运行。使用支持的队列系统时，此参数由队列环境设置。

### mp_mpi_implementation

指定要使用的底层 MPI 实现的字典或常量。通常不需要指定此变量。

字典值用于根据所使用的求解器应用 MPI 实现。字典键是 STANDARD、EXPLICIT 或 DEFAULTMPI。字典值是 PMPI、IMPI 或 NATIVE。在 Linux 上，默认设置是以下字典：

```python
mp_mpi_implementation={DEFAULTMPI: IMPI, STANDARD: PMPI}
```

常量值可以是 PMPI、IMPI 或 NATIVE。当适用于所有求解器时使用常量值。例如：

```python
mp_mpi_implementation=PMPI
```

### mp_mpirun_options

传递给基于 MPI 的并行 Abaqus 分析的 MPI 启动器的选项字典或字符串。通常不需要设置此变量。

字典键是常量 PMPI、IMPI 或 NATIVE。例如：

```yaml
mp_mpirun_options={PMPI: '-v -d -t', IMPI: '-verbose'}
```

当适用于所有 MPI 实现时使用字符串。例如：

```python
mp_mpirun_options='-v'
```

### mp_mpirun_path

定义给定 MPI 实现的 MPI 启动器完整路径的字典。例如：

```python
mp_mpirun_path={NATIVE: 'C:\\Program Files\\Microsoft MPI\\Bin\\mpiexec.exe'}
```

```python
mp_mpirun_path={PMPI: '/apps/SIMULIA/Abaqus/2023/linux_a64/code/bin/SMAExternal/pmpi/bin/mpirun',
                 IMPI: '/apps/SIMULIA/Abaqus/2023/linux_a64/code/bin/SMAExternal/impi/bin/mpirun'}
```

### mp_num_parallel_ftps

当使用基于 MPI 的并行化执行并行文件暂存时，此参数控制同时进行的 MPI 文件传输数量。第一个项控制往返临时目录的文件传输。第二个项控制往返分析工作目录的文件传输。将任一值设置为 1 将禁用并行文件暂存过程。文件暂存的使用取决于 `mp_file_system` 中指定的值。

### mp_rsh_command

用于在 `mp_host_list` 中指定的机器上打开远程 shell 的首选命令。当文件系统不共享时，Abaqus 需要打开远程 shell 来创建和删除目录和文件。此选项的默认值是平台相关的；例如：

```batch
mp_rsh_command='ssh -n -l %U %H %C'
```

使用以下占位符：

| 占位符 | 含义 |
|--------|------|
| %U | 用户名 |
| %H | 打开远程 shell 的主机 |
| %C | 要在主机上执行的命令 |

如果此参数设置为使用安全 shell，Abaqus 会自动使用安全复制 (scp) 在远程主机之间来回复制文件。默认情况下，此参数被忽略，而使用内置的 MPI rsh/scp 命令。

### order_parallel

如果您未在 abaqus 命令行上指定并行排序模式，则为 Abaqus/Standard 的默认直接求解器排序模式。如果此参数设置为 OFF，则求解器排序将不会并行执行。如果此参数设置为 ON，求解器排序将并行运行。默认并行求解器排序是 ON。

### parallel

如果您未在 abaqus 命令行上指定并行方法，则为 Abaqus/Explicit 的默认并行方程求解方法。可能的值是 DOMAIN 或 LOOP；默认值是 DOMAIN。

### standard_parallel

如果您未在 abaqus 命令行上指定并行模式，则为 Abaqus/Standard 的默认并行执行模式。如果此参数设置为 ALL，则元素操作和求解器都将并行运行。如果设置为 SOLVER，则只有求解器将并行运行。默认并行执行模式是 ALL。

### threads_per_mpi_process

`threads_per_mpi_process` 选项可与 `cpus` 选项一起使用来配置并行化。`threads_per_mpi_process` 的数量应该是每台主机上处理器数量的因数，最终是总 CPU 数量的因数。对于 Abaqus/Explicit，此参数的默认值是 1，导致纯 MPI 并行化；而对于 Abaqus/Standard，默认会自动设置一个合适的值，尽可能首选混合并行化。

## 4.5 作业定制参数

作业定制参数可用于自定义 Abaqus 分析作业。

### abq_cosimulation_lower_port

此变量指定可供两个 Abaqus 分析之间协同仿真使用的 TCP/UDP 端口号范围的最低端口号；仅对 Abaqus/CAE 有效。默认值是 48000。

### abq_cosimulation_upper_port

此变量指定可供两个 Abaqus 分析之间协同仿真使用的 TCP/UDP 端口号范围的最高端口号；仅对 Abaqus/CAE 有效。如果未指定此值，则设置为比 `abq_cosimulation_upper_port` 高 1000。

### auto_calculate

如果此参数设置为 ANALYSIS，则所有输出数据库后处理都将作为 Abaqus/Standard 分析执行的一部分进行。如果此参数设置为 ON，则如果执行过程检测到需要输出数据库后处理，则在分析结束时由后处理计算器执行输出数据库后处理。如果此参数设置为 OFF，则不会进行输出数据库后处理，即使执行过程检测到需要处理输出数据库文件。默认值是 ANALYSIS。在 Abaqus/Explicit 中，`auto_calculate=ANALYSIS` 等同于 `auto_calculate=ON`。

### average_by_section

此参数仅用于 Abaqus/Standard 分析。如果此参数设置为 OFF，则写入数据 (.dat) 文件和结果 (.fil) 文件的输出平均值区域基于元素结构。如果此参数设置为 ON，平均区域还会考虑元素属性和材料常量的底层值。在具有许多截面和/或材料定义的问题中，默认值 OFF 通常比非默认值 ON 提供更好的性能。

### cae_error_limit

此变量定义将从分析作业发送到 Abaqus/CAE 的最大错误消息数；仅对 Abaqus/CAE 有效。默认值是 50。

### cae_no_parts_input_file

此变量定义由 Abaqus/CAE 生成的输入文件的格式；仅对 Abaqus/CAE 有效。如果此变量设置为 ON，Abaqus/CAE 将生成不包含部件和装配的输入文件。默认值是 OFF。

### cae_warning_limit

此变量定义将从分析作业发送到 Abaqus/CAE 的最大警告消息数；仅对 Abaqus/CAE 有效。默认值是 200。

### double_precision

如果您未在 abaqus 命令行上指定精度版本，则为要运行的 Abaqus/Explicit 默认精度版本。可能的值是 EXPLICIT（仅以双精度运行 Abaqus/Explicit 分析）、BOTH（以双精度运行 Abaqus/Explicit 打包程序和分析）、CONSTRAINT（Abaqus/Explicit 中的约束打包程序和约束求解器以双精度运行，而 Abaqus/Explicit 打包程序和分析继续以单精度运行）或 OFF（以单精度运行 Abaqus/Explicit 打包程序和分析）。默认是 OFF。

### max_history_requests

此参数指定 Abaqus 分析中允许的最大历史请求数。默认值是 10,000。Abaqus 中的历史输出旨在对模型的较小部分进行相对频繁的输出请求，并显示在 Abaqus/CAE 的可视化模块（Ababys/Viewer）的 X-Y 图中。请求大量历史输出会导致 Abaqus 作业的分析和后处理出现性能问题。对于向量或张量值输出变量，每个分量被视为一个请求。对于单元变量，历史输出将在每个积分点生成。例如，请求 C3D10M 单元的张量变量 S（应力）的历史输出将生成 24 个历史输出请求：（6 个分量）&times;（4 个积分点）。在请求向量和张量变量的历史输出时，建议在适用的情况下选择各个分量。当需要大量历史输出时，建议将数据写入输出数据库 (.odb) 作为场输出，从中可以使用 Abaqus/CAE 的可视化模块提取历史数据。

### odb_output_by_default

如果此参数设置为 ON，将自动生成输出数据库输出。如果此参数设置为 OFF，则必须在输入文件中放置输出数据库请求关键字才能获得输出数据库输出并允许分析重新启动。默认值是 ON。

### onCaeGraphicsStartup

在 Abaqus/CAE 或 Abaqus/Viewer 开始之前要执行的可选函数。此函数允许用户更改图形选项。有关此函数的更多信息，请参阅调优图形卡。此函数通常不应更改。

### onCaeStartup

在 Abaqus/CAE 开始之前要执行的可选函数。请参阅自定义 Abaqus/CAE 启动以获取此函数的示例。

### onDesignStartup

在 Abaqus/Design 开始之前要执行的可选函数。

### onJobCompletion

在 Abaqus 作业完成后要执行的可选函数。在当前目录的 Abaqus 环境文件中指定的函数将首先执行，然后是用户主目录中的函数，最后是 Abaqus 安装环境文件中的函数。同一环境文件中的多个函数将导致仅使用最后一个定义。请参阅作业变量以获取可在此函数中使用的变量列表。

### onJobStartup

在 Abaqus 作业开始之前要执行的可选函数。请参阅作业变量以获取可在此函数中使用的变量列表。

### printed_output

默认情况下，所有 \*PREPRINT 参数的值都是 NO，不会将结果打印到数据文件。将 `printed_output` 参数设置为 ON，以在数据文件中获得与在输入文件中包含

```plaintext
\*PREPRINT, CONTACT=YES, ECHO=YES, HISTORY=YES, MODEL=YES
```

相同的前打印信息。将 `printed_output` 设置为 ON 也可能导致大量表格结果打印到数据文件（除非使用打印输出控制选项来限制输出）。如果输入文件以部件和装配的形式编写，将 `printed_output` 设置为 ON 将导致无论 \*PREPRINT 选项上的设置如何，都会在数据文件中打印部件-装配映射；这允许用户将打印的输出与输入文件中定义的部件-装配相关联。此变量的默认值是 OFF。

### run_mode

如果用户在运行分析产品时未在 abaqus 命令行上指定运行模式，则为默认运行模式 (INTERACTIVE、BACKGROUND 或 BATCH)。默认值是 BACKGROUND。除非定义了批处理队列，否则不应将此变量设置为 BATCH。

### split_dat

如果此变量设置为 ON，数据文件将分成两部分。用户输入处理的输出将放在带有 `.pre` 扩展名的文件中。分析输出文件仍将具有 `.dat` 文件扩展名。默认值是 OFF。

### unconnected_regions

如果此变量设置为 ON，Abaqus/Standard 将在数据检查分析期间为模型中未连接的区域在输出数据库中创建单元和节点集。使用此选项创建的单元和节点集名为 `MESH_COMPONENT_N`，其中 N 是组件编号。

## 4.6 系统定制参数

系统定制参数可用于自定义各种系统设置，例如防止对环境文件参数进行未经授权的修改。

### admin

此参数可防止对环境文件参数进行未经授权的修改。将此参数设置为一个环境文件参数列表，这些参数不能在较低级别的 `abaqus_v6.env` 文件中更改。除非另有说明，所有系统和作业定制参数都可以被锁定。安装目录中的命令具有最高优先级，其次是用户主目录中的命令，然后是当前工作目录中的命令。因此，Abaqus 用户无法更改由 Abaqus 账户管理员锁定的环境文件命令。

### ask_delete

如果此参数设置为 OFF，系统不会询问用户是否应删除同名旧作业文件；文件将自动删除。默认值是 ON。

### compile_cpp

C++ 编译命令。SIMULIA 使用的命令包含在安装的 `install_dir/os/SMA/site/` 子目录中的平台特定环境文件 (`win86_64.env` 或 `lnx86_64.env`) 中。此命令通常不应更改。它可以是字符串或字符串元组。如果命令是字符串元组，则每个字符串必须代表一个命令行参数。占位符的值由 Abaqus 执行过程或命令行选项确定，用户无法修改。占位符的值替换 `compile_cpp` 字符串中的占位符。

可用的占位符：

| 占位符 | 含义 |
|--------|------|
| %I | 包含文件的搜索目录 |

### compile_fortran

Fortran 编译命令。SIMULIA 使用的命令包含在安装的 `install_dir/os/SMA/site/` 子目录中的平台特定环境文件 (`win86_64.env` 或 `lnx86_64.env`) 中。此命令通常不应更改。它可以是字符串或字符串元组。如果命令是字符串元组，则每个字符串必须代表一个命令行参数。

默认情况下，不支持使用 Fortran 90 freeform 规范的 Fortran 文件编译。Abaqus 安装的 `/SMA/site/` 子目录中的 `abaqus_v6.env` 文件包含讨论编译选项的注释。

### file_format

结果文件输出的格式（ASCII 或 BINARY）。此参数仅对 Abaqus/Standard 有效。默认值是 BINARY。

### link_exe

链接后处理程序的命令。SIMULIA 使用的命令包含在安装的 `install_dir/os/SMA/site/` 子目录中的平台特定环境文件 (`win86_64.env` 或 `lnx86_64.env`) 中。此命令通常不应更改，但在没有 Fortran 编译器的 Windows 上构建后处理程序的情况下除外。在这种情况下，请参阅 `win86_64.env` 文件中建议的注释更改。此命令可以是字符串或字符串元组。如果命令是字符串元组，则每个字符串必须代表一个命令行参数。占位符的值由 Abaqus 执行过程或命令行选项确定，用户无法修改。用户指定的外部库可以用通常的链接命令链接。

`link_exe` 中使用的占位符：

| 占位符 | 含义 |
|--------|------|
| %J | 作业名称（在这种情况下是要创建的可执行文件的名称）|
| %F | 从用户源文件创建的目标文件名称 |
| %M | 内部创建的主目标文件的名称 |
| %B | 实用函数共享库的名称 |
| %O | 输出数据库应用程序公共接口的实用共享库列表 |
| %L | 包含共享库的目录列表（仅限 HP）|

### link_sl

链接共享库的命令。SIMULIA 使用的命令包含在安装的 `install_dir/os/SMA/site/` 子目录中的平台特定环境文件 (`win86_64.env` 或 `lnx86_64.env`) 中。此命令一旦其占位符被替换，必须是计算机系统上链接共享库的有效命令。此命令可以是字符串或字符串元组。如果命令是字符串元组，则每个字符串必须代表一个命令行参数。占位符的值由 Abaqus 执行过程或命令行选项确定，用户无法修改。

`link_sl` 中使用的占位符：

| 占位符 | 含义 |
|--------|------|
| %F | 编译目标文件的名称 |
| %U | 共享库的名称 |
| %A | 要链接到共享库的编译目标文件存档的名称 |
| %B | 实用函数共享库的名称 |
| %E | 包含要从共享库导出的符号的文件名称 |
| %L | 包含共享库的目录列表（仅限 HP）|

### nodb_cache_limit

临时文件目录中缓存的最大大小。当您使用网络 ODB 连接器从远程输出数据库读取时，Abaqus/CAE 使用此缓存进行本地数据存储。将 `nodb_cache_limit` 参数设置为缓存大小将被限制到的兆字节数。`nodb_cache_limit` 的最小值是 500，表示缓存大小限制为 500 MB。如果您设置的最大缓存大小大于可用空闲空间，Abaqus/CAE 会将其减少到等于可用空闲空间的值。

### plugin_central_dir

包含 Abaqus/CAE 插件的目录的完整路径名或路径名列表。在大多数情况下，这是站点上所有用户都可以访问的某个中心位置的一个或多个目录。

### usub_lib_dir

包含可选的 Abaqus/Standard 和/或 Abaqus/Explicit 用户子程序用户定义库的目录的完整路径名。有效的用户子程序库是特定于平台的，但文件基名称对所有平台都相同。基名称是 `standardU`、`explicitU` 和 `explicitU-D`。使用此变量可避免频繁使用的用户子程序的重新编译和/或重新链接成本。`abaqus make` 实用程序用于创建与此变量一起使用的共享库。用户可以通过 Abaqus/Standard 和 Abaqus/Explicit 执行过程的 user 选项创建的用户库将覆盖此目录中的任何用户库。

### verbose

如果此参数在环境文件中，则执行过程将打印更多关于作业提交的信息。可能的值是 ON、OFF、1、2 和 3。将值设置为 ON 或 1 以打印运行应用程序可执行文件使用的命令和一些性能数据。将值设置为 2 以打印许可证事务信息。将值设置为 3 以打印操作系统环境设置。与 verbose 参数相关的输出被写入标准输出。默认值是 OFF。

以下系统定制参数用于文档安装，以及指定用于在 Abaqus/CAE 中显示 SIMULIA HTML 文档和上下文相关帮助的 Web 浏览器。

### browser_path

Linux 平台上 Web 浏览器可执行文件的完整路径。此参数的值可以是字符串或字符串列表。如果指定了字符串列表，则第一个字符串必须是 Web 浏览器可执行文件的完整路径，后续字符串是用于自定义浏览器行为的参数。如果包含任何参数字符串，则至少其中一个必须包含 `%s`，SIMULIA HTML 文档的完整统一资源定位器 (URL) 将被替换为该位置。

Abaqus 会自动配置支持的浏览器以正确显示 HTML 文档。配置因每个浏览器而异。此参数可与 `browser_type` 结合使用以阐明正在使用的浏览器。如果 `browser_path` 设置为字符串且未设置 `browser_type`，系统会检查指定浏览器路径中的 Firefox。如果 Abaqus 未检测到 Firefox，Abaqus 会假定将使用不支持的浏览器，并且不会执行自动配置。此参数在 Windows 平台上被忽略。

### browser_type

Linux 平台上的 Web 浏览器。要正确显示 HTML 文档，Abaqus 会根据指定的浏览器类型自动配置浏览器。可能的设置是 FIREFOX 和 CUSTOM_BROWSER。如果您设置 `browser_type=CUSTOM_BROWSER` 以使用 Firefox 以外的 Web 浏览器，则不提供支持或自动配置。此参数可与 `browser_path` 结合使用以直接指定浏览器的可执行命令。如果 `browser_type` 设置为 Firefox 且未设置 `browser_path`，系统会在系统路径中搜索 Firefox。如果找不到指定的浏览器，则显示错误。此参数在 Windows 平台上被忽略。

### doc_root

SIMULIA HTML 文档的完整统一资源定位器 (URL) 或路径。

URL 示例：

```python
doc_root="http://<servername>:4040/English"
```

此变量仅影响 Abaqus 到文档的连接，而不影响其他 Established Products；例如 Tosca 和 fe-safe。要为所有 Established Products 配置连接，请参阅安装、许可和配置 > SIMULIA 安装 > Established Products 安装和配置 > 手动配置文档。

### doc_lang

如果有多种语言可用，则为文档的语言。默认是 "English"。

以下参数禁止通过启动文件测试许可证激活之前执行相应的模块。如果尝试执行您的站点没有许可证的分析模块，这些参数可用于提供"友好"消息。将这些参数与 `admin` 参数结合使用以确保整个站点的均匀性。

### no_aqua

如果值设置为 ON，则阻止执行 Abaqus/Aqua。

### no_background

如果值设置为 ON，则阻止 Abaqus 分析作业的后台执行。

### no_batch

如果值设置为 ON，则阻止 Abaqus 分析作业的批处理队列执行。

### no_cae

如果值设置为 ON，则阻止执行 Abaqus/CAE。

### no_design

如果值设置为 ON，则阻止执行 Abaqus/Design。

### no_explicit

如果值设置为 ON，则阻止执行 Abaqus/Explicit。

### no_interactive

如果值设置为 ON，则阻止 Abaqus 分析作业的交互式执行。

### no_standard

如果值设置为 ON，则阻止执行 Abaqus/Standard。

### no_viewer

如果值设置为 ON，则阻止执行 Abaqus/Viewer。

## 4.7 可执行文件参数

许可模块的 Abaqus 可执行文件自动放置在 Abaqus 安装的 `/code/bin/` 子目录中。可以在 Linux 系统上将前缀参数 (\*_prefix) 设置为 "time" 以确定 Abaqus 运行特定阶段的执行时间。

### exe_prefix

所有 Abaqus 分析可执行文件的可选可执行前缀。默认值是空字符串。

### explicit_prefix

Abaqus/Explicit 的可选可执行前缀。给定的此前缀的值将覆盖给 `exe_prefix` 的值。

### explicit_dp_prefix

Abaqus/Explicit 双精度版本的可选可执行前缀。给定的此前缀的值将覆盖给 `exe_prefix` 的值。

### package_prefix

Abaqus/Explicit PACKAGE 程序的可选可执行前缀。给定的此前缀的值将覆盖给 `exe_prefix` 的值。

### pre_prefix

Abaqus 分析输入文件处理器的可选可执行前缀。给定的此前缀的值将覆盖给 `exe_prefix` 的值。

### standard_prefix

Abaqus/Standard 程序的可选可执行前缀。给定的此前缀的值将覆盖给 `exe_prefix` 的值。

## 4.8 许可证管理参数

许可证管理定制参数控制基于当前网络条件和用户需求的 Abaqus 许可证服务器行为。Abaqus 许可证服务器随默认参数一起安装，这些参数应适用于大多数用户。以下参数用于定制：

### abaquslm_license_file

此参数提供运行 Abaqus FLEXnet 许可证服务器的计算机的主机名，并在产品安装期间设置。此参数不适用于 DSLS 许可证服务器。如果使用单个服务器，此参数应设置为 `port@license_server_host`，其中 port 是端口号，license_server_host 是运行服务器的计算机名称：

```python
abaquslm_license_file="27000@rose"
```

如果端口号在 27000 到 27009 之间，则不需要包含它。

如果在 Windows 平台上使用两个独立服务器，用分号分隔参数值中的服务器：

```python
abaquslm_license_file="27000@zinnia;27000@marigold"
```

如果在 Linux 平台上使用两个独立服务器，用冒号分隔参数值中的服务器：

```python
abaquslm_license_file="27000@zinnia:27000@marigold"
```

如果使用三个冗余服务器，用逗号分隔参数值中的服务器：

```python
abaquslm_license_file="27000@maple,27000@pine,27000@oak"
```

### academic

此参数指示学术 Abaqus 客户端是否应使用研究或教学许可证令牌。将此参数设置为 TEACHING 将强制 Abaqus 客户端仅使用教学许可证令牌。将此参数设置为 RESEARCH 或移除参数将强制 Abaqus 仅使用研究许可证令牌。此参数在产品安装期间自动设置：如果许可证服务器包含 Abaqus 教学许可证文件，则安装将参数设置为 TEACHING；否则，设置为 RESEARCH。在某些情况下，可能需要将此参数显式设置为 RESEARCH，而不是依赖默认的未设置值。

### cae_timeout

Abaqus/CAE 或 Abaqus/Viewer 会话由于没有用户活动而保持空闲、将其令牌返回给许可证服务器之前的分钟数。默认值是 60 分钟。

### computer_location

指示本地客户端计算机位置的字符串。此参数允许您按位置细分许可证使用报告。许可证使用报告实用程序根据 `computer_location` 名称编译和组织数据。默认值是空字符串。如果不更改此默认值，许可证使用报告不会在报告中区分不同位置。

### dsls_license_config

Dassault Systèmes 许可证服务器 (DSLS) 配置文件 (DSLicSrv.txt) 的路径。此文件确定要与 Abaqus 一起使用的 Dassault Systèmes 许可证服务器。例如：

**Linux 平台：**

```
/opt/simulia/license/DSLicSrv.txt
```

**Windows 平台：**

```
C:\\SIMULIA\\License\\DSLicSrv.txt
```

### license_model

此参数控制 Abaqus 使用的许可模式。可能的值是 AUTOMATIC（默认）、LEGACY 和 SIMUNIT。如果此参数设置为 SIMUNIT，Abaqus 使用 SimUnit 令牌或 SimUnit 信用。如果设置为 LEGACY，Abaqus 使用模拟令牌（在 SimUnit 令牌和 SimUnit 信用引入之前可用的令牌）。当设置为 AUTOMATIC 时，许可模式由许可证服务器上存在的许可证自动确定。如果许可证服务器上有 SimUnit 令牌或 SimUnit 信用可用，则使用 SimUnit 许可模式。否则，使用旧模式。此参数仅在使用 DSLS 服务器时适用（请参阅 `license_server_type` 参数）。

### license_server_type

Abaqus 客户端使用的许可证服务器软件的类型。可能的值是 FLEXNET 和 DSLS（默认）。

### license_type

此参数控制 Abaqus 使用的许可证类型。可能的值是 CREDIT 和 TOKEN（默认）。此参数仅在使用 SimUnit 许可模式时适用（请参阅 `license_model` 参数）。

### lmhanglimit

当没有可用许可证时，Abaqus 客户端在许可证队列中等待的分钟数。默认值 0 强制作业无限期保留在许可证队列中，除非被用户终止。

### lminteractivequeuing

此参数指示交互式 Abaqus/CAE 或 Abaqus/Viewer 会话是否应在没有许可证可用时排队等候。要允许交互式运行的 Abaqus/CAE 或 Abaqus/Viewer 会话排队等候许可证，请将此参数设置为 ON。默认值是 OFF。`lmlicensequeuing` 参数用于在没有图形用户界面的情况下运行的会话排队。

### lmlicensequeuing

此参数指示 Abaqus 分析作业或使用 noGUI 选项的 Abaqus/CAE 或 Abaqus/Viewer 会话是否应在没有许可证可用时排队等候。默认值是 ON。如果此参数设置为 OFF，如果没有可用许可证，作业和 Abaqus/CAE 或 Abaqus/Viewer 会话将立即终止。`lminteractivequeuing` 参数用于交互式运行的会话排队。

### lmlog

此参数指示是否应将许可证使用数据写入 FLEXnet 调试日志文件。要使用 Abaqus 许可证使用报告实用程序，此参数必须设置为 ON，这是默认值。要禁止调试日志文件中的许可证使用数据，请将此参数设置为 OFF。

### lmproject

此可选参数可用于记录有关公司内部项目名称或编号的信息。`lmproject` 参数可以设置为任何字符串值；例如：

```python
lmproject="turbomachinery-project-23"
```

可以在每个用户的主目录中的环境文件中设置此参数，并且可以在需要更改为不同项目名称时随时进行编辑。

有关 Abaqus 许可证检出和相关项目名称的信息记录在许可证服务器上，可以通过使用时 Accessor 项目获取历史报告来检索。

### lmqueuesleep

Abaqus 客户端在检查许可证队列以查看是否有足够空闲令牌之前等待的秒数。默认值是 30 秒，这是允许的最小值。增加此值将减少发生许可证排队时的网络流量。

### lmsvrdownlimit

如果许可证服务器当前不可用，Abaqus 客户端尝试连接许可证服务器的分钟数。默认值 0 强制作业无限期尝试连接，除非被用户终止。

## 4.9 作业变量

以下变量可在 `onJobStartup` 或 `onJobCompletion` 函数中使用：

| 变量 | 描述 |
|------|------|
| id | 在命令行上指定为作业选项值的作业标识符 |
| savedir | 提交作业的目录的路径名 |
| scrdir | 临时目录的路径名 |
| analysisType | 要执行的 analysis 类型。可能的值是 EXPLICIT 和 STANDARD |

此外，对于基于 MPI 的并行作业，以下变量在 `onJobStartup` 或 `onJobCompletion` 函数中可用：

| 变量 | 描述 |
|------|------|
| host_list | 用于分析的主机名列表，包括每台机器上使用的处理器数量。格式与 `mp_host_list` 环境变量相同 |
| local_host | 用于确定提交作业的主机名的标识符列表（例如主机名、IP 地址、别名等）|
| rsh_command | 用于在分析期间使用的机器上打开远程 shell 的命令。格式与 `mp_rsh_command` 环境变量相同 |
| file_system | 显示基于 MPI 的并行作业使用的文件系统类型的元组。元组中的第一项指的是提交作业的目录，第二项指的是作业的临时目录 |
| cpus | 跨所有主机求和的分析使用的总处理器数 |

以下变量可在 `onJobStartup` 和 `onJobCompletion` 函数之外使用：

| 变量 | 描述 |
|------|------|
| abaqus_version | 包含 Abaqus 版本的字符串 |
| analysisType | 要执行的 analysis 类型。可能的值是 EXPLICIT 和 STANDARD |
| applicationName | 要执行的 Abaqus 执行过程的名称；例如 analysis、cae 或 viewer |

---

[返回目录](./index.md) | [上一章：Abaqus 配置指南](./chapter-03.md) | [下一章：定义分析批处理队列](./chapter-05.md)
