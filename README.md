# hr-analytics-sql-powerbi

## Table of Contents
- [Project Overview](#project-overview)
- [Tools Used](#tools-used)
-   [Data Cleaning & Preparation](#data-cleaning--preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
 - [Result/Findings](#resultfindings)
-   [Limitations](#limitations)
 -  [Recommendations](#recommendations)


### Project Overview

This project focuses on HR data analysis using SQL for data cleaning, transformation, and deriving meaningful insights. The dataset includes employee records such as ID, birth date, hire date, termination date, gender, department, job title, and location.
The goal is to support HR decision-making by answering critical business questions related to employee demographics, attrition, hiring trends, tenure, and workforce composition.

### Datasource

The dataset used in this project was sourced from the following GitHub repository:

🔗 [Human Resources Dataset – Irene-arch/HR-Dashboard-MySQL-PowerBI](https://github.com/Irene-arch/HR-Dashboard-MySQL-PowerBI/blob/main/Human%20Resources.csv)

All credit for the dataset goes to the original author.

### Tools used

- WorkBench (MySQL Workbench) – For SQL-based data cleaning, transformation, and exploratory analysis
- Power BI – For creating dynamic dashboards and data visualizations
- GitHub – For project version control and hosting the portfolio
- 
  ### Data Cleaning & Preparation
The raw HR dataset required several cleaning steps to make it suitable for analysis. All data cleaning was performed using MySQL Workbench.

 Key Cleaning Steps:
1. Fix Column Name Encoding

Renamed the malformed ï»¿id column to EMP_ID for clarity and consistency.

2. Date Format Standardization

Converted inconsistent date formats (MM/DD/YYYY, MM-DD-YYYY) in birthdate, hire_date, and termdate to the standard YYYY-MM-DD.

Cast date strings into proper DATE data types using STR_TO_DATE() and DATE_FORMAT() functions.

3. Null Handling

Replaced empty strings in the termdate column with NULL values for accurate filtering.

Ensured non-terminated employees (i.e., currently employed) are identified by checking for termdate IS NULL.

4. Feature Engineering

Added a new column Age by calculating the difference between the current date and birthdate using TIMESTAMPDIFF().

Created Age Groups (e.g., 18–24, 25–34, etc.) to support demographic analysis.

5. Data Filtering

Filtered out employees with future termdate values (if any).

Focused many queries on active employees by filtering with the term date IS NULL.

### Exploratory Data Analysis

During the EDA phase, the following business and analytical questions were explored using SQL:

1. Employee Demographics
What is the gender breakdown of employees in the company?

What is the racial composition of the workforce?

What is the age distribution of employees?

How does age distribution vary by gender?

2. Department & Job Structure
How are employees distributed across departments?

What is the distribution of job titles across the company?

Which departments have the most or fewest employees?

3. Location-Based Analysis
How many employees work remotely vs on-site?

What is the employee distribution by location state?

4. Employee Lifecycle
What is the average tenure of employees who left the company?

Which departments have the highest turnover/termination rate?

How has the employee count changed over time (hires vs terminations)?

What is the net headcount change over the years?

5. Bonus Insight:
How does the gender distribution vary by department and job title?

### Data Analysis
include some interesting codes/features worked with
 ```ALTER TABLE HR ADD COLUMN Age INT;
UPDATE HR SET AGE = TIMESTAMPDIFF(YEAR, birthdate, CURDATE());

SELECT
  CASE
    WHEN AGE BETWEEN 18 AND 24 THEN '18-24'
    WHEN AGE BETWEEN 25 AND 34 THEN '25-34'
    WHEN AGE BETWEEN 35 AND 44 THEN '35-44'
    WHEN AGE BETWEEN 45 AND 54 THEN '45-54'
    WHEN AGE BETWEEN 55 AND 64 THEN '55-64s'
    ELSE '65+'
  END AS AGE_GROUP,
  COUNT(*) AS Count
FROM hr
WHERE term date IS NULL
GROUP BY AGE_GROUP;

### Result/findings
The Analysis result are summarized as follows:
1. Most employees are aged 25–44, indicating a mid-career workforce.

2. Gender distribution is fairly balanced; diversity exists across races.

3. The majority work on-site, with a growing number of remote employees.

4. Some departments are growing, while others face a decline in headcount.

5. Hiring outpaced terminations in some years, while others showed downsizing.

6. Job titles and departments like Sales and Engineering have the most employees.

### Recommendations
Based on the recommendations, we recommend the following actions:



- Address high turnover in specific departments through surveys or exit interviews.  
- Promote diversity and inclusion in leadership and technical roles.  
- Expand remote work opportunities to attract wider talent pools.  
- Monitor hiring vs attrition trends regularly to ensure workforce stability.  
- Focus on departments with low tenure for potential management or culture improvements.


### Limitations
1. Date format inconsistencies in birthdate, hire_date, and termdate required manual cleaning, which may not be fully error-proof.

2. Some termdate values were missing or blank, which could affect the accuracy of attrition and tenure analysis.

3. Age and tenure were calculated using approximate logic (e.g., DATEDIFF/365), which may slightly differ from exact values.

4. The analysis is based on static historical data and doesn’t reflect real-time changes or employee performance metrics.

5. Data does not include key HR dimensions like salary, job satisfaction, or performance, limiting deeper insights.







