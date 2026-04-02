# 第六章：自定义 Abaqus/CAE 和 Abaqus/Viewer

本章介绍 Abaqus/CAE 和 Abaqus/Viewer 的用户界面定制、打印机配置和图形卡调优。

Abaqus/CAE 和 Abaqus/Viewer 存在平台依赖性。这些依赖性可能在不同版本之间发生变化；因此，它们列在 www.3ds.com/simulia 的 Support 页面上，在那里发布最新信息。

## 6.1 自定义用户界面

要自定义 Abaqus/CAE 和 Abaqus/Viewer 用户界面，您可以在 Windows 平台上指定通用显示属性。

其他平台（如 Linux）上的设置也可能影响用户界面的外观及其某些功能。您还可以将 Abaqus/CAE 或 Abaqus/Viewer 用户界面中的所有操作记录到一个名为 `abaqus.guiLog` 的文件中。

### 硬件加速（所有平台）

使用某些图形设备时，Abaqus/CAE 和 Abaqus/Viewer 可能会在打开硬件加速时失败。如果完全必要，可以关闭硬件加速，但这不是推荐的。禁用硬件加速会严重降低 Abaqus/CAE 和 Abaqus/Viewer 中的图形性能。

**Linux 平台**

使用 `-mesa` 选项启动 Abaqus/CAE 或 Abaqus/Viewer：

```bash
abaqus cae -mesa
abaqus viewer -mesa
```

**Windows 平台**

在 Windows 平台上关闭硬件加速有两种方法：

- 将参数 `abaqus_no_hardware_acceleration=ON` 添加到 Abaqus 环境文件；或
- 使用以下命令创建系统环境变量：

```batch
set Abaqus_NO_HARDWARE_ACCELERATION=1
```

### Windows 平台上的常见定制

以下过程说明如何在 Windows 平台上指定一些常用设置：

**更改任何 Abaqus 快捷方式的"起始位置"**

1. 使用 Windows Explorer 转到包含 Abaqus 快捷方式的目录。这些快捷方式影响计算机上的所有用户，可能需要特殊权限才能更改。
2. 右键单击要更改其起始位置快捷方式（AbaqusCAE、Abaqus Command 或 Abaqus Viewer），然后选择属性；然后单击快捷方式选项卡。
3. 在标记为"起始位置："的文本框中，设置要用作该 Abaqus 产品创建的文件的默认保存位置的目录的完整路径。

**阻止 Abaqus/CAE 和 Abaqus/Viewer 窗口在移动对话框时被擦除**

1. 选择开始 -> 控制面板。
2. 在搜索框中输入"效果"，然后按回车。
3. 选择调整 Windows 的外观和性能。
4. 在性能选项对话框的视觉效果选项卡上，切换关闭"拖动时显示窗口内容"。
5. 单击确定保存设置并关闭性能选项对话框。

**更改 Abaqus/CAE 和 Abaqus/Viewer 中使用的颜色和字体**

您可以通过为会话应用新的颜色方案来更改 Abaqus/CAE 和 Abaqus/Viewer 中显示的颜色和字体。颜色方案决定 Windows 用于显示应用程序中每个组件的颜色和文本设置，例如其菜单、对话框和标题栏。

1. 选择开始 -> 控制面板，然后在搜索框中输入"显示"。
2. 如果需要，选择新的字体大小。
3. 选择个性化。
4. 从列表中选择预设主题。
5. 如果需要，更改所选颜色方案中各个项目的颜色或字体设置：
   a. 在搜索框中输入"窗口"。在个性化的搜索结果中选择"更改窗口颜色和度量"。
   
   b. 选择要更改颜色和字体显示的项目。
   
   c. 从颜色列表中选择新的项目颜色。
   
   d. 从底部的选项中调整所选项目的文本设置。
   
   e. 对颜色方案中的其他各个项目重复前两步。
   
   f. 单击确定关闭"窗口颜色和外观"对话框。
   
6. 单击确定保存设置并关闭"显示属性"对话框。

**更改 Abaqus/CAE 和 Abaqus/Viewer 中使用的默认字体**

默认情况下，Windows 通过引用系统字体目录中可用的字体来呈现 Abaqus/CAE 和 Abaqus/Viewer 视口窗口中的文本。您可以通过将 `hks_font_path` 参数添加到 Abaqus 环境文件来覆盖此默认行为并为会话使用其他字体。如果要为会话设置多个字体目录，请将此参数设置为多个逗号分隔的值。

### 影响 Abaqus/CAE 和 Abaqus/Viewer 的 Linux 设置

Linux 操作系统为您提供了许多定制选项。由于您可以更改其他平台上保持不变的操作环境的部分，您的 Linux 设置可能会改变 Abaqus/CAE 和 Abaqus/Viewer 中的一些基本交互。

**移除窗口标题栏**

如果您已自定义系统以不显示窗口标题栏，您对某些对话框和工具箱功能的访问可能会受到限制。没有标题栏，您可能无法移动对话框。使用 [Esc] 键是关闭没有标题栏或取消按钮的对话框或工具箱的唯一方法。

**移除窗口边框**

调整对话框大小需要您单击并拖动边框。如果您的 Linux 定制包括移除应用程序窗口边框，您可能无法在 Abaqus/CAE 和 Abaqus/Viewer 中调整对话框大小。而应使用滚动条来访问超出对话框边缘的数据。

**显示日文字符**

如果您的区域设置是日语，Abaqus/CAE 和 Abaqus/Viewer 可以在视口中显示日语文本。例如，文本注释和状态块以日语显示。要正确显示日文字符，必须将日语 TrueType 字体安装在 `/usr/lib/X11/fonts` 目录中。

### 在日志文件中记录所有用户界面操作

您可以将 Abaqus/CAE 或 Abaqus/Viewer 用户界面中采取的所有操作记录到一个名为 `abaqus.guiLog` 的文件中。可以为单个会话打开此设置，也可以将其选择为默认行为。

**在运行时启用用户界面录制**

使用 `-guiRecord` 选项启动 Abaqus/CAE 或 Abaqus/Viewer：

```bash
abaqus cae -guiRecord
abaqus viewer -guiRecord
```

**使用 ABQ_CAE_GUIRECORD 启用用户界面录制**

您可以通过从命令行设置 `ABQ_CAE_GUIRECORD` 来指定用户界面录制，在 Windows 平台上，也可以将其作为系统环境变量设置。

- 要为单个会话设置变量，请在命令提示符中输入以下命令：

```batch
set ABQ_CAE_GUIRECORD=1
```

您必须从同一个命令提示符运行 Abaqus/CAE 或 Abaqus/Viewer。

- 要在 Windows 平台上将用户界面录制启用为默认行为，请在 Windows 系统属性中保存参数 `ABQ_CAE_GUIRECORD=ON`。

## 6.2 配置打印机

对于 Windows 平台，通常不需要打印命令。Abaqus/CAE 和 Abaqus/Viewer 自动检测并列出任何已安装的 Windows 打印机。

如果您在使用 Abaqus/CAE 或 Abaqus/Viewer 中的打印工具时遇到问题，请检查计算机上已安装的 Windows 打印机，并删除任何不再有效的打印机。

当 Abaqus/CAE 或 Abaqus/Viewer 打印到 PostScript 打印机时，它会经历以下步骤：

1. **创建临时 PostScript 文件**：临时 PostScript 文件包含描述要打印的页面所需的所有 PostScript 代码。
2. **检索打印对话框中指定的打印命令**：打印对话框中指定的命令可以是任何命令，该命令将其最后一个参数的路径的文件 unmodified 副本发送到打印机。
3. **追加临时文件名并调用生成的命令**：先前创建的临时文件的名称被追加到打印命令，PostScript 文件被打印。
4. **删除临时 PostScript 文件**：如果您的打印机不支持打印假脱机，则可能在打印文件之前删除临时 PostScript 文件。

要自定义 Abaqus/CAE 或 Abaqus/Viewer 在显示打印对话框时使用的默认打印命令，请将以下行添加到主目录或 Abaqus 版本站点目录中的 `abaqus_v6.env` 文件：

```python
def onCaeStartup():
    session.printOptions.setValues(printCommand='print_command_and_arguments_here')
```

要防止临时 PostScript 文件被删除，请将以下行添加到主目录或 Abaqus 版本站点目录中的 `abaqus_v6.env` 文件：

```python
def onCaeStartup():
    session.printOptions.setValues(deleteTemporaryFiles=False)
```

## 6.3 调优图形卡

本节包含配置 Abaqus/CAE 和 Abaqus/Viewer 的图形适配器所需的信息，这些适配器尚未通过认证。

### 为什么需要调优？

SIMULIA 在每个版本之前都会调优和认证有限的图形适配器集。这些图形适配器的调优参数包含在 Abaqus 中。但是，新图形适配器和现有图形适配器的新驱动程序在版本之间可用。调优可以使您在等待 Abaqus/CAE 或 Abaqus/Viewer 新版本时利用这些新适配器和驱动程序。

Abaqus/CAE 和 Abaqus/Viewer 使用 OpenGL 进行高速图形渲染。虽然 OpenGL 标准有严格的合规性测试，但某些功能是实现相关的，需要调优才能正常工作。调优新的图形适配器或驱动程序可确保 Abaqus/CAE 和 Abaqus/Viewer 图形正确渲染，并获得每个系统的最大渲染性能。

您可以在 www.3ds.com/simulia 的 Support 页面上找到有关已认证图形适配器的最新信息。

### 如何调优参数？

Abaqus/CAE 和 Abaqus/Viewer 提供以下两种调优图形参数的方法：

1. 从主菜单栏中选择 View -> Graphics Options。Abaqus 显示图形选项对话框，可从中选择所需的设置。此方法允许您仅从最常用的调优参数中进行选择。
2. 使用 Abaqus Scripting Interface 命令选择所需的设置。您可以在命令行接口 (CLI) 中输入命令并修改调优参数的值。此方法提供对所有调优参数的完全控制。

**表 1：调优参数**

| 参数 | 标准值 | 使用图形选项对话框修改 | 仅在启动时修改 |
|------|--------|----------------------|--------------|
| displayLists | On | Yes | No |
| antiAlias | On | Yes | No |
| translucencyMode | 比 fast 更准确 | Yes | No |
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

**注释：**

1. 仅当在可视化模块中启用显示列表时，才在 Abaqus/CAE（Ababys/Viewer）的可视化模块中使用该阈值。
2. 渲染半透明对象的透射模式设置范围为 1（针对性能优化）到 5（针对准确性优化）。默认值是 4。
3. highlightMethod 直接由 Abaqus 设置为一个适合 highlightMethodHint 的值。
4. 硬件加速仅适用于 Windows 平台。
5. 您不能直接设置 hardwareOverlay 参数或设置。Ababys 通过检测系统上可用的硬件来自动设置这些值。

### 使用 Abaqus Scripting Interface 调优图形参数

您可以在命令行接口中输入 Abaqus Scripting Interface 命令来调优图形参数并找出安装在系统上的图形适配器的信息。

`GraphicsOptions` 对象确定当前图形设置。可以使用 `setValues` 方法在会话期间修改这些设置。

您可以通过在命令行接口中输入以下命令来查看图形参数的当前设置：

```python
print(session.graphicsOptions)
```

典型的输出是：

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

### 调优 polygonOffsetConstant 和 polygonOffsetSlope 参数

如果启用了显示列表，您将看不到调优这些参数的效果；因此，在尝试调优图形适配器之前，必须关闭使用显示列表。或者，您可以在命令行接口中输入以下命令：

```python
session.graphicsOptions.setValues(displayLists=OFF)
```

将拖动模式设置为 AS_IS 有助于微调参数。交互式旋转视图将向您显示是否需要微小的调整。

建议首先调优 `polygonOffsetConstant`，然后调优 `polygonOffsetSlope`。要调优这些参数，您应该首先显示示例脚本中生成的零件。

### 使图形配置永久化

一旦您对为调优参数指定的值满意，您可以通过在环境文件（`custom_v6.env` 或 `abaqus_v6.env`）中包含 `onCaeGraphicsStartup` 函数来使更改永久化。

`DefaultGraphicsOptions` 对象的成员确定启动会话时以及在图形选项对话框中单击默认值时启用的默认图形设置。

以下示例环境文件配置了您的 Abaqus/CAE 和 Abaqus/Viewer 图形设置：

```python
def onCaeGraphicsStartup():
    session.defaultGraphicsOptions.setValues(
        polygonOffsetConstant=1.0,
        polygonOffsetSlope=1.2)
```

---

[返回目录](./index.md) | [上一章：定义分析批处理队列](./chapter-05.md) | [下一章：安装子目录](./chapter-07.md)
