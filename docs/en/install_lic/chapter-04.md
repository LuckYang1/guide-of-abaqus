# Chapter 4: Customizing the Abaqus Environment

This chapter describes how to customize Abaqus execution procedures using environment file parameters, including how to define analysis batch queues. Example files are provided at the end of the sections.

## 4.1 Using Abaqus Environment Files

The Abaqus execution procedure reads environment files to determine the various parameters used for running jobs (see the Abaqus Execution Guide).

When Abaqus starts, it searches for the master environment file `abaqus_v6.env` in three directories in the following order:

1. **Installation directory** (`install_dir/os/SMA/site/`)

   The `install_dir/os/SMA/site/` subdirectory of the installation. The `abaqus_v6.env` file must exist in this directory.

   Parameter settings in this file are ignored when a job is submitted to a remote queue; in that case, settings from `install_dir/os/SMA/site/abaqus_v6.env` on the remote computer are used.

   Starting with Abaqus 2016, the `abaqus_v6.env` file imports and uses any parameter definitions from the following auxiliary environment files:

   - `custom_v6.env` - Should contain your site-specific settings, such as license and documentation parameters
   - `basic_v6.env` - Contains parameters common to all platforms
   - `win86_64.env` or `lnx86_64.env` - Contains platform-specific parameters, such as compiler and MPI settings
   - `graphicsConfig.env` - Contains the `onCaeGraphicsStartup()` function for configuring graphics card-specific settings for Abaqus/CAE and Abaqus/Viewer

   You can add parameter settings directly in the `install_dir/os/SMA/site/abaqus_v6.env` file; however, best practice is to place your site-specific settings in the `install_dir/os/SMA/site/custom_v6.env` file.

2. **`abaqus_v6.env` file in the user home directory**

   This environment file is optional and affects all jobs submitted from the user account. Each user should include only the parameters they specifically want to change in this file. This file should not be a complete copy of the `install_dir/os/SMA/site/abaqus_v6.env` file.

   On Windows platforms, for Abaqus to find the environment file in the user home directory, you must specify the full path of the user home directory using either the HOME environment variable or a combination of the HOMEDRIVE and HOMEPATH environment variables.

3. **`abaqus_v6.env` file in the current working directory**

   This environment file is optional and affects all jobs submitted from the current working directory. Each user should include only the parameters they specifically want to change in this file. This file should not be a complete copy of the `install_dir/os/SMA/site/abaqus_v6.env` file.

If the same parameter is defined in multiple environment files or multiple times within a file, the last encountered definition is used.

Individual users can override site-wide parameter settings in `install_dir/os/SMA/site/custom_v6.env` and `install_dir/os/SMA/site/abaqus_v6.env` by creating a new file named `abaqus_v6.env` in their home directory or current working directory. Any parameters set in these files are read last by Abaqus (as described above), thereby overriding the site-wide values.

If you are upgrading from an earlier release, do not simply include parameters from your earlier `abaqus_v6.env` file; check whether they are still needed first.

## 4.2 Environment File Syntax

Abaqus environment files use Python syntax. For more details on Python syntax, refer to the Abaqus Scripting User's Guide.

Environment file entries have the following syntax:

```python
parameter=value
```

All parameters must have a value. The following syntax rules also apply:

- All parameters are case-sensitive.
- String values must be enclosed in a pair of double quotes or single quotes.
- Comments begin with a pound sign (#). All characters after the pound sign on that line are ignored. A pound sign inside quotes is part of the string, not the start of a comment.
- Blank lines are ignored.
- Lists must be enclosed in square brackets ([ ]). Individual items in the list are separated by commas. Entry format:

```python
parameter=[value1, value2, value3]
```

- Tuples must be enclosed in parentheses (( )). Individual items in the tuple are separated by commas. If the tuple is enclosed in parentheses and contains only one value, you must include a comma after the value. Entry format:

```python
parameter=(value1, value2)
```

- If a single quote is embedded inside a double-quoted string, no special treatment is required. For example, `"my value's"` translates to `my value's`. The same applies to double quotes embedded in single-quoted strings. Quotes of the same type as the enclosing quotes can be embedded by prefixing them with a backslash (`\`). Strings in lists or tuples must be enclosed in quotes.

- Triple-quoted strings (`"""`) can span multiple lines, and quotes inside the string do not require special treatment. Entry format:

```python
parameter="""multi-line value"""
```

## 4.3 Memory and Disk Management Parameters

Memory and disk resource management for Abaqus/Standard and Abaqus/Explicit is discussed in detail in Managing Memory and Disk Resources. Related parameters are listed here, along with a single parameter `abq_ker_memory` for managing Abaqus/CAE and Abaqus/Viewer memory.

Available units for memory size are mb (megabytes) and gb (gigabytes). If no unit is specified, the size is assumed to be in megabytes.

### abq_ker_memory

The maximum amount of memory in MB (megabytes) that can be allocated by the Abaqus/CAE and Abaqus/Viewer kernel. If this limit is exceeded, Abaqus/CAE displays an error message.

If the kernel memory size reaches either the `abq_ker_memory` value or the machine's virtual memory limit, the following message is displayed: The operation could not be completed due to memory allocation failure.

For best performance, the memory limit should be set to less than the physical memory on the machine. The minimum allowed setting is 256 MB.

### scratch

The full pathname of the directory to use for temporary files. The default value on Linux is the value of the `$TMPDIR` environment variable; if `$TMPDIR` is not defined, it is `/tmp`. On Windows, the default value is the value of the `%TEMP%` environment variable; if `%TEMP%` is not defined, it is `\TEMP`. During analysis, a subdirectory is created under this directory to hold the analysis temporary files. The subdirectory name is composed of the user's username, job ID, and job process number. After analysis completion, the subdirectory and its contents are deleted.

### memory

The maximum amount of memory or maximum percentage of physical memory that can be allocated during input file preprocessing and the Abaqus/Standard analysis phase. The default value is 80% of the physical memory on the machine.

## 4.4 Parallelization Parameters

You can set parameters to customize parallel execution in Abaqus.

Parallelization in Abaqus is discussed in detail in the following sections:

- Parallel Execution in Abaqus/Standard
- Parallel Execution in Abaqus/Explicit

Related parameters are listed here.

### auto_convert

If this parameter is set to ON and an Abaqus/Explicit analysis is running in parallel using `parallel=domain`, the `convert=select`, `convert=state`, and `convert=odb` options are automatically run at the end of the analysis if needed. The default value is ON.

### cpus

The total number of processors to be used during the analysis run if parallel processing is available. The default value for this parameter is 1.

### direct_solver

Set this variable to DMP to explicitly select the hybrid direct sparse solver. Set it to SMP to explicitly select the pure thread-based direct sparse solver. If this parameter is not set, the default is to use the pure thread-based direct sparse solver.

### domains

The number of parallel domains in Abaqus/Explicit. If the value is greater than 1, domain decomposition is performed regardless of the values of the `parallel` and `cpus` variables. However, if `parallel=DOMAIN`, the value of `cpus` must be evenly divisible by the value of `domains`. If this parameter is not set, when `parallel=DOMAIN`, the number of domains defaults to the number of processors used during the analysis run; when `parallel=LOOP`, it defaults to 1.

### gpus

Activates the use of GPGPU hardware for direct solver acceleration in Abaqus/Standard. The value of this parameter should be the number of GPGPUs to be used for the analysis. In MPI-based parallel Abaqus/Standard analyses, this is the total number of GPGPUs used across all hosts.

### max_cpus

The maximum number of processors allowed if parallel processing is available. If this parameter is not set, the allowed number of processors equals the number of processors available on the system.

### mp_file_system

The type of file system available to MPI-based parallel Abaqus analyses. This parameter must be set to a tuple; for example:

```python
mp_file_system=(SHARED,LOCAL)
```

The first item in the tuple refers to the directory from which the job was submitted, and the second item refers to the job's temporary directory. If the file system hosting the directory is LOCAL, Abaqus copies the required analysis files to the remote host and copies the output files back at the end of the run. In this case, the directory structure for the job must be creatable on all hosts in the `mp_host_list`. A SHARED file system means that the hosts share the same file system and no file transfer is required. With the recommended default settings (DETECT, DETECT), Abaqus determines the type of file system that exists. MPI-based parallel Abaqus/Explicit analyses use the temporary directory only when user subroutines are used, while Abaqus/Standard typically writes large temporary files to this directory. Running on a local file system usually improves performance.

### mp_host_list

The list of hostnames to be used as hosts for parallel Abaqus analyses, along with the number of processors to be used on each machine; for example:

```python
mp_host_list=[['maple',1],['pine',1],['oak',2]]
```

This indicates that if four CPUs are specified for the analysis, the analysis will run using one processor on a machine named maple, one processor on a machine named pine, and two processors on a machine named oak. The total number of processors defined in the host list must be greater than or equal to the number of CPUs specified for the analysis. The `mp_host_list` is adjusted as needed to account for the `threads_per_mpi_process` value. If no host list is defined, Abaqus runs on the local system. This parameter is set by the queue environment when using a supported queue system.

### mp_mpi_implementation

A dictionary or constant specifying the underlying MPI implementation to use. This variable does not normally need to be specified.

Dictionary values are used to apply MPI implementations based on the solver being used. Dictionary keys are STANDARD, EXPLICIT, or DEFAULTMPI. Dictionary values are PMPI, IMPI, or NATIVE. On Linux, the default setting is the following dictionary:

```python
mp_mpi_implementation={DEFAULTMPI: IMPI, STANDARD: PMPI}
```

A constant value can be PMPI, IMPI, or NATIVE. Constant values are used when applicable to all solvers. For example:

```python
mp_mpi_implementation=PMPI
```

### mp_mpirun_options

A dictionary or string of options for the MPI launcher for MPI-based parallel Abaqus analyses. This variable does not normally need to be set.

Dictionary keys are the constants PMPI, IMPI, or NATIVE. For example:

```yaml
mp_mpirun_options={PMPI: '-v -d -t', IMPI: '-verbose'}
```

A string is used when applicable to all MPI implementations. For example:

```python
mp_mpirun_options='-v'
```

### mp_mpirun_path

A dictionary defining the full path to the MPI launcher for a given MPI implementation. For example:

```python
mp_mpirun_path={NATIVE: 'C:\\Program Files\\Microsoft MPI\\Bin\\mpiexec.exe'}
```

```python
mp_mpirun_path={PMPI: '/apps/SIMULIA/Abaqus/2023/linux_a64/code/bin/SMAExternal/pmpi/bin/mpirun',
                 IMPI: '/apps/SIMULIA/Abaqus/2023/linux_a64/code/bin/SMAExternal/impi/bin/mpirun'}
```

### mp_num_parallel_ftps

When performing parallel file staging with MPI-based parallelization, this parameter controls the number of simultaneous MPI file transfers. The first item controls file transfers to and from the temporary directory. The second item controls file transfers to and from the analysis working directory. Setting either value to 1 disables the parallel file staging process. The use of file staging depends on the value specified in `mp_file_system`.

### mp_rsh_command

The preferred command for opening a remote shell on machines specified in `mp_host_list`. When the file system is not shared, Abaqus needs to open a remote shell to create and delete directories and files. The default value for this option is platform-dependent; for example:

```batch
mp_rsh_command='ssh -n -l %U %H %C'
```

Use the following placeholders:

| Placeholder | Meaning |
|-------------|---------|
| %U | Username |
| %H | Host on which to open the remote shell |
| %C | Command to execute on the host |

If this parameter is set to use a secure shell, Abaqus automatically uses secure copy (scp) to copy files back and forth between remote hosts. By default, this parameter is ignored and the built-in MPI rsh/scp commands are used.

### order_parallel

The default direct solver ordering mode for Abaqus/Standard if you do not specify a parallel ordering mode on the abaqus command line. If this parameter is set to OFF, solver ordering is not performed in parallel. If this parameter is set to ON, solver ordering runs in parallel. The default parallel solver ordering is ON.

### parallel

The default parallel equation solution method for Abaqus/Explicit if you do not specify a parallel method on the abaqus command line. Possible values are DOMAIN or LOOP; the default value is DOMAIN.

### standard_parallel

The default parallel execution mode for Abaqus/Standard if you do not specify a parallel mode on the abaqus command line. If this parameter is set to ALL, both element operations and the solver run in parallel. If set to SOLVER, only the solver runs in parallel. The default parallel execution mode is ALL.

### threads_per_mpi_process

The `threads_per_mpi_process` option can be used together with the `cpus` option to configure parallelization. The number for `threads_per_mpi_process` should be a factor of the number of processors on each host, and ultimately a factor of the total number of CPUs. For Abaqus/Explicit, the default value for this parameter is 1, resulting in pure MPI parallelization; for Abaqus/Standard, a suitable value is set automatically by default, with hybrid parallelization preferred when possible.

## 4.5 Job Customization Parameters

Job customization parameters can be used to customize Abaqus analysis jobs.

### abq_cosimulation_lower_port

This variable specifies the lowest port number in the range of TCP/UDP port numbers available for co-simulation between two Abaqus analyses; valid only for Abaqus/CAE. The default value is 48000.

### abq_cosimulation_upper_port

This variable specifies the highest port number in the range of TCP/UDP port numbers available for co-simulation between two Abaqus analyses; valid only for Abaqus/CAE. If this value is not specified, it is set to 1000 higher than `abq_cosimulation_upper_port`.

### auto_calculate

If this parameter is set to ANALYSIS, all output database postprocessing is performed as part of the Abaqus/Standard analysis execution. If this parameter is set to ON, output database postprocessing is performed by the postprocessing calculator at the end of the analysis if the execution procedure detects that postprocessing of the output database is required. If this parameter is set to OFF, no output database postprocessing is performed, even if the execution procedure detects that the output database files require processing. The default value is ANALYSIS. In Abaqus/Explicit, `auto_calculate=ANALYSIS` is equivalent to `auto_calculate=ON`.

### average_by_section

This parameter is for Abaqus/Standard analyses only. If this parameter is set to OFF, the output averaging regions written to the data (.dat) file and results (.fil) file are based on the element structure. If this parameter is set to ON, the averaging regions also consider the underlying values of element properties and material constants. In problems with many section and/or material definitions, the default value OFF generally provides better performance than the non-default value ON.

### cae_error_limit

This variable defines the maximum number of error messages that are sent from an analysis job to Abaqus/CAE; valid only for Abaqus/CAE. The default value is 50.

### cae_no_parts_input_file

This variable defines the format of the input file generated by Abaqus/CAE; valid only for Abaqus/CAE. If this variable is set to ON, Abaqus/CAE generates input files that do not contain parts and assemblies. The default value is OFF.

### cae_warning_limit

This variable defines the maximum number of warning messages that are sent from an analysis job to Abaqus/CAE; valid only for Abaqus/CAE. The default value is 200.

### double_precision

The default precision version for Abaqus/Explicit to run if you do not specify the precision version on the abaqus command line. Possible values are EXPLICIT (run Abaqus/Explicit analysis only in double precision), BOTH (run Abaqus/Explicit postprocessor and analysis in double precision), CONSTRAINT (the constraint postprocessor and constraint solver in Abaqus/Explicit run in double precision, while the Abaqus/Explicit postprocessor and analysis continue to run in single precision), or OFF (run Abaqus/Explicit postprocessor and analysis in single precision). The default is OFF.

### max_history_requests

This parameter specifies the maximum number of history requests allowed in an Abaqus analysis. The default value is 10,000. History output in Abaqus is intended for relatively frequent output requests on smaller portions of the model and appears in X-Y plots in the visualization module (Abaqus/Viewer) of Abaqus/CAE. Requesting a large amount of history output can cause performance problems during analysis and postprocessing of Abaqus jobs. For vector or tensor valued output variables, each component is considered one request. For element variables, history output is generated at each integration point. For example, requesting history output for the tensor variable S (stress) for C3D10M elements generates 24 history output requests: (6 components) &times; (4 integration points). When requesting history output for vector and tensor variables, it is recommended to select individual components where applicable. When a large amount of history output is required, it is recommended to write the data to the output database (.odb) as field output, from which history data can be extracted using the visualization module of Abaqus/CAE.

### odb_output_by_default

If this parameter is set to ON, output database output is generated automatically. If this parameter is set to OFF, you must place output database request keywords in the input file to obtain output database output and to allow analysis restart. The default value is ON.

### onCaeGraphicsStartup

An optional function to execute before Abaqus/CAE or Abaqus/Viewer starts. This function allows users to change graphics options. For more information about this function, refer to Tuning Graphics Cards. This function should not normally be changed.

### onCaeStartup

An optional function to execute before Abaqus/CAE starts. Refer to Customizing Abaqus/CAE Startup for an example of this function.

### onDesignStartup

An optional function to execute before Abaqus/Design starts.

### onJobCompletion

An optional function to execute after an Abaqus job completes. Functions specified in the Abaqus environment file in the current directory are executed first, followed by functions in the user home directory, and finally functions in the Abaqus installation environment file. Multiple functions in the same environment file result in only the last definition being used. Refer to Job Variables for a list of variables that can be used in this function.

### onJobStartup

An optional function to execute before an Abaqus job starts. Refer to Job Variables for a list of variables that can be used in this function.

### printed_output

By default, all values for the \*PREPRINT parameters are NO and results are not printed to the data file. Set the `printed_output` parameter to ON to obtain the same pre-print information in the data file as would be obtained by including

```plaintext
\*PREPRINT, CONTACT=YES, ECHO=YES, HISTORY=YES, MODEL=YES
```

in the input file. Setting `printed_output` to ON may also cause large amounts of tabular results to be printed to the data file (unless print output control options are used to limit output). If the input file was written in terms of parts and assemblies, setting `printed_output` to ON causes the part-assembly mapping to be printed in the data file regardless of the settings on the \*PREPRINT options; this allows users to associate printed output with the part-assembly as defined in the input file. The default value for this variable is OFF.

### run_mode

The default run mode (INTERACTIVE, BACKGROUND, or BATCH) if you do not specify the run mode on the abaqus command line when running an analysis product. The default value is BACKGROUND. This variable should not be set to BATCH unless a batch queue is defined.

### split_dat

If this variable is set to ON, the data file is split into two parts. Output from user input processing is placed in a file with the `.pre` extension. The analysis output file continues to have the `.dat` file extension. The default value is OFF.

### unconnected_regions

If this variable is set to ON, Abaqus/Standard creates element and node sets in the output database for unconnected regions in the model during a data check analysis. Element and node sets created with this option are named `MESH_COMPONENT_N`, where N is the component number.

## 4.6 System Customization Parameters

System customization parameters can be used to customize various system settings, such as preventing unauthorized modifications to environment file parameters.

### admin

This parameter prevents unauthorized modifications to environment file parameters. Set this parameter to a list of environment file parameters that cannot be changed in lower-level `abaqus_v6.env` files. Unless stated otherwise, all system and job customization parameters can be locked. Commands in the installation directory have the highest priority, followed by commands in the user home directory, and then commands in the current working directory. Consequently, Abaqus users cannot change environment file commands locked by the Abaqus account administrator.

### ask_delete

If this parameter is set to OFF, the system does not ask the user whether old job files with the same name should be deleted; files are deleted automatically. The default value is ON.

### compile_cpp

The C++ compile command. The command used by SIMULIA is included in the platform-specific environment file (`win86_64.env` or `lnx86_64.env`) in the `install_dir/os/SMA/site/` subdirectory of the installation. This command should not normally be changed. It can be a string or a tuple of strings. If the command is a tuple of strings, each string must represent a command line argument. The values of placeholders are determined by the Abaqus execution procedure or command line options and cannot be modified by the user. The values of placeholders replace the placeholders in the `compile_cpp` string.

Available placeholders:

| Placeholder | Meaning |
|-------------|---------|
| %I | Search directories for include files |

### compile_fortran

The Fortran compile command. The command used by SIMULIA is included in the platform-specific environment file (`win86_64.env` or `lnx86_64.env`) in the `install_dir/os/SMA/site/` subdirectory of the installation. This command should not normally be changed. It can be a string or a tuple of strings. If the command is a tuple of strings, each string must represent a command line argument.

Fortran file compilation using the Fortran 90 freeform specification is not supported by default. The `abaqus_v6.env` file in the `/SMA/site/` subdirectory of the Abaqus installation contains comments discussing compilation options.

### file_format

The format of the results file output (ASCII or BINARY). This parameter is valid only for Abaqus/Standard. The default value is BINARY.

### link_exe

The command to link the postprocessor. The command used by SIMULIA is included in the platform-specific environment file (`win86_64.env` or `lnx86_64.env`) in the `install_dir/os/SMA/site/` subdirectory of the installation. This command should not normally be changed, except in the case of building the postprocessor on Windows without a Fortran compiler. In that case, refer to the suggested commented changes in the `win86_64.env` file. This command can be a string or a tuple of strings. If the command is a tuple of strings, each string must represent a command line argument. The values of placeholders are determined by the Abaqus execution procedure or command line options and cannot be modified by the user. User-specified external libraries can be linked with the usual linking commands.

Placeholders used in `link_exe`:

| Placeholder | Meaning |
|-------------|---------|
| %J | Job name (in this case, the name of the executable to be created) |
| %F | Name of the object file created from the user's source file |
| %M | Name of the internally created main object file |
| %B | Name of the utility function shared library |
| %O | List of utility shared libraries for the output database application common interface |
| %L | List of directories containing shared libraries (HP only) |

### link_sl

The command to link shared libraries. The command used by SIMULIA is included in the platform-specific environment file (`win86_64.env` or `lnx86_64.env`) in the `install_dir/os/SMA/site/` subdirectory of the installation. This command must be a valid command on the computer system for linking shared libraries once its placeholders are replaced. This command can be a string or a tuple of strings. If the command is a tuple of strings, each string must represent a command line argument. The values of placeholders are determined by the Abaqus execution procedure or command line options and cannot be modified by the user.

Placeholders used in `link_sl`:

| Placeholder | Meaning |
|-------------|---------|
| %F | Name of the compiled object file |
| %U | Name of the shared library |
| %A | Name of the archive of compiled object files to be linked into the shared library |
| %B | Name of the utility function shared library |
| %E | Name of the file containing symbols to be exported from the shared library |
| %L | List of directories containing shared libraries (HP only) |

### nodb_cache_limit

The maximum size of the cache in the temporary file directory. When you read from a remote output database using a network ODB connector, Abaqus/CAE uses this cache for local data storage. Set the `nodb_cache_limit` parameter to the number of megabytes to which the cache size will be limited. The minimum value for `nodb_cache_limit` is 500, meaning the cache size limit is 500 MB. If you set a maximum cache size greater than the available free space, Abaqus/CAE reduces it to an amount equal to the available free space.

### plugin_central_dir

The full pathname or list of pathnames of the directory or directories containing Abaqus/CAE plugins. In most cases, this is one or more directories at a central location accessible to all users at the site.

### usub_lib_dir

The full pathname of the directory containing optional Abaqus/Standard and/or Abaqus/Explicit user subroutine user-defined libraries. Valid user subroutine libraries are platform-specific, but the file base names are the same for all platforms. The base names are `standardU`, `explicitU`, and `explicitU-D`. Use this variable to avoid the cost of frequent recompilation and/or re-linking of commonly used user subroutines. The `abaqus make` utility is used to create the shared libraries for use with this variable. User-created libraries via the user option of the Abaqus/Standard and Abaqus/Explicit execution procedure will override any user libraries in this directory.

### verbose

If this parameter is in the environment file, the execution procedure prints more information about job submission. Possible values are ON, OFF, 1, 2, and 3. Set the value to ON or 1 to print the command used to run the application executable and some performance data. Set the value to 2 to print license transaction information. Set the value to 3 to print operating system environment settings. Output related to the verbose parameter is written to standard output. The default value is OFF.

The following system customization parameters are for documentation installation and for specifying the Web browser used to display SIMULIA HTML documentation and context-sensitive help in Abaqus/CAE.

### browser_path

The full path to the Web browser executable on Linux platforms. The value of this parameter can be a string or a list of strings. If a list of strings is specified, the first string must be the full path to the Web browser executable, and subsequent strings are arguments to customize browser behavior. If any argument strings are included, at least one of them must contain `%s`, which will be replaced by the full uniform resource locator (URL) of the SIMULIA HTML documentation.

Abaqus automatically configures supported browsers to display HTML documentation correctly. Configuration varies by browser. This parameter can be used with `browser_type` to clarify which browser is being used. If `browser_path` is set to a string and `browser_type` is not set, the system checks for Firefox in the specified browser path. If Abaqus does not detect Firefox, Abaqus assumes an unsupported browser will be used and does not perform automatic configuration. This parameter is ignored on Windows platforms.

### browser_type

The Web browser on Linux platforms. To display HTML documentation correctly, Abaqus automatically configures the browser based on the specified browser type. Possible settings are FIREFOX and CUSTOM_BROWSER. If you set `browser_type=CUSTOM_BROWSER` to use a Web browser other than Firefox, no support or automatic configuration is provided. This parameter can be used with `browser_path` to directly specify the browser's executable command. If `browser_type` is set to Firefox and `browser_path` is not set, the system searches for Firefox in the system path. If the specified browser is not found, an error is displayed. This parameter is ignored on Windows platforms.

### doc_root

The full uniform resource locator (URL) or pathname of the SIMULIA HTML documentation.

URL example:

```python
doc_root="http://<servername>:4040/English"
```

This variable affects only the Abaqus connection to the documentation, not other Established Products; for example, Tosca and fe-safe. To configure connections for all Established Products, refer to Installation, Licensing, and Configuration > SIMULIA Installation > Established Products Installation and Configuration > Manual Documentation Configuration.

### doc_lang

The language of the documentation if more than one language is available. The default is "English".

The following parameters forbid execution of the corresponding module before a license activation is tested via the startup file. These parameters can be used to provide "friendly" messages if you attempt to execute an analysis module for which your site does not have a license. Use these parameters in combination with the `admin` parameter to ensure uniformity across the site.

### no_aqua

If the value is set to ON, execution of Abaqus/Aqua is prevented.

### no_background

If the value is set to ON, background execution of Abaqus analysis jobs is prevented.

### no_batch

If the value is set to ON, batch queue execution of Abaqus analysis jobs is prevented.

### no_cae

If the value is set to ON, execution of Abaqus/CAE is prevented.

### no_design

If the value is set to ON, execution of Abaqus/Design is prevented.

### no_explicit

If the value is set to ON, execution of Abaqus/Explicit is prevented.

### no_interactive

If the value is set to ON, interactive execution of Abaqus analysis jobs is prevented.

### no_standard

If the value is set to ON, execution of Abaqus/Standard is prevented.

### no_viewer

If the value is set to ON, execution of Abaqus/Viewer is prevented.

## 4.7 Executable Parameters

Abaqus executables for the licensing module are automatically placed in the `/code/bin/` subdirectory of the Abaqus installation. On Linux systems, the prefix parameter (\*_prefix) can be set to "time" to determine the execution time of specific phases of an Abaqus run.

### exe_prefix

An optional executable prefix for all Abaqus analysis executables. The default value is an empty string.

### explicit_prefix

An optional executable prefix for Abaqus/Explicit. The value given to this prefix overrides the value given to `exe_prefix`.

### explicit_dp_prefix

An optional executable prefix for the Abaqus/Explicit double precision version. The value given to this prefix overrides the value given to `exe_prefix`.

### package_prefix

An optional executable prefix for the Abaqus/Explicit PACKAGE program. The value given to this prefix overrides the value given to `exe_prefix`.

### pre_prefix

An optional executable prefix for the Abaqus analysis input file processor. The value given to this prefix overrides the value given to `exe_prefix`.

### standard_prefix

An optional executable prefix for the Abaqus/Standard program. The value given to this prefix overrides the value given to `exe_prefix`.

## 4.8 License Management Parameters

License management customization parameters control the behavior of the Abaqus license server based on current network conditions and user requirements. The Abaqus license server is installed with default parameters that should be suitable for most users. The following parameters are used for customization:

### abaquslm_license_file

This parameter provides the hostname of the computer running the Abaqus FLEXnet license server and is set during product installation. This parameter does not apply to the DSLS license server. If using a single server, this parameter should be set to `port@license_server_host`, where port is the port number and license_server_host is the name of the computer running the server:

```python
abaquslm_license_file="27000@rose"
```

If the port number is between 27000 and 27009, it does not need to be included.

If using two separate servers on Windows platforms, separate the servers with semicolons in the parameter value:

```python
abaquslm_license_file="27000@zinnia;27000@marigold"
```

If using two separate servers on Linux platforms, separate the servers with colons in the parameter value:

```python
abaquslm_license_file="27000@zinnia:27000@marigold"
```

If using three redundant servers, separate the servers with commas in the parameter value:

```python
abaquslm_license_file="27000@maple,27000@pine,27000@oak"
```

### academic

This parameter indicates whether academic Abaqus clients should use research or teaching license tokens. Setting this parameter to TEACHING forces Abaqus clients to use only teaching license tokens. Setting this parameter to RESEARCH or removing the parameter forces Abaqus to use only research license tokens. This parameter is automatically set during product installation: if the license server contains Abaqus teaching license files, the installation sets the parameter to TEACHING; otherwise, it is set to RESEARCH. In some cases, it may be necessary to explicitly set this parameter to RESEARCH rather than relying on the default unset value.

### cae_timeout

The number of minutes that an Abaqus/CAE or Abaqus/Viewer session remains idle without user activity before returning its token to the license server. The default value is 60 minutes.

### computer_location

A string indicating the location of the local client computer. This parameter allows you to细分 license usage reports by location. The license usage reporting utility compiles and organizes data according to the `computer_location` name. The default value is an empty string. If this default value is not changed, license usage reports do not differentiate between locations in the report.

### dsls_license_config

The path to the Dassault Systèmes License Server (DSLS) configuration file (DSLicSrv.txt). This file determines the Dassault Systèmes license server to use with Abaqus. For example:

**Linux platforms:**

```
/opt/simulia/license/DSLicSrv.txt
```

**Windows platforms:**

```
C:\\SIMULIA\\License\\DSLicSrv.txt
```

### license_model

This parameter controls the licensing mode used by Abaqus. Possible values are AUTOMATIC (default), LEGACY, and SIMUNIT. If this parameter is set to SIMUNIT, Abaqus uses SimUnit tokens or SimUnit credits. If set to LEGACY, Abaqus uses simulation tokens (tokens available before SimUnit tokens and SimUnit credits were introduced). When set to AUTOMATIC, the licensing mode is determined automatically by the licenses present on the license server. If SimUnit tokens or SimUnit credits are available on the license server, SimUnit licensing mode is used. Otherwise, the legacy mode is used. This parameter applies only when using the DSLS server (see the `license_server_type` parameter).

### license_server_type

The type of license server software used by Abaqus clients. Possible values are FLEXNET and DSLS (default).

### license_type

This parameter controls the license type used by Abaqus. Possible values are CREDIT and TOKEN (default). This parameter applies only when using SimUnit licensing mode (see the `license_model` parameter).

### lmhanglimit

The number of minutes that an Abaqus client waits in the license queue when no licenses are available. The default value of 0 forces jobs to remain in the license queue indefinitely unless terminated by the user.

### lminteractivequeuing

This parameter indicates whether interactive Abaqus/CAE or Abaqus/Viewer sessions should queue when licenses are not available. To allow interactive running Abaqus/CAE or Abaqus/Viewer sessions to queue for licenses, set this parameter to ON. The default value is OFF. The `lmlicensequeuing` parameter is used for queuing sessions running without a graphical user interface.

### lmlicensequeuing

This parameter indicates whether Abaqus analysis jobs or Abaqus/CAE or Abaqus/Viewer sessions using the noGUI option should queue when licenses are not available. The default value is ON. If this parameter is set to OFF, jobs and Abaqus/CAE or Abaqus/Viewer sessions terminate immediately if licenses are not available. The `lminteractivequeuing` parameter is used for queuing sessions running interactively.

### lmlog

This parameter indicates whether license usage data should be written to the FLEXnet debug log file. This parameter must be set to ON to use the Abaqus license usage reporting utility, which is the default. To suppress license usage data in the debug log file, set this parameter to OFF.

### lmproject

This optional parameter can be used to record information about a company internal project name or number. The `lmproject` parameter can be set to any string value; for example:

```python
lmproject="turbomachinery-project-23"
```

This parameter can be set in the environment file in each user's home directory, and it can be edited at any time when a change to a different project name is needed.

Information about Abaqus license checkouts and associated project names is recorded on the license server and can be retrieved via historical reports using the Accessor project when used.

### lmqueuesleep

The number of seconds an Abaqus client waits before checking the license queue to see if sufficient free tokens are available. The default value is 30 seconds, which is the minimum allowed. Increasing this value reduces network traffic when license queuing occurs.

### lmsvrdownlimit

The number of minutes an Abaqus client attempts to connect to the license server if the license server is currently unavailable. The default value of 0 forces jobs to attempt to connect indefinitely unless terminated by the user.

## 4.9 Job Variables

The following variables are available for use in the `onJobStartup` or `onJobCompletion` functions:

| Variable | Description |
|----------|-------------|
| id | The job identifier specified as a job option value on the command line |
| savedir | The pathname of the directory where the job was submitted |
| scrdir | The pathname of the temporary directory |
| analysisType | The type of analysis to be performed. Possible values are EXPLICIT and STANDARD |

Additionally, for MPI-based parallel jobs, the following variables are available in the `onJobStartup` or `onJobCompletion` functions:

| Variable | Description |
|----------|-------------|
| host_list | The list of hostnames used for the analysis, including the number of processors used on each machine. The format is the same as for the `mp_host_list` environment variable |
| local_host | A list of identifiers for determining the hostname of the machine from which the job was submitted (e.g., hostname, IP address, alias, etc.) |
| rsh_command | The command to open a remote shell on machines used during the analysis. The format is the same as for the `mp_rsh_command` environment variable |
| file_system | A tuple showing the type of file system used by the MPI-based parallel job. The first item in the tuple refers to the directory from which the job was submitted, and the second item refers to the job's temporary directory |
| cpus | The total number of processors used for the analysis summed across all hosts |

The following variables are available for use outside the `onJobStartup` and `onJobCompletion` functions:

| Variable | Description |
|----------|-------------|
| abaqus_version | A string containing the Abaqus version |
| analysisType | The type of analysis to be performed. Possible values are EXPLICIT and STANDARD |
| applicationName | The name of the Abaqus execution procedure to be performed; for example, analysis, cae, or viewer |

---

[Return to Contents](./index.md) | [Previous Chapter: Abaqus Configuration Guide](./chapter-03.md) | [Next Chapter: Defining Analysis Batch Queues](./chapter-05.md)
