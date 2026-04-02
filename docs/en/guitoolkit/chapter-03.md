# Chapter 3: Building Dialog Boxes

## Chapter Overview

This section describes the components of dialog boxes and how to create them using the Abaqus GUI Toolkit.

## Chapter Contents

- [Widgets](#widgets)
- [Layout managers](#layout-managers)
- [Dialog boxes](#dialog-boxes)

---

## Widgets

This section describes how to create widgets in your application.

There are many widgets in the Abaqus GUI Toolkit; however, only the most commonly used widgets are described here. You should refer to the Abaqus GUI Toolkit Reference Guide for a complete list of widget classes.

### Labels and buttons

This section describes widgets that use labels and buttons in the Abaqus GUI Toolkit.

#### About labels and buttons

Several widgets in the Abaqus GUI Toolkit support labels.

For example, if you want to place a label in front of a text field, you should use AFXTextField instead of creating a horizontal frame and adding a label widget and a text field widget. The following sections describe the specific widgets that support labels.

Both label and button constructors accept a text string argument. This text string can consist of three parts, each separated by `\t`. The three parts of the text string are:

**Text**: The text that the widget displays.

**Tip text**: The text that is displayed when you hover the mouse pointer over the widget for a short time. You must provide tip text if the widget has only one associated icon.

**Help text**: The text that is displayed in the status bar of the application (assuming the application has a status bar).

In addition, you can define a keyboard accelerator for a widget by placing an & symbol in front of one of the characters in the text. For example, if you specify the string `&Calculate` for a button, the button label appears as shown in Figure 1. You can press the Alt key and the C key to invoke the button using the accelerator.

#### Labels

The FXLabel widget displays a read-only string. FXLabel can also display an optional icon.

```python
FXLabel(parent, 'This is an FXLabel.\tThis is\nthe tooltip')
```

#### Push buttons

The FXButton widget provides buttons that a user can click to trigger an action.

#### Check buttons

The FXCheckButton widget provides small boxes that a user can click to toggle the on/off state of an option.

#### Radio buttons

The FXRadioButton widget provides options of which only one can be selected from a group.

#### Menu buttons

The AFXMenuButton widget displays a menu pane when pressed.

#### Popup menus

You can create popup menus that appear when the user right-clicks on a widget.

#### Toolbar and toolbox buttons

The AFXToolButton widget does not display text in the button, but the button usually has a tool tip.

#### Flyout buttons

The AFXFlyoutButton widget displays a flyout popup window.

#### Color buttons

The AFXColorButton widget displays a button that, when clicked, shows a color selection dialog box.

### Text widgets

This section describes widgets in the Abaqus GUI Toolkit that allow users to enter text.

#### Single line text field widget

The AFXTextField widget provides a single-line text field.

#### Multi-line text widget

The FXText widget provides a multi-line text area.

### Lists and combo boxes

This section describes widgets in the Abaqus GUI Toolkit that allow you to select one or more items from a list.

You use a list widget when there is enough space in the GUI and all or most of the selections can be displayed at the same time.

You use a combo box when you want to save space in the GUI and display only the current selection.

#### Lists

AFXList allows single or multiple selections from its items.

AFXList supports the following selection strategies:

- **LIST_SINGLESELECT**: The user can select zero or one item.
- **LIST_BROWSESELECT**: One item is always selected.
- **LIST_MULTIPLESELECT**: The user can select zero or more items.
- **LIST_EXTENDEDSELECT**: The user can select zero or more items; drag, Shift-select, and Ctrl-select are allowed.

#### List boxes

AFXListBox is a drop-down list box that allows the user to select one item from a list.

#### Combo boxes

AFXComboBox allows the user to select from a list or enter their own value.

### Range widgets

This section describes widgets in the Abaqus GUI Toolkit that allow users to select a range of values.

#### Spinners

The AFXSpinner widget allows the user to select one value from a range by clicking the arrows on the widget.

### Tree widgets

This section describes tree widgets in the Abaqus GUI Toolkit.

#### Tree list

The FXTreeList widget displays items in a hierarchical tree structure.

### Table widget

The AFXTable widget arranges items in a spreadsheet-like manner.

#### Table widget layout

Tables laid out by the AFXTable widget can have leading rows and leading columns that serve as headers.

#### Table constructor

The AFXTable constructor is defined as follows:

```python
AFXTable(p, numVisRows, numVisColumns, numRows, numColumns,
tgt=None, sel=0, opts=AFXTABLE_NORMAL,
x=0, y=0, w=0, h=0,
pl=DEFAULT_MARGIN, pr=DEFAULT_MARGIN,
pt=DEFAULT_MARGIN, pb=DEFAULT_MARGIN)
```

#### Rows and columns

Tables support leading rows and leading columns. Leading rows are displayed at the top of the table, and leading columns are displayed at the left of the table.

#### Spanning

You can make items in header rows or columns span multiple rows or columns.

#### Justification

By default, the table displays left-justified entries. You can change the justification of items using the following table methods:

- `setColumnJustify(column, justify)`
- `setItemJustify(row, column, justify)`

#### Editing

By default, all items in the table are not editable. To make all items in the table editable, you must specify AFXTABLE_EDITABLE in the table constructor.

#### Types

By default, all items in the table are text items. However, the table widget also supports BOOL, COLOR, FLOAT, ICON, INT, LIST, and TEXT items.

### Miscellaneous widgets

#### Progress bar

The AFXProgressBar widget displays a visual indication of the progress of an operation.

### The create method

Most widgets require a call to the create() method after creation to initialize the underlying data structures.

### Widgets and fonts

The Abaqus GUI Toolkit provides the following font options:

- FONT_TIMESROMAN
- FONT_HELVETICA
- FONT_COURIER
- FONT_SERIF
- FONT_SANSSERIF
- FONT_MONOSPACE
