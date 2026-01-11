# Git 提交助手 - 使用示例

这里展示 `git-commit-helper` Skill 的使用场景和输出示例。

## 使用场景

### 场景 1：新功能提交

**运行命令**：

```bash
git-commit-helper
```

**变更内容**：

- 添加了新的用户认证 API
- 修改了 `src/api/auth.js`
- 添加了 `src/middleware/auth.js`

**生成的提交信息**：

```
feat(api): add user authentication endpoint

- Add POST /api/auth/login endpoint
- Implement JWT token generation
- Add authentication middleware
- Add input validation for credentials

Closes #123
```

---

### 场景 2：Bug 修复

**运行命令**：

```bash
git-commit-helper
```

**变更内容**：

- 修复了登录表单验证错误
- 修改了 `src/components/LoginForm.js`

**生成的提交信息**：

```
fix(ui): correct form validation in login

- Fix email validation regex pattern
- Fix password minimum length check
- Add proper error messages for invalid inputs

Fixes #456
```

---

### 场景 3：文档更新

**运行命令**：

```bash
git-commit-helper
```

**变更内容**：

- 更新了 README.md
- 添加了 API 文档
- 更新了 CONTRIBUTING.md

**生成的提交信息**：

```
docs: update project documentation

- Update README with new installation instructions
- Add comprehensive API documentation
- Update contribution guidelines
- Fix typos in getting started guide
```

---

### 场景 4：重构代码

**运行命令**：

```bash
git-commit-helper
```

**变更内容**：

- 重构了数据处理逻辑
- 提取了通用函数到 utils/
- 修改了 `src/utils/data.js`

**生成的提交信息**：

```
refactor(utils): extract data processing functions

- Extract common data transformation logic
- Create reusable utility functions
- Improve code readability
- No functional changes
```

---

## 交互流程示例

### 完整对话

**用户**：`git-commit-helper`

**Assistant**：

```markdown
# 建议的提交信息

```

feat(auth): implement OAuth2 integration

- Add Google OAuth2 provider
- Implement token refresh logic
- Add user profile sync
- Update authentication middleware

Closes #789

```

## 分析结果

**变更文件**：
- src/auth/oauth.js (new)
- src/auth/providers/google.js (new)
- src/middleware/auth.js (modified)
- package.json (modified - added dependencies)

**变更类型**：feat
**影响范围**：auth
**变更摘要**：实现 Google OAuth2 登录功能

---

是否确认使用这个提交信息？或者你想修改它？
```

**用户**：确认，但是把 Closes #789 改成 Closes #790

**Assistant**：

```markdown
好的，更新后的提交信息：

```

feat(auth): implement OAuth2 integration

- Add Google OAuth2 provider
- Implement token refresh logic
- Add user profile sync
- Update authentication middleware

Closes #790

```

正在提交...
```

[执行 git commit]

```

---

## 最佳实践

### 1. 提交前检查

在运行 `git-commit-helper` 前，确保：
- 已通过 `git add` 添加需要提交的文件
- 变更已经过测试
- 提交信息准确反映变更内容

### 2. 修改提交信息

如果生成的提交信息不完美，你可以：
- 直接告诉 AI 需要修改的地方
- 例如："把类型改成 fix"、"添加更多细节"

### 3. 提交信息模板

你也可以参考 [commit-template.md](templates/commit-template.md) 了解提交信息的最佳实践。

---

## 常见问题

### Q: 如果我只想提交部分文件怎么办？

**A**：在运行 Skill 前，使用 `git add` 只添加需要提交的文件：
```bash
git add src/api/auth.js
git-commit-helper
```

### Q: 如何修改已提交的信息？

**A**：如果提交还没有推送到远程，可以使用：

```bash
git commit --amend
```

### Q: 可以跳过确认直接提交吗？

**A**：当前版本的 Skill 总是会要求确认。这可以防止意外提交。如果需要自动化，可以修改 Skill 添加一个 `--yes` 选项。

---

## 相关资源

- [约定式提交规范](https://www.conventionalcommits.org/)
- [如何写好 Git 提交信息](https://chris.beams.io/posts/git-commit/)
