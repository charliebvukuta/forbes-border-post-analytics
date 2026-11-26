# Forbes Border Post Analytics

## 1. Problem Statement
The Forbes Border Post is experiencing significant revenue leakage due to discrepancies between what importers declare and what customs authorities actually assess. These discrepancies manifest as under-valuation, misclassification of goods, and incorrect declarations. Without a clear understanding of where and how these gaps occur, customs operations cannot effectively allocate inspection resources or maximize revenue recovery. 

## 2. Objective
The primary objective of this project is to analyze historical customs transaction data to identify patterns of revenue leakage, evaluate the effectiveness of current risk profiling and inspection strategies, and provide actionable recommendations to close the revenue gap. 

Specifically, this analysis aims to:
* Quantify the total potential revenue gap and actual revenue recovered.
* Determine if the current `Risk_Category` (Low, Medium, High) accurately predicts the likelihood of an offence.
* Identify high-risk countries of origin and commodity types (HS Codes) that contribute most to revenue loss.

## 3. Dataset and its Columns
The project utilizes a simulated dataset (`Forbes_Border_Post_Simulated_Data.xlsx`) containing customs transactions from January 2025 to August 2025. 

The dataset contains the following columns, grouped by category:

**Transaction & Logistics**
* `Declaration_ID`: Unique identifier for the customs declaration (Primary Key).
* `Declaration_Date`: The date the declaration was submitted.
* `Border_Post`: The specific border post where goods entered.
* `Importer_ID`: Unique identifier for the importing business entity.
* `Country_of_Origin`: The country where the goods were manufactured.

**Product Information**
* `Commodity_Description`: Text description of the imported goods.
* `HS_Code`: Harmonized System classification code.

**Risk & Compliance**
* `Risk_Category`: Customs risk profile assigned to the shipment (Low, Medium, High).
* `Inspection_Conducted`: Indicates whether a physical inspection was performed (Yes/No).
* `Offence_Detected`: Indicates whether a violation was found (Yes/No).
* `Offence_Type`: Category of the violation (e.g., Under-valuation, Misclassification).
* `Payment_Status`: Status of the tax/duty payment (Paid, Part-paid, Pending).

**Financials: Declared vs. Assessed**
* `Declared_Customs_Value_USD` / `Assessed_Customs_Value_USD`: Value of goods declared by the importer vs. assessed by customs.
* `Declared_Customs_Duty_USD` / `Assessed_Customs_Duty_USD`: Customs duty amounts.
* `Declared_Import_VAT_USD` / `Assessed_Import_VAT_USD`: Value Added Tax amounts.
* `Declared_Excise_USD` / `Assessed_Excise_USD`: Excise tax amounts.
* `Declared_Total_Revenue_USD` / `Assessed_Total_Revenue_USD`: Total revenue (Duty + VAT + Excise).

**Revenue Impact**
* `Potential_Revenue_Gap_USD`: The difference between assessed and declared revenue.
* `Additional_Revenue_Recovered_USD`: Actual revenue recovered after an offence is resolved.

## 4. Deliverables (Key Results)
By the end of this sprint, the following deliverables will be produced and pushed to this repository:

1.  **Cleaned Dataset and Data Dictionary**: A pristine version of the dataset with handled anomalies (e.g., truncated rows) and a comprehensive dictionary explaining all data fields.
2.  **Interactive Dashboard**: A visual representation of the findings (e.g., Power BI `.pbix` file) highlighting key revenue gaps and risk metrics.
3.  **Reproducible Model Files, Scripts, or Notebooks**: Python, SQL, or Power Query scripts used for data cleaning, exploratory analysis, and predictive modeling.
4.  **Management Brief / Final Report & Presentation Slides**: A comprehensive PDF/DOCX report and PDF/PPTX slides summarizing the methodology, key visual findings, actionable recommendations, and limitations for a live presentation session.

---
*Note: This project uses simulated data for analytics.*
