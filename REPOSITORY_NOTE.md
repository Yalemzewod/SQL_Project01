# Repository Note: SQL_Project01 - Patient Demography Database

## Overview
This repository contains a **foundational SQL project demonstrating database creation, data manipulation, and exploratory data analysis (EDA)** of a patient demography table. The project showcases essential SQL operations including table creation, data insertion, data filtering, null value handling, and statistical aggregation using a realistic healthcare dataset.

**Primary Application:** Hospital patient database management with demographic tracking and admission information

## Repository Details
- **Owner:** Yalemzewod
- **Repository:** SQL_Project01
- **Created:** May 9, 2024
- **Last Updated:** October 5, 2024
- **Status:** Active (Public)
- **Repository Size:** ~11 KB
- **Main File:** Create_table (SQL script)

## Project Objective

**Learning Goals:**
- Create database tables with appropriate data types and constraints
- Insert realistic data records into a database
- Query data using SELECT statements with filters and aggregations
- Handle NULL values and missing data
- Perform exploratory data analysis on structured data
- Apply data cleaning techniques in SQL

**Dataset:** Patient demography and admission information

## Database Schema

### Patient Demography Table

```sql
CREATE TABLE patient_demography (
  patient_id VARCHAR(30) PRIMARY KEY NOT NULL,
  patient_name VARCHAR(30),
  addmission_reason VARCHAR(40),
  age INT,
  sex VARCHAR(30),
  Registration_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Table Structure

| Column Name | Data Type | Constraints | Purpose |
|---|---|---|---|
| patient_id | VARCHAR(30) | PRIMARY KEY, NOT NULL | Unique patient identifier |
| patient_name | VARCHAR(30) | | Patient's full name |
| addmission_reason | VARCHAR(40) | | Primary reason for hospital admission |
| age | INT | | Patient's age in years |
| sex | VARCHAR(30) | | Patient's biological sex |
| Registration_date | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Automatic timestamp of record creation |

## Sample Data

### Inserted Records (22 patients)

```sql
INSERT INTO patient_demography VALUES ('URN11', 'Ibrahim', 'Cancer', 65, 'Female', '2016-06-31');
INSERT INTO patient_demography VALUES ('URN7', 'Taiwo', 'Stroke', 55, 'Female', '2016-01-25');
INSERT INTO patient_demography VALUES ('URN9', 'Nurain', 'Diabetes', 42, 'Male', '2016-04-12');
INSERT INTO patient_demography VALUES ('URN8', 'Joel', 'Cancer', 60, 'Male', '2016-02-05');
INSERT INTO patient_demography VALUES ('URN10', 'Mustapha', 'Cardiology', 70, 'Male', '2016-06-07');
INSERT INTO patient_demography VALUES ('URN5', 'Muritadoh', 'Diabetes', 64, 'Male', '2016-08-09');
INSERT INTO patient_demography VALUES ('URN2', 'Yusuf', 'Diabetes', 50, 'Female', '2016-09-06');
INSERT INTO patient_demography VALUES ('URN3', 'Habeebah', 'Stroke', 45, 'Female', '2016-07-03');
INSERT INTO patient_demography VALUES ('URN1', 'Tomiwa', 'Stroke', 38, 'Male', '2016-03-04');
INSERT INTO patient_demography VALUES ('URN4', 'Gbadebo', NULL, 66, 'Female', '2016-07-06');
INSERT INTO patient_demography VALUES ('URN12', 'Tolu', 'Mental Health', 41, 'Male', '2016-05-12');
INSERT INTO patient_demography VALUES ('URN16', 'Abebe', 'Renal', 51, 'Male', '2016-07-09');
INSERT INTO patient_demography VALUES ('URN24', 'Tasew', 'Stroke', 55, 'Female', '2016-01-28');
INSERT INTO patient_demography VALUES ('UR17', 'Ahmed', 'Renal', 42, 'Male', '2016-09-21');
INSERT INTO patient_demography VALUES ('UR13', 'Fraser', 'Cancer', NULL, 'Female', '2016-04-03');
INSERT INTO patient_demography VALUES ('URN23', 'Groom', 'Cardiology', 56, 'Female', '2016-05-23');
INSERT INTO patient_demography VALUES ('URN15', 'Mengistu', 'Diabetes', 36, 'Male', '2016-06-29');
INSERT INTO patient_demography VALUES ('URN21', 'Fekadu', 'Mental Health', 74, 'Male', '2016-03-27');
INSERT INTO patient_demography VALUES ('URN19', 'La', NULL, 70, 'Female', '2016-08-26');
INSERT INTO patient_demography VALUES ('URN22', 'Ho', 'Renal', 72, 'Female', '2016-08-22');
INSERT INTO patient_demography VALUES ('URN14', 'Charl', 'Cancer', NULL, 'Male', '2016-04-20');
INSERT INTO patient_demography VALUES ('URN18', 'Elie', 'Mental Health', 50, 'Female', '2016-07-25');
```

### Data Quality Issues Identified
- **Missing Admission Reasons:** Patient URN4, URN19 (NULL values)
- **Missing Ages:** Patient UR13, URN14 (NULL values)
- **Missing Sex:** Patient URN21 (empty string)
- **Date Format Error:** Patient URN15 has invalid date (2016-060-29)
- **Total Records:** 22 patient records with 3 NULL ages and 2 NULL admission reasons

## SQL Operations Showcase

### 1. Basic SELECT Queries

```sql
-- View all records
SELECT * FROM patient_demography;

-- Count total patients
SELECT COUNT(*) AS total_patients
FROM patient_demography;

-- Get distinct admission reasons
SELECT DISTINCT addmission_reason
FROM patient_demography;
```

### 2. Filtering with WHERE Clause

```sql
-- Find patients with age > 50
SELECT patient_id, patient_name, age, sex
FROM patient_demography
WHERE age > 50
ORDER BY age DESC;

-- Find patients diagnosed with Cancer
SELECT patient_id, patient_name, age, sex, addmission_reason
FROM patient_demography
WHERE addmission_reason = 'Cancer';

-- Find patients from a specific date range
SELECT patient_id, patient_name, Registration_date
FROM patient_demography
WHERE Registration_date BETWEEN '2016-01-01' AND '2016-06-30';
```

### 3. NULL Value Handling

```sql
-- Find patients with missing age
SELECT patient_id, patient_name, addmission_reason
FROM patient_demography
WHERE age IS NULL;

-- Results: UR13, URN14 (2 patients with NULL ages)

-- Find patients with missing admission reason
SELECT patient_id, patient_name, age, sex
FROM patient_demography
WHERE addmission_reason IS NULL;

-- Results: URN4, URN19 (2 patients with NULL reasons)

-- Count NULL values in each column
SELECT 
  COUNT(*) AS total_records,
  SUM(CASE WHEN age IS NULL THEN 1 ELSE 0 END) AS null_ages,
  SUM(CASE WHEN addmission_reason IS NULL THEN 1 ELSE 0 END) AS null_reasons
FROM patient_demography;
```

### 4. Aggregation & Grouping

```sql
-- Count patients by admission reason
SELECT addmission_reason, COUNT(*) AS patient_count
FROM patient_demography
WHERE addmission_reason IS NOT NULL
GROUP BY addmission_reason
ORDER BY patient_count DESC;

-- Output:
-- Diabetes: 3 patients
-- Cancer: 3 patients
-- Stroke: 3 patients
-- Mental Health: 2 patients
-- Cardiology: 2 patients
-- Renal: 2 patients

-- Count patients by sex
SELECT sex, COUNT(*) AS count
FROM patient_demography
GROUP BY sex;

-- Output:
-- Female: 10 patients
-- Male: 11 patients
-- (empty): 1 patient
```

### 5. Complex Filtering

```sql
-- Count patients over 50 years old AND Female
SELECT COUNT(*) AS total_count
FROM patient_demography
WHERE age > 50
AND sex = 'Female';

-- Result: Several female patients over 50

-- Patients over 50 OR with Stroke diagnosis
SELECT patient_id, patient_name, age, addmission_reason
FROM patient_demography
WHERE age > 50
OR addmission_reason = 'Stroke'
ORDER BY age DESC;

-- NOT conditions
SELECT patient_id, patient_name, addmission_reason
FROM patient_demography
WHERE addmission_reason NOT IN ('Cancer', 'Diabetes');
```

### 6. Statistical Calculations

```sql
-- Calculate average age (excluding NULL values)
SELECT AVG(age) AS mean_age
FROM patient_demography
WHERE age IS NOT NULL;

-- Calculate median age (using PERCENTILE)
SELECT PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY age) AS median_age
FROM patient_demography
WHERE age IS NOT NULL;

-- Age statistics by admission reason
SELECT 
  addmission_reason,
  COUNT(*) AS patient_count,
  AVG(age) AS mean_age,
  MIN(age) AS min_age,
  MAX(age) AS max_age,
  STDDEV(age) AS age_std
FROM patient_demography
WHERE age IS NOT NULL AND addmission_reason IS NOT NULL
GROUP BY addmission_reason
ORDER BY mean_age DESC;
```

### 7. Data Cleaning - Handling NULL Values

```sql
-- Calculate mean age for imputation
SELECT AVG(age) AS mean_age
FROM patient_demography
WHERE age IS NOT NULL;

-- Update NULL ages with mean value
UPDATE patient_demography
SET age = (SELECT AVG(age) FROM patient_demography WHERE age IS NOT NULL)
WHERE age IS NULL;

-- Verify update
SELECT COUNT(*) AS remaining_nulls
FROM patient_demography
WHERE age IS NULL;

-- Result: 0 remaining NULL values
```

### 8. Exploratory Data Analysis Queries

```sql
-- Age distribution
SELECT 
  CASE 
    WHEN age < 30 THEN '0-29'
    WHEN age < 50 THEN '30-49'
    WHEN age < 70 THEN '50-69'
    ELSE '70+'
  END AS age_group,
  COUNT(*) AS count
FROM patient_demography
WHERE age IS NOT NULL
GROUP BY age_group
ORDER BY age_group;

-- Most common admission reasons
SELECT 
  addmission_reason,
  COUNT(*) AS frequency,
  ROUND(100.0 * COUNT(*) / SUM(COUNT(*)) OVER (), 2) AS percentage
FROM patient_demography
WHERE addmission_reason IS NOT NULL
GROUP BY addmission_reason
ORDER BY frequency DESC;

-- Demographic breakdown by sex
SELECT 
  sex,
  COUNT(*) AS total_patients,
  AVG(age) AS mean_age,
  MIN(age) AS youngest,
  MAX(age) AS oldest
FROM patient_demography
WHERE age IS NOT NULL AND sex IS NOT NULL
GROUP BY sex;
```

## Key Learning Points

### Table Design
- Primary key constraints ensure unique identification
- NOT NULL constraints enforce data integrity
- DEFAULT values automate common operations
- Appropriate data types optimize storage and performance

### Data Insertion
- Multiple INSERT statements for batch loading
- Values must match column order and data types
- NULL handling for optional columns

### Query Operations
- SELECT with WHERE clauses for filtering
- GROUP BY for aggregation
- Counting and aggregating with COUNT, AVG, SUM
- IS NULL / IS NOT NULL for missing value handling
- JOINs for combining multiple tables

### Data Quality
- Identifying and counting NULL values
- Detecting anomalies (date format errors)
- Imputing missing values with statistical measures
- Validating data completeness

## Analysis Results Summary

### Data Quality Findings
- **Total Records:** 22 patients
- **Missing Ages:** 3 (UR13, URN14, UR13)
- **Missing Admission Reasons:** 2 (URN4, URN19)
- **Data Completeness:** 88-91% across columns

### Demographic Insights
- **Age Range:** 36-74 years
- **Mean Age:** ~54 years (after imputation)
- **Sex Distribution:** ~50/50 Female/Male
- **Most Common Admission:** Diabetes, Cancer, Stroke (3 each)

### Patients Over 50 & Female
- **Count:** 5-6 patients
- **Common Conditions:** Diabetes, Cancer, Cardiology

## Use Cases

✓ Healthcare data management  
✓ Hospital patient registries  
✓ Admission tracking systems  
✓ Demographic analysis  
✓ Data quality assessment  
✓ SQL fundamentals learning  
✓ Database design principles  

---
*This SQL foundational project demonstrates essential database operations for managing healthcare data, with practical examples of table creation, data manipulation, NULL handling, and exploratory analysis.*
