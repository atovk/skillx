# 基础 Skill 模板

这是一个简单的 Skill 模板，适合初学者快速开始。

## 使用方法

### 1. 复制模板

```bash
# 复制到你的项目
cp -r templates/basic-skill-template my-skill
cd my-skill
```

### 2. 重命名文件

```bash
mv SKILL.md.template SKILL.md
```

### 3. 编辑内容

打开 `SKILL.md`，修改以下部分：

- `name`: 你的 Skill 名称
- `description`: 功能描述
- `allowed-tools`: 需要的工具
- 内容部分：具体指令

### 4. 测试

在 Claude Code 中测试你的 Skill：
```
your-skill-name
```

## 模板结构

```
basic-skill-template/
├── SKILL.md.template    # 主文件模板
└── README.md            # 本文件
```

## 自定义指南

### Frontmatter

```yaml
---
name: your-skill-name              # 修改为你的技能名
description: 你的描述              # 修改为你的描述
allowed-tools:                     # 根据需要调整
  - Read
  - Write
---
```

### 内容结构

1. **标题和角色**
   - 说明你是谁
   - 你能做什么

2. **工作流程**
   - 列出主要步骤
   - 每步做什么

3. **输出格式**
   - 定义输出格式
   - 保持一致性

4. **错误处理**
   - 列出可能的错误
   - 提供解决方案

## 示例

查看 `skills/01-basics/` 目录中的示例 Skills：
- `hello-world` - 最简单的示例
- `code-explainer` - 代码解释器
- `git-commit-helper` - Git 提交助手

## 下一步

1. 完成基础 Skill
2. 查看 [高级模板](../advanced-skill-template/)
3. 阅读 [最佳实践](../../docs/03-best-practices.md)
