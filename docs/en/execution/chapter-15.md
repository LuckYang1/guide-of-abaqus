---
title: Fortran Unit Numbers
description: Abaqus Execution Guide chapter
---

# Fortran Unit Numbers

## Fortran Unit Numbers

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

Abaqus uses the Fortran unit numbers outlined in the following tables. Unless stated otherwise, you should not attempt to write to these Fortran units from user subroutines.

For Abaqus/Standard, you should specify unit numbers 15-18 or unit numbers greater than 100. For Abaqus/Explicit, specify units 16-18 or unit numbers greater than 100 and ending in 5 through 9, such as 105, 268, etc. You cannot write to the .sta file.

### Fortran Unit Numbers

#### Abaqus/Standard Unit Numbers

| Unit Number | Description |
|------------|-------------|
| 1 | Internal database |
| 2 | Solver file |
| 6 | Print output (.dat) file (you can write to this file) |
| 7 | Message (.msg) file (you can write to this file) |
| 8 | Results (.fil) file |
| 10 | Internal database |
| 12 | Restart (.res) file |
| 19-30 | Internal database (temporary files). Units 21 and 22 always write to disk |
| 73 | Text file containing mesh beam section properties (.bsp) |

#### Abaqus/Explicit Unit Numbers

| Unit Number | Description |
|------------|-------------|
| 6 | Print output (.log) file |
| 12 | Restart (.res) file |
| 13 | Old restart (.res) file (if applicable) |
| 15 | Analysis preprocessor (.dat or .pre) file |
| 23 | Communication (.023) file |
| 60 | Global package (.pac) file |
| 61 | Global state (.abq) file |
| 62 | Temporary file |
| 63 | Global selected results (.sel) file |
| 64 | Message (.msg) file |
| 65 | Output database (.odb) file |
| 67 | Old package (.pac) file (if imported from Abaqus/Explicit) |
| 68 | Old state (.abq) file (if imported from Abaqus/Explicit) |
| 69 | Internal database; temporary file |

#### Domain Parallel Unit Numbers

If using domain parallel:

| Unit Number | Description |
|------------|-------------|
| 70 | Local package (.pac.1) file for CPU #1 |
| 71 | Local state (.abq.1) file for CPU #1 |
| 73 | Local selected results (.sel.1) file for CPU #1 |
| 80 | Local package (.pac.2) file for CPU #2 |
| 81 | Local state (.abq.2) file for CPU #2 |
| 83 | Local selected results (.sel.2) file for CPU #2 |

Each additional CPU adds three files with unit numbers incrementing by 10.

---

*Source: Abaqus 2025 FD02 Execution Guide*
