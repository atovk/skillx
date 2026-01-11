# 最佳实践指南

编写高质量 Claude Code Skills 的最佳实践和设计模式。

## 核心原则

### 1. 简洁性原则

**Keep It Simple, Stupid (KISS)**

> "简单是复杂的终极形式" - 达芬奇

#### 保持 Skill 简洁

```yaml
# ❌ 不好：功能太多
---
name: do-everything
description: 处理所有开发任务
allowed-tools: []
---

# 1000+ 行复杂逻辑

# ✅ 好：单一职责
---
name: git-commit-helper
description: 生成 Git 提交信息
allowed-tools:
  - Bash
---

# 200 行清晰逻辑
```

#### 单一职责原则

一个 Skill 只做一件事：

| Skill | 职责 |
|-------|------|
| `git-commit-helper` | 生成提交信息 |
| `code-formatter` | 格式化代码 |
| `test-generator` | 生成测试 |

**不要**：

```yaml
# ❌ 一个 Skill 做所有事
---
name: dev-helper
description: Git、测试、格式化、部署...
---
```

**应该**：

```yaml
# ✅ 拆分成多个 Skills
git-commit-helper/
test-generator/
code-formatter/
deploy-helper/
```

### 2. 清晰性原则

让意图清晰明确。

#### 清晰的描述

```yaml
# ❌ 模糊
description: 一个处理代码的 skill

# ✅ 清晰
description: 分析 JavaScript 代码并提供性能优化建议
```

#### 清晰的指令

```markdown
# ❌ 不清晰
处理文件并返回结果

# ✅ 清晰
## 步骤 1: 读取文件
使用 Read 工具读取用户指定的文件

## 步骤 2: 分析内容
分析文件内容并提取关键信息

## 步骤 3: 返回结果
以 JSON 格式返回分析结果
```

### 3. 渐进式披露原则

先展示基本信息，详细内容放单独文件。

#### 主文件保持简洁

```markdown
# SKILL.md (< 500 行)

## 概述
[核心概念]

## 工作流程
[主要步骤]

详细内容请查看：
- [参考文档](reference.md)
- [使用示例](examples.md)
- [模板库](templates/)
```

#### 详细内容分离

```
my-skill/
├── SKILL.md          # 主文件（简洁）
├── reference.md      # 参考文档（详细）
├── examples.md       # 示例（丰富）
└── templates/        # 模板（完整）
```

## 设计模式

### 模式 1: 只读优先

**原则**：默认只读，明确声明写操作

```yaml
# ✅ 好：默认只读
---
name: file-analyzer
description: 分析文件结构和内容
allowed-tools:
  - Read
  - Grep
  - Glob
---

# ✅ 好：明确需要写操作
---
name: file-organizer
description: 整理和格式化文件
allowed-tools:
  - Read
  - Write
---
```

### 模式 2: 确认机制

**原则**：危险操作需要用户确认

```markdown
## 删除文件

### 步骤 1: 显示预览
```

将删除以下文件：

- file1.txt
- file2.txt

```

### 步骤 2: 请求确认
```

确认删除？(y/n)

```

### 步骤 3: 执行删除
只在用户输入 'y' 后执行
```

### 模式 3: 分步执行

**原则**：显示进度，让用户了解状态

```markdown
### 步骤 1/4: 读取文件 ⏳
正在读取文件...

### 步骤 2/4: 分析内容 ✅
已分析完成

### 步骤 3/4: 生成报告 ⏳
正在生成报告...

### 步骤 4/4: 保存结果 ✅
报告已保存到 report.md
```

### 模式 4: 错误优先

**原则**：优先考虑错误情况

```markdown
## 错误处理

### 文件不存在
```

❌ 错误：文件不存在
文件 'xyz.js' 找不到

请检查：

1. 文件路径是否正确
2. 文件是否在当前目录
3. 尝试使用绝对路径

```

### 权限不足
```

❌ 错误：权限不足
无法写入文件 'config.json'

建议：

- 检查文件权限：ls -l config.json
- 确认你有写入权限

```
```

## 命名规范

### Skill 命名

```yaml
# ✅ 好的命名
name: git-commit-helper
name: api-generator
name: code-reviewer
name: test-generator

# ❌ 不好的命名
name: gitHelper           # 驼峰命名
name: API_Generator       # 大写和下划线
name: 123helper           # 数字开头
```

### 变量命名

```markdown
# ✅ 好的变量名
- FILE_PATH
- PROJECT_NAME
- OUTPUT_DIRECTORY
- MAX_FILE_SIZE

# ❌ 不好的变量名
- path
- x
- temp
- data
```

### 目录命名

```
# ✅ 好的目录名
code-templates/
example-files/
reference-docs/

# ❌ 不好的目录名
CodeTemplates/      # 大写
example_files/      # 下划线
ref docs/           # 空格
```

## 内容组织

### 工作流设计

```markdown
## 工作流程

### 第 1 步：收集信息
询问用户的具体需求

### 第 2 步：分析请求
理解用户想要什么

### 第 3 步：执行操作
根据分析结果执行相应操作

### 第 4 步：返回结果
清晰展示操作结果
```

### 输出格式

```markdown
## 输出格式

使用一致的格式：

```markdown
# 结果标题

**文件**: file.js
**大小**: 2.5 KB

## 分析结果
- 检查项 1: ✅ 通过
- 检查项 2: ⚠️ 警告
- 检查项 3: ❌ 失败

## 建议
[具体建议]
```

```

### 错误信息

```markdown
## 错误信息格式

### 结构
1. 错误类型（标题）
2. 错误描述
3. 可能原因
4. 解决建议

### 示例
```markdown
### ❌ 错误：文件不存在

**文件**: 'xyz.js'

**可能原因**:
1. 文件路径不正确
2. 文件已被删除
3. 当前目录错误

**建议**:
- 检查文件路径：`ls -l xyz.js`
- 确认当前目录：`pwd`
- 尝试使用绝对路径
```

```

## 工具使用

### 工具声明

```yaml
# ✅ 好：明确声明
allowed-tools:
  - Read
  - Grep

# ⚠️ 谨慎：允许所有
# (不声明 allowed-tools)

# ⚠️ 危险：包含 Bash
allowed-tools:
  - Bash
# 应该有充分理由和详细的错误处理
```

### 工具选择指南

| 工具 | 何时使用 | 注意事项 |
|------|----------|----------|
| `Read` | 读取文件内容 | 处理大文件要分块 |
| `Write` | 写入文件 | 确认路径正确 |
| `Grep` | 搜索文件内容 | 限制搜索范围 |
| `Glob` | 查找文件 | 注意结果数量 |
| `Bash` | 执行命令 | 验证输入，防止注入 |

## 测试策略

### 测试金字塔

```
        /\
       /  \
      / E2E \         少量端到端测试
     /--------\
    /  集成  \       适中的集成测试
   /----------\
  /    单元    \    大量的单元测试
 /--------------\
```

### 测试清单

```markdown
## 测试清单

### 功能测试
- [ ] 正常输入正常工作
- [ ] 边界值正确处理
- [ ] 错误输入有友好提示

### 集成测试
- [ ] 工具调用正确
- [ ] 权限检查
- [ ] 错误恢复

### 用户体验测试
- [ ] 输出清晰易读
- [ ] 进度反馈及时
- [ ] 错误信息有帮助
```

## 文档规范

### README.md

```markdown
# Skill 名称

简短描述

## 功能特性
- 特性 1
- 特性 2

## 安装
[安装步骤]

## 使用
[使用方法]

## 示例
[示例]

## 常见问题
[FAQ]

## 贡献
[贡献指南]
```

### examples.md

```markdown
# 使用示例

## 示例 1: 基本用法
**场景**: [描述]
**输入**: [输入]
**输出**: [输出]

## 示例 2: 高级用法
...
```

## 性能考虑

### 大文件处理

```markdown
## 处理大文件

### 策略 1: 分块读取
不要一次性读取整个文件，分块处理

### 策略 2: 流式处理
边读边处理，不保存全部内容

### 策略 3: 显示进度
大文件处理时显示进度条
```

### 内存优化

```markdown
## 优化建议

1. 避免在内存中保存大量数据
2. 使用流式处理
3. 及时释放不需要的数据
4. 限制处理的数据量
```

## 安全考虑

### 输入验证

```markdown
## 输入验证

### 文件路径
- 检查路径是否在预期范围内
- 防止路径遍历攻击

### 命令注入
- 验证用户输入
- 转义特殊字符
- 使用白名单而非黑名单
```

### 权限管理

```markdown
## 权限原则

1. **最小权限**: 只申请需要的工具
2. **明确声明**: 在 Frontmatter 中声明
3. **用户确认**: 危险操作需要确认
```

## 代码审查清单

发布前检查：

```markdown
## 代码审查清单

### 功能
- [ ] 功能完整且正常工作
- [ ] 边界情况处理
- [ ] 错误处理完善

### 文档
- [ ] README 清晰
- [ ] 有使用示例
- [ ] 有参考文档

### 代码质量
- [ ] 命名清晰
- [ ] 格式一致
- [ ] 没有冗余代码

### 安全
- [ ] 输入验证
- [ ] 权限检查
- [ ] 敏感信息保护

### 测试
- [ ] 单元测试
- [ ] 集成测试
- [ ] 用户测试
```

## 反模式

### 避免：过度设计

```yaml
# ❌ 不好：不必要的复杂性
---
name: simple-task
description: 简单任务
allowed-tools:
  - Read
  - Write
  - Bash
  - Grep
  - Glob
model: claude-opus-4-20251101
context: fork
agent: general-purpose
hooks:
  PreToolUse:
    - ...
  PostToolUse:
    - ...
---

# 对于简单任务来说太复杂了

# ✅ 好：保持简单
---
name: simple-task
description: 简单任务
allowed-tools:
  - Read
---
```

### 避免：重复造轮子

```markdown
# ❌ 不要重复已有功能

# 如果已有 file-analyzer，不要创建 file-reader

# ✅ 应该：扩展现有 Skill
# 或：创建互补的 Skill
```

### 避免：硬编码

```markdown
# ❌ 不好：硬编码路径
读取 /home/user/project/config.json

# ✅ 好：使用变量
读取 {PROJECT_ROOT}/config.json
```

## 总结

最佳实践的核心原则：

1. **简洁性** - 保持简单，单一职责
2. **清晰性** - 意图明确，易于理解
3. **渐进披露** - 先简单，后详细
4. **确认机制** - 危险操作需确认
5. **错误优先** - 优先处理错误情况
6. **安全考虑** - 验证输入，限制权限

## 下一步

1. **学习模式**：[高级模式](04-advanced-patterns.md)
2. **实践**：完成练习题
3. **参考**：查看 [示例 Skills](../skills/)

## 参考资源

- [结构剖析](02-skill-anatomy.md)
- [教程系列](tutorials/)
- [反模式指南](reference/anti-patterns.md)
