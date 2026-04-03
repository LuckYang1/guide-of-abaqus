# 快速开始

## 前提条件

- 已安装 Abaqus 软件
- Abaqus 命令（`abaqus` 或 `abq20xx`）在系统 PATH 中
- Claude Code 已安装

## 安装

将插件目录复制到 Claude Code 的插件目录：

```
plugins/abaqus-cli/ → ~/.claude/plugins/abaqus-cli/
```

## 验证安装

在 Claude Code 中输入 `/abaqus-run --help`，如果看到帮助信息则安装成功。

## 基本使用

### 1. 提交分析作业

```
/abaqus-run model.inp cpus=8 memory=16gb
```

这将执行 `abaqus job=model cpus=8 memory=16gb`。

### 2. 监控作业状态

```
/abaqus-monitor model
```

查看 .sta 文件中的运行状态。

### 3. 提取结果数据

```
/abaqus-post extract model.odb --field S --step Step-1
```

从 ODB 中提取应力数据到 CSV 文件。

### 4. 编译用户子程序

```
/abaqus-compile UMAT.for
```

编译 Fortran 用户子程序。

### 5. 文件格式转换

```
/abaqus-translate fromNastran model.bdf
```

将 Nastran 文件转换为 Abaqus 格式。

## 使用 Agent

对于复杂工作流，可以让 AI Agent 自动管理：

- "帮我运行这个仿真，编译子程序、提交作业、监控进度、提取结果"
- "从这个 ODB 文件中提取所有分析步的应力和位移数据"

Agent 会自动调用相应的脚本完成工作流。

## 版本指定

如果系统中有多个 Abaqus 版本，在配置中指定：

```json
{
  "settings": {
    "abaqus_cmd": "abq2024"
  }
}
```

或在命令中通过 Agent 自动检测：`scripts/version_resolver.py --detect`。
