# PROGRESS · starAgent 〔本项目活记忆 · 状态机〕

> **作用**:这是项目的“存档点”。任意 AI、任意重启会话,读它即可知道当前做到哪、下一步做什么、踩过什么坑。
> **更新时机**:每完成一个有意义步骤、每次会话结束前。
> **格式要求**:时间倒序,最新在上;短、准、可接力。

---

## 当前状态 (最后更新: 2026-11-25 · by zjdmx)

- **阶段**:`初始化`
- **上一步完成**:`适配 standards 为本地+GitHub 模式；建好 .gitignore / CLAUDE.md / GIT_WORKFLOW.md`
- **下一步 (TODO 第一条)**:`创建 GitHub 仓库 starAgent（public）并首次推送 main`
- **阻塞项**:`无`

---

## 待办清单 (TODO,按优先级)

- [ ] 创建 GitHub 仓库并首次推送 main
- [ ] 初始化项目上下文:`00-project-context.md`（补全项目目标、功能）
- [ ] 确认需求与验收标准:`01-requirements.md`
- [ ] 从 `main` 开第一条 feature 分支
- [ ] 实现代码与测试
- [ ] 本地自检通过
- [ ] 提交并推送 feature 分支
- [ ] 创建 PR,等待 CI
- [ ] CI 全绿后合并 main
- [ ] 会话结束前更新本文件

---

## 关键决策记录 (ADR)

| 日期 | 决策 | 理由 |
|---|---|---|
| 2026-11-25 | 部署模式为「本地 + GitHub」两端，无服务器、无 CD | 项目现阶段仅本地开发 + GitHub 托管 |
| 2026-11-25 | git 协议用 HTTPS（gh token 免密） | gh 已登录且协议为 https，无需额外配置 |
| 2026-11-25 | 仓库 public、名 starAgent | 用户确认 |

---

## 已知坑 (GOTCHAS)

- 无。

---

## 里程碑 (DONE)

- [x] 适配 standards 为本地+GitHub 模式（标注服务器/CD/Secrets 暂不适用）
- [x] 创建 `.gitignore`（忽略 .idea/、.claude/settings.local.json、Python 缓存）
- [x] 生成 `GIT_WORKFLOW.md`（上传与日常提交命令指南）

> 反臃肿:里程碑超过 15 条时,把更早内容合并成一行摘要,保持本文件可快速阅读。
