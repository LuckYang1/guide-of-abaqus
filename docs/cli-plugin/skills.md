# Skill 参考

## job-workflow — 完整仿真工作流

从输入文件到最终结果的端到端自动化流程。

### 适用场景

- 用户提供了 .inp 文件，需要完成从提交到获取结果的全流程
- 需要编译子程序后运行分析
- 多步分析（预加载 → 主分析）

### 流程步骤

```
环境检查 → 子程序编译（如有） → 数据检查 → 提交分析 → 监控进度 → 结果提取 → 报告汇总
```

| 步骤 | 工具 | 说明 |
|------|------|------|
| 环境检查 | `version_resolver.py` | 检测可用 Abaqus 版本 |
| 子程序编译 | `abaqus_runner.py make` | 编译用户子程序 |
| 数据检查 | `abaqus_runner.py datacheck` | 验证输入文件 |
| 提交分析 | `abaqus_runner.py job` | 后台提交分析 |
| 监控进度 | `job_monitor.py` | 持续检查 .sta/.msg |
| 结果提取 | `odb_extractor.py` | 提取场输出到 CSV |
| 报告汇总 | 人工分析 | 汇总运行时间、收敛、结果 |

---

## subroutine-workflow — 子程序开发

用户子程序的编写、编译、调试迭代流程。

### 适用场景

- 开发 UMAT/VUMAT/UEL 等用户子程序
- 子程序编译失败需要调试
- 验证子程序在 datacheck 中的行为

### 流程步骤

```
编译子程序 → 检查编译结果 → datacheck 验证 → 测试分析 → 迭代调试
```

| 步骤 | 工具 | 说明 |
|------|------|------|
| 编译 | `abaqus_runner.py make` | 调用 abaqus make |
| 错误分析 | 人工分析 | 解析编译器输出 |
| datacheck | `abaqus_runner.py datacheck` | 验证子程序逻辑 |
| 调试 | 人工分析 | 结合 .msg 定位问题 |

### 常见子程序类型

| 子程序 | 用途 | 关键接口 |
|--------|------|----------|
| UMAT | 用户材料（Standard） | stress, statev, ddsdde |
| VUMAT | 用户材料（Explicit） | stress, stateNew |
| UEL | 用户单元 | rhs, amatrx |
| USDFLD | 场变量依赖 | field, statev |

---

## result-extraction — ODB 数据提取

从输出数据库中提取和分析结果数据。

### 适用场景

- 分析完成后提取应力、位移等场数据
- 将结果导出为 CSV 进行进一步处理
- 生成 ODB 内容报告

### 流程步骤

```
了解 ODB 结构 → 确定提取需求 → 执行提取 → 数据验证 → 后续处理
```

| 步骤 | 工具 | 说明 |
|------|------|------|
| ODB 结构 | `odb_extractor.py report` | 列出分析步、帧、场变量 |
| 提取 | `odb_extractor.py extract` | 提取指定场变量到 CSV |
| 转换 | `odb_extractor.py odb2sim` | ODB 转 Simpack |
| 合并 | `odb_extractor.py restartjoin` | 合并重启动文件 |
