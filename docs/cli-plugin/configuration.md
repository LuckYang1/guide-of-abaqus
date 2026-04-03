# 配置说明

## plugin.json 配置

插件配置文件位于 `plugins/abaqus-cli/.claude-plugin/plugin.json`。

### 完整配置示例

```json
{
  "name": "abaqus-cli",
  "version": "1.0.0",
  "description": "Abaqus FEA CLI 封装插件",
  "settings": {
    "abaqus_cmd": {
      "type": "string",
      "default": "abaqus",
      "description": "Abaqus 可执行命令名"
    },
    "default_cpus": {
      "type": "integer",
      "default": 4,
      "description": "默认 CPU 核心数"
    },
    "default_scratch": {
      "type": "string",
      "default": "",
      "description": "默认临时目录路径"
    },
    "default_memory": {
      "type": "string",
      "default": "8gb",
      "description": "默认内存限制"
    }
  }
}
```

### 配置项说明

| 配置项 | 类型 | 默认值 | 说明 |
|--------|------|--------|------|
| `abaqus_cmd` | string | `abaqus` | Abaqus 命令名，支持 `abaqus`、`abq2024`、`abq20xx` |
| `default_cpus` | integer | 4 | 默认 CPU 核心数 |
| `default_scratch` | string | `""` | 默认临时目录，留空使用系统默认 |
| `default_memory` | string | `8gb` | 默认内存限制 |

## 版本配置

### 自动检测

插件会自动检测系统中可用的 Abaqus 命令。使用 `scripts/version_resolver.py --detect` 查看。

### 手动指定

在 `plugin.json` 中修改 `abaqus_cmd`：

```json
{
  "settings": {
    "abaqus_cmd": {
      "default": "abq2024"
    }
  }
}
```

### 版本命名规则

| 配置值 | 等效命令 |
|--------|----------|
| `abaqus` | 系统默认 Abaqus |
| `abq2024` | Abaqus 2024 |
| `abq2025` | Abaqus 2025 |
| `abq20xx` | Abaqus 20xx |

## 运行时配置

### CPU 和内存

在命令中直接指定：

```
/abaqus-run model.inp cpus=16 memory=32gb
```

### 临时目录

指定工作目录：

```
/abaqus-run model.inp scratch=/tmp/abaqus_work
```

### 用户子程序

指定子程序文件：

```
/abaqus-run model.inp user=UMAT.for
```

## 环境变量

插件脚本依赖以下环境变量：

| 变量 | 说明 | 必需 |
|------|------|------|
| `PATH` | 需包含 Abaqus 命令目录 | 是 |
| `ABAQUS_BAT_PATH` | Windows 上的 abaqus.bat 路径 | 否 |
| `LM_LICENSE_FILE` | Abaqus 许可证服务器 | 是 |
| `INTEL_LICENSE_FILE` | Intel Fortran 许可证（如有） | 编译子程序时需要 |

## Fortran 编译器配置

编译用户子程序需要 Fortran 编译器：

### 支持的编译器

| 编译器 | Abaqus 版本 | 说明 |
|--------|-------------|------|
| Intel Fortran (ifort) | 所有版本 | 推荐 |
| gfortran | 较新版本 | 开源替代 |

### 配置步骤

1. 安装 Fortran 编译器
2. 将编译器路径添加到系统 PATH
3. 验证：`ifort --version` 或 `gfortran --version`
4. 编译测试：`/abaqus-compile test_subroutine.for`

## 路径配置

### 脚本路径

插件脚本位于插件目录的 `scripts/` 子目录下。Agent 和 Skill 通过相对路径引用这些脚本。

### 工作目录

默认在当前工作目录下查找 .inp、.sta、.msg、.odb 等文件。可通过 `--dir` 参数指定其他目录。
