# CISC7204 Team 03 香港房价变化与初婚模式

本提交包含可复现的六步年度数据分析、完整数据、带图表评价Markdown的已执行Notebook、代码手册、图表及完整PDF报告。研究期为1997-2025年；1995-1996年仅用作差分和滞后计算基期。提交材料整理日期为2026-11-26，数据固定为2026-11-06下载快照，没有将整理日期当作新的数据下载日期。

## 交付要求与入口

| 要求 | 文件与目录 |
|---|---|
| 1 README与安装指南 | 本文件、requirements.txt |
| 2 完整数据集及描述 | data/raw/、data/processed/、data/README.md、data/variable_dictionary.csv、research/source_register_v2.json |
| 3 Jupyter Notebook | Housing_Marriage_Analysis.ipynb，已执行并保留图表输出 |
| 4 代码手册 | docs/CODE_MANUAL.md、analysis/、research/prepare_data_v2.py |
| 5 视觉辅助材料 | reports/Full_Analysis_Report_V2.pdf、outputs_v2/figures/、outputs_v2/appendix/、outputs_v2/汇报版_六步主线.html、docs/VISUAL_GUIDE.md |
| 6 完整项目文件夹 | 解压后只有一个CISC7204_Team03_Submission顶层目录 |
| 7 公共GitHub仓库 | GitHub_URL.txt及本README中的仓库链接 |

第7项公共GitHub仓库：[https://github.com/bccyclwy/CISC7204-Team03-Housing-and-First-Marriage](https://github.com/bccyclwy/CISC7204-Team03-Housing-and-First-Marriage)。仓库归属账号为bccyclwy。

## 不安装也能查看

直接打开reports/Full_Analysis_Report_V2.pdf，或outputs_v2/分析结果报告_v2.html。reports/Notebook_Reading_Copy.html提供Notebook的离线阅读副本，包含全部Markdown和已执行图表；它不替代IPYNB。HTML已内嵌图表；Notebook保留运行结果。在GitHub或Jupyter中打开Notebook，可以看到每张图对应的01-05五项Markdown评价。

## 安装 Python 3.12

推荐Python 3.12，下面所有命令均在解压后的项目根目录执行。路径包含空格时请用引号包住目录。

macOS / Linux：

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m ipykernel install --prefix .venv --name cisc7204 --display-name "Python CISC7204"
python -m jupyterlab
```

Windows PowerShell：

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m ipykernel install --prefix .venv --name cisc7204 --display-name "Python CISC7204"
python -m jupyterlab
```

打开Housing_Marriage_Analysis.ipynb，选择Python CISC7204内核，执行Restart Kernel and Run All。首个计算单元定位项目根目录；后续单元先重建年度数据，再生成统计表和全部图形。依赖安装后，分析不需要网络、API密钥、GitHub登录或Moodle账号。

## 命令行复现

```bash
python research/prepare_data_v2.py
python analysis/run_analysis_v2.py
python analysis/build_report_v2.py
```

这会从包内原始文件重新生成年度表、9张主图、6张附图、主回归和敏感性结果CSV，以及HTML报告。已有PDF是报告快照，不会由这三条命令自动重新排版。不要把未执行Notebook的静态输出误认为刚刚执行成功。

执行验证：

```bash
python analysis/validate_v2.py
```

验证会检查原始文件哈希、年度变量、并列值、样本范围、相关系数、p值调整和已执行Notebook结构。详细检查结果见outputs_v2/appendix/validation_summary.json；本次提交整理的检查结果另见SUBMISSION_CHECK.json。

## 研究结论与限制

初婚年龄中位数上升，25-29岁初婚占比下降、30-34岁占比上升。短期房价关联对性别、时间设定和研究窗口敏感。四个主要HAC回归经Holm调整后均未达到5%显著水平；结果描述年度汇总关联，不作因果判断。所有结果及敏感性设定均保留，未按显著性选择研究窗口。

## 常见问题

- 找不到文件：先完整解压，不要直接在ZIP内运行Notebook；从项目根目录启动Jupyter。
- 缺少模块：确认所选Notebook内核属于安装了requirements.txt的环境。
- 房价XLS无法读取：分析读取包内research/rvd_price_indices.xlsx，它是原始XLS的读取副本，不需要本机安装LibreOffice。
- 图表含英文：用于课程汇报，中文解读在Notebook和报告内；五项视觉评价使用Markdown而不是图片内文字。
- 使用不同数据版本：不要自动替换原始数据。先记录来源及日期，再重新执行全部分析，旧结果不可混用。


## 公共仓库

https://github.com/bccyclwy/CISC7204-Team03-Housing-and-First-Marriage

```bash
git clone https://github.com/bccyclwy/CISC7204-Team03-Housing-and-First-Marriage.git
cd CISC7204-Team03-Housing-and-First-Marriage
```

后续安装与复现步骤与上文相同。仓库发布内容与提交文件夹一致，不包含本机虚拟环境、缓存或身份验证信息。
