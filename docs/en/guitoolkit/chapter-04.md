# Chapter 4: Layout Managers

## Chapter Overview

This section describes how to use the various layout managers in the Abaqus GUI Toolkit to arrange widgets in dialog boxes.

## Chapter Contents

- [About layout managers](#about-layout-managers)
- [Padding and spacing](#padding-and-spacing)
- [Horizontal and vertical frames](#horizontal-and-vertical-frames)
- [Vertical alignment for composite children](#vertical-alignment-for-composite-children)
- [General-purpose layout managers](#general-purpose-layout-managers)
- [Row and column layout manager](#row-and-column-layout-manager)
- [Resizable regions](#resizable-regions)
- [Rotating regions](#rotating-regions)
- [Tab books](#tab-books)
- [Layout hints](#layout-hints)
- [Layout examples](#layout-examples)
- [Tips for specifying layout hints](#tips-for-specifying-layout-hints)

---

## About layout managers

A layout manager places its children in some arrangement inside itself.

Layout managers use a combination of layout hints and packing styles to determine how to place and resize their children. Layout managers in the Abaqus GUI Toolkit compute relative size and relative position rather than absolute coordinates. This relative approach automatically handles changes such as different font sizes and window resizing.

The following layout managers are available in the Abaqus GUI Toolkit:

### FXHorizontalFrame

Arranges widgets horizontally. For more information, see Horizontal and vertical frames.

### FXVerticalFrame

Arranges widgets vertically. For more information, see Horizontal and vertical frames.

### AFXVerticalAligner

Vertically aligns its children to the first child. For more information, see Vertical alignment for composite children.

### FXPacker

Arranges widgets in a general way. For more information, see General-purpose layout managers.

### AFXDialog

Provides the same functionality as FXPacker. For more information, see General-purpose layout managers.

### FXGroupBox

Provides the same functionality as FXPacker but allows a titled border. For more information, see General-purpose layout managers.

### FXMatrix

Arranges widgets in rows and columns. For more information, see Row and column layout manager.

### FXSplitter

Splits regions vertically or horizontally and allows you to resize the regions. For more information, see Resizable regions.

### FXSwitcher

Manages children that are stacked on top of each other (rotating regions). For more information, see Rotating regions.

### FXTabBook

Controls the display of one "page" of widgets at a time using "tab items." For more information, see Tab books.

---

## Padding and spacing

Layout managers (and most widgets) provide some default padding so that widgets are separated from each other.

These values are typically at the end of the widget's argument list. For example:

```python
FXPacker(…, pl, pr, pt, pb, …)
```

Typically, you should accept the default values for padding. However, if you have nested layout managers, you should set the padding values to zero.

Layout managers also provide spacing between their children. These values are typically at the end of the widget's argument list. For example:

```python
FXPacker(…, hs, vs)
```

Typically, you should accept the default values for spacing.

---

## Horizontal and vertical frames

FXHorizontalFrame and FXVerticalFrame are simple layout managers that arrange widgets in a row or column, respectively.

---

## Vertical alignment for composite children

The AFXVerticalAligner widget vertically aligns its children.

---

## General-purpose layout managers

The Abaqus GUI Toolkit includes three general-purpose layout managers with similar layout functionality.

### FXPacker

FXPacker is a general-purpose layout manager.

### AFXDialog

AFXDialog provides functionality similar to FXPacker. Therefore, you do not need to provide a top-level layout manager as the first child in a dialog box; you can use the dialog box's layout functionality instead.

### FXGroupBox

FXGroupBox provides the same functionality as FXPacker. In addition, FXGroupBox can display a labeled border around its children. Abaqus/CAE uses the FRAME_GROOVE flag to produce a thin border around the children of a group box.

---

## Row and column layout manager

FXMatrix arranges widgets in rows and columns.

---

## Resizable regions

The FXSplitter widget splits regions vertically or horizontally. Users can drag the cursor between regions and resize the regions.

---

## Rotating regions

The FXSwitcher widget manages children that are stacked on top of each other.

FXSwitcher allows you to select which child should be displayed by sending a message or by calling its setCurrent method.

---

## Tab books

The FXTabBook widget uses "tab items" to control the display of one "page" at a time.

FXTabBook expects its odd-numbered children to be FXTabItems and its even-numbered children to be some kind of layout manager. The layout manager contains all the widgets to be displayed in that page. Clicking a tab item displays the layout manager associated with that tab (and all its children) while hiding all other layout managers.

You can nest tab books to provide tabs within tabs.

---

## Layout hints

FXPacker, FXTopWindow, and FXGroupBox widgets accept layout hints in their children.

### Layout hints in detail

The following layout hints are supported:

#### LAYOUT_SIDE_TOP

Attaches the widget to the top side of the cavity. LAYOUT_SIDE_TOP is the default layout hint.

#### LAYOUT_SIDE_BOTTOM

Attaches the widget to the bottom side of the cavity.

#### LAYOUT_SIDE_LEFT

Attaches the widget to the left side of the cavity.

#### LAYOUT_SIDE_RIGHT

Attaches the widget to the right side of the cavity.

All layout managers support the following layout hints:

- **LAYOUT_LEFT (default) and LAYOUT_RIGHT**: The layout manager places the widget on the left or right side of the remaining space in the container.
- **LAYOUT_TOP (default) and LAYOUT_BOTTOM**: The layout manager places the widget at the top or bottom of the remaining space in the container.
- **LAYOUT_CENTER_X and LAYOUT_CENTER_Y**: The layout manager centers the widget in the X or Y direction within the parent.
- **LAYOUT_FILL_X and LAYOUT_FILL_Y**: These layout hints allow the layout manager to stretch or shrink the widget to fit the available space.
- **LAYOUT_FIX_WIDTH and LAYOUT_FIX_HEIGHT**: These options fix the width or height of the widget to the value specified in the constructor.

---

## Layout examples

The following examples create three buttons at a time using default layout hints.

### Example 1

The first example creates a single button first on the left side of the cavity.

### Example 2

The second example shows how to use non-default layout hints.

---

## Tips for specifying layout hints

- Do not over-specify layout hints. In many cases, the default values are exactly what you need, and you do not need to specify hints.
- Think in simple rows and columns, using horizontal or vertical frames whenever possible.
- To avoid accumulating too much padding, set padding to zero in nested layout managers.
