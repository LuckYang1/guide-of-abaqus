# 第七章：安装子目录

SIMULIA 产品安装到同一目录中。

将创建以下子目录：

| 子目录 | 内容描述 |
|--------|----------|
| `install_dir/os/CAEresources/` | 配置文件 |
| `install_dir/os/code/bin/` | SIMULIA 产品可执行文件、第三方可执行文件和库 |
| `install_dir/os/code/command/` | SIMULIA 产品命令过程 |
| `install_dir/os/code/include/` | 用于使用 abaqus make 实用程序构建后处理程序的头文件链接 |
| `install_dir/os/SMA/samples/` | 与已安装产品关联的输入文件和目录，包括安装验证问题、时间测试问题、Introduction to Abaqus 研讨会文件、Getting Started 教程指南文件、应用程序简要说明文件、与 abaqus findkeyword 实用程序一起使用的文件，以及来自 Example Problems、Benchmarks 和 Verification Guides 的文件 |
| `install_dir/os/SMA/site/` | 站点特定文件：Abaqus 环境文件 (`abaqus_v6.env` 和 `custom_v6.env`)、示例环境文件 (`abaqusinc.env`)、包含文件 (`file_name.inc`)、包含用于验证过程的信息的数据文件 (`chksum.dat`) 和平台计算机表 |
| `install_dir/os/tools/SMApy` | Python 解释器 |
| `install_dir/os/code/python2.7/lib/` | Abaqus Python 模块 |

---

[返回目录](./index.md) | [上一章：自定义 Abaqus/CAE 和 Abaqus/Viewer](./chapter-06.md) | [下一章：访问远程文件系统](./chapter-08.md)
