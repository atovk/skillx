# 理解 Claude Code Skills

深入了解 Claude Code Skills 的工作原理、能力边界和使用场景。

## 什么是 Skills？

**Skills** 是 Claude Code 的一个强大功能，允许你创建可重用的自定义命令和工具。可以把它想象成给 Claude 举办的"技能培训班" - 你教它特定的任务，它就能专业地完成这些任务。

### 类比理解

想象你在餐厅：

| 角色 | 类比 |
|------|------|
| **Claude** | 知识丰富的服务员，什么都懂一点 |
| **Skill** | 专业厨师，专门擅长某道菜 |
| **使用 Skill** | 点专业厨师做特色菜 |
| **普通对话** | 让服务员帮忙推荐菜品 |

### 核心概念

```yaml
Skill = 上下文 + 指令 + 工具

上下文：告诉 Claude "你现在是代码审查专家"
指令：告诉它 "按这个标准审查代码"
工具：给它代码审查需要的能力（Read、Grep）
```

## Skills vs 其他功能

### Skills vs 普通对话

| 特性 | 普通对话 | Skills |
|------|----------|--------|
| **重用性** | 每次重新解释 | 一次定义，多次使用 |
| **一致性** | 可能不一致 | 行为一致、可预测 |
| **专业性** | 通用知识 | 专业知识 |
| **可分享** | 难以分享 | 可以分享给他人 |

### Skills vs Scripts

| 特性 | Scripts | Skills |
|------|---------|--------|
| **语言** | Python/Shell 等 | 自然语言 |
| **灵活性** | 固定逻辑 | 理解意图 |
| **维护** | 需要编程 | 易于修改 |
| **能力** | 执行命令 | 推理和决策 |

### 何时使用 Skills

使用 Skills 当：

- ✅ 任务需要多次重复
- ✅ 任务有明确的工作流
- ✅ 需要分享给团队
- ✅ 需要推理和决策

使用普通对话当：

- ✅ 一次性查询
- ✅ 探索性任务
- ✅ 不需要重用

使用 Scripts 当：

- ✅ 需要精确控制
- ✅ 性能至关重要
- ✅ 简单的命令执行

## Skills 的工作原理

### 执行流程

```
1. 用户调用 Skill
   ↓
2. Claude 加载 SKILL.md
   ↓
3. 解析 Frontmatter (元数据)
   ↓
4. 读取内容指令
   ↓
5. 根据指令执行任务
   ↓
6. 返回结果给用户
```

### Frontmatter 的作用

Frontmatter 告诉 Claude：

```yaml
---
name: my-skill              # 我是谁
description: 我做什么       # 我能帮什么忙
allowed-tools:              # 我有什么工具
  - Read
  - Write
---
```

### 内容指令的作用

内容部分告诉 Claude：

- 具体要做什么
- 按什么步骤做
- 输出什么格式
- 如何处理错误

## Skills 的能力

### 强项

1. **理解意图**
   - 可以理解自然语言
   - 能从上下文推断
   - 可以处理模糊输入

2. **灵活输出**
   - 不是固定格式
   - 可以根据情况调整
   - 易于阅读和理解

3. **工具集成**
   - 可以使用各种工具
   - 组合多个工具
   - 错误处理

### 限制

1. **不确定性**
   - 输出可能不完全一致
   - 需要仔细测试

2. **性能**
   - 需要网络请求
   - 响应时间变化

3. **复杂度**
   - 非常复杂的任务适合脚本
   - 精确控制需要其他方案

## 使用场景

### 场景 1: 代码生成

**需求**: 经常生成类似的代码结构

**方案**: 创建 `api-generator` Skill

```yaml
---
name: api-generator
description: 生成 REST API 样板代码
allowed-tools:
  - Write
---
```

**结果**: 一致、快速的代码生成

### 场景 2: 文档维护

**需求**: 保持多个文档的格式一致

**方案**: 创建 `markdown-formatter` Skill

```yaml
---
name: markdown-formatter
description: 整理和格式化 Markdown 文件
allowed-tools:
  - Read
  - Write
---
```

**结果**: 统一的文档格式

### 场景 3: 代码审查

**需求**: 定期审查代码质量

**方案**: 创建 `code-reviewer` Skill

```yaml
---
name: code-reviewer
description: 审查代码并提供改进建议
allowed-tools:
  - Read
  - Grep
---
```

**结果**: 一致的代码质量标准

## Skills 的组成

### 必需元素

```yaml
# Frontmatter
---
name: skill-name              # 必需
description: 描述             # 必需
---

# 内容
指令内容                     # 必需
```

### 可选元素

```yaml
---
name: skill-name
description: 描述
allowed-tools:               # 可选
  - Read
  - Write
model: claude-sonnet-4       # 可选
user-invocable: true         # 可选（默认 true）
hooks:                       # 可选
  PreToolUse:
    - ...
---
```

## 最佳实践

### 1. 保持简洁

一个 Skill 只做一件事：

```yaml
# ❌ 不好：太多功能
---
name: do-everything
description: 处理所有事情
---

# ✅ 好：专注单一功能
---
name: git-commit-helper
description: 生成 Git 提交信息
---
```

### 2. 清晰的描述

描述应该清楚地说明功能：

```yaml
# ❌ 模糊
description: 一个处理代码的 skill

# ✅ 清晰
description: 分析代码质量并提供改进建议
```

### 3. 限制工具

只声明需要的工具：

```yaml
# ❌ 过于宽松
allowed-tools: []

# ✅ 只读安全
allowed-tools:
  - Read
  - Grep

# ✅ 明确需要
allowed-tools:
  - Read
  - Write
  - Bash
```

## 学习路径

### 入门

1. 理解基本概念（本文档）
2. 阅读快速入门
3. 完成初级练习

### 进阶

1. 学习结构剖析
2. 掌握最佳实践
3. 完成中级练习

### 高级

1. 学习高级模式
2. 创建复杂 Skills
3. 贡献给社区

## 常见问题

### Q: Skills 会记住我之前的对话吗？

**A**: Skills 不会自动记住之前的对话。每次调用都是独立的。如果需要上下文，可以使用文件存储信息。

### Q: 可以在 Skill 中调用另一个 Skill 吗？

**A**: 不能直接调用。但可以：

- 将共享逻辑放到脚本中
- 使用参考文档共享模式
- 创建一个"协调器" Skill

### Q: Skills 有大小限制吗？

**A**: 技术上没有硬限制，但建议：

- `SKILL.md` 控制在 500 行以内
- 使用渐进式披露处理复杂内容
- 避免超过一层嵌套引用

### Q: 如何调试 Skill？

**A**:

1. 先手动执行步骤
2. 使用 `allowed-tools` 限制
3. 添加临时调试输出
4. 查看完整输出理解思考过程

## 总结

理解 Skills 的关键点：

1. **定义**：可重用的自定义命令
2. **价值**：一致性、专业性、可分享
3. **组成**：Frontmatter + 内容
4. **场景**：重复任务、明确流程、团队协作
5. **限制**：不确定性、性能考虑

## 下一步

1. **深入学习**：[结构剖析](02-skill-anatomy.md)
2. **动手实践**：[创建第一个 Skill](tutorials/tutorial-01-first-skill.md)
3. **探索示例**：[示例 Skills](../skills/)

## 参考资源

- [Claude Code 官方文档](https://code.claude.com/docs/en/skills)
- [最佳实践](03-best-practices.md)
- [教程系列](tutorials/)
