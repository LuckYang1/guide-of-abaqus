---
title: File Translation Tools (Part 2)
description: Abaqus Execution Guide chapter
---

# File Translation Tools (Part 2)

## Translating Other Solver Input to Abaqus Input

This section describes commands for translating other solver input to Abaqus input.

### In this section:

- Translating Nastran Data to Abaqus Files
- Translating ANSYS Input Files to Partial Abaqus Input Files
- Translating PAM-CRASH Input Files to Partial Abaqus Input Files
- Translating RADIOSS Input Files to Partial Abaqus Input Files
- Translating LS-DYNA Data Files to Abaqus Input Files
- Exchanging Abaqus Data with ZAERO
- Translating a Simpack Flexible Body to Abaqus Matrix Data
- Translating Moldflow Data to Abaqus Input Files

## Translating Nastran Data to Abaqus Files

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus fromNastran utility translates Nastran Bulk Data files to Abaqus input files.

### Command Summary

```
abaqus fromNastran job = job-name input = input-file
[wtmass_fixup] [loadcases] [pbar_zero_reset]
[surface_based_coupling] [beam_offset_coupling]
```

### Command Line Options

**job**: This option specifies the job name.

**input**: This option specifies the input file.

**wtmass_fixup**: This option fixes mass weight.

**loadcases**: This option translates load cases.

**pbar_zero_reset**: This option resets pbar to zero.

**surface_based_coupling**: This option enables surface-based coupling.

**beam_offset_coupling**: This option enables beam offset coupling.

## Translating ANSYS Input Files to Partial Abaqus Input Files

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus fromANSYS utility translates ANSYS input files to partial Abaqus input files.

### Command Summary

```
abaqus fromANSYS job = job-name input = input-file
```

### Command Line Options

**job**: This option specifies the job name.

**input**: This option specifies the input file.

## Translating PAM-CRASH Input Files to Partial Abaqus Input Files

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus fromPAMCrash utility translates PAM-CRASH input files to partial Abaqus input files.

### Element Numbering and Grouping

All elements must have unique element numbers. Elements assigned the same PART identification number are grouped into one element set.

Except for connector elements generated from translated SPRING and KJOIN, section properties need to be input in the PART section, not individually in the element section.

### Material Models

The translator supports only a limited material model set. All unsupported material models are translated as bilinear elastic-plastic.

### Command Summary

```
abaqus fromPAMCrash job = job-name input = input-file
[pLinkConnectors] [splitAirbagElements] [autoKJoinStops]
```

### Command Line Options

**job**: This option specifies the job name.

**input**: This option specifies the input file.

**pLinkConnectors**: This option processes pLink connectors.

**splitAirbagElements**: This option splits airbag elements.

**autoKJoinStops**: This option automatically KJoin stops.

## Translating RADIOSS Input Files to Partial Abaqus Input Files

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus fromRADIOSS utility translates RADIOSS input files to partial Abaqus input files.

### Element Numbering and Grouping

All elements must have unique element numbers.

### Material Models

The translator supports a limited set of material models.

### Include Files

RADIOSS uses include files.

### Command Summary

```
abaqus fromRADIOSS job = job-name input = input-file
[splitAirbagElements] [readAbaqusDat]
[userDefaultMass] [userDefaultInertia] [userHistoryTime]
```

### Command Line Options

**job**: This option specifies the job name.

**input**: This option specifies the input file.

**splitAirbagElements**: This option splits airbag elements.

**readAbaqusDat**: This option reads Abaqus .dat files.

**userDefaultMass**: This option uses user default mass.

**userDefaultInertia**: This option uses user default inertia.

**userHistoryTime**: This option uses user history time.

## Translating LS-DYNA Data Files to Abaqus Input Files

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus fromDyna utility translates LS-DYNA data files to Abaqus input files.

### Command Summary

```
abaqus fromDyna job = job-name input = input-file
[splitFile] [i10]
```

### Command Line Options

**job**: This option specifies the job name.

**input**: This option specifies the input file.

**splitFile**: This option splits files.

**i10**: This option uses i10 format for reading integer data.

## Exchanging Abaqus Data with ZAERO

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus zaero utility exchanges data between Abaqus and ZAERO.

### Command Summary

```
abaqus zaero job = job-name unvfile = unv-file odbname = odb-name
mtxfile = mtx-file [mode = {aeroelastic | stress}]
```

### Command Line Options

**job**: This option specifies the job name.

**unvfile**: This option specifies the Universal File.

**odbname**: This option specifies the ODB file name.

**mtxfile**: This option specifies the matrix file.

**mode**: This option specifies the mode (aeroelastic or stress).

## Translating a Simpack Flexible Body to Abaqus Matrix Data

**Products**: Abaqus/Standard

### References

- About Execution Procedures

### Overview

The abaqus fromSimpack utility translates Simpack flexible bodies to Abaqus matrix data.

### Command Summary

```
abaqus fromSimpack job = job-name
```

## Translating Moldflow Data to Abaqus Input Files

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus fromMoldflow utility translates Moldflow data to Abaqus input files.

### Command Summary

```
abaqus fromMoldflow job = job-name input = input-file
[midplane] [3D] [element_order] [initial_stress]
[material] [orientation]
```

### Command Line Options

**job**: This option specifies the job name.

**input**: This option specifies the input file.

**midplane**: This option specifies midplane mesh.

**3D**: This option specifies 3D mesh.

**element_order**: This option specifies element order.

**initial_stress**: This option includes initial stress.

**material**: This option includes material data.

**orientation**: This option includes orientation data.

---

*Source: Abaqus 2025 FD02 Execution Guide*
