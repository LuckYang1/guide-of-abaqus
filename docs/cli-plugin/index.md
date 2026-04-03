# Abaqus CLI 插件

<p align="center">
  <a href="https://github.com/LuckYang1/abaqus-cli">
    <img src="logo.svg" alt="abaqus-cli" width="200">
  </a>
</p>
<p align="center">
    <em>Abaqus 有限元分析 CLI 封装插件，专为 Claude Code 设计。AI Agent 可自主完成仿真工作流：作业提交、运行监控、后处理、子程序编译、格式翻译、联合仿真。</em>
</p>

<p align="center">
<a href="https://github.com/LuckYang1/abaqus-cli/">
<img src="https://img.shields.io/badge/version-1.0.0-blue.svg" alt="Plugin Version">
<a href="https://creativecommons.org/licenses/by/4.0/">
<img src="https://img.shields.io/badge/License-CC%20BY%204.0-green.svg" alt="License">
</p>

[Abaqus CLI](https://github.com/LuckYang1/abaqus-cli) 插件是为 AI Agent 设计的 Abaqus 有限元分析软件 CLI 封装，使 AI Agent 能自主完成仿真工作流。

## 功能特性

| 功能 | 说明 |
|------|------|
| 作业提交 | 提交分析、数据检查、继续、恢复等 |
| 作业监控 | 实时解析 .sta/.msg 文件状态 |
| 后处理 | 从 ODB 提取场/历史输出数据 |
| 子程序编译 | 编译 Fortran/C/C++ 用户子程序 |
| 文件翻译 | Nastran/ANSYS/Dyna 等格式互转 |
| 联合仿真 | CSE、FMU 支持 |

## 组成部分

### Slash 命令

- `/abaqus-run` — 作业提交
- `/abaqus-monitor` — 作业监控
- `/abaqus-post` — 后处理数据提取
- `/abaqus-compile` — 子程序编译
- `/abaqus-translate` — 文件格式翻译

### Agent

- **abaqus-job-manager** — 管理作业完整生命周期（datacheck → submit → monitor → post-process）
- **abaqus-post-processor** — 从 ODB 提取和分析结果数据

### Skill

- **job-workflow** — 从输入文件到结果的完整仿真工作流
- **subroutine-workflow** — 子程序编写、编译、调试的迭代开发流程
- **result-extraction** — ODB 数据提取与格式转换

## 版本支持

插件支持所有 Abaqus 版本，通过命令名切换：

| 写法 | 说明 |
|------|------|
| `abaqus` | 系统默认版本 |
| `abq2024` | Abaqus 2024 |
| `abq2025` | Abaqus 2025 |
| `abq20xx` | 任意版本 |

详见 [快速开始](quickstart.md) 和 [配置说明](configuration.md)。
