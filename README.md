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
* **`Average Male Salary`**: Calculates the average salary specifically for male employees.
    ```DAX
    Average Male Salary =
    CALCULATE (
        AVERAGE ( 'Employee'[Salary] ),
        'Employee'[Gender] = "Male"
    )
    ```
* **`Average Female Salary`**: Calculates the average salary specifically for female employees.
    ```DAX
    Average Female Salary =
    CALCULATE (
        AVERAGE ( 'Employee'[Salary] ),
        'Employee'[Gender] = "Female"
    )
    ```
* **`Gender Pay Gap`**: Calculates the percentage difference between average male and female salaries, representing the gender pay gap. 
    ```DAX
    Gender Pay Gap =
    DIVIDE (
        [Average Male Salary] - [Average Female Salary],
        [Average Male Salary],
        0
    )
    ```
## Visualizations
The Power BI report is organized into two main pages, providing a comprehensive view of HR analytics at Palmoria Group  
Here is a preview of the dashboard for reference:  
![Page 1](https://github.com/user-attachments/assets/fa6a4d4e-fb97-43aa-815a-66e83a70952c)
![Page 2](https://github.com/user-attachments/assets/9bbc7021-bc42-4f55-8b58-46bceb1ef5e0)

### Page 1
This page focuses on addressing the core issues of gender representation and potential pay gaps within the organization.
* **Interactive Slicers:** Dedicated slicers for `Gender`, `Department`, and `Region` enable users to dynamically filter the data and explore specific segments of the workforce.
* **Regional Employee Distribution:** A **Pie Chart** visually breaks down the total employee count by region (Kaduna, Abuja, Lagos), indicating that Kaduna has the largest share of employees at 38% (361 employees). This helps understand the geographical distribution of the workforce.
* **Total Employees by Gender:** A **Pie Chart** provides an overall breakdown of the total workforce by gender, showing Male (49.2%, 430 employees), Female (46.45%, 406 employees), and Undisclosed (4.35%, 38 employees). This offers a snapshot of the company's gender diversity.
* **Gender Distribution by Department:** A **100% Stacked Bar Chart** illustrates the gender composition within each department (Accounting, HR, Marketing, Engineering, Sales, etc), helping to identify departments with significant gender imbalances.
* **Rating by Gender:** A **Line Chart** compares employee performance ratings across genders, allowing for the identification of potential biases in performance evaluations.
* **Minimum Wage Compliance Gauges:** Two **Gauge visuals** directly display the number of "Employees Earning at least $90k" and "Employees Earning Below $90k", serving as quick visual indicators for regulatory adherence.
* **Regulation Requirement Compliance:** A **Donut Chart** shows the percentage of employees meeting versus not meeting the $90,000 minimum salary requirement, highlighting the compliance status.
* **Gender Pay Gap by Department:** A **Table Visual** displays key insights into salary disparities, containing `Department`, `Average Male Salary`, `Average Female Salary`, and `Gender Pay Gap`. This provides a direct and clear comparison of gender pay differences within each department.
* 
### Page 2: Compensation and Bonus Analysis
This page delves deeper into the company's compensation structure, compliance with minimum wage regulations, and the calculated bonus allocations.
* **Key Compensation Totals:** Card visuals show the `Sum of Salary`, `Total Bonus Company-wide` and `Total Pay Company-wide` across the entire company, providing an high-level financial overview of compensation.
* **Total Employees by Salary Band:** A **Line and Clustered Column Chart** visualizes the distribution of employees across $10,000 salary bands, indicating where the majority of the workforce falls in terms of earnings.
* **Total Bonus Company-wide by Region:** A **Clustered Column Chart** presents the total bonus amount allocated per region, showing the regional distribution of bonus payouts.
* **Total Pay Company-wide by Region:** A **Clustered Column Chart** displays the total compensation (salary inclusive of bonus) distributed across each region.
* **Bonus Allocation & Total Pay:** A **Table Visual** provides a detailed, row-level breakdown for each employee, showing their `Name`, `Department`, `Salary`, `IAnnual Bonus`, and `Total Pay`.
* 
## Recommendations & Insights
**1. Insights & Recommendations on Gender Distribution:**
* **Insight:** "The overall gender distribution shows a slight imbalance, with Males comprising 49.2% and Females comprising 46.45% of the total workforce, indicating a need for greater diversity initiatives. This imbalance is particularly pronounced in departments such as `Services` and `Business Development`, where one gender significantly outnumbers the other."
* **Recommendation:** "Implement targeted recruitment and talent development programs aimed at increasing the representation of underrepresented genders in departments identified with significant imbalances, aim to increase female representation in Product Management by 7.86%. Establish diversity metrics to track progress and hold department heads accountable."

**2. Insights & Recommendations on Performance Rating by Gender:**
* **Insight:** "Analysis of performance ratings by gender reveals a disproportionate number of males receiving 'Poor' or 'Very Poor' ratings compared to females. For instance, 16.3% of Male employees received 'Poor' ratings, versus 14.3% of Female employees."
* **Recommendation:** "Conduct a comprehensive review of the performance appraisal process to identify and mitigate potential unconscious biases. Provide mandatory bias awareness training for all managers involved in performance evaluations. Consider implementing standardized performance metrics and calibration sessions across departments."

**3. Insights & Recommendations on Salary Structure and Gender Pay Gap:**
* **Insight:** A significant gender pay gap has been identified within the company. Overall, males earn an average of 3.55% more than females. This gap is most pronounced in the Human Resources department, showing a 9.78% difference.
* **Recommendation:** Immediately initiate a detailed compensation audit, focusing on departments with the largest identified gender pay gaps, Human Resources. Develop and implement a structured plan to adjust salaries for underpaid genders to achieve pay equity, ensuring transparency in compensation policies moving forward.

**4. Insights & Recommendations on Minimum Wage Compliance:**
* **Insight:** "Palmoria Group currently has 292 employees (31%) earning below the newly adopted $90,000 minimum wage regulation, indicating a significant compliance issue for this portion of the workforce. While more employees are earning at least $90k, the presence of 292 employees below the threshold requires immediate attention."
* **Recommendation:** "Prioritize and allocate a budget of $26.5M to immediately uplift all 31% non-compliant employee salaries to meet the $90,000 minimum requirement. Establish a continuous monitoring system within HR to prevent future non-compliance and ensure all new hires meet the minimum threshold."

**5. Insights & Recommendations on Annual Bonus Allocation & Total Pay:**
* **Insight:** "The total bonus allocation for the company is $2.20M, with total pay (salary + bonus) reaching $183.29bn. While performance-based, there appears to be a pattern where some of the employees receive disproportionately lower bonus percentages relative to their performance ratings."
* **Recommendation:** "Review the current bonus allocation rules and their impact on total compensation to ensure they do not inadvertently contribute to gender pay disparities. Consider incorporating equity assessments into the annual bonus review process, ensuring fair distribution based purely on performance and contribution."

## How to Use This Report

1.  Clone this repository to your local machine.
2.  Ensure you have Power BI Desktop installed.
3.  Open the `Palmoria_HR_Analysis.pbix` file.
4.  Interact with the report using the slicers and filters to explore insights across different departments and regions.

## Author
Adepoju Emmanuel  
Connect with me on:  
[GitHub](Poju010)  
[LinkedIn](https://www.linkedin.com/in/emmanuel-adepoju-5657032b2)  
[WhatsApp](https://wa.me/2348084684382)
