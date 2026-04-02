# Chapter 11: Creating an Application

## Chapter Overview

This section explains how to create an application, such as Abaqus/CAE. It also describes the high-level infrastructure responsible for running the application.

## Chapter Contents

- [About GUI code](#about-gui-code)
- [Launch script](#launch-script)
- [Licensing and execution](#licensing-and-execution)
- [Application object](#application-object)
- [Main window](#main-window)

---

## About GUI code

When creating a customized application, you need to create the following components:

1. **Application object** - Manages the application lifecycle
2. **Main window** - Provides a container for the user interface
3. **Modules and toolsets** - Provide specific functionality
4. **Modes** - Handle user interaction

### GUI code files

A typical GUI application contains the following files:

- `application.py` - Application entry point
- `mainWindow.py` - Main window implementation
- `moduleGui.py` - GUI module definitions
- `toolsetGui.py` - GUI toolset definitions
- `modes.py` - Mode definitions

---

## Launch script

The launch script initializes the application and starts the event loop.

```python
from abaqusGui import *

# Create the application object
app = AFXApp()

# Create the main window
mainWindow = MyMainWindow(app)

# Initialize and run
app.init(sys.argv)
app.run()
```

### Launch arguments

The launch script can accept arguments to control the application's behavior.

---

## Licensing and execution

### License configuration

The license checked out when the application starts is controlled by the application configuration.

### Execution method

```bash
abaqus cae -custom myApplication -noStartup
```

---

## Application object

The AFXApp class is the application object.

### Application object methods

- `init(sys.argv)` - Initialize the application
- `run()` - Start the event loop
- `exit()` - Exit the application

---

## Main window

The AFXMainWindow class provides the main window.

### Main window components

- Title bar
- Menu bar
- Toolbar
- Context bar
- Module toolbox
- Drawing area and canvas
- Prompt area
- Message area
- Command line interface
