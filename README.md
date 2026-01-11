# SkillX - Claude Code Skills 学习资源库

> 帮助学习者快速上手 Claude Code Skills 能力的完整学习资源库

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code](https://img.shields.io/badge/Claude-Code-blue)](https://code.claude.com)

## 简介

SkillX 是一个系统性的 Claude Code Skills 学习资源库，提供从入门到精通的完整学习路径。无论你是完全的新手还是有经验的开发者，这里都有适合你的内容。

### 核心特性

- **循序渐进**：从基础概念到高级应用，适合不同水平学习者
- **实战导向**：每个技能都包含实际可运行的示例
- **最佳实践**：遵循官方规范和社区最佳实践
- **多样化覆盖**：通用工具、特定领域、教学示范三大方向

## 快速开始

### 前置要求

- 已安装 [Claude Code](https://code.claude.com)
- 基本的 Markdown 知识
- 了解基本的命令行操作

### 5 分钟上手

1. **克隆项目**

   ```bash
   git clone https://github.com/atovk/skillx.git
   cd skillx
   ```

2. **阅读快速入门**

   ```bash
   # 在 Claude Code 中
   open docs/00-getting-started.md
   ```

3. **运行第一个示例**

   ```bash
   # 在 Claude Code 中使用 hello-world skill
   ```

4. **完成第一个练习**

   ```bash
   # 查看 exercises/beginner/exercise-01-hello-skill.md
   ```

## 内容概览

### 文档指南

| 文档 | 描述 | 适合人群 |
|------|------|----------|
| [快速入门](docs/00-getting-started.md) | 5 分钟上手 Claude Code Skills | 所有学习者 |
| [理解 Skills](docs/01-understanding-skills.md) | 深入了解 Skills 工作原理 | 想要深入理解的学习者 |
| [结构剖析](docs/02-skill-anatomy.md) | Skill 文件结构和组织方式 | 所有开发者 |
| [最佳实践](docs/03-best-practices.md) | 编写高质量 Skills 的指南 | 所有开发者 |
| [高级模式](docs/04-advanced-patterns.md) | 协调器模式、反馈循环等 | 高级开发者 |

### 教程系列

1. [创建第一个 Skill](docs/tutorials/tutorial-01-first-skill.md) - 从零开始创建你的第一个 Skill
2. [渐进式披露](docs/tutorials/tutorial-02-progressive-disclosure.md) - 组织复杂内容
3. [工作流设计](docs/tutorials/tutorial-03-workflow-design.md) - 设计有效的工作流
4. [测试 Skills](docs/tutorials/tutorial-04-testing-skills.md) - 测试和验证
5. [发布与分享](docs/tutorials/tutorial-05-publishing.md) - 发布你的 Skills

### 示例 Skills

#### 基础技能

- `hello-world` - 最简单的 Skill 示例
- `code-explainer` - 代码解释器
- `git-commit-helper` - Git 提交助手

#### 文件操作

- `batch-renamer` - 批量重命名文件
- `file-analyzer` - 文件分析器
- `markdown-organizer` - Markdown 整理器

#### 代码生成

- `api-boilerplate` - API 样板代码生成器
- `test-generator` - 测试代码生成器
- `component-builder` - 组件构建器

#### 数据处理

- `csv-analyzer` - CSV 分析器
- `json-transformer` - JSON 转换器

#### Web 开发

- `nextjs-starter` - Next.js 项目启动器
- `react-component-creator` - React 组件创建器

#### 自动化

- `task-scheduler` - 任务调度器
- `log-analyzer` - 日志分析器

更多示例请查看 [skills/](skills/) 目录。

### 练习题

| 级别 | 练习数量 | 描述 |
|------|----------|------|
| [初级](exercises/beginner/) | 5 个 | 学习基本概念和创建简单 Skills |
| [中级](exercises/intermediate/) | 5 个 | 掌握工具限制、工作流设计 |
| [高级](exercises/advanced/) | 5 个 | 实现高级模式和集成外部工具 |

### 模板

- `basic-skill-template` - 基础 Skill 模板
- `advanced-skill-template` - 高级 Skill 模板
- `file-operations-template` - 文件操作模板
- `code-gen-template` - 代码生成模板

## 学习路径

### 入门阶段（1-2周）

**目标**：理解基本概念，创建简单 Skills

1. 阅读：[快速入门](docs/00-getting-started.md)
2. 教程：[创建第一个 Skill](docs/tutorials/tutorial-01-first-skill.md)
3. 练习：[初级练习 1-3](exercises/beginner/)
4. 示例：`hello-world`、`code-explainer`

**输出**：能够创建简单的单文件 Skill

### 基础阶段（2-3周）

**目标**：掌握核心模式，使用工具和模板

1. 阅读：[结构剖析](docs/02-skill-anatomy.md)、[最佳实践](docs/03-best-practices.md)
2. 教程：[渐进式披露](docs/tutorials/tutorial-02-progressive-disclosure.md)、[工作流设计](docs/tutorials/tutorial-03-workflow-design.md)
3. 练习：[初级练习 4-5](exercises/beginner/)、[中级练习 1-2](exercises/intermediate/)
4. 示例：`git-commit-helper`、`file-analyzer`

**输出**：能够创建多文件 Skill，使用模板和工具限制

### 进阶阶段（3-4周）

**目标**：实现复杂工作流，集成外部工具

1. 阅读：[高级模式](docs/04-advanced-patterns.md)
2. 教程：[测试 Skills](docs/tutorials/tutorial-04-testing-skills.md)、[发布与分享](docs/tutorials/tutorial-05-publishing.md)
3. 练习：[中级练习 3-5](exercises/intermediate/)、[高级练习 1-2](exercises/advanced/)
4. 示例：`csv-analyzer`、`nextjs-starter`

**输出**：能够创建复杂的 Skills，使用高级模式

### 精通阶段（4-6周）

**目标**：设计生产级 Skills，贡献社区

1. 阅读：所有参考文档
2. 练习：所有[高级练习](exercises/advanced/)
3. 示例：所有剩余示例
4. 实战：创建自己的 Skill 库

**输出**：能够设计和维护生产级 Skills

## 项目结构

```
skillx/
├── README.md              # 项目主页（本文件）
├── CLAUDE.md              # Claude Code 项目说明
├── docs/                  # 核心文档
├── skills/                # 示例 Skills
├── exercises/             # 练习题
├── templates/             # Skill 模板
└── resources/             # 资源文件
```

## 技术规范

### Skill 命名规范

- 使用小写字母、数字、连字符
- 动名词形式：`processing-pdfs`、`analyzing-data`
- 最大 64 字符
- 描述性强，避免模糊

### Skill 结构规范

```
skill-name/
├── SKILL.md              # 必需，主文件
├── README.md             # 可选，使用说明
├── examples.md           # 可选，示例集合
└── scripts/              # 可选，工具脚本
```

### 内容组织原则

- `SKILL.md` 控制在 500 行以内
- 使用渐进式披露（详细内容放单独文件）
- 避免超过一层嵌套引用
- 长文件添加目录

## 贡献指南

我们欢迎所有形式的贡献！

### 如何贡献

1. Fork 本项目
2. 创建你的特性分支 (`git checkout -b feature/amazing-skill`)
3. 提交你的修改 (`git commit -m 'Add amazing skill'`)
4. 推送到分支 (`git push origin feature/amazing-skill`)
5. 创建一个 Pull Request

### 贡献指南

请查看 [CONTRIBUTING.md](.github/CONTRIBUTING.md) 了解详细信息。

## 常见问题

**Q: 我需要什么编程背景？**
A: 基本的编程知识会有帮助，但不是必需的。我们从最基础的概念开始。

**Q: 需要 Claude Code Pro 订阅吗？**
A: 某些高级功能可能需要 Pro 订阅，但大部分内容可以在免费版本上学习。

**Q: 可以将我的 Skills 商业化吗？**
A: Skills 本身是开源的，但你可以基于学到的知识创建商业产品。

## 相关资源

- [Claude Code 官方文档](https://code.claude.com/docs)
- [Claude Skills 最佳实践](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- [awesome-claude-skills](https://github.com/VoltAgent/awesome-claude-skills)

## 许可证

本项目采用 [MIT License](LICENSE) 开源协议。

## 致谢

- 感谢 Anthropic 团队创建了 Claude Code
- 感谢社区贡献者的各种示例和最佳实践

---

开始你的 Claude Code Skills 之旅吧！有问题欢迎提 [Issue](https://github.com/atovk/skillx/issues)。
