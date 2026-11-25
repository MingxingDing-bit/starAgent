# GitHub 工作流指南

本文件记录 `starAgent` 项目如何上传到 GitHub，以及后续日常代码提交的相关命令。

> 仓库信息：可见性 `Public`，仓库名 `starAgent`，默认分支 `main`，使用 SSH 协议。

## 前置条件

- 已在本机配置好 GitHub SSH 私钥（用于 push/pull 免密）
- 已安装 `gh` CLI（用于创建仓库、管理 issue/PR 等）

## 一、首次初始化（一次性操作，只需做一次）

### 1. 登录 gh CLI

在终端中运行（交互式，会引导你通过浏览器或 token 完成认证）：

```bash
gh auth login
```

按提示选择：`GitHub.com` → 协议选 `SSH` → 认证方式选浏览器或粘贴 token。

验证登录成功：

```bash
gh auth status
```

### 2. 设置 git 使用 SSH 协议

让 `gh` 在生成远程地址时优先使用 SSH（配合已配置的 SSH 私钥）：

```bash
gh config set git_protocol ssh
```

验证：

```bash
gh config get git_protocol   # 应输出 ssh
```

可选：验证 SSH 连接是否正常

```bash
ssh -T git@github.com
```

### 3. 创建 `.gitignore`（忽略不应提交的本地文件）

在项目根目录新建 `.gitignore`，内容建议包含：

```
# IDE
.idea/

# 本地 Claude 配置（含本地权限，不应提交）
.claude/settings.local.json

# Python
__pycache__/
*.py[cod]
.venv/
venv/
```

### 4. 首次提交（本地）

当前仓库还没有任何 commit，需要先提交一次：

```bash
git add .
git commit -m "chore: 初始化项目"
```

### 5. 创建远程仓库并推送

在项目根目录执行（会同时完成：在 GitHub 建仓、添加 `origin` 远程、推送当前分支）：

```bash
gh repo create starAgent --public --source=. --remote=origin --push
```

若上面一步未自动推送成功，可分步执行：

```bash
gh repo create starAgent --public --source=. --remote=origin
git push -u origin main
```

> `-u`（即 `--set-upstream`）会把本地 `main` 与远程 `origin/main` 关联，之后日常推送只需 `git push`。

---

## 二、日常提交工作流（每次改动后都这样做）

```bash
# 1. 查看当前有哪些改动
git status

# 2. 暂存改动（. 表示当前目录全部改动；也可指定文件）
git add .

# 3. 提交，附上说明
git commit -m "描述本次改动"

# 4. 推送到 GitHub
git push
```

合并成一条的常见写法：

```bash
git add . && git commit -m "描述本次改动" && git push
```

> 提交信息建议能概括"做了什么、为什么"，例如：`feat: 新增用户登录接口`、`fix: 修复列表分页错误`。

---

## 三、常用命令速查

| 目的 | 命令 |
| --- | --- |
| 查看改动状态 | `git status` |
| 查看提交历史 | `git log --oneline` |
| 查看远程地址 | `git remote -v` |
| 拉取远程更新 | `git pull` |
| 查看/切换分支 | `git branch` / `git checkout -b <分支名>` |
| 查看某次改动详情 | `git diff`（未暂存）/ `git diff --staged`（已暂存） |
| 撤销未提交的改动 | `git restore <文件>` |

---

## 四、注意事项

- **首次**必须用 `git push -u origin main` 建立关联；之后日常直接 `git push` 即可。
- `.idea/` 与 `.claude/settings.local.json` 属于本机状态/配置，不要提交；`.gitignore` 已覆盖。
- 若推送前远程已有他人更新，先 `git pull`（或 `git pull --rebase`）再 `git push`。
