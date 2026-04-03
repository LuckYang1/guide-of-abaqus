# Configuration

## plugin.json Configuration

The plugin configuration file is located at `plugins/abaqus-cli/.claude-plugin/plugin.json`.

### Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `abaqus_cmd` | string | `abaqus` | Abaqus command name (`abaqus`, `abq2024`, `abq20xx`) |
| `default_cpus` | integer | 4 | Default CPU core count |
| `default_scratch` | string | `""` | Default scratch directory |
| `default_memory` | string | `8gb` | Default memory limit |

## Version Configuration

### Auto-Detection

The plugin automatically detects available Abaqus commands. Use `scripts/version_resolver.py --detect` to check.

### Manual Specification

Modify `abaqus_cmd` in `plugin.json`:

```json
{
  "settings": {
    "abaqus_cmd": {
      "default": "abq2024"
    }
  }
}
```

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `PATH` | Must include Abaqus command directory | Yes |
| `LM_LICENSE_FILE` | Abaqus license server | Yes |
| `INTEL_LICENSE_FILE` | Intel Fortran license | When compiling |

## Fortran Compiler

Compiling user subroutines requires a Fortran compiler:

| Compiler | Abaqus Version | Notes |
|----------|----------------|-------|
| Intel Fortran (ifort) | All | Recommended |
| gfortran | Recent | Open-source alternative |
