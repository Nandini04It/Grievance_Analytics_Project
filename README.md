# AI-Powered Citizen Grievance Analytics & Resolution Intelligence System

AICTE | IBM SkillsBuild — Data Analytics with AI Internship 2026 (BharatCares, 17 Aug – 30 Sep 2026)

## 1. Overview

This project analyses a real, publicly available Government of India dataset on citizen grievances
handled through **CPGRAMS** (Centralised Public Grievance Redress and Monitoring System). It
covers data cleaning, exploratory data analysis, department/state-wise comparison, received vs
disposed vs pending analysis, pendency-age (resolution-delay) insights, and two appropriate AI/ML
techniques (K-Means clustering and linear regression) applied to the genuine numeric fields in the
dataset.

**No data, statistic, or AI capability in this project has been invented.** Where the dataset does
not support something (e.g. NLP/sentiment analysis, since there is no grievance text field), that
limitation is stated explicitly rather than faked — see Section 5 below and Section 3 of the report.

## 2. Dataset & Source

| Field | Detail |
|---|---|
| Dataset | Department/State-wise Receipts, Disposal & Pendency of Public Grievances (CPGRAMS) |
| Publisher | Department of Administrative Reforms and Public Grievances (DARPG), Govt. of India |
| Platform | Open Government Data (OGD) Platform India — https://www.data.gov.in |
| Coverage | 01 Jan 2016 to 01 Nov 2019 (cumulative snapshot as on 01.11.2019) |
| Rows | 124 (88 Central Ministries/Departments + 36 States/UTs) |
| Original catalog page | https://www.data.gov.in/catalog/monthly-department-wise-public-grievance-receipts-and-disposals |
| Related catalog | https://www.data.gov.in/catalog/public-grievance-details-cpgrams-along-feedback-details |
| CPGRAMS portal | https://pgportal.gov.in |

**Provenance note:** `data.gov.in` blocks automated/bot downloads. The exact, unmodified CSV was
retrieved from a verified public mirror — https://github.com/kalyandutta209/cpgrams-statistical-analysis
— whose README documents it as the "Original government dataset" sourced from DARPG/data.gov.in.
You can independently re-download the same file from data.gov.in via a browser if you want to verify it yourself.

## 3. Folder Structure

```
project/
├── README.md                                          ← this file
├── data/│
      └── Dept_stat_receipt_disposal_raw.csv          ← original, unmodified government file 
      └── grievance_cleaned_processed.csv             ← cleaned file with engineered KPIs
├── Nandini_AI_Powered_Citizen_Grievance_Analytics.ipynb
├── charts/                                           ← PNG exports of every chart (also embedded in notebook + report)
└── Nandini_ProjectReport.docx                        ← formatted Word project report
└── requirements.txt                                  ← Python dependencies
```

## 4. How to Run

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
cd notebook
jupyter notebook AI_Powered_Citizen_Grievance_Analytics.ipynb
# Run All Cells — no internet access or API keys required, everything runs on the local CSV
```

The notebook has already been executed once top-to-bottom with no errors; all outputs and chart
images shown in it were produced directly from `data/Dept_stat_receipt_disposal_raw.csv`.

## 5. What's Inside the Analysis

1. **Data cleaning** — column renaming, whitespace/typo fixes, missing-value & duplicate checks,
   Central-vs-State/UT classification, KPI engineering (Disposal Rate %, Pendency Rate %, Chronic
   Pendency %).
2. **EDA** — distribution of disposal rate by entity type; top entities by volume received and by
   volume pending.
3. **Department/State-wise analysis** — best/worst performers in each group.
4. **Received vs Disposed vs Pending** — national totals and split.
5. **Pendency/resolution insights** — age profile of pending grievances (how much is stuck >1 year).
6. **AI/ML** — K-Means clustering (unsupervised, k chosen via silhouette score) to segment entities
   by performance; Linear Regression to quantify the receipts↔disposal relationship (R², Pearson r).
   *No NLP/sentiment analysis is included — the dataset has no grievance-text field, and this
   project does not fabricate one.*
7. **Key findings, conclusion, and future scope.**

## 6. Headline Results (reproducible from the notebook)

- Central Ministries/Departments: **96.89%** average disposal rate vs. **45.24%** for States/UTs.
- **61.13%** of all nationally pending grievances (as on 01.11.2019) had been pending **> 1 year**.
- K-Means (k=2, silhouette 0.807) split entities into a 100-strong "healthy" group (~95% disposal)
  and a 24-strong "high-backlog" group (~25% disposal, ~69% chronic pendency).
- Receipts vs. Disposal: **R² = 0.92**, Pearson **r = 0.96**.

## 7. Known Limitations

- **Single snapshot, not a time series** — cannot show a multi-year trend line of grievance volume.
- **No grievance-text data** — no NLP/sentiment/topic-modelling is included or faked.
- Figures reflect the **cumulative period 01.01.2016 – 01.11.2019** only, not the current CPGRAMS status.

## 8. Future Scope (Planned Extensions)

- **Dashboard:** rebuild the KPIs/charts as an interactive **Power BI** report or a **Streamlit** app.
- **NLP layer:** add complaint-category classification/sentiment analysis once a grievance-text-level
  CPGRAMS export is available (e.g. via an official data-sharing request).
- **True time-series trend & forecasting:** incorporate the monthly DARPG CPGRAMS reports
  (https://darpg.gov.in) to model pendency over time (e.g. Prophet/ARIMA).
- **Predictive resolution-time model:** once case-level, date-stamped records are available, predict
  expected resolution time/delay-risk for a new grievance at filing time.
- **Automated alerting** for entities crossing a chronic-pendency threshold.

## 9. Author / Internship Details

- **Program:** AICTE | IBM SkillsBuild — Data Analytics with AI Internship 2026
- **Company:** BharatCares
- **Duration:** 17 August – 30 September 2026
- **Trainer:** Mr. Kartik Hooda
