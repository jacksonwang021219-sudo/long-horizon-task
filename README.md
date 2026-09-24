# long-horizon-task

用于组织跨数小时、多会话 Agent 任务的 Skill。通过持续记录任务目标、进展、结论和接续位置，让后续会话能够找到依据、复用已有结果并继续推进。

## 适用场景

- 复杂任务有明确交付物与验收标准，需要分阶段执行。
- 研究任务需要长期探索，并保留可核验的阶段结论。
- 接手已有项目，需要补充目录导航、任务记录与共享知识。
- 新建主题工作区，希望从第一次任务开始保留可接续的上下文。

## 安装到 Codex

需要已登录 GitHub CLI，并具有本仓库的访问权限。在终端运行：

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
gh repo clone jacksonwang021219-sudo/long-horizon-task \
  "${CODEX_HOME:-$HOME/.codex}/skills/long-horizon-task"
```

目标目录须不存在。若已经安装此 Skill，请先确认现有版本及本地改动。安装后，在下一条 Codex 消息中调用它。

## 使用示例

整理已有项目：

```text
使用 $long-horizon-task 整理这个项目，补充目录导航、任务目标、
当前进度、交付物和验收标准，让后续会话可以继续推进。
```

推进一项长任务：

```text
使用 $long-horizon-task 完成这项研究。先明确范围和验收标准，
分阶段保存中间结果，并持续记录关键结论、证据和下一步。
```

接续已有任务：

```text
使用 $long-horizon-task，读取这个项目及对应任务的 README，
核对已有产物和断点状态，从记录的下一步继续。
```

## 工作方式

1. 读取工作区规则、项目与任务 README，以及用户原始要求。
2. 明确交付物、验收方法和当前接续位置。
3. 执行过程中保存中间结果，并及时更新任务记录。
4. 将可复用的数据知识和方法沉淀到共享文档。
5. 交付前核验结果，记录验收结果与尚未解决的问题。

Skill 提供工作流程和目录模板。持续执行依赖 Agent 的运行环境；包内没有后台服务、定时调度器或自动恢复进程。数据、模型、评测、飞书等具体操作仍使用对应领域的工具或 Skill。

## 仓库结构

```text
long-horizon-task/
├── SKILL.md                     # Agent 读取的技能入口
├── references/
│   ├── new-topic.md             # 新建主题工作区
│   └── adopt-existing.md        # 接手或改造已有工作区
├── assets/templates/
│   ├── topic-README.md          # 主题导航模板
│   ├── type-README.md           # 任务类型模板
│   ├── task-README.md           # 单次任务记录模板
│   └── gitignore.sample         # 工作区忽略规则模板
├── README.md                    # 安装与使用说明
├── SOURCE.md                    # 来源与维护说明
└── source-manifest.json         # 原始文件的大小与 SHA-256
```

详细规则见 [SKILL.md](SKILL.md)。使用本技能产生的研究数据、运行日志和任务产物应保存在实际任务的工作区。

## 来源与维护

本仓库归档用户提供的 `long-horizon-task.zip`，原始 7 个技能文件保持原样。作者与上游仓库尚未确认，原压缩包未附带许可证；本次整理没有追加作者归属或开放许可声明。

来源记录与校验方式见 [SOURCE.md](SOURCE.md)。
