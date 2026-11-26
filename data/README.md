# 数据集说明

## 原始数据

- raw/rvd_price_indices.xls：香港差饷物业估价署私人住宅各类单位售价指数原文件。选择Annual年表、All Classes；基期1999=100；年表覆盖1980-2025。原表说明住宅首次买卖不用于该指数分析。
- raw/115-01011.json：统计处Vital events完整API响应，选择sv=MED_AGE_1STM、SEX=M/F，单位岁。完整表覆盖1961-2025，但各指标的早期可用年份可能不同。
- raw/115-01013.json：按性别和年龄组划分的初婚人数完整API响应，覆盖1986-2025；单位人而不是夫妻对数。
- ../research/rvd_price_indices.xlsx：原始XLS转换后的读取副本，原XLS未更改。列的选择及字段代码在准备脚本中明示。

## 处理数据

processed/annual_1997_2025_v2.csv包含29行，一行一个日历年。outputs_v2/annual_analysis_data.csv进一步加入男女初婚年龄差及其变化。完整字段说明见data/variable_dictionary.csv（包含年份和额外性别差值字段）；原准备脚本字典见research/variable_dictionary_v2.csv。

年度房价变化=100*(P_t/P_(t-1)-1)，单位%。初婚年龄变化=A_t-A_(t-1)，单位岁，并恢复0.1岁精度以正确处理Spearman并列值。初婚年龄组占比=100*该组人数/同年同性别所有初婚人数，占比变化用百分点。占比不是同龄人口初婚率。

1995-1996仅作计算前置值，不增加主样本观察年数。同期与一年滞后均为1997-2025的29组配对。原始年表和JSON完整保留，能够重建所需前置值，无须外部补数。

## 来源、版本和完整性

快照下载日为2026-11-06。URL、官方说明和SHA256见research/source_register_v2.json。本次2026-11-26整理提交时没有更新数据。所选字段无缺失，不插值，不人为删除影响点。所有年龄组人数加总与同性别官方总计一致。

官方入口：https://www.rvd.gov.hk/en/publications/property_market_statistics.html
统计处：https://www.censtatd.gov.hk/en/web_table.html?id=115-01011
统计处：https://www.censtatd.gov.hk/en/web_table.html?id=115-01013

原始数据由相应香港政府部门发布；本包保留归属和出处，不对官方数据或第三方材料另行主张版权。
