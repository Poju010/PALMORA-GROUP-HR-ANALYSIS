# PROJECT TOPIC: PALMORA-GROUP-HR-ANALYSIS
## Project Overview
The Palmoria group, a manufacturing company based in Nigeria, is facing challenges bordering on gender inequality in its 3 regions. As an HR Analytics expert, my role is to analyze the company data and generate insights that the company's management team would need to address focusing on gender-related issues and using appropriate charts.
## Objectives
- Analyze gender distribution by department and region.
- Investigate performance rating across genders.
- Identify gender pay gaps and the department and regions focus should be on.
- Assess the manufacturing companies' newly adopted minimum payment of $9,000 regulation:
  1. If Palmora meets the requirement.
  2. Allocate the new payment distribution if the requirement was met.
- Allocate bonuses to individual employees based on performance rules.
- Allocate total salary to each individual
- Summarize total payouts across region and company-wide.
  
## Data Source
This project contains two datasets, provided as part of a case study by [Digital Skilled-up Africa (DSA)](https://www.linkedin.com/company/theincubatorhubng/) for training purposes. They stimulate real-world HR data from a fictional company, Palmora Group:
  1. The first dataset, Palmoria Group emp-data.csv, contains the employees records. It serves as the primary data for analyzing individual bonuses.
  2. Palmoria Group Bonus Rules.xlsx, the second dataset, contains bonus rates for various departments based on performance ratings.
     
## Data Preparation and Transformation (Power Query)

* **Gender Harmonization:** Employees who did not disclose their gender were assigned a generic gender status, "Undisclosed".
* **Employee Filtering:** Employees without an assigned salary (indicating they are no longer with the company) were removed from the dataset.
* **Department Cleaning:** Records with "NULL" departments were removed to ensure data integrity.
* **Custom Column Creation for Bonus and Total Pay:**
    * A custom column was created to calculate the **'Annual Bonus'** for each employee by multiplying 'Salary' with the 'Bonus Rate' now available in the merged table.
    * Another custom column was created to calculate the **'Total Pay (Incl. Bonus)'** for each employee by summing 'Salary' and the 'Annual Bonus').
* **Bonus Rule Unpivoting and Data Merging:** The `Palmoria Group emp-data` table was merged with the `Bonus Rules` table after unpivoting the bonus rules to have 'Rating' and 'Bonus Rate' columns to consolidate all necessary data into a single primary table for analysis. This typically involved merging on `Department` and `Rating`.
* **Data Type Correction:** Ensured all columns have appropriate data types for accurate calculations and visualizations.

