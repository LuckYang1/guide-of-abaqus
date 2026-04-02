---
title: Parallel Execution
description: Abaqus Execution Guide chapter
---

# Parallel Execution

## About Parallel Execution

### Overview

Parallel execution in Abaqus is implemented using three different schemes: threading, message passing, and a combination of both. Threads are lightweight processes that can execute different tasks simultaneously within the same application. Threads can communicate relatively easily by sharing the same memory pool. Thread parallelization is readily available on all shared memory platforms.

Parallelization using message passing employs multiple analysis processes that communicate with each other through a message passing interface (MPI). This requires installation of MPI components.

Hybrid parallelization combines MPI-based message passing between multiple analysis processes with shared memory communication between threads within each analysis process. This requires installation of MPI components.

### Parallel Processing Support for Abaqus Features

The following Abaqus/Standard features can execute in parallel: analysis input preprocessing, direct sparse solver, iterative solver, eigenproblem solver, and element operations.

### Parallel Execution on Shared Memory Computers

Abaqus/Standard and Abaqus/Explicit can execute in parallel on shared memory computers using either threading or MPI.

### Parallel Execution on Computer Clusters

Abaqus can execute in parallel on computer clusters using MPI-based parallelization. For parallel execution on computer clusters, the machine list or hosts are given through the mp_host_list environment file parameter.

### Parallel Execution Using GPGPU Hardware

The direct solver, AMS eigenproblem solver, and modal frequency response solver in Abaqus/Standard can execute in parallel on computers equipped with compute-capable GPGPU cards.

### Use with User Subroutines

User subroutines can be used when running jobs in parallel. In distributed runs, the entire model is decomposed into separate domains (partitions). Each domain is served by a separate MPI process.

## Parallel Execution in Abaqus/Standard

### Overview

Parallel execution in Abaqus/Standard:
- Reduces run time for large analyses
- Can be used on shared memory computers and computer clusters
- Can utilize GPGPU hardware

### Invoking Parallel Processing

Abaqus/Standard supports parallelization for shared memory computers and computer clusters. Parallelization is invoked using the cpus option, which specifies the total number of processors; and the threads_per_mpi_process option, which specifies how these processors are allocated.

### Thread-Based Parallelization

You can execute Abaqus/Standard in thread mode within a single node of a compute cluster.

Two thread-based parallelization options are available: the hybrid direct sparse solver and the pure thread-based direct sparse solver. The pure thread-based direct sparse solver provides better performance than the hybrid direct sparse solver in many workflows.

### MPI-Based Parallelization

Abaqus/Standard can also execute in MPI mode, which uses the message passing interface for communication between machine hosts.

### Hybrid Parallelization

You can further improve hybrid mode performance when MPI parallelization executes between hosts and thread parallelization executes within each host.

### GPGPU Acceleration

GPGPU acceleration is supported in the direct sparse solver, AMS eigenproblem solver, and modal frequency response solver.

### Parallel Execution of Steady-State Dynamic Analyses

Steady-state dynamic analysis provides the steady-state response of a system at a given frequency due to harmonic excitation. For large finite element systems, frequency response calculations can be very time-consuming.

### Consistency of Results

Some physical systems may be highly sensitive to small perturbations. When simulating such physically sensitive systems, you may see differences in numerical results between jobs running on different numbers of processors.

## Parallel Execution in Abaqus/Explicit

### Overview

Parallel execution in Abaqus/Explicit:
- Reduces execution time for analyses requiring many increments
- Reduces execution time for analyses containing large numbers of nodes and elements
- Produces analysis results independent of the number of processors used for the analysis
- Can be used on shared memory computers and computer clusters

### Invoking Parallel Processing

Parallelization in Abaqus/Explicit is implemented in two ways: domain-level and loop-level. The default and most efficient method is the domain-level parallelization method.

### Domain-Level Parallelization

The domain-level method decomposes the model into multiple topological domains. These parallel domains contain subsets of nodes and elements along with all modeling features needed to compute the solution. Domains are evenly distributed among available processors.

### Loop-Level Parallelization

The loop-level method parallelizes only low-level loops in the element and contact pair code.

### Measuring Parallel Performance

Parallel performance is measured by comparing the total time required to run on a single processor (serial run) with the total time required to run on multiple processors (parallel run).

### Output

There are no output limitations.

---

*Source: Abaqus 2025 FD02 Execution Guide*
