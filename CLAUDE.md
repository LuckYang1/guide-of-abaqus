# CLAUDE.md — guide-of-abaqus

## 项目概述

Abaqus 有限元分析软件中文用户指南文档，基于 MkDocs + Material 主题构建。

## 目录结构

```
├── docs/                    # MkDocs 文档源文件
│   ├── index.md             # 首页
│   ├── install_lic/         # 安装与许可（9 章）
│   ├── execution/           # 执行指南（15 章）
│   ├── guitoolkit/          # GUI 工具包（14 章）
│   ├── cli-plugin/          # CLI 插件文档（7 页）
│   ├── en/                  # 英文镜像
│   └── community.md         # 社区页
├── plugins/                 # Claude Code 插件
│   └── abaqus-cli/          # Abaqus CLI 封装插件
│       ├── .claude-plugin/plugin.json
│       ├── commands/        # Slash 命令（5 个）
│       ├── agents/          # Agent 定义（2 个）
│       ├── skills/          # Skill 定义（3 个）
│       └── scripts/         # Python 脚本（4 个）
├── mkdocs.yml               # MkDocs 配置
├── requirements.txt         # Python 依赖
└── CLAUDE.md                # 本文件
```

## 技术栈

- **文档生成**: MkDocs + mkdocs-material
- **国际化**: mkdocs-static-i18n (zh/en)
- **版本管理**: mike
- **CI/CD**: GitHub Actions → GitHub Pages
- **插件脚本**: Python 3

## 常用命令

```bash
# 本地预览文档
mkdocs serve

# 构建文档
mkdocs build

# 验证 Python 脚本语法
python -m py_compile plugins/abaqus-cli/scripts/version_resolver.py
python -m py_compile plugins/abaqus-cli/scripts/abaqus_runner.py
python -m py_compile plugins/abaqus-cli/scripts/job_monitor.py
python -m py_compile plugins/abaqus-cli/scripts/odb_extractor.py
```

## 开发规范

- 文档使用简体中文，英文版放在 `docs/en/` 目录
- 导航结构在 `mkdocs.yml` 的 `nav` 字段中维护
- CLI 插件使用 kebab-case 命名
- Python 脚本使用 argparse 提供 CLI 接口
- 插件路径引用使用 `$CLAUDE_PLUGIN_ROOT` 环境变量
