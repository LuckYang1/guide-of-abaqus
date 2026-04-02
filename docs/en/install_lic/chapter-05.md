# Chapter 5: Defining Analysis Batch Queues

Analysis batch queues are used to configure how Abaqus analysis jobs are run. They are particularly useful for integrating Abaqus with third-party batch queue systems.

Running an Abaqus job requires two pieces of information: the command syntax for executing the job and job-specific information. The command for executing the job is obtained from queue definitions in the Abaqus environment file. Job-specific information is obtained from command line options and analysis parameters defined in the Abaqus environment file. Command line options are described in the Abaqus Execution Guide.

The command syntax and job-specific information are used to construct the command for running an Abaqus job in the analysis queue. Two interfaces are available for defining analysis batch queues: the object-oriented interface and the string-based interface. The object-oriented interface is preferred because it is easy to customize and extend. This section discusses the object-oriented interface; for information on the string-based interface, refer to String-Based Batch Queue Parameters.

## 5.1 Object-Oriented Batch Queue Parameters

The object-oriented interface for defining analysis batch queues is easy to customize and extend. Once instantiated and inserted into the analysis queue dictionary, analysis batch queues are available from the Abaqus execution procedure command line.

In the Abaqus environment file, predefined (built-in) queue classes are available for instantiating user-defined queue objects. In addition to the predefined queue classes, users can create their own queue classes to customize how analysis jobs are executed. New queue classes can be derived from the predefined queue classes to reduce the user's coding effort. The `driverQueues` module must be imported to instantiate predefined queues or derive custom queue classes. The predefined classes are described in Queue Classes and Predefined Derived Classes.

### queues

A dictionary of queue names and objects. Queue names and their corresponding object instances are inserted into the dictionary as key/value pairs. The special queue name `default` can be used to specify the default queue. The default queue is used when `run_mode` is set to BATCH and no queue option is specified on the command line. The default queue is also used when a queue option is specified on the command line but the named queue is empty or does not exist in the queue dictionary.

## 5.2 String-Based Batch Queue Parameters

The string-based interface for defining analysis batch queues allows access to a fixed number of options. The parameters below are available for constructing command strings to control the execution of Abaqus analyses. The only requirement is that the string must be a valid command on the computer system that executes it.

### after_prefix

An optional prefix that is output as part of the submission command when the after option is specified on the command line. The default value is an empty string.

### queue_cmd

The default command for submitting batch jobs when `run_mode` is set to BATCH. This parameter must be a valid command on the computer system that executes it once its placeholders are replaced. The values of placeholders are defined by input specified on the Abaqus execution procedure command line or by environment file parameters. The values of placeholders replace the placeholders in the `queue_cmd` string.

Available placeholders:

| Placeholder | Meaning |
|-------------|---------|
| %% | The percent (%) character |
| %A | When the after option is specified on the command line, the `after_prefix` string replaces %A |
| %L | The log file name. This token is replaced with `job-name.log`, where `job-name` is the value defined by the job command line option |
| %P | When a queue name is specified on the command line, the `queue_prefix` string (see below) replaces %P |
| %Q | The queue name from the queue command line option |
| %S | The command script file name. This token is replaced with `job-name.com`, where `job-name` is the value defined by the job command line option |
| %T | The time from the after command line option |
| %J | The job name from the job command line option |
| %E | Replaced with the full path to the Python executable |
| %O | The full path to the output directory |

### queue_name

A list of names for batch commands, typically used for jobs submitted to queues other than the default queue (defined by `queue_cmd`). These command aliases must then appear on the left side of an equal sign elsewhere in the environment file, with the desired command string on the right. This command string has the same format as the `queue_cmd` parameter. It can use replaceable placeholders in its construction as long as the end result is a valid system command.

### queue_prefix

An optional prefix that is output as part of the submission command when a queue name is specified. The default value is an empty string.

## 5.3 Queue Classes

The Queue class is an abstract base class. All other analysis batch queue classes are derived from it. The class has no explicit constructor or members. The following queue class methods are common to all derived classes:

### __repr__(...)

This method returns the class name as a string. When `abaqus information=environment` is executed, this string is printed as the description of the queue. Derived classes should override this method to provide a useful description of the queue objects instantiated from them.

### createScript(...)

This method creates a Python script named `job-name.com` in the current working directory. This script is used to run the analysis. This method is called by the analysis execution procedure before the submit method. If the `job-name.com` file cannot be written in the current working directory, a `FileCreationError` exception is raised. The following parameter is required:

- **options**: A dictionary containing analysis options.

### getDriverName(...)

This method returns the command name used to invoke the Abaqus execution procedure.

### getPython(...)

This method returns the absolute path to the Abaqus Python interpreter as a string.

### getNumRequiredTokens(...)

This method returns the number of license tokens required for the analysis as an integer. The following parameter is required:

- **options**: A dictionary containing analysis options.

### spawn(...)

This method executes the command in a new process, waits for its completion, and returns an integer representing the command's exit status. If the command cannot be executed, a `SpawnError` exception is raised. The following parameters are required:

- **cmd**: A valid command string to execute in a new process. If an analysis is submitted to this queue from Abaqus/CAE, the command must return status immediately; otherwise, the ability to monitor analysis job progress in Abaqus/CAE may fail. Examples of commands that return status immediately are qsub, bsub, at, batch, etc.
- **env**: A dictionary of environment variables available to the process.

The following parameter is optional:

- **verbose**: A boolean value specifying whether the command string is printed to stdout. The default value is OFF.

### submit(...)

This abstract method must be implemented by derived classes. This method is called by the analysis execution procedure to submit the analysis to the queue. The submit method must return an integer; 0 for success, non-zero for failure. When this method is called, the analysis execution procedure provides the following required parameters:

- **options**: A dictionary containing analysis options.
- **env**: A dictionary of environment variables available to the process.

Most derived classes call the spawn method from this method and return its exit status.

## 5.4 Predefined Derived Classes

The following analysis batch queue classes are derived from the Queue base class:

### AtQueue Class

The AtQueue class uses the Linux at command to execute analyses. This class overrides the following base class methods:

- **__repr__(...)**: This method returns a string describing the class.
- **submit(...)**: This method executes the Linux at command to run the `job-name.com` analysis script at the time specified by the after option on the command line. If the after option is not specified on the command line, a QueueError exception is raised.

### BatchQueue Class

The BatchQueue class uses the Linux batch command to execute analyses. This class overrides the following base class methods:

- **__repr__(...)**: This method returns a string describing the class.
- **submit(...)**: This method executes the `job-name.com` analysis script under the Linux batch command.

### HoldQueue Class

The HoldQueue class creates the `job-name.com` file and exits. This class overrides the following base class methods:

- **__repr__(...)**: Reimplemented to provide a useful description.
- **submit(...)**: This method prints a message stating that the `job-name.com` script was not submitted and returns 0.

### LSFQueue Class

The LSFQueue class submits analyses to the LSF queue specified when the object is instantiated. If a name is not specified, analyses are submitted to the default LSF queue. The following constructor parameter is optional:

- **name**: The name of a valid LSF queue.

This class overrides the following base class methods:

- **submit(...)**: This method calls the LSF bsub command to submit the `job-name.com` analysis script to the LSF batch cluster and returns the exit status of the bsub command.

### NQSQueue Class

The NQSQueue class submits analyses to the NQS queue specified when the object is instantiated. If a name is not specified, analyses are submitted to the default NQS queue. The following constructor parameter is optional:

- **name**: The name of a valid NQS queue.

This class overrides the following base class methods:

- **submit(...)**: This method calls the NQS qsub command to submit the `job-name.com` analysis script to the NQS system and returns the exit status of the qsub command.

### PBSQueue Class

Queues instantiated from the PBSQueue class create a `job-name.pbs` script and run the command `qsub job-name.pbs`. The `job-name.inp` and `job-name.com` files are copied to the execution host, where the `job-name.com` script is executed. When the job completes, all output files are copied back to the submission host. The following constructor parameter is optional:

- **name**: The name of a valid PBS queue.

This class overrides the following base class methods:

- **submit(...)**: This method calls the PBS qsub command to submit the `job-name.pbs` script to the PBS system and returns the exit status of the qsub command.

## 5.5 Examples

### Example Environment File

The following is an example of a Windows environment file. This file can also work on Linux systems if the temporary directory settings are changed appropriately. An example environment file `abaqusinc.env` showing the options used by SIMULIA is included in the installation subdirectory `install_dir/os/SMA/site/`.

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

### Notifying Users When Jobs Complete

The following is an example of how environment file commands can be used to notify users when their jobs complete on Linux systems. The notification method used depends on how the job was run and whether the user is logged in. If run interactively, users are not notified that the job has completed. If the user is still logged in when the job completes, a message is sent to the screen. If the user has logged out when the job completes, mail is sent to the user.

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

### Using Predefined Derived Classes

The following example shows the instantiation of some predefined derived classes and how they are inserted into the queue dictionary:

```python
run_mode = BATCH
from driverQueues import *
queues['atq'] = AtQueue()
queues['batchq'] = BatchQueue()
queues['hold'] = HoldQueue()
```

To submit an analysis using one of these queues, specify the queue name as the value in the analysis execution procedure queue parameter.

### Deriving and Using Custom Queue Classes

To derive a custom queue class, the `driverQueues` module must be imported, and the class must inherit from the Queue class directly or indirectly. A derived queue must provide an implementation for the submit method. Derived class methods may raise exceptions as needed. The predefined `QueueError` exception is provided as a general exception.

The following example shows the derivation and use of a custom queue class:

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

### Defining String-Based Analysis Batch Queues

The following example shows how to use the environment file parameters for defining string-based analysis batch queues:

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

### Locking Modification of Environment File Parameters

In the following example, all Abaqus jobs run in batch mode by default, and execution of Abaqus/Aqua jobs is not allowed. The inclusion of the `admin` parameter prevents these settings from being modified in lower-level environment files. If this parameter is part of the environment file in the installation directory, the values of `run_mode` and `no_aqua` override any corresponding values in the user's local directory or on the command line. Consequently, this example restricts all jobs at your site to run in batch mode.

```python
run_mode = BATCH
no_aqua = ON
admin = ['run_mode','no_aqua']
```

The `no_aqua` parameter is typically used to provide "friendly" messages to users when your site does not have an Abaqus/Aqua license.

---

[Return to Contents](./index.md) | [Previous Chapter: Customizing the Abaqus Environment](./chapter-04.md) | [Next Chapter: Customizing Abaqus/CAE and Abaqus/Viewer](./chapter-06.md)
