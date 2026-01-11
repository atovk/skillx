# 教程 2: 渐进式披露

当 Skill 变得复杂时，如何组织内容让用户容易理解？**渐进式披露**是解决这个问题的有效方法。

## 教程目标

完成本教程后，你将：

- 理解什么是渐进式披露
- 知道何时使用多文件结构
- 掌握组织复杂内容的技巧
- 能够创建易于维护的 Skills

## 什么是渐进式披露？

**渐进式披露**（Progressive Disclosure）是一种设计原则，指：

- 先展示基本信息和核心功能
- 详细内容放到单独的文件中
- 用户需要时再查看详细信息

### 类比理解

想象你在餐厅点餐：

1. **菜单**：显示菜品名称和简介（主文件）
2. **详情页**：扫描二维码看详细配料和营养信息（参考文件）
3. **食谱书**：在厨房想学习制作时查看（详细文档）

## 为什么需要渐进式披露？

### 问题：单文件过长

```markdown
---
name: api-generator
description: 生成 API 样板代码
---

# API 生成器

[500 行详细内容...]

## Express 模板详解
[100 行 Express 内容...]

## FastAPI 模板详解
[100 行 FastAPI 内容...]

## Next.js API 模板详解
[100 行 Next.js 内容...]

[更多详细内容...]
```

**问题**：

- ❌ 难以阅读和维护
- ❌ 新手被详细信息淹没
- ❌ 修改某个模板容易破坏其他部分

### 解决方案：多文件结构

```
api-generator/
├── SKILL.md          # 主文件（100 行）
├── templates/
│   ├── express.md    # Express 详细模板
│   ├── fastapi.md    # FastAPI 详细模板
│   └── nextjs.md     # Next.js 详细模板
└── examples.md       # 使用示例
```

**优势**：

- ✅ 主文件简洁，易于理解
- ✅ 详细内容独立，易于维护
- ✅ 用户按需查看

## 实践：重构复杂 Skill

让我们将一个单文件 Skill 重构为多文件结构。

### 原始版本（单文件）

```markdown
---
name: rest-api-generator
description: 生成 REST API 样板代码，支持 Express、FastAPI、Spring Boot
allowed-tools:
  - Read
  - Write
---

# REST API 生成器

你是 REST API 样板代码生成专家。

## 支持的框架

### Express (Node.js)

Express 是一个流行的 Node.js Web 框架...

[200 行详细说明和模板]

### FastAPI (Python)

FastAPI 是一个现代、快速的 Python Web 框架...

[200 行详细说明和模板]

### Spring Boot (Java)

Spring Boot 是 Java 企业级开发的标准选择...

[200 行详细说明和模板]

[更多内容...]
```

### 重构后（多文件）

```
rest-api-generator/
├── SKILL.md          # 主文件（50 行）
├── README.md         # 使用说明
├── reference.md      # 参考文档
├── templates/        # 模板目录
│   ├── express.md
│   ├── fastapi.md
│   └── spring-boot.md
└── examples.md       # 示例
```

#### SKILL.md（主文件）

```markdown
---
name: rest-api-generator
description: 生成 REST API 样板代码，支持 Express、FastAPI、Spring Boot
allowed-tools:
  - Read
  - Write
---

# REST API 生成器

你是 REST API 样板代码生成专家，帮助开发者快速创建 API 项目。

## 工作流程

1. **选择框架**：询问用户想使用的框架
2. **收集信息**：项目名称、端口、中间件等
3. **生成代码**：根据选择生成样板代码
4. **保存文件**：创建项目结构和文件

## 支持的框架

查看 [templates/](templates/) 目录了解每个框架的详细模板：

- **[Express](templates/express.md)** - Node.js Web 框架
- **[FastAPI](templates/fastapi.md)** - 现代 Python Web 框架
- **[Spring Boot](templates/spring-boot.md)** - Java 企业级框架

## 快速开始

### Express 示例

**用户**: rest-api-generator

**Assistant**: 请选择框架：
1. Express (Node.js)
2. FastAPI (Python)
3. Spring Boot (Java)

**用户**: 1

**Assistant**: 请提供以下信息：
- 项目名称：my-api
- 端口：3000
- 需要的中间件（cors, body-parser, etc.）：cors, body-parser

正在生成 Express API...

更多示例请查看 [examples.md](examples.md)。
```

#### templates/express.md（详细模板）

```markdown
# Express API 模板

## Express 简介

Express 是最小且灵活的 Node.js Web 应用框架...

## 项目结构

```

my-api/
├── src/
│   ├── index.js
│   ├── routes/
│   ├── controllers/
│   └── middleware/
├── tests/
└── package.json

```

## 模板代码

### index.js

\`\`\`javascript
const express = require('express');
const cors = require('cors');
const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(cors());
app.use(express.json());

// Routes
app.get('/', (req, res) => {
  res.json({ message: 'Welcome to the API' });
});

// Start server
app.listen(PORT, () => {
  console.log(\`Server running on port \${PORT}\`);
});
\`\`\`

[更多详细模板...]
```

## 组织技巧

### 1. 嵌套层次不超过 2 层

❌ 避免过深的嵌套：

```markdown
## 主文档
详细内容请查看 [reference.md](reference.md)

# reference.md
## 某个主题
更多细节请查看 [details.md](details.md)

# details.md
## 更多细节
超深细节请查看 [deep-details.md](deep-details.md)  ← 太深了！
```

✅ 推荐的扁平结构：

```markdown
## 主文档 (SKILL.md)
- 核心指令
- 链接到 [reference.md](reference.md)

## 参考文档 (reference.md)
- 详细信息
- 直接内容，不再引用其他文件
```

### 2. 按功能组织文件

```
complex-skill/
├── SKILL.md              # 主文件
├── README.md             # 使用说明
├── reference.md          # 完整参考
├── examples.md           # 示例集合
├── patterns.md           # 设计模式
└── templates/            # 模板目录
    ├── template-1.md
    └── template-2.md
```

### 3. 文件命名规范

| 文件名 | 用途 | 内容 |
|--------|------|------|
| `SKILL.md` | 主文件 | 核心指令（< 500 行） |
| `README.md` | 使用说明 | 快速开始、安装、配置 |
| `reference.md` | 参考文档 | 完整的 API/选项参考 |
| `examples.md` | 示例 | 实际使用案例 |
| `patterns.md` | 模式 | 设计模式和最佳实践 |
| `troubleshooting.md` | 故障排除 | 常见问题和解决方案 |
| `changelog.md` | 变更日志 | 版本更新记录 |

### 4. 使用清晰的链接

❌ 模糊的链接：

```markdown
更多信息请看这里。
```

✅ 清晰的链接：

```markdown
更多配置选项请查看 [配置参考](reference.md#configuration)。

实际使用示例请查看 [examples.md](examples.md)。
```

## 实践练习

### 练习 1: 识别需要重构的 Skill

这个 Skill 需要重构吗？

```markdown
---
name: data-processor
description: 处理各种数据格式
allowed-tools:
  - Read
  - Write
---

# 数据处理器

## CSV 处理
[150 行详细内容...]

## JSON 处理
[150 行详细内容...]

## XML 处理
[150 行详细内容...]

## Excel 处理
[150 行详细内容...]
```

**答案**：是的！应该重构为：

```
data-processor/
├── SKILL.md
├── formats/
│   ├── csv.md
│   ├── json.md
│   ├── xml.md
│   └── excel.md
└── examples.md
```

### 练习 2: 重构 Skill

重构这个 Skill，使用渐进式披露：

```markdown
---
name: test-generator
description: 为各种语言和框架生成测试代码
---

# 测试生成器

[每个框架 100 行...]

## Jest
[100 行...]

## Mocha
[100 行...]

## Pytest
[100 行...]

## JUnit
[100 行...]
```

**提示**：

1. 创建 `templates/` 目录
2. 将每个框架的详细内容移到单独文件
3. 在主文件中保留简短说明和链接

## 最佳实践

### 1. 主文件 (SKILL.md) 应该

- ✅ 包含核心指令
- ✅ 说明基本工作流
- ✅ 链接到详细信息
- ✅ 控制在 500 行以内
- ❌ 不包含大量代码模板
- ❌ 不包含详细参考信息

### 2. 参考文件应该

- ✅ 自包含完整信息
- ✅ 可以独立阅读
- ✅ 有清晰的标题结构
- ❌ 不依赖其他参考文件

### 3. 示例文件应该

- ✅ 包含真实场景
- ✅ 有输入输出示例
- ✅ 展示最佳实践
- ✅ 可以复制粘贴使用

## 工具推荐

### 查看文件结构

```bash
# 查看目录树
tree skill-name

# 或使用 find
find skill-name -type f | sort
```

### 检查文件大小

```bash
# 统计行数
wc -l SKILL.md

# 如果超过 500 行，考虑重构
```

## 常见问题

### Q: 什么时候应该使用多文件结构？

**A**: 出现以下情况时考虑：

- `SKILL.md` 超过 500 行
- 有大量模板或代码示例
- 需要频繁更新某个部分
- 有多种使用场景

### Q: 引用文件会不会让内容分散？

**A**: 如果组织得当，反而会让内容更清晰：

- 主文件提供"大局观"
- 参考文件提供"深度信息"
- 用户按需查看

### Q: 如何避免引用链过长？

**A**: 遵循"最多一层引用"原则：

- 主文件 → 参考文件 ✅
- 主文件 → 参考文件 → 详细文件 ❌

## 总结

渐进式披露的关键原则：

1. **主文件简洁** - 只包含核心指令（< 500 行）
2. **详细信息分离** - 大段内容放到单独文件
3. **清晰的链接** - 使用描述性的链接文本
4. **扁平结构** - 避免超过一层嵌套引用
5. **自包含文件** - 参考文件应该完整独立

## 下一步

现在你已经学会了如何组织复杂内容：

1. **练习**：完成 [中级练习 6：渐进式披露](../../exercises/intermediate/exercise-06-progressive-disclosure.md)
2. **学习**：阅读 [教程 3：工作流设计](tutorial-03-workflow-design.md)
3. **探索**：查看 [api-boilerplate 示例](../../skills/03-code-generation/api-boilerplate/)

## 参考资源

- [最佳实践：简洁性](../03-best-practices.md#简洁性原则)
- [Skill 结构剖析](../02-skill-anatomy.md)
- [多文件 Skill 示例](../../skills/03-code-generation/)
