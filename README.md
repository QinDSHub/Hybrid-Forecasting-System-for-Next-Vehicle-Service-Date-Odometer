## Notes on Project Materials

The PDF included in this repository was originally prepared for a project presentation. Although it reflects the presentation style and documentation standards of the time, it preserves the technical design, analytical process, and modeling decisions behind the project.

It provides an overview of the end-to-end modeling workflow, including:
- Problem definition
- Data exploration and processing
- Feature engineering
- Model design and development
- Offline evaluation

For more projects and technical discussions, visit my LinkedIn:  
https://www.linkedin.com/in/qinluu

I'm always happy to connect and exchange ideas.

---

## Hybrid Forecasting System for Next Vehicle Service Date & Odometer

### Project Overview

This project addressed the challenge of predicting each customer's next vehicle service date and odometer reading, including users with limited or noisy maintenance histories.

The solution combined LightGBM with a rule-based fallback approach to accommodate differences in data quality and distribution. The key business KPI was the proportion of predictions falling within 30 days of the actual service date.

### Key Technical Approaches

**Data Governance & Feature Engineering**
- Cleaned, validated, and transformed fragmented customer and maintenance records.
- Restructured transactional data from a long-table into a wide-table representation to support prediction based on historical service records.
- Engineered features to capture maintenance intervals and mileage patterns while aligning historical inputs with the prediction timeline.

**Hybrid Machine Learning & Rule-Based Architecture**
- **LightGBM:** Applied gradient boosting to structured, high-quality customer data.
- **Rule-Based Model:** Handled noisy, sparse, and long-tail data that could not be reliably corrected through conventional data cleaning or statistical methods.
- **Full-Coverage Strategy:** Combined both approaches to generate predictions across the customer base, including users with limited historical records.

**Batch-Wise Prediction Strategy**

Designed a batch-wise training and prediction pipeline based on historical service records. Users with *n + 1* service records provided training examples for predicting the next maintenance interval and mileage interval from *n* historical visits.

For the rule-based pipeline, the next service date and mileage were estimated by smoothing the intervals between the user's two most recent service visits.

**Multi-Metric Evaluation**

Evaluated model performance using MSE, MAE, R², and the proportion of predicted service dates falling within the client's 30-day tolerance window.

### Tech Stack

- **Machine Learning:** LightGBM
- **Data Processing:** Python, Pandas, NumPy, PySpark
- **Evaluation:** MSE, MAE, R², Business KPI Analysis
- **Prediction Architecture:** Hybrid Machine Learning + Rule-Based Modeling

### Results & Business Impact

The hybrid solution was accepted by the client and subsequently migrated from a Python implementation to a PySpark-based production deployment within the client's environment.

**Offline evaluation results:**
- **LightGBM:** 41% of predicted service dates fell within the 30-day tolerance window.
- **Rule-Based Model:** 31% of predicted service dates fell within the 30-day tolerance window.

The solution provided a data-driven foundation for service reminders and personalized automotive parts recommendations, supporting more targeted customer engagement.

### Key Contributions

- **Data Governance:** Addressed fragmented, inconsistent, and noisy customer data at scale.
- **Feature Engineering:** Redesigned the data representation to align with the temporal prediction task.
- **Hybrid Modeling:** Combined LightGBM with rule-based fallbacks to accommodate heterogeneous data quality and long-tail user behavior.
- **Production Transition:** Supported the migration from Python-based modeling to PySpark deployment in the client's environment.
