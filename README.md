# Daily Worklist Manager

Daily Worklist Manager 是一套基于 Markdown 文件持久化的工作流 skill，用于持续记录工作内容、维护长期记忆、动态排序优先级，并生成每日行动清单。

它适用于支持文件读写的 agent 环境。

## 能力概览
- 接收用户零散工作输入
- 区分 **背景** 与 **具体事项**
- 用 Markdown 文件维护长期记忆
- 随背景变化动态调整优先级
- 生成：
  - 今日必做 3 件事
  - 今日挑战完成 3 件事
  - “再给我一件事”建议
- 保留原始输入追溯记录

## 目录结构

```text
daily-worklist-manager/
├── SKILL.md
├── README.md
├── memory/
│   ├── background.md
    ├── tasks_active.md
    ├── tasks_archive.md
    ├── tasks_index.md
    ├── today.md
    └── inbox.md
└── templates/
    ├── background_template.md
    ├── task_template.md
    └── daily_template.md

## 核心记忆文件
- `memory/background.md`：背景总结，影响优先级判断
- `memory/tasks_active.md`：当前活跃任务，参与日常排序
- `memory/tasks_archive.md`：历史归档任务，默认不参与日常排序
- `memory/tasks_index.md`：任务总览摘要
- `memory/today.md`：每日计划视图
- `memory/inbox.md`：原始输入日志

## 长期使用原则
为控制长期 token 消耗与读取复杂度，Daily Worklist Manager 采用“活跃任务 / 归档任务 / 索引摘要”三层结构。

日常优先级判断默认只读取：
- background.md
- tasks_active.md
- tasks_index.md
- today.md

只有在需要查询历史时，才读取 tasks_archive.md。

本 skill 支持通过 snapshots/ + memory/changes.md 进行回滚