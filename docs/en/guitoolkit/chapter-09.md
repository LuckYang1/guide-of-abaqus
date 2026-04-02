# Chapter 9: Creating a GUI Toolset

## Chapter Overview

A toolset is similar to a module but can be used across multiple modules. Toolsets typically have less functionality than modules because toolsets specialize in performing a specific task, such as partition.

## Steps for creating a GUI toolset

To create a new GUI toolset, you must follow these steps:

1. Derive a new class from the toolset base class.
2. Create menus in the menu bar (optional).
3. Create items in the Tools menu (optional).
4. Create buttons in the toolbar (optional).
5. Create buttons in the toolbox (optional).
6. Create modes to gather user input and issue commands.

## Chapter Contents

- [GUI toolset example](#gui-toolset-example)
- [Creating toolset components](#creating-toolset-components)
- [Registering a toolset](#registering-a-toolset)

---

## GUI toolset example

The AFXToolsetGui base class provides various toolset infrastructure support functions.

```python
from abaqusGui import *

class MyToolsetGui(AFXToolsetGui):
    def __init__(self):
        AFXToolsetGui.__init__(self, toolsetName)
        # Create menus, toolbar buttons, etc.
```

---

## Creating toolset components

### Menus and menu commands

Toolsets can create components in both the menu bar and the Tools menu.

### Toolbar and toolbox buttons

Toolsets can create buttons in both the toolbar and the toolbox.

---

## Registering a toolset

### Registering a toolset in a module

A module can register toolsets, making those toolsets available when that module is the current module.

### Registering a toolset in the main window

Toolsets can also be registered at the main window level so that they are available throughout the session.
