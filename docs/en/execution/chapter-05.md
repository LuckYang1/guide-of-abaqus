---
title: Abaqus Execution (Part 2)
description: Abaqus Execution Guide chapter
---

# Abaqus Execution (Part 2)

## Abaqus Job Execution Control

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The execution procedures for job execution control include abaqus suspend, abaqus resume, and abaqus terminate. These utilities are used to suspend, resume, and terminate Abaqus analysis jobs. Suspending an analysis job will stop its execution and release its license tokens to the free-token pool. Resuming an analysis will reactivate a suspended job and check out license tokens for that job if they are available. The job will be placed in the license queue if license tokens are not available. Terminating an analysis job will stop the executable for the analysis and release its license tokens. A terminated analysis job cannot be resumed.

You can execute these commands remotely; you are not required to execute these commands on the machine running the analysis.

### Command Summary

```
abaqus {suspend | resume | terminate} {job = job-name | host = hostname port = port-number}
```

### Command Line Options

**job**: This option is used to specify the name of the analysis job to suspend, resume, or terminate. When using this option, the command must be executed from the working directory of the job. The command reads the job-name.cid file to obtain the host name and port number used to signal the job.

**host**: This option is used to specify the host name for the connection running the analysis job. This option must be used in conjunction with the port option. The host name can be identified by reading the last line of the job-name.cid file, which lists hostname:port-number.

**port**: This option is used to specify the port number for the connection running the analysis job. This option must be used in conjunction with the host option. The port number can be identified by reading the last line of the job-name.cid file, which lists hostname:port-number.

## Abaqus/CAE Execution

**Products**: Abaqus/CAE

### References

- About Execution Procedures

### Overview

Abaqus/CAE, an interactive environment for creating, submitting, monitoring, and evaluating results from Abaqus simulations, is executed by running the Abaqus execution procedure and specifying the cae parameter.

### Command Summary

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

### Command Line Options

**database**: This option specifies the name of the model database file or output database file to open.

**replay**: This option specifies the name of the file from which Abaqus/CAE commands are to be replayed.

**recover**: This option specifies the name of the file from which a model database is to be rebuilt.

**startup**: This option specifies the name of the file containing Python configuration commands to be run at application startup.

**script**: Same as startup.

**noGUI**: This option specifies that Abaqus/CAE is to be run without the graphical user interface (GUI). If no file name is specified, an Abaqus/CAE license is checked out and the Python interpreter is initialized to allow interactive entry of Python or Abaqus Scripting Interface commands. If a file name is specified, Abaqus/CAE runs the commands in the file and exits upon their completion.

**noenvstartup**: This option specifies that all configuration commands in the environment files should not be run at application startup.

**noSavedOptions**: This option specifies that Abaqus/CAE should not apply the display options settings stored in abaqus_2025.gpr.

**noSavedGuiPrefs**: This option specifies that Abaqus/CAE should not apply the GUI settings stored in abaqus_2025.gpr.

**noStartupDialog**: This option specifies that the Start Session dialog box for Abaqus/CAE should not be displayed.

**custom**: This option specifies the name of the file containing Abaqus GUI Toolkit commands.

**guiTester**: This option starts a separate user interface containing the Abaqus Python development environment along with Abaqus/CAE.

**guiRecord**: This option enables you to record your actions in the Abaqus/CAE user interface.

**guiNoRecord**: This option enables you to disable user interface recording when the environment variable ABQ_CAE_GUIRECORD is set.

### Examples

**Opening a Model Database**:

```
abaqus cae database=beam
```

**Passing Arguments to a Script**:

```
abaqus cae script=try.py -- argument1
```

**Running Abaqus/CAE without the Graphical User Interface**:

```
abaqus cae noGui=checkPartValidity.py -- test.cae Model-1 Part-1
```

## Abaqus/Viewer Execution

**Products**: Abaqus/Viewer

### References

- About Execution Procedures

### Overview

Abaqus/Viewer, a subset of Abaqus/CAE that contains only the postprocessing capabilities of the Visualization module, is executed by running the Abaqus execution procedure and specifying the viewer parameter.

### Command Summary

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

### Command Line Options

**database**: This option specifies the name of the output database file to use.

**replay**: This option specifies the name of the file from which Abaqus/Viewer commands are read.

**startup**: This option specifies the name of the file containing Python configuration commands to be run at application startup.

**script**: Same as startup.

**noGUI**: This option specifies that Abaqus/Viewer is to be run without the graphical user interface (GUI).

**guiTester**: This option starts a separate user interface containing the Python development environment along with Abaqus/Viewer.

**guiRecord**: This option enables you to record your actions in the Abaqus/Viewer user interface.

**guiNoRecord**: This option enables you to disable user interface recording when the environment variable ABQ_CAE_GUIRECORD is set.

## Making User-Defined Executables and Subroutines

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus make utility is used to create user postprocessing executables and user-defined libraries of Abaqus user subroutines. The commands used to compile and link a user-supplied program or user subroutine source file can be changed using the appropriate Abaqus environment file parameters.

### Command Summary

```
abaqus make {job = job-name | library = source-file}
[user = {source-file | object-file}]
[directory = library-dir]
[object_type = {fortran | c | cpp}]
[uniquelibs]
```

### Command Line Options

**job**: This option is used to create a user-supplied postprocessing program.

**library**: This option is used to create user subroutine object files and shared libraries.

**user**: This option is valid only when used in conjunction with the job option.

**directory**: This option is valid only when used in conjunction with the library option.

**object_type**: This option is valid only when used in conjunction with the job option.

**uniquelibs**: This option is valid only when used in conjunction with the library option.

### Examples

```
abaqus make job=pprocess
```

## Optimization Execution

**Products**: Abaqus/CAE

### References

- About Execution Procedures

### Overview

Optimization using TOSCA for Abaqus is executed by running the Abaqus execution procedure and by providing the name of the parameter file, which, in turn, refers to an Abaqus input file.

### Command Summary

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

### Command Line Options

**task**: This option is used to specify the file containing parameters for executing optimization.

**job**: This option is used to specify the folder name for storing optimization results.

**cpus**: This option specifies the total number of processors to use during an analysis run.

**gpus**: This option specifies acceleration of the Abaqus/Standard direct solver.

**memory**: This option specifies maximum memory or maximum percentage of physical memory that can be allocated during analysis.

**interactive**: This option will cause the job to run interactively.

**globalmodel**: This option specifies the name of the global model's results file, ODB output database file, or SIM database file.

**scratch**: This option is used to specify the name of the directory used for scratch files.

### Examples

```
abaqus optimization task=WeightReduction job=WeightReductionResults
```

## Parametric Studies

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures
- Abaqus/Standard and Abaqus/Explicit Execution

### Overview

The abaqus script tool indicates that a parametric study is to be executed. Each analysis involved in the design can be executed using the execute command.

### Command Summary

```
abaqus script [=script-file]
[startup = startup file-name]
[noenvstartup]
```

### Command Line Options

**script-file**: When a script file name is specified, the parametric study module is imported and the instructions in the parametric study script file are executed.

**startup**: This option specifies the name of the file containing Python configuration commands to be run at application startup.

**noenvstartup**: This option specifies that all configuration commands in the environment files should not be run at application startup.

### Examples

```
abaqus script=parstudy
```

## Abaqus Documentation

**Products**: Abaqus/Standard Abaqus/Explicit Abaqus/CAE

### References

- About Execution Procedures
- Obtaining Help

### Overview

Abaqus documentation is installed separately from the products and is viewed through a web browser.

### Using Abaqus Documentation

The documentation contains the following guides:

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

### Viewing Documentation

1. Enter `abaqus doc`. The documentation opens in a web browser.
2. Click on a book's title to display it.
3. Expand topic headings in the table of contents.

### Command Summary

```
abaqus doc
```

---

*Source: Abaqus 2025 FD02 Execution Guide*
