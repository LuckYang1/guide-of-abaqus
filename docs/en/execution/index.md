---
title: Abaqus 2025 FD02 Execution Guide
description: Abaqus Execution Procedures English Version
---

# Abaqus 2025 FD02 Execution Guide

## Document Overview

This guide describes in detail the execution procedures for Abaqus/Standard, Abaqus/Explicit, Abaqus/CAE, and several utilities provided with Abaqus. This guide is an important part of the Abaqus documentation collection, which describes all the capabilities of Abaqus finite element analysis technology used in SIMULIA applications.

## Chapter Structure

This guide contains the following main chapters:

### Part I: Execution Procedures Fundamentals

- [Chapter 1: Trademarks and Legal Notices](chapter-01.md) - Trademarks, Legal Notices, About Execution Procedures
- [Chapter 2: What's New](chapter-02.md) - What's New in versions 2025 FD02 to 2024 FD01
- [Chapter 3: Execution Procedures Overview](chapter-03.md) - Execution Procedures, Conventions, Environment Settings, Port Selection

### Part II: Abaqus Execution

- [Chapter 4: Abaqus Execution (Part 1)](chapter-04.md) - Obtaining Information, Abaqus/Standard and Abaqus/Explicit Execution
- [Chapter 5: Abaqus Execution (Part 2)](chapter-05.md) - Job Execution Control, Abaqus/CAE Execution, Abaqus/Viewer Execution
- [Chapter 6: User Subroutines and Advanced Features](chapter-06.md) - User-Defined Executables, Optimization Execution, Parametric Studies, Abaqus Documentation

### Part III: Co-Simulation

- [Chapter 7: Co-Simulation](chapter-07.md) - SIMULIA Co-Simulation Engine, FMU Co-Simulation Execution

### Part IV: Abaqus Utilities

- [Chapter 8: System and Scripting Tools](chapter-08.md) - Hardware System Verification, Python Execution, Licensing Tools, Query Tools
- [Chapter 9: Database Tools](chapter-09.md) - Output Database Upgrade, SIM Database Tools, Report Generation, File Joining
- [Chapter 10: File Translation Tools (Part 1)](chapter-10.md) - Encryption/Decryption, Results File Translation
- [Chapter 11: File Translation Tools (Part 2)](chapter-11.md) - External Solver Input Translation (Nastran, ANSYS, LS-DYNA, etc.)

### Part V: Environment and Resource Management

- [Chapter 12: Environment File Settings](chapter-12.md) - Environment File Hierarchy, Parameter Settings, Troubleshooting
- [Chapter 13: Memory and Resource Management](chapter-13.md) - Memory Management, Disk Management, Resource Parameters
- [Chapter 14: Parallel Execution](chapter-14.md) - Parallel Execution in Abaqus/Standard and Abaqus/Explicit

### Part VI: Appendices

- [Chapter 15: Files and Extensions](chapter-15.md) - File Extension Definitions, Fortran Unit Numbers

## Quick Reference

### Common abaqus Commands

```bash
# Run analysis
abaqus job=job-name analysis

# Data check
abaqus job=job-name datacheck

# Continue execution
abaqus job=job-name continue

# Convert to specified format
abaqus job=job-name convert=odb

# Obtain information
abaqus information=system

# Run Abaqus/CAE
abaqus cae

# Run Python script
abaqus python script.py

# Job control
abaqus suspend job=job-name
abaqus resume job=job-name
abaqus terminate job=job-name
```

### Product Descriptions

- **Abaqus/Standard**: General purpose finite element analysis solver
- **Abaqus/Explicit**: Explicit dynamic analysis solver
- **Abaqus/CAE**: Interactive pre-processing and post-processing environment
- **Abaqus/Viewer**: Post-processing subset of Abaqus/CAE

### TCP/UDP Port Selection

TCP/UDP port numbers range from 0 to 65535:
- 0-1023: Well-known ports used by system processes (such as FTP, SSH, SMTP, etc.), should not be used
- 1024-49151: Registered ports that may conflict with software installed on the system
- 49152-65535: Unreserved ports that can be freely used

---

*Source: Abaqus 2025 FD02 Execution Guide*
