# 水稻营养机理论文复现报告

## 1. 论文研究概述

### 1.1 论文信息
- 题目: **Reduced phosphorus bioavailability in rice paddies intensified by elevated CO2-driven warming**
- 期刊: Nature Geoscience
- 发表日期: **2026-02-03**
- 文章 DOI: https://doi.org/10.1038/s41561-026-01917-2
- 数据 DOI: https://doi.org/10.6084/m9.figshare.30773867.v1

### 1.2 研究主题与机制
本文关注升高 CO2 与增温条件下，稻田土壤磷（P）生物有效性下降的机制，重点涉及：
- 土壤可利用磷（Available P）变化
- 土壤 C:P 化学计量变化
- Fe-有机碳复合对磷有效性的影响
- 磷矿化速率（PMR）动态

---

## 2. 数据准备

### 2.1 数据来源
- Figshare 数据集: https://figshare.com/articles/dataset/Reduced_phosphorus_bioavailability_in_rice_paddies_intensified_by_elevated_CO2-driven_warming-_experimental_data/30773867
- 下载文件: `Data.xlsx`（49,143 bytes）

### 2.2 本地目录结构
- `raw_data/Data.xlsx`
- `scripts/reproduce_analysis.ps1`
- `extracted_data/*.csv`
- `results/*.csv`
- `reproducibility_report.md`

---



## 3. 数据处理流程

### 3.1 工作表抽取
`Data.xlsx` 共抽取 15 个工作表为 CSV（例如 `Available P and SoilP fractions.csv`、`Soil total C N P content.csv`、`PMR.csv` 等）。

### 3.2 关键变量
- AP: `AP (mg kg-1)`
- C:P: `Total C (g kg-1) / Total P (g kg-1)`
- Fe-bound OC: `Fe bound OC (g kg-1)`
- PMR: `PMR （mg kg-1 d-1)`

---

## 4. 统计分析与复现结果

### 4.1 按处理汇总的 AP 变化（相对 Ambient）
| Treatment | AP 均值 (mg/kg) | 相对 Ambient 变化 |
|---|---:|---:|
| Ambient | 44.547 | 0.00% |
| CO2 | 30.913 | -32.13% |
| Temp | 33.191 | -27.13% |
| CO2+Temp | 28.849 | -35.66% |

### 4.2 按处理汇总的 C:P 变化（相对 Ambient）
| Treatment | C:P 均值 | 相对 Ambient 变化 |
|---|---:|---:|
| Ambient | 20.226 | 0.00% |
| CO2 | 22.483 | +11.16% |
| Temp | 21.058 | +3.11% |
| CO2+Temp | 25.323 | +30.14% |

### 4.3 单因素 ANOVA（Treatment）
| 指标 | N | F | p 值 | eta² |
|---|---:|---:|---:|---:|
| AP | 36 | 13.8339 | 3.16e-06 | 0.5817 |
| C:P | 36 | 15.4940 | 1.17e-06 | 0.6073 |

### 4.4 机制相关性复现（Fe-bound OC vs AP）
- 按“Year × Treatment”聚合后（n=12）：
- Pearson r = **-0.7112**
- p = **0.0095**

结果支持“Fe-有机碳复合增强与可利用磷下降相关”的机制方向。

### 4.5 PMR 初期响应
Day 1 的均值显示：
- Ambient: 2.167
- Temp: 2.667
- CO2+Temp: 2.250

与论文“增温初期促进磷矿化”这一描述方向一致。

---

## 5. 未能完全复现的部分（关键说明）

### 5.1 不能 1:1 复现的结果
论文摘要描述“所有气候处理使 AP 下降 32–54%”。本次基于公开 `Data.xlsx` 复算得到：
- 按处理总体均值: **27.13%–35.66%**
- 按年份分层对比: **19.69%–43.22%**

未复现到 54% 的上界。

### 5.2 原因判断
- 公开数据中 AP 主要为 2020–2022 的观测值（3 年），而论文是 decade-long 实验框架。
- 数据包未提供论文主文中全部模型脚本（如混合模型/年际整合参数/作图脚本）。
- 因此无法完全还原文中“32–54%”区间的精确计算链路。


### 7.3 结果文件
- `results/analysis_results_summary.csv`
- `results/analysis_anova_summary.csv`
- `results/analysis_yearly_changes.csv`
- `results/analysis_ap_feoc_joined.csv`
- `results/analysis_correlation_summary.csv`
- `results/analysis_pmr_day_treatment_means.csv`

---

## 8. 复现结论

本次复现为**部分成功**：
- 成功复现了主要方向性结论（AP 下降、C:P 上升、Fe-bound OC 与 AP 负相关、PMR 初期响应）。
- 但未能 1:1 复现摘要中 AP 下降区间上界（54%），原因是公开数据与模型细节不足以完整重建原文统计流程。
