# Skill Reference

## job-workflow — Complete Simulation Workflow

End-to-end automation from input file to final results.

### Scenarios

- User provides a .inp file and needs the full workflow from submission to results
- Subroutine compilation is required before running analysis
- Multi-step analysis (pre-load → main analysis)

### Steps

```
Environment Check → Subroutine Compile → Data Check → Submit → Monitor → Extract Results → Report
```

---

## subroutine-workflow — Subroutine Development

Iterative development workflow for user subroutines.

### Scenarios

- Developing UMAT/VUMAT/UEL user subroutines
- Subroutine compilation failure requiring debugging
- Verifying subroutine behavior in datacheck

### Steps

```
Compile → Check Results → Datacheck → Test Analysis → Iterative Debug
```

### Common Subroutine Types

| Subroutine | Purpose | Key Interface |
|------------|---------|---------------|
| UMAT | User material (Standard) | stress, statev, ddsdde |
| VUMAT | User material (Explicit) | stress, stateNew |
| UEL | User element | rhs, amatrx |
| USDFLD | Field dependency | field, statev |

---

## result-extraction — ODB Data Extraction

Extract and analyze result data from output databases.

### Scenarios

- Extract stress, displacement, and other field data after analysis
- Export results to CSV for further processing
- Generate ODB content reports

### Steps

```
Understand ODB Structure → Determine Extraction Needs → Execute → Validate → Post-Process
```
