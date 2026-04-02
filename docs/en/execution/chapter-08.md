---
title: System and Scripting Tools
description: Abaqus Execution Guide chapter
---

# System and Scripting Tools

## Hardware System Verification Process

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus verify process checks the installation and configuration of the hardware system.

### Command Summary

```
abaqus verify
```

## Python Execution

**Products**: Abaqus/Standard Abaqus/Explicit Abaqus/CAE

### References

- About Execution Procedures

### Overview

You can run Python scripts using the Abaqus execution procedure. Python is installed with Abaqus and configured with the appropriate environment variables.

### Command Summary

```
abaqus python script-file [arguments]
```

### Command Line Options

**script-file**: This option specifies the Python script file to execute.

**arguments**: Optional arguments to pass to the script.

### Examples

```
abaqus python script.py
abaqus python script.py arg1 arg2
```

## Licensing Utilities

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

Abaqus provides utilities for managing licenses.

### License Information

Use the following command to display license information:

```
abaqus information=support
```

## Querying the Keyword/Problem Database

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus fetch utility retrieves sample input files from the Abaqus installation.

### Command Summary

```
abaqus fetch job = job-name
```

### Command Line Options

**job**: This option specifies the name of the job to fetch.

### Examples

```
abaqus fetch job=beam
```

## Reducing Analysis Database File Sizes for Restart

**Products**: Abaqus/Standard

### References

- About Execution Procedures

### Overview

The abaqus compact utility reduces the size of analysis database files for restart.

### Command Summary

```
abaqus compact job = job-name
```

### Command Line Options

**job**: This option specifies the job name.

## Output Database Upgrade Utility

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus upgrade utility upgrades output database files to the current release format.

### Command Summary

```
abaqus upgrade input = input-file output = output-file
```

### Command Line Options

**input**: This option specifies the input file to upgrade.

**output**: This option specifies the upgraded output file.

---

*Source: Abaqus 2025 FD02 Execution Guide*
