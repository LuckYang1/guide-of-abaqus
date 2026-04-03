# Agent 参考

## abaqus-job-manager — 作业生命周期管理

管理 Abaqus 仿真作业的完整生命周期。

### 功能

- 自动执行 datacheck → submit → monitor → post-process 流程
- 解析 .sta/.msg 文件检测错误和警告
- 根据分析结果状态做出智能决策

### 触发场景

当用户要求：
- "帮我运行这个仿真"
- "提交这个作业并监控进度"
- "检查分析是否完成"

### 工作流程

1. **预检**：运行 datacheck 验证输入文件
2. **提交**：提交分析作业（后台模式）
3. **监控**：持续检查 .sta/.msg 文件状态
4. **报告**：汇总结果（状态、错误、警告、ODB 大小）

### 决策逻辑

| 状态 | 动作 |
|------|------|
| datacheck 失败 | 停止，报告 .dat 中的错误 |
| TERMINATED | 报告 .msg 中的 ERROR 根本原因 |
| COMPLETED | 检查 WARNING 数量，提取关键结果 |
| ABORTED | 分析 .msg 定位中断原因 |

---

## abaqus-post-processor — 结果提取

从 ODB 文件中提取和分析结果数据。

### 功能

- 提取场输出数据（应力、位移、应变等）
- 生成 ODB 内容报告
- 数据格式转换（CSV、Simpack）
- 合并重启动文件

### 触发场景

当用户要求：
- "从 ODB 里提取应力数据"
- "生成分析结果报告"
- "把结果导出为 CSV"

### 场输出变量

| 变量名 | 说明 | 维度 |
|--------|------|------|
| S | 应力 | 6（对称张量） |
| U | 位移 | 3 |
| E | 应变 | 6 |
| RF | 反力 | 3 |
| CF | 集中力 | 3 |
| PE | 塑性应变 | 6 |
| TEMP | 温度 | 1 |

### 输出格式

CSV 格式：

```csv
node_or_element, label, value_1, value_2, value_3
ASSEMBLY, 1, 1.23e6, -4.56e5, 0.0
ASSEMBLY, 2, 9.87e5, -2.34e5, 0.0
```
