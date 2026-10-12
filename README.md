# 我的共享技能库

统一维护 Codex、Kimi Code 等本地 Agent 可复用的技能。

## 目录

- `skills/`：共享技能，每项使用 `skills/<name>/SKILL.md`。
- 技能可以包含 `scripts/`、`references/`、`assets/`。
- 产品内置技能、插件缓存、账号凭据不纳入本仓库。

## 本机配置

仓库：`C:\Users\Randall\Documents\agent-skills`

共享入口：`C:\Users\Randall\.agents\skills`

共享入口通过 Windows 目录联接指向仓库的 `skills` 文件夹，修改任意入口都会修改同一份文件。

Codex 支持用户级 `~/.agents/skills`。Kimi Code 也支持这个目录；若存在 `~/.config/agents/skills`，或有自定义技能配置，需要检查其目录优先级。网页版和远程环境需要单独导入或克隆。

## 新建技能

创建 `skills/my-skill/SKILL.md`，内容示例：

```markdown
---
name: my-skill
description: 清楚说明技能解决什么任务，以及何时使用。
---

# 任务

说明目标、需要的输入、操作步骤和交付要求。
```

使用唯一名称和相对路径。通用步骤避免绑定某一产品的工具名；产品专用能力分别适配。新增技能后开启新会话确认是否发现。

## 同步到 GitHub

在仓库目录执行：

```powershell
git status
git add skills README.md
git commit -m "Update shared skills"
git push
```

在其他设备修改前执行 `git pull --ff-only`。GitHub 同步是手动的，本机目录联接即时生效。

## 在另一台 Windows 电脑连接

先克隆仓库，然后建立共享入口（目标入口必须不存在，已有目录需先检查合并，不能直接覆盖）：

```powershell
gh repo clone Rundong-Lee/agent-skills "$env:USERPROFILE\Documents\agent-skills"
New-Item -ItemType Directory -Path "$env:USERPROFILE\.agents" -Force
New-Item -ItemType Junction -Path "$env:USERPROFILE\.agents\skills" -Target "$env:USERPROFILE\Documents\agent-skills\skills"
```

## 参考

- [Codex 技能文档](https://learn.chatgpt.com/docs/build-skills)
- [Kimi Code 技能文档](https://moonshotai.github.io/kimi-cli/en/customization/skills.html)
