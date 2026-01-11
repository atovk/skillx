# Git 提交信息模板

这是一个标准的 Git 提交信息模板，遵循[约定式提交](https://www.conventionalcommits.org/)规范。

## 格式

```
<type>(<scope>): <subject>

<body>

<footer>
```

## 类型 (type)

| 类型 | 说明 | 示例 |
|------|------|------|
| `feat` | 新功能 | feat(api): add user endpoint |
| `fix` | 修复 bug | fix(ui): resolve button spacing |
| `docs` | 文档变更 | docs: update README |
| `style` | 代码格式（不影响功能） | style: format code with prettier |
| `refactor` | 重构 | refactor(auth): simplify login flow |
| `perf` | 性能优化 | perf(cache): implement memoization |
| `test` | 添加测试 | test(api): add integration tests |
| `chore` | 构建或辅助工具变更 | chore: update dependencies |

## 范围 (scope)

范围说明变更影响的模块：

- `api` - API 相关
- `ui` - 用户界面
- `auth` - 认证相关
- `db` - 数据库
- `config` - 配置文件
- `build` - 构建系统

## 描述 (subject)

- 使用现在时态："add" 而不是 "added" 或 "adds"
- 首字母小写
- 不要以句号结尾
- 限制在 50 个字符以内

## 正文 (body)

- 说明"是什么"和"为什么"，而不是"怎么做"
- 每行限制在 72 个字符以内
- 使用列表列出关键变更点

## 页脚 (footer)

- 关联 issue：`Closes #123` 或 `Fixes #456`
- 破坏性变更：`BREAKING CHANGE: API endpoint changed`

## 示例

### 完整示例

```
feat(auth): implement OAuth2 login

- Add Google OAuth2 provider
- Implement token refresh logic
- Add user profile synchronization
- Update authentication middleware

Closes #789
```

### 简单示例

```
fix(ui): correct button alignment

Fixes #456
```

### 破坏性变更

```
feat(api): change user endpoint response format

BREAKING CHANGE: User endpoint now returns nested object
instead of flat structure. Update all consumers.
```
