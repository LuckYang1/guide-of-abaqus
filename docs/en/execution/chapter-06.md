---
title: User Subroutines and Advanced Features
description: Abaqus Execution Guide chapter
---

# User Subroutines and Advanced Features

## SIMULIA Co-Simulation Engine Director Execution

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

Co-simulation between Abaqus/Standard and Abaqus/Explicit is controlled by an additional process called the SIMULIA Co-Simulation Engine (CSE) director. Generally, you do not need to invoke the CSE director process; it is called automatically when you run an Abaqus co-simulation, or if you submit a co-simulation from Abaqus/CAE.

If you are unable to use the Abaqus co-simulation execution procedure or Abaqus/CAE and need to submit a co-simulation analysis separately using the Abaqus execution procedure, you must invoke the CSE director as described in this section.

### Command Summary

```
abaqus cse job = cosim-job-name
configure = configuration file-name
listenerport = listener port-number
[datacheck]
[interactive]
[license_type = {token | credit}]
```

### Command Line Options

**job**: This option specifies the name of the co-simulation summary log file generated during the run.

**configure**: This option specifies the name of the SIMULIA Co-Simulation Engine configuration file that governs the co-simulation.

**listenerport**: This option is used to specify the TCP/UDP port number for co-simulation inbound messages to the director.

**datacheck**: This option causes the director to check the configuration file for correctness only.

**interactive**: This option causes the director to run interactively.

**license_type**: This option is used to control the type of license Abaqus uses for the SimUnit license model. The possible values are token and credit. The default value is token.

### Examples

**Running Abaqus/Standard to Abaqus/Explicit Co-Simulation**:

Use the following command to allow the first Abaqus analysis (running on machine "earth") to connect to the co-simulation director (running on machine "mercury" and listening on port 44444):

```
abaqus job=explicit csedirector=mercury:44444
```

Use the following command to allow the second Abaqus analysis (running on machine "venus") to connect to the co-simulation director:

```
abaqus job=standard csedirector=mercury:44444
```

Use the following command to allow the co-simulation director (running on machine "mercury") to operate according to the co-simulation configuration defined in the file explicit_standard_config.xml and receive communications through port 44444:

```
abaqus cse job=cosim listenerport=44444 configure=explicit_standard_config.xml
```

## Abaqus/Standard, Abaqus/Explicit, and FMU Co-Simulation Execution

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

Co-simulation between Abaqus/Standard and Abaqus/Explicit, as well as co-simulation with Functional Mockup Unit (FMU) files, can be executed by running the Abaqus co-simulation execution procedure. Several parameters can be set either on the command line or in the environment file.

The co-simulation analysis executes specified "child" analyses and directs communication according to the co-simulation configuration file specification.

### Command Line Parameter Composition

You can specify command line arguments for participating child analyses using a comma-separated list of options. Command line arguments are divided into:

- Global options, taking a single argument
- Options applicable to Abaqus child analyses, taking a comma-separated list
- Options applicable to FMUs, taking a comma-separated list

### Allocating CPUs to Abaqus Jobs for Parallel Processing

Your CPU allocation specification applies to Abaqus/Standard and Abaqus/Explicit child jobs. Functional Mockup Units (FMU) do not support multi-CPU usage. Three methods are available for allocating CPUs for parallel processing: specifying the number of CPUs per job, distributing CPUs among analysis jobs, and distributing CPUs among analysis products.

**Specifying the Number of CPUs per Job**: The most straightforward approach is to use the cpus parameter to specify the number of CPUs used by each child analysis.

**Distributing CPUs among Analysis Jobs**: You can specify the total number of CPUs for the co-simulation analysis and weight factors that determine how CPUs are distributed among the child analyses.

**Distributing CPUs among Analysis Products**: You can specify the total number of CPUs for the co-simulation analysis and weight factors for distributing CPUs among the analysis products participating in the co-simulation.

### Limitations

The following limitations apply to co-simulation execution:

- An analysis can run on a single machine or on a compute cluster whose head node can be shared by two child analysis jobs.
- This execution procedure does not support co-simulation with third-party applications.

### Command Summary

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

### Examples

**Running Abaqus/Standard to FMU Co-Simulation Interactively**:

```
abaqus cosimulation cosimjob=cosim_controls job=plant configure=cosim_controls fmu=controller interactive
```

**Submitting Abaqus/Standard to Abaqus/Explicit Co-Simulation to Batch Queue**:

```
abaqus cosimulation cosimjob=beam job=beam,beam2 configure=beam_config cpus=8,4 queue=long
```

## SIMULIA Co-Simulation Engine FMU Execution

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures
- SIMULIA Co-Simulation Engine Director Execution

### Overview

Any number of Functional Mockup Unit (FMU) files can be used for signal/actuator co-simulation with Abaqus/Standard or Abaqus/Explicit. FMU files comply with the Functional Mockup Interface (FMI) standard defined by the Modelisar organization.

### Warning

This procedure is recommended only when the more general co-simulation execution procedure does not support your FMU co-simulation use case.

### Command Summary

```
abaqus fmu csedirector = CSE director hosts:port-number
fmu = fmu-file-name
instance = co-simulation-instance-name
[interactive]
[timeout = timeout value in seconds]
```

### Command Line Options

**csedirector**: This option is used to specify the connection for co-simulation messages between the CSE director and FMU execution.

**fmu**: This option specifies the FMU file name to be used for co-simulation.

**instance**: This option specifies the instance name of the FMU.

**interactive**: This option causes the director to run interactively.

**timeout**: This option is used to specify a timeout value in seconds for establishing the co-simulation director connection.

### Examples

**Running Co-Simulation Director**:

```
abaqus cse job=cosim listenerport=44444 configure=cosim_config.xml
```

**Running First FMU-based Simulation**:

```
abaqus fmu fmu=controller.fmu instance=controller1 csedirector=mercury:44444
```

**Running Second FMU-based Simulation**:

```
abaqus fmu fmu=controller.fmu instance=controller2 csedirector=mercury:44444
```

**Running Abaqus/Standard Simulation**:

```
abaqus job=standard csedirector=mercury:44444
```

---

*Source: Abaqus 2025 FD02 Execution Guide*
