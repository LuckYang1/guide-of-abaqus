# Chapter 8: Creating a GUI Module

## Chapter Overview

This section describes how to create a GUI module.

## Steps for creating a GUI module

To create a new GUI module, you must follow these steps:

1. Derive a new class from the module base class.
2. Create menus in the menu bar.
3. Create icons in the toolbar (optional).
4. Create icons in the toolbox (optional).
5. Create modes to gather user input and issue commands. Modes include procedures and dialog boxes.
6. Create methods to handle any special behavior not handled by the module's modes (optional).

## Chapter Contents

- [Examining a GUI module example](#examining-a-gui-module-example)
- [Registering a GUI module](#registering-a-gui-module)
- [Switching to a GUI module](#switching-to-a-gui-module)

---

## Examining a GUI module example

This section shows how to create a module GUI.

The AFXModuleGui base class provides various module infrastructure support functions. For example, the AFXModuleGui base class keeps track of the module's menus and its toolbar and toolbox icons.

### Deriving a new module class

To create your own module GUI, first derive a new class from the AFXModuleGui base class.

```python
from abaqusGui import *

class MyModuleGui(AFXModuleGui):
    def __init__(self):
        mw = getAFXApp().getAFXMainWindow()
        AFXModuleGui.__init__(self, moduleName='My Module',
            displayTypes=AFXModuleGui.PART)
        # Menu items
        menu = AFXMenuPane(self)
        AFXMenuTitle(self, '&Menu1', None, menu)
        AFXMenuCommand(self, menu, '&Item 1', None, mode_1,
            AFXMode.ID_ACTIVATE)
```

### Tree tabs

By default, the tabs in TreeToolsetGui are not visible when the user switches to a custom module.

### Menu bar items

Menu bar items consist of menu titles that govern menu panes.

### Toolbar items

Toolbar items are displayed at the top of the main window below the menu bar, and consist of buttons containing icons.

### Toolbox items

Toolbox items are displayed at the left edge of the main window, and consist of buttons containing icons.

### Registering toolsets

A module can include toolsets through simple registration.

### Kernel module initialization

A GUI module is designed to provide an interface to a kernel module.

After the GUI gathers input from the user, it builds a command string and sends it to the kernel for processing.

```python
def getKernelInitializationCommand(self):
    return 'import myModule'
```

### Instantiating the GUI module

The final step in the module GUI code is to construct the module:

```python
MyModuleGui()
```

---

## Registering a GUI module

To make a GUI module accessible to the GUI infrastructure, the module must be registered in the main window code:

```python
self.registerModule(displayedName='My Module',
    moduleImportName='myModuleGui')
```

---

## Switching to a GUI module

When the user selects a module from the module list in the context bar, the GUI infrastructure calls the deactivate method of the current GUI module and calls the activate method of the GUI module selected by the user.

```python
switchModule('My Module')
```
