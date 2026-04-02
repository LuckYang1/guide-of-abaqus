# Chapter 2: Getting Started with Abaqus GUI Toolkit

## Chapter Overview

This chapter provides an overview of customizing GUI applications.

## Chapter Contents

- [Kernel and GUI](#kernel-and-gui)
- [Components of an Abaqus GUI application](#components-of-an-abaqus-gui-application)
- [Plug-ins and customized applications](#plug-ins-and-customized-applications)
- [Running the prototype application](#running-the-prototype-application)

---

## Kernel and GUI

Abaqus/CAE executes as two separate processes: the kernel and the GUI.

The kernel's role is to provide access to the Abaqus database and the commands that create and modify it. The GUI's role is to gather user input, then package it as command strings and send them to the kernel for execution. The GUI is not required for Abaqus to execute -- you can build, analyze, and postprocess an entire model using kernel scripts without ever invoking the GUI.

Typically, when you develop some custom functionality, you first create the kernel commands that implement that functionality. These commands can be debugged by executing them in the Abaqus/CAE command line interface (CLI). Once you have verified that the kernel commands work correctly in the CLI, you can design a GUI to gather the user input required by the commands.

---

## Components of an Abaqus GUI application

Creating a GUI application involves a number of components.

The figure below shows an overview of these components and how they connect. This section briefly introduces each component. These components are discussed in detail in later chapters.

![Figure 1: Abaqus GUI application overview](./images/cbbc39debc18afb4a5b487630c1650c57717dfb6dfec08a40985970afa33c12c.jpg)

### Widgets

At the lowest level of your application, you use widgets to gather input from users through the graphical user interface. For example, a text field widget presents a box into which a user can enter numbers. Similarly, a check button widget presents a small box that a user can click to toggle the on/off state of an option.

### Layout managers

Layout managers arrange widgets by providing alignment options. For example, a horizontal frame arranges widgets in a row. A vertical frame arranges widgets in a column.

### Dialog boxes

Dialog boxes group widgets inside layout managers and present all the input required for a particular function. For example, a print dialog box presents all the widgets that allow a user to specify what should be printed and how it should be printed.

### Modes

A mode is a GUI mechanism that controls a particular user interface display. A mode is also responsible for issuing the commands associated with that user interface. For example, when you select File->Print, a mode is launched. This mode displays the print dialog box and issues the print command when the user clicks OK.

### Modules and toolsets

Modules and toolsets group functionality together. A GUI module is a grouping of similar functionality, such as the Part module in Abaqus/CAE. A GUI toolset is similar to a GUI module in that it groups similar functionality together, but it typically contains more specific functionality that can be used by one or more GUI modules. An example of a GUI toolset in Abaqus/CAE is the Datum tool.

### The application

The application is responsible for high-level activities such as managing the GUI processes used by the application and updating the state of widgets. In addition, the application is responsible for interacting with the desktop window manager.

---

## Plug-ins and customized applications

You can use the Abaqus GUI Toolkit in two ways -- through the plug-in architecture or by creating a customized application.

### Plug-in

The plug-in toolset sits on top of Abaqus/CAE. First, the Abaqus/CAE application is built; then, the plug-in toolset searches specific directories for files that add items to the top-level Plug-ins menu. If you only intend to add functionality to the standard Abaqus/CAE application, and accessing that functionality through the Plug-ins menu in the main menu bar is sufficient, the plug-in toolset may meet your needs. For detailed information on plug-ins, see Using plug-ins.

### Customized application

By contrast, to create a customized application, you need to build the application from scratch. You should write a customized application if you want to modify some standard functionality of Abaqus/CAE in addition to adding functionality to it. While creating a customized application provides the most flexibility, it requires more work than using the plug-in toolset. However, a customized application allows you to modify aspects of the application that the plug-in toolset cannot control. Specifically, a customized application allows you to:

- **Remove Abaqus/CAE modules or toolsets**: When creating a customized application, you determine which modules and toolsets are loaded into the application and the order in which they appear.

- **Modify Abaqus/CAE modules or toolsets**: If you want to add or delete functionality from an Abaqus/CAE module, you must derive a module from the Abaqus/CAE module and then register your module instead of the Abaqus/CAE module. Follow similar steps if you want to add or delete functionality from an Abaqus/CAE toolset.

- **Change the application name and version number**: When creating a customized application, you create a launch script that initializes the application object with the name of your application and its version number.

- **Control startup commands and license tokens used**: When creating a customized application, you can modify the site configuration file that defines the commands used to launch the application. You can also modify the same site configuration file to specify the license token that is checked out when the application starts.

---

## Running the prototype application

The SIMULIA Community provides a customized application called the prototype application. The prototype application allows you to experiment with the contents of dialog boxes until you produce a design that satisfies you. You can launch the prototype application, change the code that controls the contents of a dialog box, and immediately see those changes in the application.

The SIMULIA Community (SIMULIA Community > Learning Resources > 3DEXPERIENCE and Traditional Products > Abaqus > Plug-ins/Scripts) provides examples of plug-ins and customized applications, as well as access to a user community that fosters the development of the Abaqus Scripting Interface and Abaqus GUI Toolkit. Search for "Prototype Example" in that community to download the zip file for the prototype application, then unzip the file and go to the directory containing the downloaded files. To use the prototype application, open the file testDB.py in a text editor. Enter the following from the system prompt:

```bash
abaqus cae -custom prototypeApp -noStartup
```

The `-custom` argument indicates that you are running a customized version of Abaqus/CAE. The `-noStartup` argument indicates that you want to start Abaqus/CAE without displaying the startup screen. For more information, see Abaqus/CAE Execution.

The application creates two icons in the toolbox, as shown in Figure 1.

![Figure 1: Prototype application](./images/660851fb4d03bc7e2c65f0654b4c82e0184ea2be31825db561e17a4c1dadd81c.jpg)

- Icon reloads the form code (testForm.py)
- Icon reloads the dialog code (testDB.py)

If you make changes to the form code, click the icon to reload that file. If you make changes to the dialog code, click the icon to reload that file. You do not need to quit and restart Abaqus/CAE to see your changes in the form or dialog.

For example, try the following:

1. Click the icon to display the dialog box, and note the text labels displayed in the dialog box.
2. Click Cancel in the dialog box to close it.
3. Change one of the labels in testDB.py and save the file.
4. Click the icon again to display the dialog box. You will see the modified label in the dialog box.

When you click OK in a dialog box, the kernel commands issued by the dialog box are written to the message area instead of being executed by Abaqus/CAE. This allows you to debug the commands before trying to execute them in the kernel.

After you have debugged your form and dialog code, you can modify the form to issue commands to the kernel following the example in the form example. You can attach the form to your GUI following the example shown in Checking the GUI module example, instead of attaching it to the icon.
