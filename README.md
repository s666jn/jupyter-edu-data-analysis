# jupyter-edu-data-analysis

面向 **课程 / 作业级 Jupyter 数据分析报告** 的 Cursor Agent Skill：规范章节顺序、稳健样本（`df_robust`）、少而典型的图表、Matplotlib 中文缺字处理，以及结论中的统计表述边界（相关≠因果等）。

## 技能标识

| 字段 | 值 |
|------|-----|
| **name**（技能 slug） | `jupyter-edu-data-analysis` |
| **入口文件** | `SKILL.md` |
| **自动唤起** | 已关闭（`disable-model-invocation: true`） |

## 安装位置（当前）

本仓库为 **个人技能**，默认路径：

`~/.cursor/skills/jupyter-edu-data-analysis/`

（Windows 下多为 `C:\Users\<用户名>\.cursor\skills\jupyter-edu-data-analysis\`。）

若要 **随项目共享**，可将整个文件夹复制到仓库：

`.cursor/skills/jupyter-edu-data-analysis/`

## 如何使用

1. 在 Cursor 对话中通过 **@** 菜单引用技能，选择 **`jupyter-edu-data-analysis`**（或与 Cursor 列表中显示的名称一致的一项）。
2. 说明你的作业要求：数据集路径、必做小节、是否加分项（相关 / 检验）、图表与结论偏好等。
3. Agent 将按 `SKILL.md` 中的骨架与约束协助改 notebook / 写结论；**未被 @ 时不会依赖本 skill 自动挂载**。

## 文档说明

- **`SKILL.md`**：给 Agent 阅读的完整指令（YAML frontmatter + Markdown 正文）。
- **`README.md`**（本文件）：给人看的安装与使用说明。

## 可选依赖

报告中若含 Pearson p 值、Welch t 检验等，建议在环境中安装 **scipy**；Skill 内建议对缺失依赖做 `try/except` 并提示 `pip install scipy`。

## 维护

修改行为时请编辑 **`SKILL.md`**；更新安装说明或人与仓库协作流程时编辑 **`README.md`**。
