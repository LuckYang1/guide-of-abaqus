# 第十章：自定义现有模块或工具集

## 本章概述

前面的章节描述了如何创建新的模块或工具集。或者，Abaqus GUI Toolkit 允许您从现有模块或工具集派生新模块或工具集，并从中添加或删除功能。

## 本章内容

- [修改和访问 Abaqus/CAE GUI 模块和工具集](#修改和访问-abaqus-cae-gui-模块和工具集)
- [File 工具集](#file-工具集)
- [Tree 工具集](#tree-工具集)
- [Selection 工具集](#selection-工具集)
- [Help 工具集](#help-工具集)
- [自定义工具集示例](#自定义工具集示例)

---

## 修改和访问 Abaqus/CAE GUI 模块和工具集

Abaqus GUI Toolkit 允许您对 Abaqus/CAE GUI 模块和工具集进行有限的更改。

### 可进行的修改

- 添加新的菜单项或菜单
- 移除现有的菜单项或菜单
- 修改菜单项的行为

### 访问现有组件

您可以访问现有的 Abaqus/CAE 模块和工具集来修改它们。

---

## File 工具集

File 工具集提供文件操作菜单。

---

## Tree 工具集

Tree 工具集管理模型树。

### 树选项卡

树工具集提供多个选项卡，每个选项卡显示不同类型的数据。

---

## Selection 工具集

Selection 工具集管理对象选择行为。

### 选择模式

- **_single select（单选）**：用户只能选择一个对象。
- **browse select（浏览选择）**：始终有一个对象被选中。
- **multi-select（多选）**：用户可以选择多个对象。

---

## Help 工具集

Help 工具集提供帮助功能。

---

## 自定义工具集示例

```python
class MyCustomToolset(AFXToolsetGui):
    def __init__(self):
        AFXToolsetGui.__init__(self, 'CustomToolset')
        # Add custom functionality
```
