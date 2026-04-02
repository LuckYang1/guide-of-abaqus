---
title: Environment File Settings
description: Abaqus Execution Guide chapter
---

# Environment File Settings

## Overview

The Abaqus execution procedure uses environment parameters to customize the execution of a job. These settings can be changed using one of the Abaqus environment files: custom_v6.env or abaqus_v6.env.

If the same job parameter is defined in more than one environment file or is defined more than once within the same environment file, the last definition encountered will be used.

## Environment Settings Hierarchy

Abaqus environment settings have the following hierarchy (from lowest to highest priority):

1. **abaqus_v6.env**: Default environment file created during Abaqus installation
2. **custom_v6.env**: User-customized environment file
3. **Command line arguments**: Parameters specified directly on the command line

## Syntax

Environment files are text files containing a series of environment variable assignments. Each line has the format:

```
variable_name = value
```

### Variable Types

- **Integer variables**: e.g., `cpus = 4`
- **Float variables**: e.g., `memory = 80%`
- **String variables**: e.g., `scratch = /tmp/abaqus`
- **Boolean variables**: e.g., `standard_parallel = all`

## Troubleshooting

### Checking Environment Settings

Use the following command to display current environment settings:

```
abaqus information=environment
```

### Common Issues

- If job behavior is abnormal, check environment file syntax
- Ensure variables are not defined multiple times in the same file
- Use `abaqus information=system` to check system configuration

## Command Line Default Parameters

### cpus

Specifies the number of CPUs for analysis. The default is typically 1.

```
cpus = 4
```

### domains

Specifies the number of parallel domains in Abaqus/Explicit.

```
domains = 4
```

### double_precision

Specifies double precision execution.

```
double_precision = explicit
```

### parallel

Specifies the parallel method (domain or loop).

```
parallel = domain
```

### run_mode

Specifies the run mode (interactive or background).

```
run_mode = background
```

### scratch

Specifies the scratch directory.

```
scratch = /tmp/abaqus
```

### standard_parallel

Specifies the standard parallel option (all or solver).

```
standard_parallel = all
```

### gpus

Specifies the number of GPUs.

```
gpus = 2
```

### unconnected_regions

Specifies whether to create sets for unconnected regions.

```
unconnected_regions = yes
```

## System Resource Parameters

### memory

**Syntax**: `memory = memory_specification`

**Description**: Specifies the maximum amount of memory or maximum percentage of physical memory that Abaqus can use during analysis.

**Example**:
```
memory = 80%
memory = 4GB
```

## System Customization Parameters

### ask_delete

Specifies whether to prompt for confirmation before overwriting existing files.

```
ask_delete = off
```

### auto_calculate

Enables automatic calculation.

```
auto_calculate = on
```

### auto_convert

Specifies automatic conversion options.

```
auto_convert = all
```

### average_by_section

Averages output by section.

```
average_by_section = on
```

### mp_host_list

Specifies the MPI host list.

```
mp_host_list = [['host1', 4], ['host2', 4]]
```

### odb_output_by_default

Enables ODB output by default.

```
odb_output_by_default = on
```

### output_warnings_level

Specifies the warning level.

```
output_warnings_level = 1
```

### onCaeStartup

Specifies scripts to run at startup.

```
onCaeStartup = ['script1.py', 'script2.py']
```

## Export of Environment Variables during Parallel Execution

During parallel execution, certain environment variables are exported to child processes.

## Co-Simulation Parameters

### cosimulation_port

Specifies the co-simulation port number.

```
cosimulation_port = 48000
```

### cosimulation_timeout

Specifies the co-simulation timeout value in seconds.

```
cosimulation_timeout = 3600
```

### cpus_weight_std

Specifies the CPU weight for Abaqus/Standard.

```
cpus_weight_std = 2
```

### cpus_weight_xpl

Specifies the CPU weight for Abaqus/Explicit.

```
cpus_weight_xpl = 1
```

### portpool

Specifies the port pool range.

```
portpool = [51000, 52000]
```

## Environment File Examples

### Linux Environment File

```bash
# Linux Environment File Example
cpus = 4
memory = 80%
scratch = /tmp/abaqus
standard_parallel = all
```

### Windows Environment File

```batch
@REM Windows Environment File Example
set cpus=4
set memory=80%
set scratch=C:\TEMP\abaqus
set standard_parallel=all
```

---

*Source: Abaqus 2025 FD02 Execution Guide*
