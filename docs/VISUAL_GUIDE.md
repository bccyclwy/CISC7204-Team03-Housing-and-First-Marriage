# 视觉材料索引与使用说明

正文图01-09位于outputs_v2/figures，诊断图位于outputs_v2/appendix。每张图提供PNG及SVG。完整报告PDF在reports，六步汇报HTML在outputs_v2，可直接查看。

Notebook对下列15张图逐一以Markdown回答01设计准则、02真实性、03实用性、04美感、05洞察。外观只能帮助发现误导，无法证明数据真实；真实性还要核验来源、计算和不确定性。

课程Moodle的How Charts Lie PDF当前无法直接读取，不声称逐页遵循该PDF。可访问的Alberto Cairo本人访谈说明了truthful、functional、beautiful、insightful及enlightening；本Notebook据此和课程题目作具体评价，而不把封面样式当成统计正确性的保证。

参考：[Alberto Cairo访谈，Infogram，2016](https://infogram.com/blog/interview-alberto-cairo-and-the-truthful-art/)。

## 图表目录

- `figures/01_long_term_trends.png`：房价与初婚年龄的长期趋势
- `figures/02_annual_changes.png`：年度房价与初婚年龄变化
- `figures/03_age_group_shares.png`：男女初婚年龄组占比
- `figures/04_gender_age_gap.png`：男女初婚年龄中位数差
- `figures/05_same_year_scatter.png`：同期房价与初婚年龄变化
- `figures/06_lagged_scatter.png`：一年滞后关联
- `figures/07_regression_effect_sizes.png`：回归系数与HAC区间
- `figures/08_sensitivity_comparison.png`：不同窗口的效应与不确定性
- `figures/09_window_comparison.png`：研究窗口与相关系数矩阵
- `appendix/A02_change_series_acf.png`：变化量自相关
- `appendix/A03_age_share_associations.png`：年龄组变化的探索性相关
- `appendix/A04_diagnostics_male_same_year.png`：男性同期回归诊断
- `appendix/A04_diagnostics_male_lag1.png`：男性一年滞后回归诊断
- `appendix/A04_diagnostics_female_same_year.png`：女性同期回归诊断
- `appendix/A04_diagnostics_female_lag1.png`：女性一年滞后回归诊断