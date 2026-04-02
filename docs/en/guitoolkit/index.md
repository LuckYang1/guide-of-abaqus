---
title: Abaqus GUI Toolkit User's Guide
description: Abaqus GUI Toolkit English Version
---

# Abaqus GUI Toolkit User's Guide

## Document Overview

This guide describes the Abaqus GUI Toolkit, which allows you to customize the Abaqus/CAE graphical user interface by creating your own dialog boxes, GUI modules, and even complete applications. This guide is designed to guide you through the process of writing applications, explaining how to use the components of the toolkit and providing example code snippets.

This guide is part of the Abaqus documentation collection that describes all aspects of Abaqus finite element analysis technology for SIMULIA applications.

## Document Structure

This guide contains the following major sections:

### Part I: Getting Started

- [Chapter 1: Introduction](./chapter-01.md) - Abaqus GUI Toolkit overview, prerequisites, and basics
- [Chapter 2: Getting Started with Abaqus GUI Toolkit](./chapter-02.md) - Kernel and GUI, application components, plug-ins and customized applications, running the prototype application

### Part II: Dialog Box Building

- [Chapter 3: Building Dialog Boxes](./chapter-03.md) - Overview of dialog box components
- [Chapter 4: Widgets](./chapter-04.md) - Labels, buttons, text, lists, ranges, trees, tables, and other widgets
- [Chapter 5: Layout Managers](./chapter-05.md) - Using layout managers
- [Chapter 6: Dialog Boxes](./chapter-06.md) - Message dialog boxes, custom dialog boxes, data dialog boxes, common dialog boxes

### Part III: Core Concepts

- [Chapter 7: Commands](./chapter-07.md) - Kernel commands, GUI commands, targets and messages
- [Chapter 8: Modes](./chapter-08.md) - Mode processing, form modes, procedure modes

### Part IV: Application Development

- [Chapter 9: Creating a GUI Module](./chapter-09.md) - How to create a GUI module
- [Chapter 10: Creating a GUI Toolset](./chapter-10.md) - How to create a GUI toolset
- [Chapter 11: Customizing an Existing Module or Toolset](./chapter-11.md) - Customizing and accessing Abaqus/CAE GUI modules and toolsets

### Part V: Application Infrastructure

- [Chapter 12: Creating an Application](./chapter-12.md) - Creating applications, GUI code, launch scripts, licensing and execution
- [Chapter 13: Application Object](./chapter-13.md) - Application object and its methods
- [Chapter 14: The Main Window](./chapter-14.md) - Layout, components, and behavior of the main window

## Technical Terminology

This guide retains the original English names for many technical terms to ensure consistency and accuracy with official Abaqus documentation. Key terms include:

- **Kernel** - The core process of Abaqus/CAE, responsible for database access and command execution
- **GUI** - Graphical User Interface
- **Widget** - User interface elements in the GUI, such as buttons and text boxes
- **Mode** - A mechanism for gathering user input and sending commands to the kernel
- **Module** - A grouping of functionality, such as the Part module
- **Toolset** - A grouping of functionality similar to a module but more specific
- **Dialog Box** - A window for gathering user input
- **Layout Manager** - A mechanism for arranging widgets in dialog boxes

## Version Information

- **Document Version**: Abaqus 2025 FD04
- **Original Language**: English
- **Translation**: April 2026

---

*For questions, please visit the [Community](../community.md) page*
