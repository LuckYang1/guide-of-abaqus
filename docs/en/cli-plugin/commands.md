# Slash Command Reference

## /abaqus-run — Job Submission

Submit Abaqus analysis jobs.

**Usage:**

```
/abaqus-run <input_file> [parameters...]
```

**Parameters:**

| Parameter | Description | Default |
|-----------|-------------|---------|
| `cpus` | Number of CPU cores | 4 |
| `gpus` | Number of GPUs | - |
| `memory` | Memory limit | 8gb |
| `scratch` | Scratch directory | System default |
| `user` | User subroutine file | - |
| `double` | Double precision | - |

**Modes:**

- Default: Full analysis
- `--datacheck`: Data check only
- `--continue`: Continue interrupted job
- `--recover`: Recover from restart

**Examples:**

```
/abaqus-run beam.inp cpus=8 memory=16gb
/abaqus-run model.inp --datacheck user=umat.for
/abaqus-run model.inp --continue cpus=4
```

---

## /abaqus-monitor — Job Monitoring

Monitor Abaqus job running status.

**Usage:**

```
/abaqus-monitor <job_name> [--watch] [--interval seconds]
```

**Parameters:**

| Parameter | Description | Default |
|-----------|-------------|---------|
| `--watch` | Continuous monitoring mode | - |
| `--interval` | Refresh interval (seconds) | 10 |

**Output:**

- Job status (COMPLETED / RUNNING / TERMINATED / ABORTED)
- Increment count
- Warning/error count
- ODB file size

---

## /abaqus-post — Post-Processing

Extract result data from ODB files.

**Usage:**

```
/abaqus-post <operation> <odb_file> [parameters...]
```

**Operations:**

| Operation | Description |
|-----------|-------------|
| `report` | Generate ODB content report |
| `extract` | Extract field output to CSV |
| `odb2sim` | Convert to Simpack format |
| `restartjoin` | Merge restart files |

---

## /abaqus-compile — Subroutine Compilation

Compile Abaqus user subroutines.

**Usage:**

```
/abaqus-compile <source_file> [--standard|--explicit|--cfd]
```

---

## /abaqus-translate — File Translation

Convert model files between Abaqus and other solvers.

**Export:** `toNastran`

**Import:** `fromNastran`, `fromANSYS`, `fromDyna`, `fromPamcrash`, `fromRadioss`, `fromMoldflow`, `fromSimpack`, `fromAdams`, `fromExcite`
