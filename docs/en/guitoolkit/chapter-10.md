# Chapter 10: Customizing an Existing Module or Toolset

## Chapter Overview

The preceding chapters described how to create new modules or toolsets. Alternatively, the Abaqus GUI Toolkit allows you to derive new modules or toolsets from existing ones and add or delete functionality from them.

## Chapter Contents

- [Customizing and accessing Abaqus/CAE GUI modules and toolsets](#customizing-and-accessing-abaqus-cae-gui-modules-and-toolsets)
- [File toolset](#file-toolset)
- [Tree toolset](#tree-toolset)
- [Selection toolset](#selection-toolset)
- [Help toolset](#help-toolset)
- [Custom toolset example](#custom-toolset-example)

---

## Customizing and accessing Abaqus/CAE GUI modules and toolsets

The Abaqus GUI Toolkit allows you to make limited changes to Abaqus/CAE GUI modules and toolsets.

### Modifications you can make

- Add new menu items or menus
- Remove existing menu items or menus
- Modify the behavior of menu items

### Accessing existing components

You can access existing Abaqus/CAE modules and toolsets to modify them.

---

## File toolset

The File toolset provides menus for file operations.

---

## Tree toolset

The Tree toolset manages the model tree.

### Tree tabs

The tree toolset provides multiple tabs, each displaying different types of data.

---

## Selection toolset

The Selection toolset manages object selection behavior.

### Selection modes

- **single select**: The user can select only one object.
- **browse select**: There is always one object selected.
- **multi-select**: The user can select multiple objects.

---

## Help toolset

The Help toolset provides help functionality.

---

## Custom toolset example

```python
class MyCustomToolset(AFXToolsetGui):
    def __init__(self):
        AFXToolsetGui.__init__(self, 'CustomToolset')
        # Add custom functionality
```
