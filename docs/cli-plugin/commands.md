# Slash 命令参考

## /abaqus-run — 作业提交

提交 Abaqus 分析作业。

**基本用法：**

```
/abaqus-run <input_file> [参数...]
```

**参数：**

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `cpus` | CPU 核心数 | 4 |
| `gpus` | GPU 数量 | - |
| `memory` | 内存限制 | 8gb |
| `scratch` | 临时目录 | 系统默认 |
| `user` | 用户子程序文件 | - |
| `double` | 双精度计算 | - |

**模式：**

- 默认：完整分析
- `--datacheck`：仅数据检查
- `--continue`：继续中断的作业
- `--recover`：从重启动恢复

**示例：**

```
/abaqus-run beam.inp cpus=8 memory=16gb
/abaqus-run model.inp --datacheck user=umat.for
/abaqus-run model.inp --continue cpus=4
```

**作业控制：**

| 操作 | 命令 | 说明 |
|------|------|------|
| 暂停 | `/abaqus-suspend <job>` | 冻结状态，不丢失进度 |
| 恢复 | `/abaqus-resume <job>` | 从暂停点继续，无需 .res 文件 |
| 终止 | `/abaqus-run <job> --continue` | 需要 .res 重启动文件 |

---

## /abaqus-suspend — 暂停作业

暂停正在运行的 Abaqus 作业，保留内存状态，后续可用 `/abaqus-resume` 恢复。

**基本用法：**

```
/abaqus-suspend <job_name>
```

**示例：**

```
/abaqus-suspend model
```

---

## /abaqus-resume — 恢复作业

恢复被 `/abaqus-suspend` 暂停的 Abaqus 作业。

**基本用法：**

```
/abaqus-resume <job_name>
```

**示例：**

```
/abaqus-resume model
```

**注意：** 只能恢复被 suspend 暂停的作业。如果是 terminate 终止的，需使用 `/abaqus-run --continue`（需要 .res 文件）。

---

## /abaqus-monitor — 作业监控

监控 Abaqus 作业的运行状态。

**基本用法：**

```
/abaqus-monitor <job_name> [--watch] [--interval 秒数]
```

**参数：**

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `--watch` | 持续监控模式 | - |
| `--interval` | 刷新间隔（秒） | 10 |

**输出内容：**

- 作业状态（COMPLETED / RUNNING / SUSPENDED / TERMINATED / ABORTED）
- 迭代步数
- 警告/错误数量
- ODB 文件大小

**示例：**

```
/abaqus-monitor model
/abaqus-monitor model --watch --interval 30
/abaqus-monitor model1 model2 model3
```

---

## /abaqus-post — 后处理

从 ODB 文件中提取结果数据。

**基本用法：**

```
/abaqus-post <操作> <odb_file> [参数...]
```

**操作：**

| 操作 | 说明 |
|------|------|
| `report` | 生成 ODB 内容报告 |
| `extract` | 提取场输出到 CSV |
| `odb2sim` | 转换为 Simpack 格式 |
| `restartjoin` | 合并重启动文件 |

**extract 参数：**

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `--step` | 分析步名称 | Step-1 |
| `--frame` | 帧索引 | -1（最后一帧） |
| `--field` | 场变量名 | S |
| `--output` | 输出文件路径 | 自动生成 |

**示例：**

```
/abaqus-post report model.odb
/abaqus-post extract model.odb --field S --step Step-1
/abaqus-post extract model.odb --field U --step Load --output displacements.csv
/abaqus-post odb2sim model.odb
/abaqus-post restartjoin --output merged --input step1 --input step2
```

---

## /abaqus-compile — 子程序编译

编译 Abaqus 用户子程序。

**基本用法：**

```
/abaqus-compile <source_file> [--standard|--explicit|--cfd]
```

**参数：**

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `--standard` | Standard 求解器 | 默认 |
| `--explicit` | Explicit 求解器 | - |
| `--cfd` | CFD 求解器 | - |

**支持的子程序类型：**

UMAT, VUMAT, UEL, VUEL, UEXPAN, UHARD, USDFLD, UTRACLOAD, DLOAD, UVARM

**示例：**

```
/abaqus-compile UMAT.for
/abaqus-compile VUMAT.for --explicit
/abaqus-compile UEL.for --standard
```

---

## /abaqus-translate — 文件翻译

在 Abaqus 和其他求解器之间转换模型文件。

**基本用法：**

```
/abaqus-translate <command> <input_file>
```

**导出命令：**

| 命令 | 目标格式 |
|------|----------|
| `toNastran` | Nastran (.bdf) |

**导入命令：**

| 命令 | 源格式 |
|------|--------|
| `fromNastran` | Nastran |
| `fromANSYS` | ANSYS |
| `fromDyna` | LS-DYNA |
| `fromPamcrash` | PAM-CRASH |
| `fromRadioss` | RADIOSS |
| `fromMoldflow` | Moldflow |
| `fromSimpack` | Simpack |
| `fromAdams` | Adams |
| `fromExcite` | EXCITE |

**示例：**

```
/abaqus-translate toNastran model.inp
/abaqus-translate fromNastran nastran.bdf
/abaqus-translate fromDyna model.k
/abaqus-translate fromANSYS ansys.cdb
```
