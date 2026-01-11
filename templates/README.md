# Skill 模板目录

这里有可复用的 Skill 模板，帮助你快速开始创建新的 Skills。

## 可用模板

### 基础模板

**目录**: `basic-skill-template/`

**适合**: 初学者、简单的 Skills

**特点**:
- 简单的结构
- 清晰的注释
- 完整的基本要素

**使用**:
```bash
cp -r basic-skill-template my-skill
cd my-skill
mv SKILL.md.template SKILL.md
# 编辑 SKILL.md
```

### 高级模板

**目录**: `advanced-skill-template/`

**适合**: 复杂的 Skills、多文件结构

**特点**:
- 多文件结构
- 完整的文档
- 参考和示例

**使用**:
```bash
cp -r advanced-skill-template my-complex-skill
cd my-complex-skill
# 编辑所有 .template 文件（去掉 .template 后缀）
```

### 专用模板

#### 文件操作模板
**目录**: `file-operations-template/`

**适合**: 需要读写文件的 Skills

**特点**:
- Read/Write 工具
- 文件验证
- 错误处理

#### 代码生成模板
**目录**: `code-gen-template/`

**适合**: 生成代码的 Skills

**特点**:
- 模板系统
- 多语言支持
- 示例模式

## 使用流程

### 1. 选择模板

根据你的 Skill 复杂度选择合适的模板

### 2. 复制模板

```bash
# 复制到你的项目
cp -r [template-name] my-skill
cd my-skill
```

### 3. 重命名文件

如果有 `.template` 后缀，去掉它：

```bash
find . -name "*.template" -exec sh -c 'mv "$1" "${1%.template}"' _ {} \;
```

### 4. 自定义内容

编辑所有文件，修改：
- Frontmatter 元数据
- Skill 名称和描述
- 工作流程和指令
- 示例和文档

### 5. 测试

在 Claude Code 中测试：
```
your-skill-name
```

## 模板对比

| 特性 | 基础模板 | 高级模板 | 文件操作 | 代码生成 |
|------|---------|---------|----------|----------|
| 文件数量 | 1 | 5+ | 2 | 3 |
| 复杂度 | 简单 | 中等 | 中等 | 中等 |
| 文档 | 基础 | 完整 | 中等 | 中等 |
| 适合 | 初学者 | 进阶 | 特定场景 | 特定场景 |

## 贡献模板

如果你想贡献新的模板：

1. 遵循现有模板的结构
2. 包含清晰的 README
3. 提供使用示例
4. 添加注释说明

查看 [贡献指南](../.github/CONTRIBUTING.md) 了解更多信息。

## 相关资源

- [快速入门](../docs/00-getting-started.md)
- [Skill 结构剖析](../docs/02-skill-anatomy.md)
- [最佳实践](../docs/03-best-practices.md)
