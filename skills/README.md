# Skills 示例目录

这个目录包含各种 Claude Code Skills 示例，按类别和难度组织。

## 目录结构

```
skills/
├── 01-basics/              # 基础技能（入门必学）
├── 02-file-operations/     # 文件操作（初级）
├── 03-code-generation/     # 代码生成（初级）
├── 04-data-processing/     # 数据处理（中级）
├── 05-web-development/     # Web 开发（中级）
└── 06-automation/          # 自动化（高级）
```

## 学习路径

### 第一步：基础技能（01-basics）

从这些简单的示例开始：

1. **[hello-world](01-basics/hello-world/)** - 最简单的示例
   - 学习基本结构
   - 理解 Frontmatter

2. **[code-explainer](01-basics/code-explainer/)** - 代码解释器
   - 学习如何组织输出
   - 使用工具限制

3. **[git-commit-helper](01-basics/git-commit-helper/)** - Git 提交助手
   - 学习工作流设计
   - 使用 Bash 工具

### 第二步：文件操作（02-file-operations）

学习如何操作文件系统：

- **batch-renamer** - 批量重命名文件
- **file-analyzer** - 分析文件内容
- **markdown-organizer** - 整理 Markdown 文件

### 第三步：代码生成（03-code-generation）

学习如何生成代码：

- **api-boilerplate** - 生成 API 样板代码
- **test-generator** - 生成测试代码
- **component-builder** - 生成 UI 组件

### 第四步：数据处理（04-data-processing）

学习如何处理数据：

- **csv-analyzer** - 分析 CSV 数据
- **json-transformer** - 转换 JSON 数据

### 第五步：Web 开发（05-web-development）

学习 Web 开发相关的 Skills：

- **nextjs-starter** - Next.js 项目启动器
- **react-component-creator** - React 组件创建器

### 第六步：自动化（06-automation）

学习自动化任务：

- **task-scheduler** - 任务调度
- **log-analyzer** - 日志分析

## 如何使用这些示例

### 1. 阅读代码

```bash
cd skills/01-basics/hello-world
cat SKILL.md
```

### 2. 在 Claude Code 中测试

```bash
# 在 Claude Code 中
hello-world
```

### 3. 修改和实验

```bash
# 复制示例到你的项目
cp -r skills/01-basics/hello-world my-skills/
cd my-skills/hello-world

# 修改 SKILL.md
# 然后在 Claude Code 中测试
```

## Skill 目录结构

每个 Skill 示例包含：

```
skill-name/
├── SKILL.md          # 主文件（必需）
├── README.md         # 使用说明（可选）
├── examples.md       # 使用示例（可选）
└── scripts/          # 辅助脚本（可选）
```

## 按难度查找

| 难度 | 类别 | 学习时间 |
|------|------|----------|
| 入门 | 01-basics | 1-2 周 |
| 初级 | 02-file-operations, 03-code-generation | 2-3 周 |
| 中级 | 04-data-processing, 05-web-development | 3-4 周 |
| 高级 | 06-automation | 4+ 周 |

## 贡献新的示例

如果你想贡献新的 Skill 示例：

1. 选择合适的类别目录
2. 遵循现有的目录结构
3. 包含清晰的文档和示例
4. 确保代码可以运行

查看 [贡献指南](../../.github/CONTRIBUTING.md) 了解更多信息。

## 相关资源

- [快速入门指南](../docs/00-getting-started.md)
- [最佳实践](../docs/03-best-practices.md)
- [练习题](../exercises/)
