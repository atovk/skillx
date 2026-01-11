# 练习 9: 构建模板系统

**难度**：⭐⭐ 中级
**预计时间**：40 分钟

## 学习目标

完成这个练习后，你将：

- 理解如何设计模板系统
- 掌握变量替换的方法
- 能够创建可复用的代码模板

## 前置知识

- 完成中级练习 6-8
- 熟悉文件操作
- 了解代码生成基础

## 任务描述

创建一个 **配置文件生成器**，使用模板系统生成各种配置文件。

### 场景

开发者经常需要创建各种配置文件（.env, config.json, docker-compose.yml 等）。
我们将创建一个 Skill 使用模板系统快速生成这些文件。

## 要求

### 1. 模板设计

创建一个模板系统，支持：

#### 变量替换

```markdown
使用 {变量名} 格式：

# .env.template
DATABASE_URL={database_url}
API_KEY={api_key}
DEBUG={debug_mode}
PORT={port}
```

#### 条件块

```markdown
使用 {{#if}} 条件：

{{#if use_redis}}
REDIS_URL=redis://localhost:6379
{{/if}}
```

#### 列表

```markdown
使用 {{#each}} 循环：

{{#each servers}}
SERVER_{@index}=#{this}
{{/each}}
```

### 2. 模板目录结构

```
config-generator/
├── SKILL.md
├── templates/
│   ├── .env.template
│   ├── config.json.template
│   ├── docker-compose.yml.template
│   └── nginx.conf.template
└── examples.md
```

### 3. 工作流程

```markdown
## 工作流程

### 第 1 步: 选择模板
询问用户要生成哪种配置：
1. .env (环境变量)
2. config.json (配置文件)
3. docker-compose.yml (Docker 编排)
4. nginx.conf (Nginx 配置)

### 第 2 步: 收集变量
根据模板需要的变量收集用户输入

### 第 3 步: 替换变量
将用户输入替换到模板中

### 第 4 步: 生成文件
将生成的内容写入文件

### 第 5 步: 验证
验证生成的文件格式正确
```

## 模板示例

### .env 模板

```markdown
# templates/.env.template

# Application
APP_NAME={app_name}
APP_ENV={environment}
DEBUG={debug}
PORT={port}

# Database
DATABASE_URL={database_url}
DATABASE_POOL_SIZE={pool_size}

# Redis
{{#if use_redis}}
REDIS_URL={redis_url}
REDIS_PORT={redis_port}
{{/if}}

# API
API_KEY={api_key}
API_SECRET={api_secret}

# Logging
LOG_LEVEL={log_level}
LOG_FILE={log_file}
```

### 变量收集

```markdown
## 收集变量

对于 .env 模板，需要以下变量：

### 必需变量
- app_name: 应用名称
- environment: 环境 (development/production)
- debug: 调试模式 (true/false)
- port: 端口号
- database_url: 数据库连接
- pool_size: 连接池大小
- api_key: API 密钥
- api_secret: API 密钥
- log_level: 日志级别
- log_file: 日志文件

### 可选变量
- use_redis: 是否使用 Redis (true/false)
- redis_url: Redis URL (如果 use_redis=true)
- redis_port: Redis 端口 (如果 use_redis=true)
```

### 替换逻辑

```markdown
## 变量替换

### 基本替换
{app_name} → MyApp

### 条件块
{{#if use_redis}}
REDIS_URL={redis_url}
{{/if}}

如果 use_redis = true：
REDIS_URL=redis://localhost:6379

如果 use_redis = false：
（整个块被移除）

### 列表
{{#each servers}}
SERVER_{@index}=#{this}
{{/each}}

如果 servers = ["server1", "server2", "server3"]：
SERVER_0=server1
SERVER_1=server2
SERVER_2=server3
```

## 实践练习

### 练习 1: 基础模板替换

创建一个简单的 .env 生成器：

```markdown
## 基本 .env 生成器

模板：
```

PORT={port}
HOST={host}
DEBUG={debug}

```

变量：
- port: 默认 3000
- host: 默认 localhost
- debug: 默认 false
```

### 练习 2: 添加条件逻辑

添加条件块：

```markdown
## 带条件的 .env 生成器

模板：
```

PORT={port}
{{#if use_database}}
DATABASE_URL={database_url}
{{/if}}
{{#if use_cache}}
CACHE_URL={cache_url}
{{/if}}

```

根据 use_database 和 use_cache 的值决定是否包含这些块
```

### 练习 3: 支持多种模板

支持生成多种配置文件：

- .env
- config.json
- .yaml
- .toml

每种格式有不同的模板和变量

## 提示

### 提示 1: 使用 Read 读取模板

```markdown
## 读取模板

1. 使用 Read 工具读取模板文件
2. 将内容存储在内存中
3. 准备变量替换
```

### 提示 2: 变量默认值

```markdown
## 默认值处理

为每个变量提供默认值：

| 变量 | 默认值 | 说明 |
|------|--------|------|
| port | 3000 | 应用端口 |
| host | localhost | 主机地址 |
| debug | false | 调试模式 |

如果用户不提供，使用默认值
```

### 提示 3: 验证生成的文件

```markdown
## 验证逻辑

生成后验证：

### JSON 格式
尝试解析 JSON，失败则报错

### YAML 格式
检查 YAML 语法

### 环境变量格式
检查 = 号，确保格式正确
```

### 提示 4: 提供预览

```markdown
## 生成预览

在写入文件前，先显示预览：

```text
# 生成的配置文件预览

PORT=3000
HOST=localhost
DEBUG=false
DATABASE_URL=postgresql://localhost/mydb
```

确认写入？(y/n)

```

## 输出格式

```markdown
# 配置文件生成完成

**文件**: .env
**位置**: /project/.env

## 生成的配置

```text
PORT=3000
HOST=localhost
DEBUG=false
DATABASE_URL=postgresql://localhost/mydb
```

## 下一步

1. 将 .env 添加到 .gitignore
2. 创建 .env.example 作为模板
3. 运行应用测试配置

```

## 验收标准

完成练习后，检查：
- [ ] 有清晰的模板系统
- [ ] 支持变量替换
- [ ] 支持条件块（可选）
- [ ] 有默认值机制
- [ ] 提供预览功能
- [ ] 验证生成的文件
- [ ] 有错误处理

## 延伸挑战

1. **添加模板继承**
   支持基础模板和扩展模板

2. **添加变量验证**
   验证变量类型和格式

3. **支持自定义模板**
   允许用户提供自己的模板

## 参考答案

完成练习后，可以查看 `solutions/intermediate/exercise-09.md` 对比参考答案。

## 相关资源

- [api-boilerplate 示例](../../skills/03-code-generation/api-boilerplate/)
- [test-generator 示例](../../skills/03-code-generation/test-generator/)
- [最佳实践：代码生成](../../docs/03-best-practices.md#代码生成)
