# Chapter 6: Customizing Abaqus/CAE and Abaqus/Viewer

This chapter describes user interface customization, printer configuration, and graphics card tuning for Abaqus/CAE and Abaqus/Viewer.

Abaqus/CAE and Abaqus/Viewer have platform dependencies. These dependencies may change between releases; therefore, they are listed on the Support page at www.3ds.com/simulia, where the latest information is published.

## 6.1 Customizing the User Interface

To customize the Abaqus/CAE and Abaqus/Viewer user interface, you can specify common display properties on Windows platforms.

Settings on other platforms (such as Linux) may also affect the appearance of the user interface and some of its functionality. You can also record all operations performed in the Abaqus/CAE or Abaqus/Viewer user interface to a file named `abaqus.guiLog`.

### Hardware Acceleration (All Platforms)

Abaqus/CAE and Abaqus/Viewer may fail when hardware acceleration is turned on with some graphics devices. Turning off hardware acceleration can be done if absolutely necessary, but it is not recommended. Disabling hardware acceleration significantly reduces graphics performance in Abaqus/CAE and Abaqus/Viewer.

**Linux Platforms**

Start Abaqus/CAE or Abaqus/Viewer with the `-mesa` option:

```bash
abaqus cae -mesa
abaqus viewer -mesa
```

**Windows Platforms**

There are two methods for turning off hardware acceleration on Windows platforms:

- Add the parameter `abaqus_no_hardware_acceleration=ON` to the Abaqus environment file; or
- Create a system environment variable using the following command:

```batch
set Abaqus_NO_HARDWARE_ACCELERATION=1
```

### Common Customization on Windows Platforms

The following procedures describe how to specify some common settings on Windows platforms:

**Changing the "Start in" Location of any Abaqus Shortcut**

1. Using Windows Explorer, navigate to the directory containing the Abaqus shortcuts. These shortcuts affect all users on the computer and may require special permissions to change.
2. Right-click the shortcut whose Start in location you want to change (AbaqusCAE, Abaqus Command, or Abaqus Viewer), and select Properties; then click the Shortcut tab.
3. In the text box labeled "Start in:", set the full path of the directory you want to use as the default save location for files created by that Abaqus product.

**Preventing Abaqus/CAE and Abaqus/Viewer Windows from Being Erased When Moving Dialog Boxes**

1. Select Start -> Control Panel.
2. In the search box, type "effects", and press Enter.
3. Select Adjust the appearance and performance of Windows.
4. On the Visual Effects tab of the Performance Options dialog, toggle off "Show window contents while dragging".
5. Click OK to save your settings and close the Performance Options dialog.

**Changing Colors and Fonts Used in Abaqus/CAE and Abaqus/Viewer**

You can change the colors and fonts displayed in Abaqus/CAE and Abaqus/Viewer by applying a new color scheme to the session. The color scheme determines the color and text settings that Windows uses to display each component of the application, such as its menus, dialog boxes, and title bars.

1. Select Start -> Control Panel, and then type "display" in the search box.
2. If necessary, select a new font size.
3. Select Personalize.
4. Select a preset theme from the list.
5. If necessary, change the color or font settings for individual items in the selected color scheme:
   a. Type "window" in the search box. Select "Change window colors and metrics" from the search results under Personalize.

   b. Select the item whose color and font display you want to change.

   c. Select a new color for the item from the color list.

   d. Adjust the text settings for the selected item from the options at the bottom.

   e. Repeat the previous two steps for other individual items in the color scheme.

   f. Click OK to close the Window Color and Appearance dialog.

6. Click OK to save your settings and close the Display Properties dialog.

**Changing Default Fonts Used in Abaqus/CAE and Abaqus/Viewer**

By default, Windows renders text in Abaqus/CAE and Abaqus/Viewer viewport windows by referencing fonts available in the system font directory. You can override this default behavior and use different fonts for the session by adding the `hks_font_path` parameter to the Abaqus environment file. If you want to set multiple font directories for the session, set this parameter to multiple comma-separated values.

### Linux Settings That Affect Abaqus/CAE and Abaqus/Viewer

The Linux operating system provides you with many customization options. Since you can change parts of the operating environment that remain constant on other platforms, your Linux settings may change some basic interactions in Abaqus/CAE and Abaqus/Viewer.

**Removing the Window Title Bar**

If you have customized your system to not display window title bars, your access to some dialog box and toolbox functionality may be limited. Without a title bar, you may be unable to move dialog boxes. Using the [Esc] key is the only method for closing dialog boxes or toolboxes that have neither a title bar nor a Cancel button.

**Removing Window Borders**

Resizing dialog boxes requires that you click and drag the borders. If your Linux customization includes removing application window borders, you may be unable to resize dialog boxes in Abaqus/CAE and Abaqus/Viewer. Instead, use scroll bars to access data beyond the edges of dialog boxes.

**Displaying Japanese Characters**

If your locale is set to Japanese, Abaqus/CAE and Abaqus/Viewer can display Japanese text in the viewport. For example, text annotations and the status block are displayed in Japanese. For Japanese characters to display correctly, Japanese TrueType fonts must be installed in the `/usr/lib/X11/fonts` directory.

### Recording All User Interface Operations to a Log File

You can record all operations performed in the Abaqus/CAE or Abaqus/Viewer user interface to a file named `abaqus.guiLog`. This setting can be enabled for a single session or selected as a default behavior.

**Enabling User Interface Recording at Runtime**

Start Abaqus/CAE or Abaqus/Viewer with the `-guiRecord` option:

```bash
abaqus cae -guiRecord
abaqus viewer -guiRecord
```

**Enabling User Interface Recording Using ABQ_CAE_GUIRECORD**

You can specify user interface recording by setting `ABQ_CAE_GUIRECORD` from the command line. On Windows platforms, you can also set this as a system environment variable.

- To set the variable for a single session, enter the following command at the command prompt:

```batch
set ABQ_CAE_GUIRECORD=1
```

You must run Abaqus/CAE or Abaqus/Viewer from the same command prompt.

- To enable user interface recording as a default behavior on Windows platforms, save the parameter `ABQ_CAE_GUIRECORD=ON` in Windows system properties.

## 6.2 Configuring Printers

For Windows platforms, print commands are not normally necessary. Abaqus/CAE and Abaqus/Viewer automatically detect and list any installed Windows printers.

If you have problems using the print tools in Abaqus/CAE or Abaqus/Viewer, check the installed Windows printers on your computer and remove any printers that are no longer valid.

When Abaqus/CAE or Abaqus/Viewer prints to a PostScript printer, it goes through the following steps:

1. **Creating a Temporary PostScript File**: The temporary PostScript file contains all the PostScript code required to describe the pages to be printed.
2. **Retrieving the Print Command Specified in the Print Dialog**: The command specified in the print dialog can be any command that sends an unmodified copy of the file in its last argument to the printer.
3. **Appending the Temporary File Name and Calling the Resulting Command**: The name of the temporary file created earlier is appended to the print command, and the PostScript file is printed.
4. **Deleting the Temporary PostScript File**: The temporary PostScript file may be deleted before printing if your printer does not support print spooling.

To customize the default print command used by Abaqus/CAE or Abaqus/Viewer when the print dialog is displayed, add the following line to the `abaqus_v6.env` file in your home directory or the Abaqus version site directory:

```python
def onCaeStartup():
    session.printOptions.setValues(printCommand='print_command_and_arguments_here')
```

To prevent the temporary PostScript file from being deleted, add the following line to the `abaqus_v6.env` file in your home directory or the Abaqus version site directory:

```python
def onCaeStartup():
    session.printOptions.setValues(deleteTemporaryFiles=False)
```

## 6.3 Tuning Graphics Cards

This section contains the information needed to configure graphics adapters for Abaqus/CAE and Abaqus/Viewer that have not been certified.

### Why Is Tuning Needed?

SIMULIA tunes and certifies a limited set of graphics adapters before each release. Tuning parameters for these graphics adapters are included in Abaqus. However, new graphics adapters and new drivers for existing graphics adapters become available between releases. Tuning enables you to take advantage of these new adapters and drivers while waiting for a new version of Abaqus/CAE or Abaqus/Viewer.

Abaqus/CAE and Abaqus/Viewer use OpenGL for high-speed graphics rendering. Although the OpenGL standard has strict conformance tests, certain features are implementation-dependent and may require tuning to work correctly. Tuning new graphics adapters or drivers ensures that Abaqus/CAE and Abaqus/Viewer graphics render correctly and achieve the maximum rendering performance for each system.

You can find the latest information about certified graphics adapters on the Support page at www.3ds.com/simulia.

### How Are Tuning Parameters Adjusted?

Abaqus/CAE and Abaqus/Viewer provide the following two methods for tuning graphics parameters:

1. Select View -> Graphics Options from the main menu bar. Abaqus displays the Graphics Options dialog, from which you can select desired settings. This method allows you to choose only from the most commonly used tuning parameters.
2. Use Abaqus Scripting Interface commands to select the desired settings. You can enter commands in the command line interface (CLI) and modify the values of tuning parameters. This method provides complete control over all tuning parameters.

**Table 1: Tuning Parameters**

| Parameter | Standard Value | Modifiable via Graphics Options Dialog | Modifiable at Startup Only |
|-----------|---------------|---------------------------------------|---------------------------|
| displayLists | On | Yes | No |
| antiAlias | On | Yes | No |
| translucencyMode | More accurate than fast | Yes | No |
| highlightMethod | Hardware | Yes | No |
| highlightMethodHint | Hardware | Yes | No |
| dragMode | As-is | Yes | No |
| autoFitAfterRotate | Off | Yes | No |
| backgroundColor | #33366 | Yes | No |
| backgroundBottomColor | #acacc1 | Yes | No |
| backgroundStyle | Gradient | Yes | No |
| backgroundOverride | On | Yes | No |
| doubleBuffering | on | No | No |
| polygonOffsetConstant | 0.0 to 100.0 | No | No |
| polygonOffsetSlope | 0.0 to 100.0 | No | No |
| printPolygonOffsetConstant | 0.0 to 100.0 | No | No |
| printPolygonOffsetSlope | 0.0 to 100.0 | No | No |
| textureMapping | On | No | No |
| printTextureMapping | On | No | No |
| vertexArrays | On | No | No |
| vertexArraysInDisplayLists | On | No | No |
| backfaceCulling | on | No | No |
| directRendering | on | No | Yes |
| accelerateOffScreen | Off | No | Yes |
| backingStore | on | No | No |
| hardwareAcceleration | on | No | Yes |
| hardwareOverlay | None | No | Yes |
| hardwareOverlayAvailable | None | No | N/A |
| shadersAvailable | None | No | N/A |
| viewManipDisplayListThreshold | 40 | No | No |
| contourRangeTexturePrecision | 5.0x10-6 | No | No |

**Notes:**

1. The threshold is used in the visualization module of Abaqus/CAE (Abqus/Viewer) only when display lists are enabled in the visualization module.
2. The transmission mode setting for rendering translucent objects ranges from 1 (optimized for performance) to 5 (optimized for accuracy). The default value is 4.
3. highlightMethod is set directly by Abaqus to a value appropriate for highlightMethodHint.
4. Hardware acceleration applies to Windows platforms only.
5. You cannot set the hardwareOverlay parameter or settings directly. Abaqus sets these automatically by detecting what is available on the system hardware.

### Tuning Graphics Parameters Using the Abaqus Scripting Interface

You can enter Abaqus Scripting Interface commands in the command line interface to tune graphics parameters and to find information about the graphics adapter installed on your system.

The `GraphicsOptions` object determines the current graphics settings. These settings can be modified during the session using the `setValues` method.

You can view the current settings of graphics parameters by entering the following command in the command line interface:

```python
print(session.graphicsOptions)
```

Typical output is:

```python
({'accelerateOffScreen': OFF,
'antiAlias': ON,
'autoFitAfterRotate': OFF,
'backfaceCulling': ON,
'backgroundBottomColor': '#acacc1',
'backgroundColor': '#333366',
'backgroundOverride': ON,
'backgroundStyle': GRADIENT,
'backingStore': ON,
'contourRangeTexturePrecision': 5.0e-06
'directRendering': ON,
'displayLists': ON,
'doubleBuffering': ON,
'dragMode': AS_IS,
'graphicsDriver': OPEN_GL,
'hardwareAcceleration': ON,
'hardwareOverlay': OFF,
'hardwareOverlayAvailable': False,
'highlightMethod': SOFTWARE_OVERLAY,
'highlightMethodHint': (HARDWARE_OVERLAY,
SOFTWARE_OVERLAY, XOR, BLEND),
'polygonOffsetConstant': 2.0,
'polygonOffsetSlope': 0.75,
'printPolygonOffsetConstant': 1.0,
'printPolygonOffsetSlope': 0.75,
'printTextureMapping': ON,
'shadersAvailable': True,
'stencil': False,
'textureMapping': ON,
'translucencyMode': 3,
'vertexArrays': ON,
'vertexArraysInDisplayLists': ON,
'viewManipDisplayListThreshold': 40})
```

### Tuning the polygonOffsetConstant and polygonOffsetSlope Parameters

You will not see the effect of tuning these parameters if display lists are enabled; therefore, you must turn off display lists before attempting to tune graphics adapters. Alternatively, you can enter the following command in the command line interface:

```python
session.graphicsOptions.setValues(displayLists=OFF)
```

Setting the drag mode to AS_IS helps fine-tune the parameters. Interactively rotating the view shows you if small adjustments are needed.

It is recommended to tune `polygonOffsetConstant` first and then `polygonOffsetSlope`. To tune these parameters, you should first display the parts generated by the example script.

### Making Graphics Configuration Permanent

Once you are satisfied with the values you have specified for the tuning parameters, you can make the changes permanent by including the `onCaeGraphicsStartup` function in your environment file (`custom_v6.env` or `abaqus_v6.env`).

The members of the `DefaultGraphicsOptions` object determine the default graphics settings that are enabled when a session starts and when you click Default in the Graphics Options dialog.

The following example environment file configures your Abaqus/CAE and Abaqus/Viewer graphics settings:

```python
def onCaeGraphicsStartup():
    session.defaultGraphicsOptions.setValues(
        polygonOffsetConstant=1.0,
        polygonOffsetSlope=1.2)
```

---

[Return to Contents](./index.md) | [Previous Chapter: Defining Analysis Batch Queues](./chapter-05.md) | [Next Chapter: Installation Subdirectories](./chapter-07.md)
