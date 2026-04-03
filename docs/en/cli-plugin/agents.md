# Agent Reference

## abaqus-job-manager — Job Lifecycle Management

Manages the complete lifecycle of Abaqus simulation jobs.

### Capabilities

- Automatically runs the datacheck → submit → monitor → post-process workflow
- Parses .sta/.msg files to detect errors and warnings
- Makes intelligent decisions based on analysis result status

### Trigger Scenarios

When the user asks:
- "Run this simulation for me"
- "Submit this job and monitor its progress"
- "Check if the analysis is done"

### Workflow

1. **Pre-check**: Run datacheck to validate input files
2. **Submit**: Submit analysis job (background mode)
3. **Monitor**: Continuously check .sta/.msg file status
4. **Report**: Summarize results (status, errors, warnings, ODB size)

---

## abaqus-post-processor — Result Extraction

Extracts and analyzes result data from ODB files.

### Capabilities

- Extract field output data (stress, displacement, strain, etc.)
- Generate ODB content reports
- Data format conversion (CSV, Simpack)
- Merge restart files

### Trigger Scenarios

When the user asks:
- "Extract stress data from this ODB"
- "Generate an analysis results report"
- "Export results to CSV"

### Field Output Variables

| Variable | Description | Dimension |
|----------|-------------|-----------|
| S | Stress | 6 (symmetric tensor) |
| U | Displacement | 3 |
| E | Strain | 6 |
| RF | Reaction force | 3 |
| CF | Concentrated force | 3 |
| PE | Plastic strain | 6 |
| TEMP | Temperature | 1 |
