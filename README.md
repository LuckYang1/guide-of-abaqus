# Abaqus 中文文档

[![Material for MkDocs](https://img.shields.io/badge/MkDocs-Material-blue.svg)](https://squidfunk.github.io/mkdocs-material/)
[![License](https://img.shields.io/badge/License-CC%20BY%204.0-green.svg)](https://creativecommons.org/licenses/by/4.0/)

Abaqus 软件官方用户指南中文版，基于 MkDocs + Material 主题构建。

## 🌐 在线访问

**直接访问 GitHub Pages**：https://LuckYang1.github.io/guide-of-abaqus/

支持简体中文和 English 双语言切换。

## 📖 文档内容

本项目包含 Abaqus 三大核心指南：

| 指南 | 章节数 | 语言 |
|------|--------|------|
| [执行指南](docs/execution/index.md) | 15 章 | 中文 / English |
| [GUI 工具包](docs/guitoolkit/index.md) | 14 章 | 中文 / English |
| [安装与许可](docs/install_lic/index.md) | 9 章 | 中文 / English |

## 🛠️ 本地运行

### 环境要求

- Python 3.8+
- pip

### 安装步骤

```bash
# 1. 克隆仓库
git clone https://github.com/LuckYang1/guide-of-abaqus.git
cd guide-of-abaqus

# 2. 安装依赖
pip install -r requirements.txt

# 3. 启动本地服务器
mkdocs serve -a localhost:8001
```

访问 [http://localhost:8001](http://localhost:8001) 查看文档。

### 构建静态站点

```bash
mkdocs build
```

构建产物在 `site/` 目录中。

## 🚀 部署到 GitHub Pages

本项目使用 GitHub Actions 自动部署。每次推送到 `master` 分支时会自动构建并发布。

### 手动部署

```bash
# 构建并推送到 gh-pages 分支
mkdocs gh-deploy
```

### 设置 GitHub Pages

1. 进入仓库 **Settings** → **Pages**
2. **Source** 选择 **GitHub Actions**
3. 保存即可

## 🎨 文档特性

- 🌙 **暗色/亮色模式** - 右上角切换按钮
- 🔍 **全文搜索** - 支持高亮和分享
- 🌐 **多语言支持** - 简体中文 / English
- 📋 **代码高亮** - 支持复制功能
- 🏷️ **标签系统** - 内容标签索引
- 📱 **响应式设计** - 适配各种屏幕尺寸
- ⬆️ **返回顶部** - 快速回到页面顶部

## 📂 项目结构

```
guide-of-abaqus/
├── docs/                    # 文档源文件
│   ├── index.md            # 首页
│   ├── community.md         # 社区页面
│   ├── glossary.md          # 术语表
│   ├── tags.md              # 标签索引
│   ├── execution/           # 执行指南章节
│   ├── guitoolkit/          # GUI 工具包章节
│   └── install_lic/         # 安装与许可章节
├── docs/en/                 # 英文文档
├── .github/workflows/       # GitHub Actions 配置
├── mkdocs.yml              # MkDocs 配置
└── requirements.txt        # Python 依赖
```

## ✍️ 翻译原则

- 所有正文内容翻译为中文
- 技术术语保留英文原名，确保与官方文档一致性
- 示例命令保留英文，添加中文注释说明
- 标题层级清晰，便于阅读和导航

## 🤝 参与贡献

欢迎参与文档改进！

1. Fork 本仓库
2. 创建分支 (`git checkout -b feature/improve-docs`)
3. 提交更改 (`git commit -m '改进文档'`)
4. 推送分支 (`git push origin feature/improve-docs`)
5. 创建 Pull Request

## 📄 许可证

本文档采用 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 许可证。

> Abaqus © Dassault Systèmes. 本文档为社区志愿者翻译整理，不隶属于 Dassault Systèmes 官方。

## 📬 联系方式

- GitHub Issues: [提交 Bug 或功能请求](https://github.com/LuckYang1/guide-of-abaqus/issues)

---

*最后更新：2026 年 4 月*
