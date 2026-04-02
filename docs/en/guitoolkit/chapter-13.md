# Chapter 13: The Main Window

## Chapter Overview

This section describes the layout, components, and behavior of the Abaqus main window.

## Main window components

### Title bar

The title bar displays the application name and version.

### Menu bar

The menu bar provides access to application functionality.

### Toolbar

The toolbar provides quick access to commonly used commands.

### Context bar

The context bar contains the module combo box and other context-related controls.

### Module toolbox

The module toolbox contains icons for commonly used tools of the current module.

### Drawing area and canvas

The canvas provides infinite space for creating and manipulating viewports. The drawing area is a window into the visible portion of the canvas.

### Prompt area

The prompt area displays prompts to guide users, as well as work-in-progress (WIP) messages.

### Message area

The application uses the message area to display informational and warning messages.

```python
mainWindow = getAFXApp().getAFXMainWindow()
mainWindow.writeToMessageArea('Warning: Some items failed!')
```

### Command line interface

The command line interface (CLI) provides an interface to the kernel-side Python command interpreter.

Users can enter Abaqus Scripting Interface commands in the CLI, which are then sent to the kernel for processing.

```python
# Hide the CLI
mainWindow = getAFXApp().getAFXMainWindow()
mainWindow.hideCli()
```
