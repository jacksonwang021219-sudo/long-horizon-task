---
name: long-horizon-task
description: 组织并执行跨数小时或多会话的自主任务，持续落盘可信上下文并建设 Agent 友好的 topic 工作区。用户要求长程执行、离线期间自主探索、从现有记录续跑，或新建/改造 topic 目录时使用。
---

# long-horizon-task

面向两类任务：

1. 有明确交付与验收标准的复杂任务。
2. 用户长时间离线，由 Agent 自主探索并形成交付的研究任务。

## 选择方案

- 已有 topic：读取 [references/adopt-existing.md](references/adopt-existing.md)。
- 新建 topic：读取 [references/new-topic.md](references/new-topic.md)。

## 工作原则

1. 自主规划、排障和推进，尽量少打断用户。
2. 按需使用 subagent 管理复杂研究和上下文。
3. 优先读取工作区规则、topic/任务类型/单次任务 README，以及用户原始对话。自动 context summary 不作为可信依据。
4. 及时把阶段进展、结论和可复用经验写回对应 README。
5. 高成本步骤保存中间结果，支持断点续跑并避免重复计算。
6. 优先复用已有数据、脚本、模型、worker、领域 skill 和方法经验。
7. 交付前验证结果；探索得到负结果也可以是有效结论。
8. 如无必要不删除内容。

只有需求确实不清楚，或问题无法解决且用户可能知道捷径时，再询问用户。

## 目录约定

```text
<topic>/                              # git 仓库
  README.md                           # topic 须知
  <任务类型>/
    README.md                         # 类型须知
    _TEMPLATE/
    <单次任务>/
      README.md                       # 单次任务可信上下文
      *.py  *.sh                      # <10 MiB，整体入 git
  out/<任务类型>/<单次任务>/           # 可重算中间产物，不入 git
  raw/<任务类型>/<单次任务>/           # 不可重算原始落盘，不入 git
  state/  logs/                       # 断点状态、运行日志，不入 git
  shared/{DATA,METHOD}.md             # 跨类型共享，按需生长
```

目录可按 topic 实际情况调整。已有项目不为套模板而强制重排。

## 文档职责

- topic README：目录入口、共通知识和任务导航。
- 任务类型 README：该类型的流程、资源、约定和任务索引。
- 单次任务 README：任务定义、交付、进展、结论和接续位置。
- `shared/`：真正跨任务类型复用的数据知识与方法。

其他文档按需增加，不作强制要求。

## Git

- 入 git：README、共享知识、模板，以及单次任务下小于 10 MiB 的脚本。
- 不入 git：`out/`、`raw/`、`state/`、`logs/` 和其他大文件。
- 新 topic 先写 `.gitignore`，再生成数据。
- 已进入 git 历史的大文件只报告，不自动清理或改写历史。

## 边界

本 skill 负责工作区组织和长程上下文管理。具体数据、模型、评测、worker、飞书等操作继续使用对应领域 skill。
