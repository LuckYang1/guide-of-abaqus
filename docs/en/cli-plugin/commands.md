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

**Job Control:**

| Action | Command | Description |
|--------|---------|-------------|
| Suspend | `/abaqus-suspend <job>` | Freeze state, no progress loss |
| Resume | `/abaqus-resume <job>` | Continue from suspension, no .res file needed |
| Terminate/Continue | `/abaqus-run <job> --continue` | Requires .res restart file |

---

## /abaqus-suspend — Suspend Job

Suspend a running Abaqus job, preserving memory state. Resume later with `/abaqus-resume`.

**Usage:**

```
/abaqus-suspend <job_name>
```

**Example:**

```
/abaqus-suspend model
```

---

## /abaqus-resume — Resume Job

Resume an Abaqus job suspended by `/abaqus-suspend`.

**Usage:**

```
/abaqus-resume <job_name>
```

**Example:**

```
/abaqus-resume model
```

**Note:** Can only resume jobs suspended with suspend. For terminated jobs, use `/abaqus-run --continue` (requires .res file).

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

- Job status (COMPLETED / RUNNING / SUSPENDED / TERMINATED / ABORTED)
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
