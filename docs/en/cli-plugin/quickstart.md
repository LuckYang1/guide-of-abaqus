# Quick Start

## Prerequisites

- Abaqus software installed
- Abaqus command (`abaqus` or `abq20xx`) in system PATH
- Claude Code installed

## Installation

Copy the plugin directory to Claude Code's plugin directory:

```
plugins/abaqus-cli/ → ~/.claude/plugins/abaqus-cli/
```

## Verify Installation

Type `/abaqus-run --help` in Claude Code. If you see help output, the installation is successful.

## Basic Usage

### 1. Submit an Analysis Job

```
/abaqus-run model.inp cpus=8 memory=16gb
```

This executes `abaqus job=model cpus=8 memory=16gb`.

### 2. Monitor Job Status

```
/abaqus-monitor model
```

View the running status from the .sta file.

### 3. Extract Results

```
/abaqus-post extract model.odb --field S --step Step-1
```

Extract stress data from ODB to a CSV file.

### 4. Compile User Subroutine

```
/abaqus-compile UMAT.for
```

Compile a Fortran user subroutine.

### 5. File Format Conversion

```
/abaqus-translate fromNastran model.bdf
```

Convert a Nastran file to Abaqus format.

## Using Agents

For complex workflows, let the AI Agent manage automatically:

- "Run this simulation for me — compile the subroutine, submit the job, monitor progress, extract results"
- "Extract stress and displacement data from all steps in this ODB file"

The agent will automatically invoke the corresponding scripts to complete the workflow.

## Version Specification

If you have multiple Abaqus versions, specify in the configuration:

```json
{
  "settings": {
    "abaqus_cmd": "abq2024"
  }
}
```

Or auto-detect with the agent: `scripts/version_resolver.py --detect`.
