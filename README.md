# Forbes Border Post Analytics

**The role of data analytics in identifying revenue collection leakages at Forbes Border Post, Zimbabwe**

Analysis of 480 simulated customs declarations (1 January – 30 December 2025) to find where revenue leaks, test whether the current risk profiling sends inspectors to the right shipments, and recommend evidence-based interventions.

> The dataset is simulated training data. All records, importer IDs, values and outcomes are fictional and are not actual ZIMRA or Forbes Border Post records. `Potential_Revenue_Gap_USD` is an analytical estimate, not proof of revenue loss or fraud.

## 1. Problem statement
Revenue leaks when importers declare less than customs later assesses, through under-valuation, misclassification, incorrect declarations and quantity discrepancies. Without knowing where and how these gaps arise, inspection resources cannot be targeted and recovery cannot be maximised.

## 2. Objectives
1. Quantify the potential revenue gap, revenue recovered and performance against monthly targets.
2. Test whether the `Risk_Category` (Low / Medium / High) and physical inspections target the shipments where under-declaration actually occurs.
3. Identify the countries, commodities, offence types, months and importers contributing most to the gap.
4. Build and evaluate a predictive risk indicator that flags likely under-declarations before clearance.
5. Recommend interventions to strengthen compliance and revenue collection.

## 3. Key results
| Indicator | Value |
|---|---|
| Revenue assessed / declared | $905,753 / $872,289 |
| Potential revenue gap | **$33,801** (3.7% of assessed) |
| Revenue recovered | $9,057 (**26.8%** recovery rate) |
| Revenue vs annual target | **93.0%** ($67,762 short; target missed in all 12 months) |
| Gap in shipments never inspected | **65%** ($22,085), with 0% recovered |
| Recovery where an offence was detected | **85%** |
| Inspection hit rate | 16.0% (25 offences / 156 inspections) |

- **The gap is a detection problem, not a collection problem.** Most of it sits in shipments nobody inspected.
- **The risk profile is inverted.** Low-risk shipments are under-declared most often (33%) and carry 58% of the gap, but only 12% are inspected (chi-square p = 0.004).
- **Valuation offences** account for 87% of the detected gap.
- **Model:** a simple data-driven risk ranking (logistic regression) reaches a cross-validated ROC-AUC of 0.59, against 0.41 for the current rule. With the same 156 inspections it would catch **42.7% of the gap vs 34.7% today (+23%)**.

## 4. Repository structure
```
├── data/
│   ├── raw/Forbes_Border_Post_Simulated_Data.xlsx      # original workbook (transactions + monthly targets)
│   └── processed/
│       ├── cleaned_customs_transactions.csv            # 480 × 29, output of notebook 01
│       ├── monthly_targets.csv                         # cleaned monthly targets
│       └── model_risk_scores.csv                       # model gap probability per declaration
├── notebooks/
│   ├── 01_data_cleaning_and_dictionary.ipynb           # cleaning, data-quality checks, data dictionary
│   ├── 02_exploratory_data_analysis.ipynb              # KPIs, risk, geography, offences, targets, importers
│   └── 03_predictive_risk_model.ipynb                  # model, cross-validation, business evaluation
├── dashboard/
│   ├── Forbes_Border_Post_Dashboard.pbip               # open this in Power BI Desktop
│   ├── Forbes_Border_Post_Dashboard.Report/            # 3 report pages (PBIR format)
│   ├── Forbes_Border_Post_Dashboard.SemanticModel/     # data model, relationships, DAX measures
│   └── page*.png                                       # screenshots of the 3 dashboard pages
├── reports/
│   ├── Forbes_Border_Post_Final_Report.docx / .pdf     # management report
│   ├── data_dictionary.csv
│   ├── model_performance.csv, model_targeting_comparison.csv
│   └── *.png                                           # charts used in the report and slides
└── docs/Project proposal.docx
```

## 5. Dataset
- **Customs_Transactions:** 480 declarations × 24 fields covering the importer (60), country of origin (6), commodity/HS code (10), risk category, declared vs assessed value, duty, VAT and excise, inspection and offence outcome, potential revenue gap, revenue recovered and payment status. The full field list is in `reports/data_dictionary.csv`.
- **Monthly_Targets:** monthly revenue target, January–December 2025.
- **Data quality:** no duplicates or truncated rows. 11 rows (2.3%) are flagged rather than removed: 7 where the assessed tax components don't sum to the assessed total, and 4 over-declarations recorded with a $0 gap.

## 6. How to reproduce
1. **Python** (3.10+): `pip install pandas numpy matplotlib seaborn scipy scikit-learn openpyxl jupyter`
2. Run the notebooks in order from the `notebooks/` folder: **01 → 02 → 03**. Each one writes its outputs to `data/processed/` and `reports/`.
3. **Dashboard:** open `dashboard/Forbes_Border_Post_Dashboard.pbip` in Power BI Desktop, then go to **Home → Transform data → Edit parameters** and set `ProjectFolder` to your local copy of this repository (with a trailing `\`). Then click **Refresh**.

## 7. Deliverables
| Deliverable | Location |
|---|---|
| Cleaned dataset and data dictionary | `data/processed/`, `reports/data_dictionary.csv` |
| Interactive dashboard | `dashboard/` (Power BI project, 3 pages) |
| Reproducible notebooks | `notebooks/` |
| Management report | `reports/Forbes_Border_Post_Final_Report.pdf` (and `.docx`) |
| Presentation slides | `reports/` (to be added) |

## 8. Limitations
The data is simulated, covers one border post for one year, and is small (25 detected offences). The revenue gap depends on customs' own assessment and is one-sided. Offences are only observed on inspected shipments. The model's predictive power is modest (AUC 0.59), so it should support officers' judgement, not replace it.

---
*Part of a simulated data analytics internship sprint.*
