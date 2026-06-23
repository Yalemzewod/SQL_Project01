# SQL_Project01

## Key Learning Points

1. Table Design
- Primary key constraints ensure unique identification
- NOT NULL constraints enforce data integrity
- DEFAULT values automate common operations
- Appropriate data types optimize storage and performance
  
2. Data Insertion
- Multiple INSERT statements for batch loading
- Values must match column order and data types
- NULL handling for optional columns
3. Query Operations
- SELECT with WHERE clauses for filtering
- GROUP BY for aggregation
- Counting and aggregating with COUNT, AVG, SUM
- IS NULL / IS NOT NULL for missing value handling
- JOINs for combining multiple tables

4. Data Quality
- Identifying and counting NULL values
- Detecting anomalies (date format errors)
- Imputing missing values with statistical measures
- Validating data completeness
- Analysis Results Summary

## What is in the data - overview
1. Data Quality Findings
- Total Records: 22 patients
- Missing Ages: 3 (UR13, URN14, UR13)
- Missing Admission Reasons: 2 (URN4, URN19)
- Data Completeness: 88-91% across columns

2. Demographic Insights
- Age Range: 36-74 years
- Mean Age: ~54 years (after imputation)
- Sex Distribution: ~50/50 Female/Male
- Most Common Admission: Diabetes, Cancer, Stroke (3 each)
- Patients Over 50 & Female
- Count: 5-6 patients
- Common Conditions: Diabetes, Cancer, Cardiology


## Use Cases
✓ Healthcare data management
✓ Hospital patient registries
✓ Admission tracking systems
✓ Demographic analysis
✓ Data quality assessment
✓ SQL fundamentals learning
✓ Database design principles
- Create table and data manipulation using SQL
  
## Sample query
```
DROP TABLE IF EXISTS patient_demography;
-- Create table
CREATE TABLE patient_demography (
  patient_id VARCHAR(30) PRIMARY KEY NOT NULL,
  patient_name VARCHAR(30),
  addmission_reason VARCHAR(40),
  age INT,
  sex VARCHAR(30),
  Registration_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
View all rows and columns in the table
```
-- View all field names
SELECT *
FROM patient_demography;
```
Patients where age is null
```
-- Filter patient_id where age is null
SELECT patient_id, COUNT(*)
FROM patient_demography
WHERE age IS NULL
GROUP BY patient_id;
```
UR13	1
URN14	1

Select count where age is >50 and female
```
-- count patient age >50 and Female
SELECT COUNT(*) AS total_count
FROM patient_demography
WHERE age > 50
AND sex ='Female';

```
