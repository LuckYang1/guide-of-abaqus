# Chapter 7: Modes

## Chapter Overview

A mode is a mechanism for gathering user input, processing the input, and then issuing commands to the kernel. This section describes the modes available in the Abaqus GUI Toolkit.

## Chapter Contents

- [About modes](#about-modes)
- [Mode processing](#mode-processing)
- [Form modes](#form-modes)
- [Procedure modes](#procedure-modes)
- [Picking in procedure modes](#picking-in-procedure-modes)

---

## About modes

A mode is activated through widgets in the GUI, typically a menu button. Once a mode is activated, it is responsible for:

1. Gathering user input
2. Processing the input
3. Issuing commands
4. Performing any error handling associated with the mode or its issued commands

The Abaqus GUI Toolkit provides two modes:

### Form modes

Form modes provide a dialog box interface. Form modes use one or more dialog boxes to gather user input.

### Procedure modes

Procedure modes provide an interface that guides users through a sequence of steps by prompting for input in the prompt area of the application.

---

## Mode processing

A mode performs command processing and sends commands to the kernel.

When the user interacts with the GUI, the mode:

1. Gathers user input from dialog boxes
2. Builds the input into a kernel command string
3. Sends the command to the kernel process via the IPC protocol
4. Receives and processes the kernel's response

---

## Form modes

Form modes provide a dialog box interface.

Form modes use the AFXForm class to manage dialog boxes and data input.

### Form mode example

Form modes are typically used with AFXDataDialog to create data input dialog boxes.

---

## Procedure modes

Procedure modes provide an interface that guides users through a sequence of steps by prompting for input in the prompt area of the application.

Procedure modes use the AFXProcedure class as a base class.

### Procedure mode example

```python
class MyProcedure(AFXProcedure):
    def __init__(self, command):
        AFXProcedure.__init__(self, command)

    def getFirstStep(self):
        # Return the first step
        pass

    def getNextStep(self, currentStep):
        # Return the next step
        pass
```

---

## Picking in procedure modes

Procedure modes often require users to input by picking objects in the graphic area.

### Picking types

- **Point picking**: The user clicks to select a point.
- **Object picking**: The user selects objects.
- **Coordinate picking**: The user enters coordinate values.

### Picking modes

Abaqus/CAE uses AFXPickMode to manage picking operations.
