# Axion Ray Data Analytics Assignment

This repository contains the detailed analysis, code, and findings for the Solution Architect Data Analytics Assignment. The project is structured into three progressive tasks, moving from data cleaning to integration and finally advanced financial analysis.

## Project Structure & Workflow

*   **Task 1**: Data Quality Assessment & Cleaning (`task_1.ipynb`)
*   **Task 2**: Data Integration & Relational Modeling (`task_2.ipynb`)
*   **Task 3**: Financial & Temporal Analysis (`task_3.ipynb`)

---

## Task 1: Data Cleaning & Component Analysis

**Objective**: Clean raw transaction data and identify key cost drivers.

### Analysis Performed
1.  **Data Ingestion**: Loaded `SA - Data for Task 1.xlsx` containing transaction records.
2.  **Column-Wise Audit**:
    *   Analyzed unique value counts and null percentages for all columns.
    *   Identified high-null columns (e.g., `CAMPAIGN_NBR` was 100% null) for removal.
    *   Standardized categorical text (e.g., converting 'STEERING WHEEL' and 'Steering wheel' to shared case).
3.  **Data Integration**:
    *   Merged `Sheet1` (Transaction Data) with `Sheet2` (Verbatim/Notes) using `TRANSACTION_ID` as the primary key.
    *   Applied **Left Join** logic to preserve main transaction records while enriching with verbatim details.
4.  **Exploratory Analysis**:
    *   Conducted Correlation Analysis between `TOTALCOST`, `LBRCOST` (Labor), and `Part Cost`.
    *   Performed segmentation by `DEALER_NAME` and `CAUSAL_PART_NM`.

### Key Findings
*   **Data Quality**: Identified and removed empty columns like `CAMPAIGN_NBR`. Found inconsistent casing in 'Verbatim' fields requiring normalization.
*   **Cost Correlations**: Strong positive correlation (approx 0.9+) observed between Labor Cost and Total Cost, indicating labor is a primary driver of repair expenses.
*   **Top Dealers**: Specific dealers (e.g., *AutoNation*) showed significantly higher average labor costs compared to the median.
*   **Failure Modes**: 'Steering Wheel' components were identified as the most frequent `CAUSAL_PART_NM` in this dataset.

---

## Task 2: Data Modeling & Integration

**Objective**: Integrate Work Order and Repair Data to build a unified analytical dataset.

### Analysis Performed
1.  **Schema Analysis**:
    *   Analyzed `Work Order Data` (Header level) vs. `Repair Data` (Line-item level).
    *   Identified `Primary Key` (Composite of Order + Segment) as the linking variable.
2.  **Duplicate Handling**:
    *   Discovered `Primary Key` duplicates in `Repair Data`.
    *   *Correction Step*: Determined duplicates represented **multiple parts per work order segment**, validating a 1-to-many relationship rather than data error.
3.  **Dataset Merging**:
    *   Executed a **Left Join** of Repair Data onto Work Orders.
    *   This preserved all Work Orders (even those without repair details) while expanding rows for multi-part repairs.
4.  **Feature Engineering**:
    *   Standardized Date formats for `Order Date` and `Invoice Date`.
    *   Validated `Segment Total $` against individual Cost components.

### Key Findings
*   **Relationship Structure**: The relationship between Work Orders and Repair Data is **One-to-Many**. A single Work Order Segment frequently consumes multiple parts (e.g., Filter + Oil + Gasket), necessitating row expansion during merge.
*   **Data Totals**: The merge expanded the original 500 Work Orders into 503 rows, capturing all line-item details.
*   **Outcome**: Produced `Task_2_Integrated_Data.xlsx`, a clean, granular dataset ready for time-series analysis.

---

## Task 3: Advanced Analysis (Financial & Temporal)

**Objective**: Derive actionable business insights from the integrated dataset regarding revenue and trends.

### Analysis Performed
1.  **Temporal Aggregation**:
    *   Converted `Order Date` to monthly periods (`YYYY-MM`).
    *   Aggregated `Segment Total $` (Revenue) and `Order_Count` by month.
2.  **Trend Visualization**:
    *   Plotted Revenue vs. Time to identify seasonality and anomalies.
    *   Plotted Order Volume vs. Time to track demand consistency.

### Key Findings
*   **Major Revenue Anomaly**: A massive revenue spike was detected in **May 2022**, reaching approximately **$1.34 Million** in a single month.
    *   *Context*: Comparison months (e.g., April 2022, March 2023) averaged significantly lower revenue ($5k - $70k range).
    *   *Insight*: This outlier suggests either a bulk fleet transaction, a data entry error in the raw source, or a specific high-value campaign during that period.
*   **Volume vs. Value**: While Order Counts showed a steady, organic increase into 2023 (rising from ~5 to ~44 orders/month), they did *not* correlate proportionally with the May 2022 revenue spike, indicating the May revenue was driven by *value* per order, not *volume*.

---

## Setup & Usage

1.  **Installation**:
    ```bash
    pip install -r requirements.txt
    ```
2.  **Execution**:
    Run the notebooks in order:
    1.  `task_1.ipynb` -> Generates `Task_1_Cleaned_Analysis.xlsx`
    2.  `task_2.ipynb` -> Generates `Task_2_Integrated_Data.xlsx`
    3.  `task_3.ipynb` -> Uses `Task_2_Integrated_Data.xlsx` for final reporting.
