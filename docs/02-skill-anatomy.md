# Skill 结构剖析

深入了解 Claude Code Skills 的文件结构、组织方式和命名规范。

## 文件结构

### 单文件 Skill

最简单的 Skill 只需要一个文件：

```
my-skill.md
```

**适用场景**：

- 简单的功能
- 内容不超过 500 行
- 不需要大量模板或示例

### 多文件 Skill

对于复杂的 Skill，推荐使用多文件结构：

```
my-skill/
├── SKILL.md              # 主文件（必需）
├── README.md             # 使用说明（推荐）
├── examples.md           # 使用示例（推荐）
├── reference.md          # 参考文档（可选）
├── patterns.md           # 设计模式（可选）
├── troubleshooting.md    # 故障排除（可选）
└── templates/            # 模板目录（可选）
    ├── template-1.md
    └── template-2.md
```

**适用场景**：

- 复杂的功能
- 需要大量示例
- 有多个模板
- 需要参考文档

## SKILL.md 结构

### Frontmatter（元数据）

```yaml
---
name: skill-name
description: 清晰描述功能（最多 1024 字符）
allowed-tools:
  - Read
  - Write
  - Bash
model: claude-sonnet-4-20250514
context: fork
agent: general-purpose
user-invocable: true
hooks:
  PreToolUse:
    - matcher: "Bash"
      hooks:
        - type: command
          command: "./scripts/validate.sh $TOOL_INPUT"
---
```

### 字段详解

#### name（必需）

Skill 的唯一标识符。

**规则**：

- 只能包含小写字母、数字、连字符
- 不能以连字符开头或结尾
- 不能包含空格
- 最大 64 字符

**示例**：

```yaml
# ✅ 好的命名
name: git-commit-helper
name: code-reviewer
name: api-generator

# ❌ 不好的命名
name: Git Commit Helper    # 空格
name: git-commit-helper-   # 结尾连字符
name: 123helper           # 数字开头
```

**命名模式**：

| 模式 | 示例 | 用途 |
|------|------|------|
| 动词-名词 | `process-pdf` | 处理操作 |
| 名词-助手 | `git-helper` | 辅助工具 |
| 名词-生成器 | `code-generator` | 生成器 |

#### description（必需）

Skill 的功能描述。

**规则**：

- 最多 1024 字符
- 清楚说明功能和使用场景
- 使用现在时态
- 适合 50-100 字符

**示例**：

```yaml
# ✅ 好的描述
description: 分析 Git diff 并生成符合规范的提交信息
description: 审查代码质量并提供具体的改进建议
description: 将 Markdown 文件转换为 HTML 格式

# ❌ 不好的描述
description: 一个 Git skill           # 太模糊
description: 处理代码                 # 不清楚
description: This is a very long description that goes on and on...  # 太长
```

#### allowed-tools（可选）

声明 Skill 可以使用的工具。

**可用工具**：

| 工具 | 功能 | 典型用途 |
|------|------|----------|
| `Read` | 读取文件 | 读取代码、配置 |
| `Write` | 写入文件 | 生成代码、保存结果 |
| `Grep` | 搜索内容 | 查找函数、变量 |
| `Glob` | 查找文件 | 列出文件、匹配模式 |
| `Bash` | 执行命令 | 运行脚本、系统操作 |

**使用建议**：

```yaml
# ✅ 原则：最小权限
allowed-tools:
  - Read      # 只读操作

# ✅ 需要写操作时明确声明
allowed-tools:
  - Read
  - Write

# ✅ 避免使用 Bash（除非必要）
allowed-tools:
  - Read
  - Grep
  - Glob

# ⚠️ 谨慎使用 Bash
allowed-tools:
  - Bash      # 可能执行任意命令
```

#### model（可选）

指定使用的模型。

**值**：

```yaml
# 使用最新模型
model: claude-sonnet-4-20250514

# 使用特定模型
model: claude-opus-4-20251101
```

**使用场景**：

- 需要特定模型的能力
- 成本考虑
- 性能优化

#### context（可选）

控制执行上下文。

```yaml
# 默认：共享上下文
# (不设置 context)

# Fork：独立上下文
context: fork
```

**使用场景**：

- `context: fork` - 每个 Tool 调用独立
- 不设置 - 共享上下文（默认）

#### agent（可选）

指定使用的 agent 类型。

```yaml
# 使用通用 agent
context: fork
agent: general-purpose

# 使用特定 agent
agent: specialist-agent
```

**注意**：需要配合 `context: fork` 使用。

#### hooks（可选）

在工具调用前后的钩子。

```yaml
hooks:
  PreToolUse:
    - matcher: "Bash"
      hooks:
        - type: command
          command: "./scripts/validate.sh $TOOL_INPUT"
  PostToolUse:
    - matcher: "Read"
      hooks:
        - type: command
          command: "./scripts/log-read.sh"
```

## 内容结构

### 推荐的组织方式

```markdown
---
[Frontmatter]
---

# [Skill 名称]

[简介：你是谁，做什么]

## 工作流程

[步骤说明]

## 使用方法

[如何使用]

## 输出格式

[输出模板]

## 错误处理

[错误情况]

## 示例

[使用示例]
```

### 内容长度建议

| 部分 | 建议长度 | 说明 |
|------|----------|------|
| SKILL.md | < 500 行 | 主文件保持简洁 |
| README.md | 100-300 行 | 使用说明 |
| examples.md | 不限 | 可以很长 |
| reference.md | 不限 | 参考文档 |

## 命名规范

### 文件命名

**主文件**：必须是 `SKILL.md`（全大写）

**其他文件**：使用小写和连字符

```
my-skill/
├── SKILL.md           # 必须全大写
├── README.md          # 大写（习惯）
├── examples.md        # 小写
├── reference.md       # 小写
└── code-templates.md  # 小写加连字符
```

### 目录命名

使用小写和连字符：

```
✅ good-skill-name/
✅ api-generator/
✅ code-review-helper/

❌ BadSkillName/
❌ API_Generator/
❌ code_review_helper/
```

### 变量命名

在指令中，使用清晰的大写变量：

```markdown
## 变量命名

✅ 好的命名
- FILE_PATH
- PROJECT_NAME
- OUTPUT_DIR

❌ 不好的命名
- path
- x
- temp
```

## 目录结构示例

### 简单 Skill

```
hello-world/
└── SKILL.md
```

### 中等复杂度

```
code-explainer/
├── SKILL.md
├── README.md
└── examples.md
```

### 复杂 Skill

```
api-generator/
├── SKILL.md
├── README.md
├── examples.md
├── reference.md
├── CHANGELOG.md
└── templates/
    ├── express.md
    ├── fastapi.md
    └── spring-boot.md
```

### 包含脚本的 Skill

```
batch-processor/
├── SKILL.md
├── README.md
├── scripts/
│   ├── process.py
│   ├── validate.sh
│   └── utils.js
└── templates/
    └── config.json
```

## 组织技巧

### 1. 按功能组织

```
data-processor/
├── SKILL.md
├── formats/
│   ├── csv.md
│   ├── json.md
│   └── xml.md
└── examples/
    ├── csv-example.md
    └── json-example.md
```

### 2. 按使用场景组织

```
test-generator/
├── SKILL.md
├── frameworks/
│   ├── jest.md
│   ├── pytest.md
│   └── junit.md
└── examples/
    └── usage-examples.md
```

### 3. 使用清晰的目录名

```
✅ 好的目录名
- templates/
- examples/
- scripts/
- docs/
- formats/

❌ 不好的目录名
- stuff/
- things/
- files/
- misc/
```

## Frontmatter 验证

### YAML 格式检查

使用 YAML 验证工具：

```bash
# 使用 yamllint
yamllint SKILL.md

# 使用 Python
python -c "import yaml; yaml.safe_load(open('SKILL.md'))"
```

### 常见错误

```yaml
---
# ❌ 错误：缺少分隔符
name: my-skill
description: my description

---

# ✅ 正确
---
name: my-skill
description: my description
---
```

```yaml
---
# ❌ 错误：缩进不正确
name: my-skill
allowed-tools:
- Read
- Write

---

# ✅ 正确
---
name: my-skill
allowed-tools:
  - Read
  - Write
---
```

## 最佳实践

### 1. 主文件 (SKILL.md)

应该包含：

- ✅ 清晰的 Frontmatter
- ✅ 核心指令
- ✅ 工作流程
- ✅ 错误处理

不应该包含：

- ❌ 大量代码模板
- ❌ 详细参考信息
- ❌ 过长的示例

### 2. 多文件组织

```
my-skill/
├── SKILL.md              # 核心指令（< 500 行）
├── README.md             # 快速开始
├── reference.md          # 详细参考
├── examples.md           # 示例集合
└── templates/            # 模板文件
```

### 3. 避免深层嵌套

```markdown
# ❌ 不好：深层嵌套
## 主文档
详见 reference.md

# reference.md
## 主题
详见 details.md

# details.md
## 更多
详见 deep-details.md  ← 太深了！

# ✅ 好：扁平结构
## SKILL.md
- 核心内容
- 链接到 reference.md

## reference.md
- 完整信息
- 不再引用其他文件
```

## 工具推荐

### 查看结构

```bash
# 使用 tree
tree my-skill

# 使用 find
find my-skill -type f | sort

# 使用 exa（如果安装）
exa -T my-skill
```

### 检查文件大小

```bash
# 统计行数
wc -l SKILL.md

# 查看文件大小
ls -lh SKILL.md

# 查找大文件
find . -type f -size +50k
```

## 总结

Skill 结构的关键点：

1. **SKILL.md** - 必需的主文件
2. **Frontmatter** - 元数据声明
3. **多文件** - 复杂 Skill 使用多文件
4. **命名规范** - 小写、连字符
5. **组织清晰** - 按功能或场景组织
6. **避免嵌套** - 最多一层引用

## 下一步

1. **实践**：[创建第一个 Skill](tutorials/tutorial-01-first-skill.md)
2. **学习**：[最佳实践](03-best-practices.md)
3. **参考**：[元数据参考](reference/skill-metadata-reference.md)

## 参考资源

- [最佳实践：简洁性](03-best-practices.md#简洁性原则)
- [教程：渐进式披露](tutorials/tutorial-02-progressive-disclosure.md)
- [示例 Skills](../skills/)
