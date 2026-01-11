# 练习 6: 实现渐进式披露

**难度**：⭐⭐ 中级
**预计时间**：30 分钟

## 学习目标

完成这个练习后，你将：

- 理解何时需要使用渐进式披露
- 掌握多文件 Skill 的组织方式
- 能够将复杂内容分离到独立文件

## 前置知识

- 完成初级练习 1-5
- 熟悉 Skill 的基本结构
- 了解 Frontmatter 格式

## 任务描述

我们将改进练习 4 中的 `code-review-helper` Skill，使用渐进式披露将复杂内容分离。

### 原始 Skill 问题

当前的 `code-review-helper` 可能包含：

- 工作流程说明
- 多种编程语言的检查规则
- 代码风格指南
- 最佳实践建议
- 常见陷阱

如果全部放在 `SKILL.md` 中，可能会超过 500 行，难以维护。

## 要求

### 1. 分析复杂度

首先评估现有内容：

```
如果 SKILL.md 超过 300 行
→ 考虑分离

如果某个主题超过 50 行
→ 放到独立文件

如果有大量代码示例
→ 放到 examples.md
```

### 2. 设计文件结构

创建这样的结构：

```
code-reviewer/
├── SKILL.md              # 主文件（< 300 行）
├── README.md             # 使用说明
├── reference.md          # 检查规则参考
├── patterns.md           # 常见模式
└── examples.md           # 审查示例
```

### 3. SKILL.md 应该包含

**必需内容**：

- 角色定位
- 主要工作流程
- 链接到详细文档
- 基本输出格式

**示例**：

```markdown
---
name: code-reviewer
description: 审查代码质量并提供改进建议
allowed-tools:
  - Read
  - Grep
---

# 代码审查器

你是代码审查专家，帮助提高代码质量。

## 工作流程

1. 读取代码文件
2. 分析代码质量
3. 生成审查报告

## 检查标准

详细的检查规则请查看 [reference.md](reference.md)

- 代码风格
- 错误处理
- 性能考虑
- 安全性

## 输出格式

详见 [examples.md](examples.md)

开始审查...
```

### 4. reference.md 应该包含

完整的检查标准：

```markdown
# 代码检查参考

## 代码风格

### 命名规范
[详细的命名规则]

### 格式规范
[详细的格式要求]

...

## 错误处理
[详细的错误处理标准]

## 性能
[详细的性能考虑]

## 安全
[详细的安全检查]
```

### 5. examples.md 应该包含

真实的审查示例：

```markdown
# 代码审查示例

## 示例 1: JavaScript 函数

### 输入代码
```javascript
function d(x,y){return x+y;}
```

### 审查结果

[详细的审查结果]

```

## 提示

### 提示 1: 识别需要分离的内容

**需要分离的内容**：
- ✅ 超过 50 行的详细说明
- ✅ 大量代码示例
- ✅ 框架特定的规则
- ✅ 参考信息

**保留在主文件**：
- ✅ 核心工作流程
- ✅ 基本使用说明
- ✅ 链接到详细文档

### 提示 2: 创建清晰的链接

```markdown
# ❌ 模糊的链接
更多信息请看这里

# ✅ 清晰的链接
详细的检查规则请查看 [reference.md](reference.md#javascript)

实际示例请查看 [examples.md](examples.md)
```

### 提示 3: 保持文件自包含

每个参考文件应该完整包含该主题的信息，不要再引用其他文件：

```markdown
# reference.md

## JavaScript 检查规则
[完整的规则，不引用其他文件]

## Python 检查规则
[完整的规则，不引用其他文件]
```

### 提示 4: 使用目录

对于较长的文件，添加目录：

```markdown
# 代码检查参考

## 目录

- [代码风格](#代码风格)
  - [命名规范](#命名规范)
  - [格式规范](#格式规范)
- [错误处理](#错误处理)
- [性能](#性能)
- [安全](#安全)
```

## 验收标准

完成练习后，检查：

- [ ] `SKILL.md` 在 300 行以内
- [ ] 主文件只包含核心流程
- [ ] 详细内容在独立文件中
- [ ] 链接清晰明确
- [ ] 参考文件自包含
- [ ] 文件组织合理

## 延伸挑战

1. **创建多个参考文件**

   ```
   reference/
   ├── style-guide.md
   ├── security-checklist.md
   └── performance-patterns.md
   ```

2. **添加交互式导航**
   根据用户选择动态加载相关参考文档

3. **创建框架特定的检查**
   为不同编程语言创建独立的检查规则文件

## 参考答案

完成练习后，可以查看 `solutions/intermediate/exercise-06.md` 对比参考答案。

## 相关资源

- [教程：渐进式披露](../../docs/tutorials/tutorial-02-progressive-disclosure.md)
- [最佳实践：简洁性](../../docs/03-best-practices.md#简洁性原则)
- [api-boilerplate 示例](../../skills/03-code-generation/api-boilerplate/)
