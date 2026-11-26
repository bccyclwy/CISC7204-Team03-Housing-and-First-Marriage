# 代码手册

## 六步计算链

1. research/prepare_data_v2.py读取原始JSON和房价读取副本，标准化年份，筛选官方指标，核验重复键与初婚人数总数，先保留1995-1996，再计算差分与滞后，最后截取1997-2025。
2. analysis/run_analysis_v2.py中的load_data()检查29年数据；descriptive()输出样本标准差等描述统计；trend_figures()生成水平和年度变化图。
3. structure()生成年龄组占比、男女年龄差，并区分首次交叉年份和此后持续交叉年份。
4. association()对两个初婚年龄变化及四个年龄组占比变化分别估计同期和一年滞后模型。fit_hac()是核心回归函数。
5. diagnostics()输出ADF、KPSS、ACF、Ljung-Box、Breusch-Godfrey、Breusch-Pagan和Cook距离。
6. sensitivity()输出完整样本、去掉1997、2004年后、2020年前、疫情剔除、HAC带宽0/1/2及逐年剔除。supplements()输出固定长度环形区块Bootstrap和窗口比较图。

## 核心模型与推断

同期：Delta A_t = alpha + beta*g_t + error_t。
滞后：Delta A_t = alpha + beta*g_(t-1) + error_t。

分别拟合，不把两者系数解释为相互控制后的效应。没有加入未取得的控制变量。beta单位是房价涨幅每增加1个百分点对应的初婚年龄年度变化；报告主要换算成10个百分点。

采用OLS和Bartlett HAC(1)，n/(n-k)修正，t(n-k)逐模型区间。完整样本n=29、k=2。HAC按真实日历年距离计算，缺年后不压缩间隔；连续样本的协方差与statsmodels实现交叉验证。四个主要模型作Holm调整，八个年龄组模型作BH调整；两个探索性性别斜率差对比另作Holm调整。普通相关的iid p值只作参考。

年龄差分按原始0.1岁精度恢复并列值，避免浮点相减人为打破相同增幅的排名。年龄组占比不按显示的一位小数舍入后再计算。

## 稳健性与解释

所有窗口先计算连续年份的差分/滞后，再筛选。严格疫情剔除检查年龄差和房价差所需的每个原始年份；同期n=25、滞后n=24。影响点保留在主样本，逐年剔除只用于诊断。Bootstrap以2/3/4年环形区块对年度配对成对重抽样10000次，固定种子20261106，相关区间不作多重比较调整。

HAC区间是回归斜率区间，Bootstrap区间是相关系数区间，不是同一程序。没有进行因果识别、复杂预测或通过反复选择窗口追求显著结果。

## Notebook结构

Housing_Marriage_Analysis.ipynb内嵌分析函数定义，并按六步调用。计算和图表解读分开。15张用于正文或诊断的图均单独显示，紧邻Markdown单元按01-05说明设计、真实性、实用性、美感和洞察，包含数据核验方式与可见图形不能证明的内容。

## 输出与验证

outputs_v2/tables包含主要数值结果；appendix包含诊断及完整敏感性结果；figures同时导出PNG与SVG。PNG便于直接插图，SVG便于后续编辑。analysis/validate_v2.py从原始数据独立复核核心数值和已执行Notebook。SUBMISSION_CHECK.json核对Notebook与本次六项交付要求的对应。

## 方法参考

- statsmodels HAC：https://www.statsmodels.org/stable/generated/statsmodels.regression.linear_model.RegressionResults.get_robustcov_results.html
- SciPy并列排名：https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.rankdata.html
- arch环形区块Bootstrap：https://bashtage.github.io/arch/bootstrap/generated/arch.bootstrap.CircularBlockBootstrap.html


## 本次测试环境

本次在macOS arm64的独立Python 3.12虚拟环境中按requirements.txt安装，并实际执行24个代码单元。详细版本见SUBMISSION_CHECK.json及TESTED_ENVIRONMENT_FREEZE.txt。冻结清单记录本次平台，不作为跨平台安装清单；Windows请使用README及requirements.txt，未声称已在Windows实测。
