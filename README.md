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

```
-- View all field names
SELECT *
FROM patient_demography;
``
