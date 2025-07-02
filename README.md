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

## Key DAX Measures and Calculated Columns
While many calculations were handled in Power Query, several DAX (Data Analysis Expressions) measures were created to derive the required aggregations and insights dynamically:

* `Total Employees`: Counts the total number of employees.
* `Average Salary`: Calculates the average salary across different segments.
* `Employees Below Minimum Wage`: Identifies employees earning less than $90,000.
* `Employees Above Minimum Wage`: Identifies employees earning at least $90,000.
* `Total Bonus Company-wide`: Aggregates all individual bonus amounts (from the Power Query custom column).
* `Total Pay Company-wide`: Aggregates all total pay amounts (from the Power Query custom column).
## Visualizations

The Power BI report is organized into two main pages, providing a comprehensive view of HR analytics at Palmoria Group.

### Page 1: Gender Diversity and Compensation Analysis
This page focuses on addressing the core issues of gender representation and potential pay gaps within the organization.

* **Key Performance Indicators (KPIs):** Card visuals prominently display `Total Employees`, `Total Female`, `Total Male`, `Undisclosed` employees, and the `Total Employees Below $90,000` minimum wage, offering a quick snapshot of the workforce and compliance.
* **Gender Distribution:** A **Donut Chart** visually represents the overall percentage breakdown of employees by gender (Male, Female, Undisclosed), providing an immediate understanding of the company's gender composition.
    * ![Overall Gender Distribution](screenshots/1st_page_Capture.PNG) *(You might crop this image to show just the donut chart or the overall page)*
* **Gender Distribution by Department:** A **100% Stacked Bar Chart** illustrates the gender composition within each department (Finance, HR, Marketing, Operations, Sales), helping to identify departments with significant gender imbalances.
* **Rating by Gender:** A **Clustered Column Chart** compares employee performance ratings across genders, allowing for the identification of potential biases in performance evaluations.
* **Average Salary by Department & Gender:** A **Clustered Bar Chart** displays the average salary for each gender within different departments, crucial for identifying and quantifying potential gender pay gaps at the departmental level.
* **Average Salary by Location & Gender:** A **Clustered Column Chart** presents the average salary by gender across the company's three regions (North, South, West), highlighting regional pay disparities and their impact on gender equality.
* **Interactive Slicers:** Dedicated slicers for `Department`, `Location`, and `Gender` enable users to dynamically filter the data and explore specific segments of the workforce.

