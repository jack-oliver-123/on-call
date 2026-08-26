# Issue tracker：GitHub

本仓库的执行与协作事项存放在 GitHub Issues。需求和验收要求仍以 OpenSpec 为准，不在 Issue 中维护第二套独立规格。所有操作使用 `gh` CLI。

## 常用操作

- 创建：`gh issue create --title "..." --body "..."`
- 长正文：使用 UTF-8 临时文件并传入 `--body-file`
- 读取：`gh issue view <number> --comments`
- 列表：`gh issue list --state open --json number,title,body,labels,comments`
- 评论：`gh issue comment <number> --body "..."`
- 添加标签：`gh issue edit <number> --add-label "..."`
- 移除标签：`gh issue edit <number> --remove-label "..."`
- 关闭：`gh issue close <number> --comment "..."`

在仓库克隆目录中运行命令，由 `gh` 根据 `git remote -v` 自动确定仓库。

## Pull requests 作为 triage 入口

**PRs as a request surface: no.**

若以后改为 `yes`，外部 PR 使用同一套标签和状态，并通过 `gh pr` 命令处理。GitHub Issues 与 PR 共用编号；遇到 `#42` 等裸编号时，先运行 `gh pr view 42`，失败后再运行 `gh issue view 42`。

## Skill 术语

当 skill 要求“发布到 issue tracker”时，创建 GitHub Issue。

当 skill 要求“获取相关 ticket”时，运行：

`gh issue view <number> --comments`

## Wayfinding 操作

`/wayfinder` 使用一个 map Issue 和多个 child Issue：

- Map：使用 `wayfinder:map` 标签，正文保存 Notes、Decisions-so-far 和 Fog。
- Child ticket：优先使用 GitHub sub-issue；不可用时，在 map 中添加任务列表，并在 child 正文顶部写入 `Part of #<map>`。
- 类型标签：使用 `wayfinder:research`、`wayfinder:prototype`、`wayfinder:grilling` 或 `wayfinder:task`。
- 阻塞关系：优先使用 GitHub 原生 issue dependencies；不可用时，在正文顶部写入 `Blocked by: #<n>`。
- Frontier：从 map 的未关闭 child 中排除仍有开放 blocker 或已有 assignee 的事项，按 map 顺序选择第一项。
- Claim：`gh issue edit <n> --add-assignee @me`。
- Resolve：评论结论、关闭 child，并把上下文链接追加到 map 的 Decisions-so-far。
