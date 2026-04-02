---
title: File Translation Tools (Part 1)
description: Abaqus Execution Guide chapter
---

# File Translation Tools (Part 1)

## Encrypting and Decrypting Abaqus Input Data

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus encrypt utility encrypts Abaqus input data, and the abaqus decrypt utility decrypts encrypted Abaqus input data.

When you encrypt a file, Abaqus adds the following unencrypted comment line at the beginning of the file:

"Do not modify or delete this header comment. You can, however, insert additional comment lines between this header comment and the first line of encrypted data."

You can insert additional comment lines after this encrypted header comment, but you cannot add comments within the encrypted data lines.

### Security and Support Notes

Encrypted files are password protected. If you lose the password, Dassault Systèmes cannot recover it.

### Command Summary

```
abaqus encrypt input = input-file output = output-file
[password = password] [license = license-type]
[siteid = site-id] [include_only = {encrypt | decrypt | all}]
```

```
abaqus decrypt input = input-file output = output-file
[password = password]
```

### Command Line Options

**input**: This option specifies the name of the data file to encrypt or decrypt.

**output**: This option specifies the name of the data file after encryption or decryption.

**password**: This option specifies the password for this encryption or decryption. Passwords are case-sensitive.

**license**: This option applies only to file encryption. This option specifies the Abaqus feature that the end user must be licensed to use.

**siteid**: This option applies only to file encryption. This option specifies the Abaqus site ID where the end user can include or decrypt this encrypted data file.

**include_only**: This option specifies that the encrypted input data cannot be decrypted using the abaqus decrypt execution procedure.

### Examples

```
abaqus encrypt input=model.inp output=model_encrypted.inp password=secret
```

## ASCII Translation of Results (.fil) Files

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus ascfil utility converts Abaqus results (.fil) files from binary format to ASCII format.

### Command Summary

```
abaqus ascfil job = job-name
```

### Command Line Options

**job**: This option specifies the job name.

## Joining Results (.fil) Files

**Products**: Abaqus/Standard

### References

- About Execution Procedures

### Overview

The abaqus append utility joins results files together.

### Command Summary

```
abaqus append job = job-name oldjob = oldjob-name
```

### Command Line Options

**job**: This option specifies the new job name.

**oldjob**: This option specifies the old job name.

### Examples

```
abaqus append job=combined oldjob=run1
```

## Translating Abaqus Files to Nastran Bulk Data Files

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus toNastran utility translates Abaqus input files to Nastran Bulk Data files.

### Command Summary

```
abaqus toNastran job = job-name input = input-file
[bdf_format = {standard | crash}]
```

### Command Line Options

**job**: This option specifies the job name.

**input**: This option specifies the input file.

**bdf_format**: This option specifies the Bulk Data format.

## Translating Abaqus Output Database Files to Nastran Output2 Results Files

**Products**: Abaqus/Standard Abaqus/Explicit

### References

- About Execution Procedures

### Overview

The abaqus toNastranOdb utility translates Abaqus output database files to Nastran Output2 results files.

### Command Summary

```
abaqus toNastranOdb job = job-name odb = odb-file-name
[step = step-number] [increment = increment-number]
[slim] [quad4corner] [quad4stress_bisector]
```

### Command Line Options

**job**: This option specifies the job name.

**odb**: This option specifies the output database file.

**step**: This option specifies the step number.

**increment**: This option specifies the increment number.

**slim**: This option enables slim format.

**quad4corner**: This option is for quad4 corner stress.

**quad4stress_bisector**: This option is for quad4 stress bisector.

## Translating an Abaqus Substructure to an MSC.Adams Flexible Body

**Products**: Abaqus/Standard

### References

- About Execution Procedures

### Overview

The abaqus toAdams utility translates Abaqus substructures to MSC.Adams flexible bodies.

### Command Summary

```
abaqus toAdams job = job-name substructure_sim = sim-file-name
[adams_mnf_block_16]
```

### Command Line Options

**job**: This option specifies the job name.

**substructure_sim**: This option specifies the SIM file name.

**adams_mnf_block_16**: This option uses 16-bit MNF block format.

## Translating an Abaqus Substructure to a Simpack Flexible Body

**Products**: Abaqus/Standard

### References

- About Execution Procedures

### Overview

The abaqus toSimpack utility translates Abaqus substructures to Simpack flexible bodies.

### Command Summary

```
abaqus toSimpack job = job-name substructure_sim = sim-file-name
```

### Command Line Options

**job**: This option specifies the job name.

**substructure_sim**: This option specifies the SIM file name.

## Translating an Abaqus Substructure to an EXCITE Flexible Body

**Products**: Abaqus/Standard

### References

- About Execution Procedures

### Overview

The abaqus toExcite utility translates Abaqus substructures to EXCITE flexible bodies.

### Command Summary

```
abaqus toExcite job = job-name substructure_sim = sim-file-name
[hide_mesh] [recovery_matrix]
```

### Command Line Options

**job**: This option specifies the job name.

**substructure_sim**: This option specifies the SIM file name.

**hide_mesh**: This option hides the mesh.

**recovery_matrix**: This option includes the recovery matrix.

---

*Source: Abaqus 2025 FD02 Execution Guide*
