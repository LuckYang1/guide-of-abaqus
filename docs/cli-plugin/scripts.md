# 脚本 API 参考

插件包含 4 个 Python 脚本，位于 `plugins/abaqus-cli/scripts/` 目录下。

---

## version_resolver.py — 版本解析

将版本字符串解析为实际的 Abaqus 命令名。

### 命令行接口

```bash
python version_resolver.py --resolve <version>
python version_resolver.py --validate <command>
python version_resolver.py --detect
python version_resolver.py --info [command]
```

### 函数

#### `resolve_command(version_str) -> str`

将版本字符串解析为命令名。

```python
resolve_command("2024")    # "abq2024"
resolve_command("abq2025") # "abq2025"
resolve_command("abaqus")  # "abaqus"
```

#### `validate_command(cmd) -> bool`

检查命令是否在 PATH 中可用。

#### `auto_detect() -> str`

自动检测系统中可用的 Abaqus 命令。按版本从新到旧依次尝试。

#### `get_version_info(cmd) -> str`

执行 `abaqus information=version` 获取版本信息。

---

## abaqus_runner.py — 命令构建与执行

基于 COMMAND_REGISTRY 的统一命令封装。

### 命令行接口

```bash
python abaqus_runner.py <subcommand> [key=value...] [--abaqus-cmd CMD] [--dry-run] [--list]
```

### 支持的子命令

| 子命令 | 类别 | 说明 |
|--------|------|------|
| job | 作业 | 提交分析作业 |
| datacheck | 作业 | 数据检查 |
| continue | 作业 | 继续中断作业 |
| convert | 作业 | 转换重启动格式 |
| recover | 作业 | 恢复重启动 |
| syntaxcheck | 作业 | 语法检查 |
| suspend | 控制 | 暂停作业 |
| resume | 控制 | 恢复作业 |
| terminate | 控制 | 终止作业 |
| make | 编译 | 编译用户子程序 |
| toNastran | 翻译 | 导出 Nastran |
| fromNastran | 翻译 | 导入 Nastran |
| fromANSYS | 翻译 | 导入 ANSYS |
| fromDyna | 翻译 | 导入 LS-DYNA |
| odbreport | 数据库 | ODB 报告 |
| odb2sim | 数据库 | ODB 转 Simpack |
| restartjoin | 数据库 | 合并重启动 |
| cse | 联合仿真 | CSE 引擎 |
| cosimulation | 联合仿真 | 运行联合仿真 |
| fmu | 联合仿真 | 导出 FMU |
| encrypt | 加密 | 加密 Python |
| decrypt | 加密 | 解密 Python |
| optimization | 优化 | 运行优化 |

### 函数

#### `parse_kv_args(args_list) -> dict`

解析 `key=value` 参数列表。

#### `build_command(subcommand, params, abaqus_cmd) -> list`

根据子命令和参数构建完整命令行。自动验证必需参数，过滤未知参数。

#### `execute_command(cmd, timeout, background) -> CompletedProcess`

执行构建好的命令。支持超时和后台模式。

---

## job_monitor.py — 作业监控

解析 .sta / .msg 文件获取作业运行状态。

### 命令行接口

```bash
python job_monitor.py <job_name>... [--dir DIR] [--watch] [--interval SEC]
```

### 数据类

#### `JobStatus`

| 字段 | 类型 | 说明 |
|------|------|------|
| job_name | str | 作业名称 |
| status | str | COMPLETED/TERMINATED/RUNNING/ABORTED/UNKNOWN |
| iterations | int | 增量步数 |
| errors | int | 错误数 |
| warnings | int | 警告数 |
| odb_file | str | ODB 文件路径 |

#### `MsgInfo`

| 字段 | 类型 | 说明 |
|------|------|------|
| error_lines | list[str] | 错误行列表 |
| warning_lines | list[str] | 警告行列表 |

### 函数

#### `parse_sta_file(sta_path) -> JobStatus`

解析 .sta 文件，通过正则匹配 COMPLETED / TERMINATED / RUNNING / ABORTED 标记。

#### `parse_msg_file(msg_path) -> MsgInfo`

解析 .msg 文件，提取所有 ERROR: 和 WARNING: 行。

#### `find_job_files(job_name, search_dir) -> dict`

查找作业相关的 .sta / .msg / .inp / .odb / .dat / .log 文件。

#### `monitor_jobs(job_names, search_dir, watch, interval) -> list[JobStatus]`

监控一个或多个作业。支持 `--watch` 持续轮询模式。

---

## odb_extractor.py — ODB 数据提取

从 ODB 文件中提取场输出数据。

### 命令行接口

```bash
python odb_extractor.py report <odb> [--output FILE]
python odb_extractor.py extract <odb> [--step STEP] [--frame N] [--field VAR] [--output FILE]
python odb_extractor.py odb2sim <odb> [--output FILE]
python odb_extractor.py restartjoin --output NAME --input F1 --input F2...
```

### 函数

#### `run_odbreport(odb_path, output, abaqus_cmd) -> CompletedProcess`

调用 `abaqus odbreport` 生成 ODB 内容报告。

#### `extract_field_output(odb_path, step_name, frame_index, field_name, output_file, abaqus_cmd) -> str`

生成 Abaqus Python 提取脚本并执行，将场输出数据写入 CSV。

#### `run_odb2sim(odb_path, output, abaqus_cmd) -> CompletedProcess`

将 ODB 转换为 Simpack 格式。

#### `run_restartjoin(output, input_files, abaqus_cmd) -> CompletedProcess`

合并多个重启动文件。
