# Chapter 14: Customizing the Main Window

## Chapter Overview

The main window base class provides GUI infrastructure to allow user interaction, module operations, and display of objects in viewports. This section describes how to add functionality to your application by deriving from the main window base class and then registering modules and toolsets.

## Chapter Contents

- [Modules and toolsets](#modules-and-toolsets)
- [Abaqus/CAE main window example](#abaqus-cae-main-window-example)
- [Icons](#icons)
- [Colors and RGB values](#colors-and-rgb-values)

---

## Modules and toolsets

A module is one of the basic concepts of an interactive Abaqus application. A module groups functionality into logical units; for example, the unit that creates parts or the unit that meshes assemblies.

A toolset is similar to a module in that it groups functionality into logical units. However, a toolset typically contains less functionality than a module because the toolset focuses on one specific task; for example, partition. A toolset can be used by multiple modules.

### Registering modules

Registering a module puts the module name in the module combo box in the context bar.

```python
self.registerModule(displayedName='My Module',
    moduleImportName='myModuleGui')
```

### Registering toolsets

Toolsets are available when the application first starts after they are registered in the main window.

```python
self.registerToolset(FileToolsetGui(),
    GUI_IN_MENUBAR|GUI_IN_TOOLBAR)
```

---

## Abaqus/CAE main window example

```python
from abaqusGui import *

class CaeMainWindow(AFXMainWindow):
    def __init__(self, app, windowTitle=''):
        # Construct the GUI infrastructure
        AFXMainWindow.__init__(self, app, windowTitle)

        # Register the "persistent" toolsets
        self.registerToolset(FileToolsetGui(),
            GUI_IN_MENUBAR|GUI_IN_TOOLBAR)
        self.registerToolset(ModelToolsetGui(),
            GUI_IN_MENUBAR)

        # Register modules
        self.registerModule('Part', 'Part')
        self.registerModule('Property', 'Property')
        self.registerModule('Assembly', 'Assembly')
```

---

## Icons

The Abaqus GUI Toolkit supports the following icon formats: XPM, BMP, GIF, and PNG.

### Creating icons

```python
icon = afxCreatePNGIcon('myIcon.png')
FXLabel(self, 'A label with an icon', icon)
```

### XPM icons

XPM image data can be defined as a list of Python strings:

```python
blueIconData = [
    "12 12 2 1",
    "  c None s None",
    ". c #0000FF",
    "            ",
    "   ......   ",
    "  ........  ",
    " .......... ",
    "............",
    "............",
    "  ........  ",
    "   ......   ",
    "            "
]
blueIcon = FXXPMIcon(getAFXApp(), blueIconData)
```

---

## Colors and RGB values

The Abaqus GUI Toolkit provides predefined colors and RGB value support.

### Predefined colors

- `FX_RED` - Red
- `FX_GREEN` - Green
- `FX_BLUE` - Blue
- `FX_BLACK` - Black
- `FX_WHITE` - White

### RGB values

You can specify custom colors using RGB values:

```python
# RGB values are specified as hex strings
color = "#FF0000"  # Red
```
