# SQL_Project01

- Create table and data manipulation using SQL

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
