# HR-Analytics
## Introduction:
A company which is active in Big Data and Data Science wants to hire data scientists among people who successfully pass some courses which conduct by the company.
Many people signup for their training. Company wants to know which of these candidates are really wants to work for the company after training or looking for a new employment because it helps to reduce the cost and time as well as the quality of training or planning the courses and categorization of candidates.
Information related to demographics, education, experience are in hands from candidates signup and enrollment.
## Dataset:

1. Enrollies' data
The source: https://docs.google.com/spreadsheets/d/1VCkHwBjJGRJ21asd9pxW4_0z2PWuKhbLR3gUHm-p4GI/edit?usp=sharing
enrollee_id: unique ID of an enrollee
full_name: full name of an enrollee
city: the name of an enrollie's city
gender: gender of an enrollee
The source: https://docs.google.com/spreadsheets/d/1VCkHwBjJGRJ21asd9pxW4_0z2PWuKhbLR3gUHm-p4GI/edit?usp=sharing

2. Enrollies' education
https://assets.swisscoding.edu.vn/company_course/enrollies_education.xlsx
This table contains the following columns:
enrollee_id: A unique identifier for each enrollee. This integer value uniquely distinguishes each participant in the dataset.
enrolled_university: Indicates the enrollee's university enrollment status. Possible values include no_enrollment, Part time course, and Full time course.
education_level: Represents the highest level of education attained by the enrollee. Examples include Graduate, Masters, etc.
major_discipline: Specifies the primary field of study for the enrollee. Examples include STEM, Business Degree, etc.

3. Enrollies' working experience
Educational department stores it in the CSV format here: https://assets.swisscoding.edu.vn/company_course/work_experience.csv
This table contains the following columns:
enrollee_id: A unique identifier for each enrollee. This integer value uniquely distinguishes each participant in the dataset.
relevent_experience: Indicates whether the enrollee has relevant work experience related to the field they are currently studying or working in. Possible values include Has relevent experience and No relevent experience.
experience: Represents the number of years of work experience the enrollee has. This can be a specific number or a range (e.g., >20, <1).
company_size: Specifies the size of the company where the enrollee has worked, based on the number of employees. Examples include 50−99, 100−500, etc.
company_type: Indicates the type of company where the enrollee has worked. Examples include Pvt Ltd, Funded Startup, etc.
last_new_job: Represents the number of years since the enrollee's last job change. Examples include never, >4, 1, etc.

4. Training hours
A number of training hours for each student that they have completed.
Database credentials:
Database type: MySQL
Host: 112.213.86.31
Port: 3360
Login: etl_practice
Password: 550814
Database name: company_course
Table name: training_hours

5. City development index
https://sca-programming-school.github.io/city_development_index/index.html

6. Employment:
Database type: MySQL
Host: 112.213.86.31
Port: 3360
Login: etl_practice
Password: 550814
Database name: company_course
Table name: employment

## Processing data:
### 1. Import library:
Installs the pymysql library, which enables Python to interact with a MySQL database using the PyMySQL protocol.

### 2. Extract data:
#### 2.1 Enrollies' data:

Import excel file and info data.
![image](https://github.com/user-attachments/assets/6c725aae-4300-4c9c-b191-a8d957760810)

#### 2.2 Enrollies' education:
Upload the excel file name's enrollies_education.xlsx and reveiw data.
![image](https://github.com/user-attachments/assets/21ff05e0-17f4-40dc-b047-86693381f6a3)

#### 2.3 Enrollies' working experience
Load the csv data
![image](https://github.com/user-attachments/assets/93f3d284-fad3-4aba-bba5-720573b47e7f)

#### 2.4 Training hours
Connects to a MySQL database and extracts the training_hours table for further data analysis in Python.
Creates a SQLAlchemy engine to connect to the MySQL database.
![image](https://github.com/user-attachments/assets/2b1f30d0-2126-496e-8be8-c9da693e3069)

#### 2.5 City development index
In this step, we extract data from a public HTML table available online. The target dataset contains the City Development Index, which quantitatively represents the general development level of various cities.
The result is a list of tables (tables), where each item is a DataFrame
![image](https://github.com/user-attachments/assets/8b0341cb-073c-4743-bb88-c0c4dc3164b3)

#### 2.6 Employment
In this step, we connect to the SQL database and extract the employment table, which records the employment status of each enrollee.
Let's use engine we already created, connect to the SQL database and extract the employment table, which records the employment status of each enrollee.
![image](https://github.com/user-attachments/assets/11493e18-7cf0-4146-b1d3-5c443205a11f)

### 3 Transform Data:
#### 3.1  Enrollies' data:

Initial Data Inspection
![image](https://github.com/user-attachments/assets/c743fdc6-7acc-4d94-b071-8db86febf84b)
19,158 records, 4 columns
Only gender contains missing values
Check duplicate value gender
Change data type: [full_name], [gender]/ [city] are string.
cleaning missing data by mode for [gender]

#### 3.2 Enrollies' education:

Initial Data Overview
![image](https://github.com/user-attachments/assets/cfdd0112-dbe0-4983-81b7-e9b101bfb8de)
Total rows: 19,158
Missing values detected in:
enrolled_university (286 missing)
education_level (270 missing)
major_discipline (813 missing)

Filling Missing Values with Mode:

✅ Filled missing values in 'enrolled_university' with mode: no_enrollment
✅ Filled missing values in 'education_level' with mode: Graduate
✅ Filled missing values in 'major_discipline' with mode: STEM

Unique Value Exploration
Data Type 

#### 3.3 Enrollies' working experience:
Overview data
![image](https://github.com/user-attachments/assets/3f4e3499-d844-4c73-aff1-103344632de0)

The dataset contains 19,158 records across 6 columns, with several object-type fields.
Missing values were detected in:
experience (165 records)
company_size (1,938 records)
company_type (1,840 records)
last_new_job (321 records)

The missing values are experience , company_size, company_type, last_new_job columns. So handling them one by mode for each one.

✅ Filled missing values in 'experience' with mode: >20
✅ Filled missing values in 'company_size' with mode: 50-99
✅ Filled missing values in 'company_type' with mode: Pvt Ltd
✅ Filled missing values in 'last_new_job' with mode: 1

Exploring Unique Values (Category Distribution)
Converts all object-type columns into category dtype

#### 3.4 Training hours:
Overview:
![image](https://github.com/user-attachments/assets/57640cbb-17be-47df-b27c-785ff731ded2)

Dataset contains 19,158 rows with 2 fields:
enrollee_id: unique identifier
training_hours: number of hours each enrollee has undergone training

📌 No missing values are present, both columns are in int64 format.

This summary provides essential statistical indicators:
Mean: 65.37 hours
Median (50%): 47 hours
Standard Deviation: 60.06 hours (relatively high dispersion)
Max value: 336 hours

🧠 This suggests the presence of potential outliers, especially on the upper end.

##### Outlier Detection Function – IQR Method
Method: Interquartile Range (IQR) filtering
Logic:
Detects and filters out values significantly below Q1 or above Q3
Only values within range 𝑄 1 − 1.5 × 𝐼 𝑄 𝑅 , 𝑄 3 + 1.5 × 𝐼 𝑄 𝑅 Q1−1.5×IQR,Q3+1.5×IQR are retained
Apply Outlier Removal on training_hours Column

#### 3.5 City development index:
Overview:
![image](https://github.com/user-attachments/assets/89f5a7bd-dedc-4cf3-8025-6a08f743d108)

Unique Value Exploration
Convert 'City' to String Type
Check Unique Values of City Development Index

#### 3.6 Employment:
Overview:
![image](https://github.com/user-attachments/assets/447591f2-33d2-4a23-a8c2-5b22a8768409)

The dataset contains 19,158 rows and 2 columns:
enrollee_id: unique identifier for each individual (currently int64)
employed: employment status (likely binary or boolean-style encoded as float64)

✅ No missing values in either column

📌 employed is likely a target variable in a classification problem (e.g., predicting job status)

Data Type Conversion for ID Field

### 4 Load Data:

💾 SQLite Data Warehouse Export
This code exports all cleaned and preprocessed DataFrames to an SQLite database called data_warehouse.db, creating a lightweight yet queryable data warehouse structure.
Initializes a connection to a local SQLite database
Enables Pandas to interact with SQL seamlessly using SQLAlchemy

📋 Tables Written to Database


