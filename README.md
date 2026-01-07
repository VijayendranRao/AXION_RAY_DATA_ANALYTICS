# Axion Ray Data Analysis Project

## Executive Summary
This project delivers a comprehensive analysis of vehicle fleet repair data, processing **500+ service records** to identify critical cost drivers and operational inefficiencies. By integrating disparately structured data sources (`Work Orders` and `Repair Logs`), we uncovered a **$1.34M cost anomaly** in May 2022 and identified specific component failure clusters (Coolant/Oil systems) driving 60% of unscheduled downtime.

## Key Achievements
- **Data Engineering**: Built a robust ETL pipeline using `Pandas` to merge heterogeneous datasets, preserving 100% of parent work order integrity via strategic Left Joins.
- **Root Cause Analysis**: Correlated labor intensity with total cost ($r=0.68$), validating that labor efficiency programs would yield higher ROI than parts negotiation.
- **Statistical Anomaly Detection**: Detected a 560% volume surge in May 2022, enabling targeted operational audits.

---

## Strategic Roadmap: Advanced AI & GAN Implementation
To further elevate the predictive capabilities of this analytics suite, the following advanced machine learning architecture is proposed for the next phase.

### Synthetic Data Augmentation with GANs
One of the primary challenges in fleet maintenance data is **class imbalance**—catastrophic failures are fortunately rare, but this makes training predictive models difficult.

**Proposed Solution: CTGAN (Conditional Tabular Generative Adversarial Network)**
We aim to deploy a state-of-the-art **CTGAN** to generate high-fidelity synthetic repair records. This will allow us to:
1.  **Up-sample Rare Failure Modes**: Generate synthetic examples of critical engine failures (e.g., "Main Bearing Spun") to train more robust classifiers.
2.  **Privacy-Preserving Data Sharing**: Create statistically identical synthetic datasets that can be shared with third-party vendors without exposing sensitive VINs or pricing data.
3.  **Adversarial Training**: Use the *Generator* (G) to create plausible service logs and the *Discriminator* (D) to distinguish them from real logs, forcing the system to learn the deep latent correlations between `Labor Codes`, `Part Costs`, and `Vehicle Age`.

### Architecture for Predictive Maintenance
*   **Input**: Historical Time-Series (Sensors + Logs)
*   **Augmentation**: **GAN-generated synthetic failures** to balance the dataset.
*   **Model**: LSTM (Long Short-Term Memory) networks for Remaining Useful Life (RUL) estimation.
*   **Output**: Real-time failure probability scores.

---

## Technical Stack
*   **Python**: Core analysis (Pandas, NumPy).
*   **Visualization**: Matplotlib/Seaborn for trend analysis and Pareto charts.
*   **Reporting**: Automated report generation via `python-docx`.

## Project Structure
*   `task_1.ipynb`: Data Cleaning & EDA (Missing value imputation, Schema validation).
*   `task_2.ipynb`: Data Integration (Relational merging of Work Orders and Repair Parts).
*   `task_3.ipynb`: Advanced Analytics (Correlation matrices, Time-series decomposition).
*   `generate_report.py`: Automation script for executive reporting.
*   `Evaluation_Report.docx`: Final executive presentation.

---
*Author: Vijayendran Suriya Pra*
*Tag: #DataScience #GAN #PredictiveMaintenance #AI*