# 练习 8: 创建条件工作流

**难度**：⭐⭐ 中级
**预计时间**：35 分钟

## 学习目标

完成这个练习后，你将：

- 掌握条件分支的设计
- 理解如何根据不同输入执行不同流程
- 能够创建灵活的 Skills

## 前置知识

- 完成中级练习 6-7
- 理解基本工作流设计
- 熟悉多文件组织

## 任务描述

创建一个 **智能项目初始化器**，根据项目类型选择不同的初始化流程。

### 场景

开发者需要创建新项目时，根据不同的技术栈需要不同的初始化步骤。我们需要一个 Skill 能够：

1. 自动检测项目类型
2. 根据类型选择相应的初始化流程
3. 执行对应的初始化命令

## 要求

### 1. 识别项目类型

检测以下项目类型：

#### A) Node.js 项目

- 有 `package.json`
- 有 `node_modules/` 目录

#### B) Python 项目

- 有 `requirements.txt`
- 有 `setup.py` 或 `pyproject.toml`

#### C) Rust 项目

- 有 `Cargo.toml`

#### D) Go 项目

- 有 `go.mod`

#### E) 通用项目

- 有 README.md
- 有 .git 目录

### 2. 设计分支流程

```markdown
## 工作流程

### 第 1 步: 识别项目类型
检查目录结构，识别项目类型

### 第 2 步: 选择流程

#### 流程 A: Node.js 项目
1. 检查 package.json
2. 运行 npm install
3. 运行 npm test（如果有）
4. 运行 npm build（如果有）

#### 流程 B: Python 项目
1. 创建虚拟环境
2. 安装依赖
3. 运行测试（如果有）
4. 检查代码格式（如果有配置）

#### 流程 C: Rust 项目
1. 运行 cargo build
2. 运行 cargo test

#### 流程 D: Go 项目
1. 下载依赖
2. 运行 go build
3. 运行 go test

#### 流程 E: 通用项目
1. 初始化 Git（如果需要）
2. 创建 .gitignore
3. 创建 README.md

### 第 3 步: 执行并报告
执行选定的流程并报告结果
```

### 3. 条件判断

使用清晰的条件语句：

```markdown
### 判断逻辑

if (存在 package.json) {
  → 执行 Node.js 流程
}
else if (存在 requirements.txt 或 setup.py) {
  → 执行 Python 流程
}
else if (存在 Cargo.toml) {
  → 执行 Rust 流程
}
else if (存在 go.mod) {
  → 执行 Go 流程
}
else {
  → 执行通用项目流程
}
```

### 4. 每个流程的详细步骤

为每种项目类型定义详细步骤：

```markdown
## Node.js 流程

### 检查 1: 依赖安装
```bash
npm install
```

检查 package.json 中的 dependencies

### 检查 2: 运行测试

如果有 test 脚本：

```bash
npm test
```

### 检查 3: 构建

如果有 build 脚本：

```bash
npm run build
```

### 检查 4: 代码检查

如果有 lint 脚本：

```bash
npm run lint
```

```

## 条件设计模式

### 模式 1: 顺序判断

```markdown
按优先级判断：
if (条件 A) → 流程 A
else if (条件 B) → 流程 B
else → 默认流程
```

### 模式 2: 多重匹配

```markdown
检查多个条件：
if (条件 A && 条件 B) → 流程 AB
if (条件 A && !条件 B) → 流程 A
if (!条件 A && 条件 B) → 流程 B
```

### 模式 3: 用户选择

```markdown
自动检测后询问用户：

检测到这是 Node.js 项目

建议执行：
1. npm install
2. npm test
3. npm run build

选择要执行的步骤（输入编号，多个用逗号分隔）：
或输入 'all' 执行所有步骤
```

## 实践练习

### 练习 1: 基础条件流程

创建一个 Skill，根据文件扩展名选择不同的分析方式：

```markdown
## 文件分析器

if (文件是 .js) {
  → JavaScript 分析
}
else if (文件是 .py) {
  → Python 分析
}
else if (文件是 .java) {
  → Java 分析
}
else {
  → 通用文本分析
}
```

### 练习 2: 添加确认机制

在执行前请求用户确认：

```markdown
### 第 2 步: 确认流程

检测到这是 Node.js 项目

将执行以下步骤：
1. npm install
2. npm test
3. npm run build

是否继续？(y/n)
> n

跳过。是否选择特定步骤？
> 1,3

只执行步骤 1 和 3...
```

### 练习 3: 处理组合情况

处理混合项目（如 Node.js + Python）：

```markdown
### 检测到混合项目

检测到：
- package.json (Node.js)
- requirements.txt (Python)

选择要初始化的环境：
1. Node.js
2. Python
3. 两者都初始化

> 3

首先初始化 Node.js...
然后初始化 Python...
```

## 提示

### 提示 1: 使用 Glob 检测文件

```markdown
## 检测项目类型

使用 Glob 工具查找特征文件：

1. 查找 package.json
   如果存在 → Node.js 项目

2. 查找 requirements.txt
   如果存在 → Python 项目

3. 查找 Cargo.toml
   如果存在 → Rust 项目
```

### 提示 2: 处理模糊情况

```markdown
## 处理多种特征

如果同时存在多个特征文件：
1. 询问用户主要使用哪种技术
2. 或者按优先级选择
3. 或者支持多个技术栈
```

### 提示 3: 提供默认选项

```markdown
### 默认行为

检测到 Node.js 项目

建议操作：
1. npm install
2. npm test

[a] 全部执行 [s] 选择步骤 [s] 跳过

> a

执行所有建议步骤...
```

### 提示 4: 记录决策

```markdown
### 决策日志

记录为什么选择特定流程：

**项目**: /path/to/project
**检测到的特征**: package.json
**选择流程**: Node.js
**原因**: 存在 package.json
**执行步骤**: npm install, npm test
```

## 输出格式

### 成功执行

```markdown
# 项目初始化完成

**项目类型**: Node.js
**项目路径**: /path/to/project

## 执行步骤

✅ npm install (完成，耗时 5s)
✅ npm test (通过，15 个测试)
⚠️ npm run build (警告，有 2 个 lint 错误)

## 总结

项目已成功初始化！
- 依赖已安装
- 测试通过
- 构建完成（有警告）

建议：修复 lint 错误
```

### 用户取消

```markdown
# 项目初始化已取消

检测到 Node.js 项目
建议执行：npm install, npm test

用户取消操作。

如需重新初始化，请再次运行此 Skill。
```

## 验收标准

完成练习后，检查：

- [ ] 能正确识别项目类型
- [ ] 每种类型有对应的流程
- [ ] 流程步骤清晰明确
- [ ] 有用户确认机制
- [ ] 输出格式统一
- [ ] 有错误处理

## 延伸挑战

1. **添加配置文件**
   支持自定义初始化配置

2. **并行执行**
   如果有多个独立的初始化步骤，并行执行

3. **缓存结果**
   避免重复初始化

## 参考答案

完成练习后，可以查看 `solutions/intermediate/exercise-08.md` 对比参考答案。

## 相关资源

- [教程：工作流设计](../../docs/tutorials/tutorial-03-workflow-design.md)
- [高级模式：条件工作流](../../docs/04-advanced-patterns.md#条件工作流模式)
- [最佳实践：工作流设计](../../docs/03-best-practices.md#工作流设计)
