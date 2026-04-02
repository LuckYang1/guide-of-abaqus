# 第五章：定义分析批处理队列

分析批处理队列用于配置 Abaqus 分析作业的运行方式。它们对于将 Abaqus 与第三方批处理队列系统集成特别有用。

运行 Abaqus 作业需要两条信息：执行作业的命令语法和作业特定信息。执行作业的命令从 Abaqus 环境文件中的队列定义获取。作业特定信息从命令行选项和 Abaqus 环境文件中定义的分析参数获取。命令行选项在 Abaqus Execution Guide 中描述。

命令语法和作业特定信息用于构造在分析队列中运行 Abaqus 作业的命令。定义分析批处理队列有两种接口可用：面向对象的接口和基于字符串的接口。面向对象的接口是首选，因为它易于定制和扩展。本节讨论面向对象的接口；有关基于字符串的接口的信息，请参阅基于字符串的批处理队列参数。

## 5.1 面向对象的批处理队列参数

定义分析批处理队列的面向对象接口易于定制和扩展。一旦实例化并插入到分析队列字典中，就可以从 Abaqus 执行过程命令行获得分析批处理队列。

在 Abaqus 环境文件中，预定义（内置）队列类可用作实例化用户定义的队列对象。除了预定义队列类，用户还可以创建自己的队列类来定制分析作业的执行方式。新的队列类可以从预定义的队列类派生以减少用户的编码工作。必须导入 `driverQueues` 模块才能实例化预定义队列或派生自定义队列类。预定义类在队列类和预定义派生类中描述。

### queues

队列名称和对象的字典。队列名称及其对应的对象实例作为键/值对插入到字典中。特殊的队列名称 `default` 可用于指定默认队列。当 `run_mode` 设置为 BATCH 且命令行上未指定队列选项时，使用默认队列。当在命令行上指定队列选项但命名队列为空或不存在于队列字典中时，也使用默认队列。

## 5.2 基于字符串的批处理队列参数

定义分析批处理队列的基于字符串的接口允许访问固定数量的选项。下面的参数可用于构造命令字符串来控制 Abaqus 分析的执行。唯一的要求是字符串必须是执行它的计算机系统上的有效命令。

### after_prefix

当在命令行上指定 after 选项时，作为提交命令的一部分输出的可选前缀。默认值是空字符串。

### queue_cmd

当 `run_mode` 设置为 BATCH 时，用于提交批处理作业的默认命令。此参数一旦其占位符被替换，必须是执行它的计算机系统上的有效命令。占位符的值由 Abaqus 执行过程的命令行上指定的输入或环境文件参数定义。占位符的值替换 `queue_cmd` 字符串中的占位符。

可用的占位符：

| 占位符 | 含义 |
|--------|------|
| %% | 百分号 (%) 字符 |
| %A | 当在命令行上指定 after 选项时，`after_prefix` 字符串替换 %A |
| %L | 日志文件名。此令牌将替换为 `job-name.log`，其中 `job-name` 是作业命令行选项定义的值 |
| %P | 当在命令行上指定队列选项时，`queue_prefix` 字符串（见下文）替换 %P |
| %Q | 来自队列命令行选项的队列名称 |
| %S | 命令脚本文件名。此令牌将替换为 `job-name.com`，其中 `job-name` 是作业命令行选项定义的值 |
| %T | 来自 after 命令行选项的时间 |
| %J | 来自作业命令行选项的作业名称 |
| %E | 替换为 Python 可执行文件的完整路径 |
| %O | 输出目录的完整路径 |

### queue_name

批处理命令的名称列表，通常用于提交到默认队列以外的队列的作业（由 `queue_cmd` 定义）。然后，在环境文件的其他地方，这些命令别名必须出现在等号左侧，右侧是所需的命令字符串。此命令字符串与 `queue_cmd` 参数具有相同的格式。它可以使用其构造中的可替换占位符，只要最终结果是有效的系统命令。

### queue_prefix

当指定队列名称时，作为提交命令的一部分输出的可选前缀。默认值是空字符串。

## 5.3 队列类

队列类是一个抽象基类。所有其他分析批处理队列类都派生自它。该类没有显式构造函数或成员。以下队列类方法对所有派生类都是通用的：

### __repr__(...)

此方法返回类名作为字符串。当执行 `abaqus information=environment` 时，该字符串被打印为队列的描述。派生类应覆盖此方法以提供从其实例化的队列对象的有用描述。

### createScript(...)

此方法在当前工作目录中创建一个名为 `job-name.com` 的 Python 脚本。此脚本用于运行分析。此方法在提交方法之前由分析执行过程调用。如果无法在当前工作目录中写入 `job-name.com` 文件，则引发 `FileCreationError` 异常。以下参数是必需的：

- **options**：包含分析选项的字典。

### getDriverName(...)

此方法返回用于调用 Abaqus 执行过程的命令名称。

### getPython(...)

此方法将 Abaqus Python 解释器的绝对路径作为字符串返回。

### getNumRequiredTokens(...)

此方法将分析所需许可证令牌的数量作为整数返回。以下参数是必需的：

- **options**：包含分析选项的字典。

### spawn(...)

此方法在新进程中执行命令，等待其完成，并返回表示命令退出状态的整数。如果无法执行命令，则引发 `SpawnError` 异常。以下参数是必需的：

- **cmd**：在新进程中执行的有效命令字符串。如果从 Abaqus/CAE 提交到此队列的分析，则命令必须立即返回状态；否则，可能会导致在 Abaqus/CAE 中监控分析作业进度的能力失败。立即返回状态的命令示例有 qsub、bsub、at、batch 等。
- **env**：可供进程使用的环境变量字典。

以下参数是可选的：

- **verbose**：一个布尔值，指定是否将命令字符串打印到 stdout。默认值是 OFF。

### submit(...)

此抽象方法必须由派生类实现。此方法由分析执行过程调用以将分析提交到队列。提交方法必须返回一个整数；0 表示成功，非零值表示失败。调用此方法时，分析执行过程提供以下必需参数：

- **options**：包含分析选项的字典。
- **env**：可供进程使用的环境变量字典。

大多数派生类从此方法调用 spawn 方法并返回其退出状态。

## 5.4 预定义派生类

以下分析批处理队列类派生自队列基类：

### AtQueue 类

AtQueue 类使用 Linux at 命令执行分析。此类覆盖以下基类方法：

- **__repr__(...)**：此方法返回一个描述该类的字符串。
- **submit(...)**：此方法执行 Linux at 命令，以在命令行上 after 选项指定的时间运行 `job-name.com` 分析脚本。如果未在命令行上指定 after 选项，则引发 QueueError 异常。

### BatchQueue 类

BatchQueue 类使用 Linux batch 命令执行分析。此类覆盖以下基类方法：

- **__repr__(...)**：此方法返回一个描述该类的字符串。
- **submit(...)**：此方法在 Linux batch 命令下执行 `job-name.com` 分析脚本。

### HoldQueue 类

HoldQueue 类创建 `job-name.com` 文件并退出。此类覆盖以下基类方法：

- **__repr__(...)**：重新实现以提供有用的描述。
- **submit(...)**：此方法打印一条消息，说明 `job-name.com` 脚本未被提交，并返回 0。

### LSFQueue 类

LSFQueue 类将分析提交到实例化对象时指定的 LSF 队列。如果未指定名称，则将分析提交到默认 LSF 队列。以下构造函数参数是可选的：

- **name**：有效 LSF 队列的名称。

此类覆盖以下基类方法：

- **submit(...)**：此方法调用 LSF bsub 命令将 `job-name.com` 分析脚本提交到 LSF 批处理集群，并返回 bsub 命令的退出状态。

### NQSQueue 类

NQSQueue 类将分析提交到实例化对象时指定的 NQS 队列。如果未指定名称，则将分析提交到默认 NQS 队列。以下构造函数参数是可选的：

- **name**：有效 NQS 队列的名称。

此类覆盖以下基类方法：

- **submit(...)**：此方法调用 NQS qsub 命令将 `job-name.com` 分析脚本提交到 NQS 系统，并返回 qsub 命令的退出状态。

### PBSQueue 类

从 PBSQueue 类实例化的队列将创建 `job-name.pbs` 脚本并运行命令 `qsub job-name.pbs`。`job-name.inp` 和 `job-name.com` 文件将被复制到执行主机，在那里将执行 `job-name.com` 脚本。作业完成后，所有输出文件将被复制回提交主机。以下构造函数参数是可选的：

- **name**：有效 PBS 队列的名称。

此类覆盖以下基类方法：

- **submit(...)**：此方法调用 PBS qsub 命令将 `job-name.pbs` 脚本提交到 PBS 系统，并返回 qsub 命令的退出状态。

## 5.5 示例

### 示例环境文件

以下是 Windows 环境文件的示例。如果适当更改临时目录设置，此文件也可以在 Linux 系统上工作。安装子目录 `install_dir/os/SMA/site/` 中包含一个示例环境文件 `abaqusinc.env`，用于显示 SIMULIA 使用的选项。

```python
scratch = "c:/temp"
if applicationName in ('analysis','datacheck','continue'):
    memory = "4 gb"

def onCaeStartup():
    # Graphics preferences
    session.graphicsOptions.setValues(dragMode=AS_IS, displayLists=ON)
    # Print preferences
    session.printOptions.setValues(vpDecorations=OFF,
        vpBackground=OFF, rendition=COLOR,
        printCommand='lpr -S marley -P hp3')
    session.psOptions.setValues(date=OFF)
    # Job preferences
    def setJobPreferences(module, userData):
        session.Queue(name='long', hostName='server',
            queueName='large', directory='/tmp')
        addImportCallback('job', setJobPreferences)
    # Visualization preferences
    def setVisPreferences(module, userData):
        session.defaultOdbDisplay.contourOptions.setValues(
            renderStyle=SHADED, visibleEdges=EXTERIOR,
            contourStyle=CONTINUOUS)
        addImportCallback('visualization', setVisPreferences)
```

### 作业完成时通知用户

以下是环境文件命令如何用于在 Linux 系统用户作业完成时通知他们的示例。使用的通知方法取决于作业的运行方式以及用户是否已登录。如果交互式运行，用户不会收到作业已完成的通知。如果用户在作业完成时仍已登录，则会向屏幕输出消息。如果用户在作业完成时已注销，则会向用户发送邮件。

```python
def onJobCompletion():
    import os, re
    userName = os.environ['USER']
    msg = 'Job %s has completed' % id
    # Run "who" command, pipe the output, and read into a list
    whopipe = os.popen('who', 'r')
    output = whopipe.readlines()
    whopipe.close()
    # Find out if the user is logged in
    loggedIn = 'no'
    terminal = []
    for line in output:
        columns = re.split('[ ]+', line)  # Split into blank separated columns
        name = columns[0]  # User name is in the first column
        if name == userName:
            terminal.append(columns[1])  # Terminal at which user is logged in
            loggedIn = 'yes'
    # Use "write" command if the user is logged in, use mail otherwise
    if loggedIn == 'no':
        logFile = savedir + id + ".log"
        if os.path.exists(logFile):
            os.system('cat %s | Mail -s "%s" %s' % (logFile, msg, userName))
        else:
            os.system('Mail -s "%s" %s' % (msg, userName))
    else:
        for termNum in terminal:
            os.system('echo "%s" write %s %s' % (msg, userName, termNum))
```

### 使用预定义派生类

以下示例说明了一些预定义派生类的实例化以及它们如何插入到队列字典中：

```python
run_mode = BATCH
from driverQueues import *
queues['atq'] = AtQueue()
queues['batchq'] = BatchQueue()
queues['hold'] = HoldQueue()
```

要使用其中一个队列提交分析，请在分析执行过程队列参数中指定队列名称作为值。

### 派生和使用自定义队列类

要派生自定义队列类，必须导入 `driverQueues` 模块，并且该类必须直接或间接从队列类继承。派生队列必须为 submit 方法提供实现。派生类方法可以根据需要引发异常。提供了预定义的 `QueueError` 异常作为通用异常。

以下示例说明自定义队列类的派生和使用：

```python
run_mode = BATCH
from driverQueues import *

class NiceQueue(Queue):
    def __repr__(self):
        return 'Executes analysis using Linux nice command.'

    def submit(self, options, env):
        job = options['job']
        after = options.get('after', '')
        verbose = options.get('verbose', 0)
        if options.get('after', ''):
            raise QueueError, \
                '"after" is not a valid argument for this queue.'
        # run nice under bourne shell to eliminate platform dependencies
        cmd = "/bin/sh -c 'nice %s python ./%s.com 1>./%s.log 2>&1 &'" \
            % (self.getDriverName(), job, job)
        return self.spawn(cmd, env, verbose)

class LSF_ResvQueue(LSFQueue):
    # For integration with LSF. This queue class supports cpu, memory,
    # and license reservations.
    def __init__(self, name, memReserve=0, cpusReserve=0):
        LSFQueue.__init__(self, name)
        self.memReserve = memReserve
        self.cpusReserve = cpusReserve

    def __repr__(self):
        return 'Submits to LSF %s queue (run "bqueues -l %s" for description)' \
            % (self.name, self.name)

    def submit(self, options, env):
        job = options['job']
        verbose = options.get('verbose', 0)
        queue = self.name
        cpus = options.get('cpus', '1')
        if self.cpusReserve:
            cpus = self.cpusReserve
        resLst = []
        # license reservation
        resLst.append('abqtokens=%d' % self.getNumRequiredTokens(options))
        # memory reservation
        if self.memReserve:
            from math import ceil
            resLst.append('mem=%d' % int(ceil(self.memReserve/float(cpus))))
        resStr = ''
        if resLst:
            import string
            resStr = '-R rusage[%s]' % string.join(resLst, ':')
        bsub = 'bsub -q %s -J %s -n %s -o %s.log -N %s %s python %s.com' % \
            (queue, job, cpus, job, resStr, self.getDriverName(), job)
        return self.spawn(bsub, env, verbose)

# queue definitions
queues['default'] = NiceQueue()
queues['hold'] = HoldQueue()
queues['benchmark'] = LSF_ResvQueue(name='benchmark', cpusReserve=16)
queues['dedicated'] = LSF_ResvQueue(name='dedicated')
queues['a500M'] = LSF_ResvQueue(name='a500M', memReserve=500)
queues['a1500M'] = LSF_ResvQueue(name='a1500M', memReserve=1500)
queues['a3000M'] = LSF_ResvQueue(name='a3000M', memReserve=3000)
queues['a6000M'] = LSF_ResvQueue(name='a6000M', memReserve=6000)
```

### 定义基于字符串的分析批处理队列

以下示例说明如何使用基于字符串的分析批处理队列定义的环境文件参数：

```python
try:
    queue_name=list(queue_name)
except:
    queue_name = []
queue_name=queue_name + ["aba_short", "aba_long", "hold "]
after_prefix="-a"
queue_prefix="-q"
queue_cmd="qsub -nr -me %P %Q %A %T -x -eo -o %L %S"
aba_short="qsub -nr -me -q short %A %T -x -eo -o %L %S"
aba_long="qsub -nr -me -q long %A %T -x -eo -o %L %S"
hold="printf 'Job %S not submitted\n' "
```

### 锁定环境文件参数的修改

在以下示例中，所有 Abaqus 作业默认将以批处理模式运行，并且不允许执行 Abaqus/Aqua 作业。`admin` 参数的包含可防止在较低级别的环境文件中修改这些设置。如果此参数是安装目录中环境文件的一部分，则 `run_mode` 和 `no_aqua` 的值将覆盖用户本地目录或命令行中的任何相应值。因此，此示例限制您站点的所有作业以批处理模式运行。

```python
run_mode = BATCH
no_aqua = ON
admin = ['run_mode','no_aqua']
```

`no_aqua` 参数通常用于在您的站点没有 Abaqus/Aqua 许可证时向用户提供"友好"消息。

---

[返回目录](./index.md) | [上一章：自定义 Abaqus 环境](./chapter-04.md) | [下一章：自定义 Abaqus/CAE 和 Abaqus/Viewer](./chapter-06.md)
