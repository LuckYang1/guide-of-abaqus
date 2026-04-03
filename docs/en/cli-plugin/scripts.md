# Script API Reference

The plugin contains 4 Python scripts in the `plugins/abaqus-cli/scripts/` directory.

---

## version_resolver.py — Version Resolution

Resolves version strings to actual Abaqus command names.

### CLI

```bash
python version_resolver.py --resolve <version>
python version_resolver.py --validate <command>
python version_resolver.py --detect
python version_resolver.py --info [command]
```

### Functions

| Function | Description |
|----------|-------------|
| `resolve_command(version_str)` | Convert version string to command name |
| `validate_command(cmd)` | Check if command is available in PATH |
| `auto_detect()` | Auto-detect available Abaqus command |
| `get_version_info(cmd)` | Get version information |

---

## abaqus_runner.py — Command Builder & Executor

Unified CLI wrapper based on COMMAND_REGISTRY.

### CLI

```bash
python abaqus_runner.py <subcommand> [key=value...] [--abaqus-cmd CMD] [--dry-run] [--list]
```

### Supported Subcommands

| Subcommand | Category | Description |
|------------|----------|-------------|
| job | Job | Submit analysis |
| datacheck | Job | Data check |
| continue | Job | Continue interrupted job |
| recover | Job | Recover from restart |
| syntaxcheck | Job | Syntax check |
| suspend/resume/terminate | Control | Job control |
| make | Build | Compile user subroutine |
| toNastran/fromNastran/... | Translate | Format conversion |
| odbreport/odb2sim/restartjoin | Database | ODB operations |
| cse/cosimulation/fmu | Cosim | Co-simulation |
| encrypt/decrypt | Crypto | Script encryption |
| optimization | Optimize | Run optimization |

### Functions

| Function | Description |
|----------|-------------|
| `parse_kv_args(args_list)` | Parse key=value argument list |
| `build_command(subcommand, params)` | Build complete command line |
| `execute_command(cmd, timeout, background)` | Execute the command |

---

## job_monitor.py — Job Monitoring

Parse .sta / .msg files to get job running status.

### CLI

```bash
python job_monitor.py <job_name>... [--dir DIR] [--watch] [--interval SEC]
```

### Data Classes

**JobStatus**: job_name, status, iterations, errors, warnings, odb_file

**MsgInfo**: error_lines, warning_lines

### Functions

| Function | Description |
|----------|-------------|
| `parse_sta_file(sta_path)` | Parse .sta file for status |
| `parse_msg_file(msg_path)` | Parse .msg file for errors/warnings |
| `find_job_files(job_name, search_dir)` | Find job-related files |
| `monitor_jobs(job_names, dir, watch, interval)` | Monitor one or more jobs |

---

## odb_extractor.py — ODB Data Extraction

Extract field output data from ODB files.

### CLI

```bash
python odb_extractor.py report <odb> [--output FILE]
python odb_extractor.py extract <odb> [--step STEP] [--frame N] [--field VAR] [--output FILE]
python odb_extractor.py odb2sim <odb> [--output FILE]
python odb_extractor.py restartjoin --output NAME --input F1 --input F2...
```

### Functions

| Function | Description |
|----------|-------------|
| `run_odbreport(odb_path, output, cmd)` | Generate ODB content report |
| `extract_field_output(...)` | Extract field output to CSV |
| `run_odb2sim(odb_path, output, cmd)` | Convert ODB to Simpack |
| `run_restartjoin(output, inputs, cmd)` | Merge restart files |
