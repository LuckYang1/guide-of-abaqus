# Chapter 5: Dialog Boxes

## Chapter Overview

This section describes the dialog boxes you can create with the Abaqus GUI Toolkit.

## Chapter Contents

- [About dialog boxes](#about-dialog-boxes)
- [Modal versus modeless](#modal-versus-modeless)
- [Showing and hiding dialog boxes](#showing-and-hiding-dialog-boxes)
- [Message dialog boxes](#message-dialog-boxes)
- [Custom dialog boxes](#custom-dialog-boxes)
- [Data dialog boxes](#data-dialog-boxes)
- [Common dialog boxes](#common-dialog-boxes)

---

## About dialog boxes

The following common types of dialog boxes are available in the Abaqus GUI Toolkit: message dialog boxes, custom dialog boxes, data dialog boxes, and common dialog boxes.

### Message dialog boxes

Message dialog boxes allow you to issue error, warning, or information messages.

### Custom dialog boxes

Custom dialog boxes allow you to build any custom interface. However, you must provide the infrastructure needed to make the dialog box work as required.

### Data dialog boxes

Data dialog boxes provide support for dialog boxes that accept user input. Data dialog boxes are designed to work with forms that automatically issue commands.

### Common dialog boxes

Common dialog boxes are dialog boxes that provide standard functionality common to many applications. A file selection dialog box is a typical common dialog box.

---

## Modal versus modeless

Dialog boxes can be modal or modeless.

### Modal

A modal dialog box prevents interaction with the rest of the application until the user closes the dialog box.

### Modeless

A modeless dialog box allows the user to interact with other parts of the GUI while the dialog box is displayed. In Abaqus/CAE, all secondary dialog boxes except prompts should be modal dialog boxes.

A dialog box itself is not defined as modal or modeless -- that behavior comes from the method used to display the dialog box.

---

## Showing and hiding dialog boxes

Dialog boxes have show and hide methods that display or hide the dialog box from the screen.

In most cases, you do not need to call these methods because the mode infrastructure calls them for you. However, you may want to write your own show and hide methods to perform some special processing that will occur before the application displays or hides the dialog box.

```python
def show(self):
    # Do some special processing here.
    ...
    # Call base class method.
    AFXDataDialog.show(self)

def hide(self):
    # Do some special processing here.
    ...
    # Call base class method.
    AFXDataDialog.hide(self)
```

---

## Message dialog boxes

The AFXMessageDialog class extends the FXMessageDialog class by enforcing certain characteristics of the dialog box (such as window title and message symbols).

### Message dialog box types

#### Error dialog boxes

Error dialog boxes display error messages.

#### Warning dialog boxes

Warning dialog boxes display warning messages.

#### Information dialog boxes

Information dialog boxes display informational messages.

#### Specialized message dialog boxes

Specialized message dialog boxes provide specific functionality.

---

## Custom dialog boxes

Custom dialog boxes allow you to build any custom interface.

### About custom dialog boxes

#### Constructor

The AFXDialog constructor defines the parent, title, and options for the dialog box.

```python
AFXDialog(parent, title, opts=0, x=0, y=0, w=0, h=0)
```

#### Sizing and location

The size and location specified in the dialog box constructor are the initial suggested size and location. The actual size may vary depending on the dialog box contents.

#### Action area

The action area typically contains buttons such as OK, Cancel, Apply, etc.

#### Custom action area button names

You can customize the names of buttons in the action area.

#### Action button handling

Dialog boxes typically have buttons such as OK, Cancel, and Apply. The handling of these buttons is managed by the AFXDialog class.

---

## Data dialog boxes

Data dialog boxes provide support for dialog boxes that accept user input.

### About data dialog boxes

The AFXDataDialog class extends the AFXDialog class to provide support for data input dialog boxes.

#### Constructor

The AFXDataDialog constructor is more complex than the AFXDialog constructor because it needs to interact with forms and modes.

#### Bailout

Bailout is cleanup that is performed when the user cancels an operation.

#### Constructor contents

A data dialog box constructor typically contains widget creation, layout setup, and message handler setup.

#### Transitions

Data dialog boxes can have transitional states, such as transitions between steps.

#### Updating your GUI

When data changes, you may need to update the GUI.

#### Action area

The action area of a data dialog box is similar to that of a custom dialog box.

---

## Common dialog boxes

Common dialog boxes are dialog boxes that provide standard functionality.

### File/Directory selector

AFXFileSelector provides file selection functionality.

### Print dialog box

AFXPrintDialog provides print functionality.

### Color selector dialog box

AFXColorSelector provides color selection functionality.
