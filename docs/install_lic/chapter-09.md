# 第九章：验证程序

验证程序检查所有许可 Abaqus 产品的安装，并报告每个产品的验证成功或失败。

验证程序在 Abaqus 安装程序完成后自动运行，但只验证产品的子集。验证程序也可以作为 Abaqus 命令选项运行。

该程序为每个许可产品运行验证问题，并将结果与参考值进行比较。命令行选项不受许可证类型的影响；也就是说，验证程序尝试验证命令中命名的所有产品。在运行验证程序之前，会检查所选产品的许可证要求。如果检测到教学学术许可证，则在安装期间运行的验证程序仅检查 Abaqus/Standard、Abaqus/Explicit 和 Abaqus/CAE。

如果产品未获得许可，则跳过产品验证。可以使用 `-noLic` 命令行选项绕过这些检查。所有 Abaqus 产品的验证问题在安装期间自动从磁盘提取。

## 从命令行运行验证程序

通过输入以下命令来运行程序：

```tcl
abaqus verify [-adams -all -ams -tosca -cae -catiav4 -cPerf -dcatiav5 -design -docUrl -exp -foundation -help -install -ioPerf -log -make -moldflow -noGui -noLic -parallel -param -parasolid -proe -retainFiles -scripting -std -swi -user_exp -user_std -verbose -viewer]
```

## 常用选项

| 选项 | 描述 |
|------|------|
| -all | 验证所有许可产品。所有其他验证选项都会被忽略，但 log 和 noLic 除外。 |
| -help | 打印验证用法摘要。 |
| -install | 验证 Abaqus 参数研究和 Abaqus/CAE。 |
| -log | 将所有输出定向到当前工作目录中名为 `verify.log` 的文件。 |

## 产品选项

| 选项 | 描述 |
|------|------|
| -ams | 验证 Abaqus/AMS。 |
| -tosca | 验证 Tosca for Abaqus。 |
| -cae | 验证 Abaqus/CAE。 |
| -design | 验证 Abaqus/Design。 |
| -exp | 验证 Abaqus/Explicit。 |
| -foundation | 验证 Abaqus/Foundation。 |
| -param | 验证 Abaqus 中的参数研究。 |
| -std | 验证 Abaqus/Standard。 |
| -user_exp | 验证带有用户子程序的 Abaqus/Explicit。 |
| -user_std | 验证带有用户子程序的 Abaqus/Standard。 |
| -viewer | 验证 Abaqus/Viewer。 |

## 翻译器选项

| 选项 | 描述 |
|------|------|
| -adams | 验证 MSC.ADAMS 的 Abaqus Interface。 |
| -catiav4 | 验证 CATIA V4 的几何翻译器。 |
| -dcatiav5 | 验证 CATIA V5 的直接几何导入（Abaqus/CAE 中的几何导入功能；不验证 CATIA V5 Associative Interface 插件的安装或功能）。 |
| -moldflow | 验证 Moldflow 的 Abaqus Interface。 |
| -parasolid | 验证 Parasolid 的几何翻译器。 |
| -proe | 验证 Pro/ENGINEER 的几何翻译器（Abaqus/CAE 中的几何导入功能；不验证 Pro/ENGINEER Associative Interface 插件的安装或功能）。 |
| -swi | 验证 SolidWorks 的几何翻译器（Abaqus/CAE 中的几何导入功能；不验证 SolidWorks Associative Interface 插件的安装或功能）。 |

## 附加选项

| 选项 | 描述 |
|------|------|
| -cPerf | 验证 Abaqus/CAE 性能。 |
| -docUrl | 验证 Abaqus HTML 文档 URL。 |
| -ioPerf | 验证 I/O 性能。 |
| -make | 验证 abaqus make 实用程序。 |
| -noGui | 验证 Abaqus/CAE 和 Abaqus/Viewer 的 -noGUI 选项。 |
| -noLic | 需要 -all、-install 或产品选项列表。运行指定产品的验证程序，但绕过所有许可证检查。该程序尝试验证所有选定产品，无论许可情况如何。 |
| -parallel | 使用并行化验证 Abaqus 分析作业。 |
| -scripting | 验证 Abaqus scripting 接口。 |
| -retainFiles | 在验证成功后保留 verify 目录中的所有文件（默认情况下，文件会被删除）。 |
| -verbose | 包含用于调试目的的其他详细信息。 |

## 审查和解决验证程序失败

如果验证程序成功完成，所有文件和 verify 目录都会被删除（除非您使用 retainFiles 选项）。所有验证失败产品的错误诊断保留在 verify 目录中。审查这些错误消息非常重要。

安装验证后，可以在 `install_dir/InstallDate/logs/.../tmp/` 目录中找到 verify 目录和结果。

以下建议可能帮助您纠正导致验证程序失败的常见安装错误：

1. 确保许可证文件已正确安装。如果许可证文件有问题，错误消息会被写入标准输出。
2. 确保您没有尝试执行未获得许可的 Abaqus 产品。
3. 确保操作系统和编译器级别与本版本在 Program Directory 中指定的级别一致。

如果您仍然无法解决问题，请联系您当地的办公室或代表寻求帮助。

---

[返回目录](./index.md) | [上一章：访问远程文件系统](./chapter-08.md)
