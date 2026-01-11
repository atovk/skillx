# 练习 3: 完善元数据

**难度**：⭐ 初级
**预计时间**：15 分钟

## 学习目标

完成这个练习后，你将：

- 理解 Skill 元数据的完整格式
- 知道如何编写高质量的 description
- 了解可选的元数据字段

## 前置知识

- 已完成练习 1 和 2
- 熟悉 Frontmatter 格式

## 任务描述

本练习提供了一个"不完整"的 Skill，你需要完善它的元数据。

### 不完整的 Skill

```markdown
---
name: todo-helper
description: 一个 todo skill
---

你是一个待办事项助手。
```

## 要求

### 1. 改进 description

原 description 太模糊，需要改进为：

**好的 description**：

- ✅ 清楚说明功能
- ✅ 描述使用场景
- ✅ 控制在 50-100 字符
- ✅ 使用现在时态

**示例**：

```yaml
description: 帮助管理待办事项列表，支持添加、完成和删除任务
```

### 2. 添加可选元数据

考虑是否需要添加以下字段：

```yaml
---
name: todo-helper
description: [改进后的描述]
allowed-tools:  # 如果需要工具
  - Read
  - Write
model: claude-sonnet-4-20250514  # 可选，指定模型
user-invocable: true  # 可选，默认 true
---
```

### 3. 完善内容

添加清晰的结构和使用说明：

```markdown
# 待办事项助手

## 功能
- [列出功能]

## 使用方法
[说明如何使用]

## 注意事项
[说明需要注意的地方]
```

## 提示

### 提示 1: Description 写作

```yaml
# 差的描述
description: 处理 todos

# 好的描述
description: 管理待办事项列表，支持添加、完成和删除任务

# 更好的描述（包含场景）
description: 管理项目待办事项，支持添加任务、标记完成和删除已完成的项目
```

### 提示 2: 是否需要 allowed-tools？

如果 Skill 需要：

- 读取文件 → 添加 `Read`
- 修改文件 → 添加 `Write`
- 运行命令 → 添加 `Bash`
- 搜索文件 → 添加 `Grep` 或 `Glob`

### 提示 3: 内容组织

```markdown
# [Skill 名称]

## 这个 Skill 做什么？

[简要说明]

## 如何使用

1. [步骤 1]
2. [步骤 2]
3. [步骤 3]

## 示例

[使用示例]
```

## 验收标准

完成练习后，检查：

- [ ] `name` 是有效的（小写、连字符）
- [ ] `description` 清楚且具体（50-100 字符）
- [ ] 如果需要工具，正确声明 `allowed-tools`
- [ ] 内容结构清晰
- [ ] 包含使用说明
- [ ] 包含至少一个示例

## 参考答案

完成练习后，可以查看 `solutions/beginner/exercise-03.md` 对比参考答案。

## 延伸挑战

1. 添加 `model` 字段指定不同的模型
2. 研究 hooks 并尝试添加一个 pre-hook
3. 创建一个完整的多文件 Skill（包含 README.md）

## 相关资源

- [Skill 结构剖析](../../docs/02-skill-anatomy.md)
- [元数据参考](../../docs/reference/skill-metadata-reference.md)
- [git-commit-helper 示例](../../skills/01-basics/git-commit-helper/)
