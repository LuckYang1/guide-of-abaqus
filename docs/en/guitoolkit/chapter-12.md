# Chapter 12: The Application Object

## Chapter Overview

This section describes the Abaqus application object. The application object manages the message queue, timers, chores, GUI updates, and other system facilities.

## Application object methods

### Initialization methods

- `init(sys.argv)` - Initialize the application

### Event loop

- `run()` - Start the main event loop
- `exit()` - Exit the event loop

### Window access

- `getAFXMainWindow()` - Get the main window instance

### Resource management

The application object also manages the following resources:

- Fonts
- Icons
- Colors

## Common methods

### Message handling

The application object handles messages from the operating system and user interface.

### Timers

The application object supports timer events.

```python
# Create a timer
app.addTimer(interval, callback)
```

### Chores

The application object can schedule background chores.

```python
# Schedule a chore
app.addChore(func, data)
```
