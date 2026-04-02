# Chapter 6: Commands

## Chapter Overview

This section describes how dialog boxes issue commands to the Abaqus/CAE kernel.

## Chapter Contents

- [Command overview](#command-overview)
- [Kernel and GUI processes](#kernel-and-gui-processes)
- [Executing commands](#executing-commands)
- [Kernel commands](#kernel-commands)
- [GUI commands](#gui-commands)
- [AFXTargets](#afxtargets)
- [Accessing kernel data from the GUI](#accessing-kernel-data-from-the-gui)
- [Receiving notification of kernel data changes](#receiving-notification-of-kernel-data-changes)

---

## Command overview

There are two classes of commands in Abaqus/CAE: kernel commands and GUI commands.

### Kernel commands

Kernel commands are used to build, analyze, and postprocess finite element models. Kernel commands are documented in the Abaqus Scripting Reference Guide.

### GUI commands

GUI commands are used by the user interface to process input gathered from users and to build kernel command strings that are sent to the kernel for execution. GUI commands are documented in the Abaqus GUI Toolkit Reference Guide.

---

## Kernel and GUI processes

Abaqus/CAE executes as two processes: the kernel process and the GUI process.

### Kernel process

The kernel process holds all the data and methods that Abaqus/CAE uses to perform modeling operations; for example, creating parts and meshing assemblies. The kernel process can run independently of the GUI process.

### GUI process

The GUI is a convenient way for users to specify input to Abaqus/CAE. Kernel command strings are sent from the GUI process to the kernel process via an interprocess communication (IPC) protocol. The kernel process interprets and executes the kernel command strings. If a kernel command throws an exception, the exception is propagated back to the GUI process, where it should be properly caught and handled, typically by displaying an error dialog box.

---

## Executing commands

All commands are ultimately executed in the kernel process, but there are several ways this can be accomplished:

- You can execute kernel commands from a file using the `-start` or `-replay` option on the command line.
- You can execute kernel commands from a file using File->Run Script.
- You can type kernel commands in the Abaqus/CAE CLI.
- The GUI mode infrastructure can send command strings from the GUI to the kernel process for execution.
- You can issue kernel commands directly from the GUI using the `sendCommand` function.

### sendCommand function

The `sendCommand` function accepts three arguments:

- A required string argument specifying the command to execute in the kernel.
- Two optional boolean arguments, `writeToReplay` and `writeToJournal`.

Typically, you should wrap the `sendCommand` function in a try block to catch any exceptions that kernel commands might throw.

```python
from abaqusGui import sendCommand
try:
    sendCommand("mdb.customData.myCommand('Cmd-1', 50, 200)")
except ValueError as x:
    print('an exception was raised: ValueError: %s' % (x))
except:
    exc_type, exc_value = sys.exc_info()[:2]
    print('error. %s.%s'%(exc_type.__name__, exc_value))
```

---

## Kernel commands

Kernel commands can include methods, objects, and arguments.

A kernel command can consist of the following parts:

```
object + method + arguments (keywords)
```

Commands do not always have objects or even arguments, but they always have methods.

---

## GUI commands

GUI commands are designed to work with modes.

A mode performs command processing and sends commands to the kernel. This section describes how to construct and use GUI commands.

### Constructing GUI commands

Use the `AFXGuiCommand` class to construct GUI commands.

The `AFXGuiCommand` class accepts the following arguments:

- **mode**: The mode that activates through widgets in the GUI, typically a menu button.
- **method**: A string specifying the kernel command method.
- **objectName**: A string specifying the kernel command object.
- **registerQuery**: A boolean specifying whether to register a query on the object.

### GUI commands and current objects

Most Abaqus/CAE commands operate on a current object; for example, the current viewport or the current part.

Modes recognize a special syntax when interpreting objects specified in GUI commands. If you place `%s` between square brackets after some repository, the mode replaces `%s` with the current name.

Supported current objects:

| Object specification | Mode interpretation |
|---------------------|---------------------|
| `mdb.models[%s]` | Current model |
| `mdb.models[%s].parts[%s]` | Current part |
| `mdb.models[%s].sketches[%s]` | Current sketch |
| `session.odbs[%s]` | Current output database |
| `session.viewports[%s]` | Current viewport |

### Targets and messages

The Abaqus GUI Toolkit uses a target/message system to accomplish communication within the GUI process.

A message consists of two parts:

- **Message type**: Indicates what type of event has occurred.
- **Message ID**: Identifies the sender of the message.

The two most common message types are SEL_COMMAND and SEL_UPDATE.

---

## AFXTargets

AFXTargets is used for communication between the GUI and the kernel.
