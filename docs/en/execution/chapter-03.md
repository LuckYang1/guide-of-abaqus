---
title: Execution Procedures Overview
description: Abaqus Execution Guide chapter
---

# Execution Procedures Overview

## About Execution Procedures

### Overview

Abaqus is executed by using the Abaqus execution procedure. In the following discussion the command to run the execution procedure is assumed to be abaqus. However, you can customize the execution procedure to run Abaqus using any alias you choose. (See the Abaqus Configuration Guide for details.)

The abaqus command is described in Execution Procedures. The following sections contain further information about running Abaqus jobs:

- Environment File Settings
- Managing Memory and Disk Resources
- Parallel Execution
- File Extension Definitions
- Fortran Unit Numbers

### Conventions

The following conventions are used in these sections:

- Each discussion includes a "Command summary" section that provides the syntax for the command in the left column and the syntax for its options in the right column. The full command must appear first, followed by the options. In some cases the command has multiple words, such as abaqus fetch; you must enter all words of the command before issuing any option statements.
- Options are presented in boldface. They can appear in any order and can be abbreviated.
- Default options are underlined ( __ ).
- Items enclosed in square brackets ([ ]) are optional.
- Items appearing in a list separated by bars ( | ) are mutually exclusive.
- One value must be selected from a list of values enclosed by curly brackets ({ }).
- You must supply values in italics.
- Blanks are used as separators between options and must not precede nor follow an equal sign.
- An alternate syntax of -optionvalue can be used instead of the option=value format.

If abaqus is typed with no options, prompts are issued for all options.

### Environment Settings

The Abaqus execution procedure uses environment parameters to customize the execution of a job. These settings can be changed using one of the Abaqus environment files: custom_v6.env or abaqus_v6.env.

If the same job parameter is defined in more than one environment file or is defined more than once within the same environment file, the last definition encountered will be used. Some exceptions to this rule are noted in Environment File Settings. These environment files can be used to customize the behavior of Abaqus, including modification of the default options.

### Selecting TCP/UDP Port Numbers

Several of the execution procedure command line options, such as port and listenerport, require that you specify a port number. TCP/UDP port numbers can range from 0 to 65535.

Port numbers 0 to 1023 are well-known ports used by system processes (such as FTP, SSH, SMTP, etc.) and should never be used. Port numbers 1024 to 49151 are registered ports with the Internet Assigned Number Authority (IANA) by software vendors. These ports can be used, but you should be careful that you are not conflicting with any software installed on your system that may be using this port. Port numbers 49152 to 65535 are unreserved and can be used freely, as long as no other application uses them.

Ports may be blocked by a firewall. Contact your system administrator to ensure that the ports that you want to specify are not blocked.

You can use the netstat command to obtain information on TCP/UDP network connections.

## Execution Procedures

This section describes using the abaqus command to run Abaqus.

This section contains the following subsections:

- Abaqus Execution
- Abaqus Co-Simulation
- Abaqus Utilities
- Translating Other Solver Input to Abaqus Input
- Translating Abaqus Output to Another Format

### Abaqus Execution

This section describes using the abaqus command to run Abaqus and the abaqus doc command to run Abaqus documentation.

This section contains the following subsections:

- Obtaining Information
- Abaqus/Standard and Abaqus/Explicit Execution
- Abaqus Job Execution Control
- Abaqus/CAE Execution
- Abaqus/Viewer Execution
- Making User-Defined Executables and Subroutines
- Optimization Execution
- Parametric Studies
- Abaqus Documentation

## Obtaining Information

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The Abaqus execution procedure can be used to obtain help regarding command syntax or information about the installation and computing environment.

### Command Summary

```
abaqus {help | information = {environment | local | memory | release | support | system | all} [job = job-name] | whereami}
```

### Command Line Options

**help**: This option prints a summary of the abaqus command syntax.

**information**: This option writes information about the installation and the environment that is in effect to the screen. The following information is output for all information requests: the current release, the directory in which Abaqus is located, and the directory in which the information files are located.

- If information=environment, the current settings of the environment file options are displayed.
- If information=local, the local installation notes are output.
- If information=memory, some suggestions for setting memory parameters for analysis jobs are output.
- If information=release, information is provided about where to locate the current release notes.
- If information=support, information on diagnosing hardware-related issues is provided. Please send this information to systems support when requesting assistance.
- If information=system, information is provided about system software and hardware resources (operating system level, compiler levels, processor type, graphics board, memory, etc).
- If information=all, information on all of the above information topics is output.

**job**: If a job-name is specified, the information text is written to the file job-name.log.

**whereami**: This option prints the location of the Abaqus release directory.

### Examples

Use the following command to display the local installation notes:

```
abaqus information=local
```

The following command will write the local installation notes to the file support.log:

```
abaqus information=local job=support
```

---

*Source: Abaqus 2025 FD02 Execution Guide*
