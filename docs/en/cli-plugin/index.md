# Abaqus CLI Plugin

The Abaqus CLI Plugin is a CLI wrapper for the Abaqus FEA software, designed for AI Agents to autonomously complete simulation workflows.

## Features

| Feature | Description |
|---------|-------------|
| Job Submission | Submit analysis, datacheck, continue, recover, etc. |
| Job Monitoring | Real-time .sta/.msg file status parsing |
| Post-Processing | Extract field/history output from ODB |
| Subroutine Compilation | Compile Fortran/C/C++ user subroutines |
| File Translation | Nastran/ANSYS/Dyna and other format conversion |
| Co-Simulation | CSE and FMU support |

## Components

### Slash Commands

- `/abaqus-run` — Job submission
- `/abaqus-monitor` — Job monitoring
- `/abaqus-post` — Post-processing data extraction
- `/abaqus-compile` — Subroutine compilation
- `/abaqus-translate` — File format translation

### Agents

- **abaqus-job-manager** — Manages the complete job lifecycle (datacheck → submit → monitor → post-process)
- **abaqus-post-processor** — Extracts and analyzes result data from ODB files

### Skills

- **job-workflow** — End-to-end simulation workflow from input file to results
- **subroutine-workflow** — Iterative subroutine development, compilation, and debugging
- **result-extraction** — ODB data extraction and format conversion

## Version Support

The plugin supports all Abaqus versions via command name switching:

| Syntax | Description |
|--------|-------------|
| `abaqus` | System default version |
| `abq2024` | Abaqus 2024 |
| `abq2025` | Abaqus 2025 |
| `abq20xx` | Any version |

See [Quick Start](quickstart.md) and [Configuration](configuration.md) for details.
