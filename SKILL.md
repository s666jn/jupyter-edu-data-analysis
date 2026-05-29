---

## name: jupyter-edu-data-analysis

description: >-
  Guides course-style Jupyter data analysis reports (read/clean, EDA, group
  comparisons, optional correlation and hypothesis tests, synthesized
  conclusions). Applies robust trimming for mean-based summaries
  (typically df_robust via per-score-column quantile bands), minimal chart
  count, matplotlib Chinese font setup, and careful wording on correlation
  vs causation and confounding. Load only when the user @-mentions this skill
  by name (jupyter-edu-data-analysis).
disable-model-invocation: true

# 课程级 Jupyter 数据分析报告

## 何时启用

**仅在用户通过 @ 引用本技能时出现**（技能名：`jupyter-edu-data-analysis`）。不要在未被 @ 的对话里主动套用本 skill。

适用场景：撰写或修改 **作业/实验 Jupyter**、教育类 **CSV**、**EDA → 对比 →（可选）相关/检验 → 结论** 类报告。

## 推荐章节骨架（可按作业删减）

1. 数据读取与字段理解（规模、类型、缺失、合理范围）
2. **EDA**：描述统计 + **少量**互补图形（如分布 + 箱线图）
3. **对比分析**：分组均值/箱线图；类别结构可用 **单图多行 100% 堆积条** 代替多张饼图
4. **（加分）关系分析**：Pearson 矩阵 + **一张**热力图；注明相关≠因果
5. **（加分）检验**：独立样本 **Welch t**（`equal_var=False`）等；注明多重比较（如 Bonferroni）
6. **综合结论**：3–5 条，**重要性递减**；每条能指回图表或数值

## 稳健样本 df_robust（均值类图表 / 检验）

- 对「分数」列分别算全样本 **分位数（quantile）**，常用 **1%～99%**。
- **保留**三门（或作业规定的数值列）**同时落在各自区间内**的行 → `df_robust`。
- 在 `df_robust` 上 **重算**派生列（如 `average total score`）。
- **样本构成 / 人数占比**若题目要求描述总体结构，可用 **全样本 `df`**，与稳健推断口径区分开。
- 结论 Markdown 中简短交代剔除规则与剩余 **n**。

## 图表原则

- **优先**：分析到位；其次 **图少而典型**（分组柱、箱线、热力图、单行堆积结构条）。
- 总体追求美观。浮动标注（图例、注释框）避免挡柱条：**靠下或下角**，或与用户约定位置。
- 需要保存矢量图时：`plt.savefig(..., bbox_inches="tight")`；路径与前几节一致。
- 能用简洁代码，优先简洁，如用seaborn。

## Matplotlib 中文与缺字

- 设置 `plt.rcParams["axes.unicode_minus"] = False`。
- `font.sans-serif`：优先 **Microsoft YaHei / SimHei / KaiTi** 等；可用 `matplotlib.font_manager` 在已注册字体中选首个命中。
- Seaborn 主题在字体设置 **之前** 调用，顺序不可换，否则中文显示出错。
- 正确示例
  ```python
  #配置sns背景，再配置中文字体，顺序不可换，否则中文显示出错
  sns.set_theme(style="whitegrid")

  matplotlib.rcParams['font.family'] = 'sans-serif'
  matplotlib.rcParams['font.sans-serif'] = ['SimHei', 'Microsoft YaHei', 'WenQuanYi Micro Hei']
  matplotlib.rcParams['axes.unicode_minus'] = False
  ```

## 统计表述边界（必须在结论中体现）

- **相关≠因果**；观测数据慎谈干预效果。
- **备考 / 培训**等「自选」分组：提示 **自选择偏差（self-selection）**。
- **性别 / 民族等差异**：显著性≠机制解释；提醒混杂（家庭背景等）。

## 代码习惯（中文课程）

- **代码注释使用中文**；技术术语首次出现可中英并列。
- 用户对回复语言有规则时（如简体中文），遵守用户规则。

## 交付检查

- 稳健口径与全样本口径未混用误读  
- 结论数字与 `display`/图一致  
- 加分项（相关、检验）若缺依赖（如 scipy），`try/except` + `pip` 提示

更多篇幅的技能说明拆到单独 reference，本文件保持简短。