# 快速入门指南

欢迎来到 SkillX！这个指南将帮助你在 5 分钟内了解 Claude Code Skills 并创建你的第一个 Skill。

## 什么是 Claude Code Skills?

**Skills** 是 Claude Code 的一个强大功能，它允许你创建可重用的自定义命令和工具。可以把 Skills 想象成：

- **自定义命令**：创建你自己的快捷指令
- **专业助手**：针对特定任务优化的 AI 助手
- **工作流自动化**：将复杂任务自动化

### 一个简单的例子

假设你经常需要分析 Git 提交并生成规范的提交信息。你可以创建一个 `git-commit-helper` Skill，每次只需要运行它，就能自动分析代码变更并生成规范的提交信息。

## 安装 Claude Code

### 前置要求

- macOS 或 Linux 系统
- Node.js 18+ (如果需要使用 MCP 工具)

### 安装步骤

1. **安装 Claude Code**

   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

2. **初始化 Claude Code**

   ```bash
   claude init
   ```

3. **登录你的账号**

   ```bash
   claude login
   ```

### 验证安装

```bash
claude --version
```

如果显示版本号，说明安装成功！

## 理解 Skill 的基本结构

一个 Skill 就是一个 Markdown 文件，包含两个部分：

### 1. Frontmatter（元数据）

文件顶部的 YAML 格式元数据：

```yaml
---
name: my-first-skill
description: 这是我的第一个 Skill
---
```

### 2. 内容（指令）

告诉 Claude 如何工作的指令：

```markdown
你是代码分析专家。当用户运行这个 Skill 时：
1. 询问用户要分析哪个文件
2. 读取并分析文件内容
3. 提供代码质量建议
```

## 创建你的第一个 Skill

让我们创建一个简单的 "Hello World" Skill！

### 步骤 1：创建 Skill 文件

创建文件 `my-first-skill.md`：

```markdown
---
name: my-first-skill
description: 我的第一个 Claude Code Skill
---

# 你好，世界！

你是一个友好的助手。当用户运行这个 Skill 时：
1. 向用户问好
2. 询问用户今天想做什么
3. 根据用户的回答提供帮助
```

### 步骤 2：使用 Skill

在 Claude Code 中使用你的 Skill：

```bash
# 在 Claude Code 对话中
my-first-skill
```

或者直接作为 slash 命令：

```bash
/my-first-skill
```

### 步骤 3：测试

你应该会看到 Claude 向你问好，然后询问你想做什么！

## Skill 的核心概念

### 1. Name（名称）

- 使用小写字母、数字、连字符
- 描述性强，容易记忆
- 例如：`git-commit-helper`、`code-explainer`

### 2. Description（描述）

- 清楚说明 Skill 的功能
- 最多 1024 个字符
- 好的描述示例：

  ```yaml
  description: 分析 Git diff 并生成符合规范的提交信息
  ```

  不好的描述示例：

  ```yaml
  description: 一个 Git skill
  ```

### 3. Content（内容）

- 使用 Markdown 编写
- 告诉 Claude 具体要做什么
- 可以包含：
  - 步骤说明
  - 代码示例
  - 输出格式要求
  - 错误处理

### 4. Allowed Tools（可选）

限制 Skill 可以使用的工具：

```yaml
---
name: file-reader
description: 只读文件，不修改任何内容
allowed-tools:
  - Read
  - Grep
---
```

## 实用示例

### 示例 1：代码解释器

```markdown
---
name: code-explainer
description: 用简单的语言解释代码的工作原理
---

你是代码解释专家。当用户提供代码时：

1. **整体功能**：用一句话说明代码做什么
2. **逐步分析**：分解每个重要部分
3. **类比说明**：使用日常生活中的类比
4. **潜在改进**：指出可以改进的地方

保持解释简单易懂，适合初学者理解。
```

### 示例 2：文件整理器

```markdown
---
name: markdown-organizer
description: 整理和格式化 Markdown 文件
allowed-tools:
  - Read
  - Write
---

你是 Markdown 整理专家。当用户提供文件路径时：

1. 读取文件内容
2. 检查并修复：
   - 标题层级（使用 # ## ###）
   - 列表格式
   - 代码块语法
   - 空行和间距
3. 询问用户是否应用修改
4. 如果用户同意，写入修改后的内容

保持原有的语义，只改进格式。
```

## 最佳实践

### 1. 保持简洁

- 一个 Skill 只做一件事
- 如果功能复杂，拆分成多个 Skills
- 使用渐进式披露（下面会讲到）

### 2. 使用渐进式披露

对于复杂的内容，将详细信息放到单独的文件：

```markdown
---
name: complex-task
description: 执行复杂任务
---

# 复杂任务

基本步骤在下面说明。

详细参考信息请查看：[reference.md](reference.md)

## 使用示例

查看 [examples.md](examples.md) 了解更多示例。
```

### 3. 测试你的 Skill

创建后，多测试几次：

- 不同输入会怎样？
- 出错时如何处理？
- 输出格式是否一致？

### 4. 编写好的描述

好的描述帮助用户（和 Claude）理解 Skill 的用途：

```yaml
# 好的描述
description: 分析 Python 代码的性能瓶颈，提供优化建议

# 不好的描述
description: 分析代码
```

## 常见问题

### Q: Skill 和普通对话有什么区别？

**A**: Skills 是可重用的、标准化的命令。它们：

- 可以作为 slash 命令使用
- 有明确的功能边界
- 可以分享给他人使用
- 行为一致，可预测

### Q: 一个 Skill 应该多复杂？

**A**: 尽量保持简单。一个 Skill 应该只做一件事并做好。如果功能变复杂，考虑：

- 拆分成多个 Skills
- 使用脚本辅助（`scripts/` 目录）
- 将详细内容移到参考文档

### Q: 如何调试 Skill？

**A**:

1. 先手动执行 Skill 中的步骤
2. 使用 `allowed-tools` 限制避免意外操作
3. 添加详细的错误处理说明
4. 查看 Claude 的输出，理解它的思考过程

### Q: Skills 可以调用其他 Skills 吗？

**A**: 不直接支持。但你可以：

- 将共享逻辑放到脚本中
- 使用参考文档共享模式
- 创建一个"协调器" Skill 调用多个脚本

## 下一步

现在你已经创建了第一个 Skill，接下来可以：

1. **完成第一个练习**
   - 查看 `exercises/beginner/exercise-01-hello-skill.md`
   - 动手实践创建 Skill

2. **学习更多概念**
   - 阅读 [理解 Skills](01-understanding-skills.md)
   - 了解 [Skill 结构剖析](02-skill-anatomy.md)

3. **探索示例**
   - 查看 `skills/01-basics/` 目录
   - 运行并修改示例 Skills

4. **学习最佳实践**
   - 阅读 [最佳实践指南](03-best-practices.md)
   - 了解如何编写高质量的 Skills

## 获取帮助

如果遇到问题：

- 查看 [常见问题](../README.md#常见问题)
- 提交 [Issue](https://github.com/atovk/skillx/issues)
- 阅读官方文档：[Claude Code Skills](https://code.claude.com/docs/en/skills)

---

开始探索 Claude Code Skills 的世界吧！记住：最好的学习方式就是动手实践。
