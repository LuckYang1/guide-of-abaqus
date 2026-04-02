---
title: What's New
description: Abaqus Execution Guide chapter
---

# What's New

This page describes recent changes in Abaqus Execution.

## 2025 FD02

### Improved Substructure Results Recovery for Abaqus-Simpack Flexible Body Dynamics

You can now recover results obtained from Simpack dynamic time domain and frequency domain analyses.

**Benefits**: These enhancements improve the Abaqus-Simpack workflow for flexible body dynamic analysis. The abaqus substructurerecover utility now supports recovery of results obtained from Simpack dynamic time domain and frequency domain analyses.

For more information, see "Environment File Settings" and "Recovering Results from a Substructure."

## 2025 FD01

### Environment File Setting Customizes Warnings Level

You can now specify whether common warnings are reported by the Abaqus analysis input file processor.

**Benefits**: Reducing the number of warnings makes evaluation of the preprocessed model more convenient.

The Abaqus analysis input file processor now suppresses common warnings for unsupported output requests by default. However, you can use the new environment variable output_warnings_level to specify if common warnings are reported.

Many warnings issued by the Abaqus analysis input file processor for invalid output requests, such as those issued for output requests that are not supported for specific element types or procedure types, are informational only and warrant no action by the user. For large models the number of these warnings can be very high and may make evaluation of the preprocessed model difficult.

For more information, see "Environment File Settings."

### PDF Guides Available

You can download PDF versions of the Abaqus guides from each guide overview.

**Benefits**: You can easily access the PDF versions of the guides.

In earlier releases, PDF versions of the guides were updated only for the GA (General Availability) release and could be downloaded from the Dassault Systèmes Knowledge Base. As of 2025 FD01, the PDF guides will be updated with each release of the HTML versions of the guides.

For more information, see "Abaqus Execution Guide."

## 2024 FD04

### Optimization and Parallel Execution

For parallel execution using GPGPU acceleration, you now specify the number of GPUs as the total number of GPUs for the analysis rather than specifying the number of GPUs per MPI process.

**Benefits**: Specifying GPGPU acceleration using the total number of GPUs is more consistent with how you specify the number of CPUs allocated to an analysis and permits greater flexibility for job execution in heterogeneous compute environments.

For more information, see "Abaqus/Standard and Abaqus/Explicit Execution," "Optimization Execution," "Environment File Settings," "Parallel Execution in Abaqus/Standard," and "Parallel Execution in Abaqus/Explicit."

## 2024 FD03

### Direct Sparse Solver Support for Steps with Unsymmetric Matrix Storage

For shared memory parallel (SMP) execution of steady-state dynamic direct procedures with unsymmetric matrix storage, Abaqus/Standard now uses the pure thread-based complex solver by default.

**Benefits**: The pure thread-based complex solver provides a solution that is typically at least twice as fast as the previous default option, the hybrid direct sparse solver.

For more information, see "Parallel Execution in Abaqus/Standard."

## 2024 FD02

### Execution Procedures User Assistance Reorganized

Content in the Execution Procedures section of the Abaqus Execution Guide is now divided into several subsections.

**Benefits**: The new organization makes it easier to locate user assistance for the abaqus commands you want to run. Topics are now divided into the following subsections:

- Abaqus Execution
- Abaqus Co-Simulation
- Abaqus Utilities
- Translating Other Solver Input to Abaqus Input
- Translating Abaqus Output to Another Format

For more information, see "Execution Procedures."

## 2024 FD01

### Enhanced Translation of LS-DYNA Keyword Files to Abaqus

You can now translate LS-DYNA keyword files that use the i10 format option in reading integer data.

**Benefits**: The ability to read these data improves the usability of the abaqus fromdyna translator. You can specify the format for individual keywords by appending the percent sign at the end of the keyword, as shown in the following examples:

- `*ELEMENT_BEAM %`
- `*ELEMENT_SHELL %`
- `*ELEMENT_SOLID %`
- `*NODE %`

Additionally, you can specify the format globally for all applicable keywords in the LS-DYNA keyword file by adding an option to the translator's execution command or by declaring the following keyword option:

`*KEYWORD i10=y`

For more information, see "Translating LS-DYNA Data Files to Abaqus Input Files."

---

*Source: Abaqus 2025 FD02 Execution Guide*
