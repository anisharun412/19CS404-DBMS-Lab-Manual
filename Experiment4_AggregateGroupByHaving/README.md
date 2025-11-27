# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
How many appointments are scheduled for each doctor?
Sample table:Appointments Table

| AppointmentID | PatientID | DoctorID | AppointmentDateTime     | Purpose               | Status     |
|---------------|-----------|----------|--------------------------|-----------------------|------------|
| 1             | 1         | 1        | 2024-02-15 09:00:00      | Routine checkup       | Confirmed  |
| 2             | 2         | 2        | 2024-02-16 10:30:00      | Vaccination           | Confirmed  |
| 3             | 3         | 3        | 2024-02-17 11:00:00      | Follow-up on surgery  | Confirmed  |

```sql
select DoctorID, count(DoctorID) as TotalAppointments from Appointments group by DoctorID;
```

**Output:**

<img width="875" height="719" alt="image" src="https://github.com/user-attachments/assets/4d587aac-0b52-489a-92a8-c124fd13ad6a" />

**Question 2**
---
Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table
| RecordID | PatientID | DoctorID | Date       | Diagnosis                | Treatment                   | Medications               |
|----------|-----------|----------|------------|---------------------------|-----------------------------|---------------------------|
| 1        | 1         | 1        | 2024-01-10 | High blood pressure       | Prescribed medication       | Lisinopril                |
| 2        | 2         | 2        | 2023-12-20 | Childhood vaccination     | Administered vaccines       | MMR, DPT                  |
| 3        | 3         | 3        | 2024-01-05 | Fractured femur           | Performed surgery           | Ibuprofen, Calcium supplement |


```sql
select PatientID, count(Medications) as AvgMedications from MedicalRecords group by PatientID;
```

**Output:**

<img width="883" height="693" alt="image" src="https://github.com/user-attachments/assets/cc027b33-52ea-4e1e-a9cb-924ca737b7ba" />

**Question 3**
---
What is the total number of medications prescribed for each patient?

Sample tablePrescriptions Table
| PrescriptionID | PatientID | DoctorID | Date       | Medication  | Dosage | Frequency       |
|----------------|-----------|----------|------------|-------------|--------|-----------------|
| 1              | 1         | 1        | 2024-01-10 | Lisinopril  | 10 mg  | Once daily      |
| 2              | 2         | 2        | 2023-12-20 | MMR         | 0.5 mL | Once            |
| 3              | 3         | 3        | 2024-01-05 | Ibuprofen   | 400 mg | Every 6 hours   |

```sql
select PatientID, count(Medication) as TotalMedications from Prescriptions group by Medication order by PatientID;
```

**Output:**

<img width="880" height="834" alt="image" src="https://github.com/user-attachments/assets/96675f80-0ad0-4811-a2c0-4bbc592bc157" />

**Question 4**
---
Write a SQL query to find the number of employees whose age is greater than 32.

Sample table: employee
| id | name  | age | address    | salary |
|----|-------|-----|------------|--------|
| 1  | Paul  | 32  | California | 20000  |
| 4  | Mark  | 25  | Richtown   | 65000  |
| 5  | David | 27  | Texas      | 85000  |

```sql
select count(*) as COUNT from employee where age > 32;
```

**Output:**

<img width="880" height="404" alt="image" src="https://github.com/user-attachments/assets/c27a6191-b8e1-4ed8-9221-ae20f5b8490d" />

**Question 5**
---
Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.

Table: employee
| name   | type     |
|--------|----------|
| id     | INTEGER  |
| name   | TEXT     |
| age    | INTEGER  |
| city   | TEXT     |
| income | INTEGER  |


```sql
select (max(age)-min(age)) as age_difference from employee;
```

**Output:**

<img width="876" height="397" alt="image" src="https://github.com/user-attachments/assets/98a1bdb1-d390-4852-aafc-1b5a39ecacb2" />

**Question 6**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is not Noida.

Sample table: customer
| id | name         | city      | email             | phone      |
|----|--------------|-----------|-------------------|------------|
| 1  | Ravi Kumar   | Delhi     | ravi@gmail.com    | 985664321  |
| 2  | Neha Sharma  | Mumbai    | neha@gmail.com    | 987654321  |
| 3  | Rohit Singh  | Bangalore | rohit@gmail.com   | 887694721  |

```sql
select count(*) as COUNT from customer where city<>'Noida';
```

**Output:**

<img width="886" height="405" alt="image" src="https://github.com/user-attachments/assets/cf4137fa-2b6b-4b45-a9b1-8a109b52ebdf" />

**Question 7**
---
Write a SQL query to find the average length of email addresses (in characters):

Table: customer-- Paste Question 7 here
| name  | type     |
|-------|----------|
| id    | INTEGER  |
| name  | TEXT     |
| city  | TEXT     |
| email | TEXT     |
| phone | INTEGER  |

```sql
select avg(length(email)) as avg_email_length from customer;
```

**Output:**

<img width="876" height="399" alt="image" src="https://github.com/user-attachments/assets/a586675b-e5af-4554-a00b-a77792f23527" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.

Sample table: employee1

| id | name     | occupation | jdate | workhour |
|----|----------|------------|-------|----------|
| 1  | Joseph   | Business   | 2006  | 10       |
| 2  | Stephen  | Doctor     | 2006  | 15       |
| 3  | Mark     | Engineer   | 2006  | 12       |
| 4  | Peter    | Teacher    | 2006  | 9        |


```sql
select occupation, MIN(workhour) from employee1 group by occupation;
```

**Output:**

<img width="880" height="571" alt="image" src="https://github.com/user-attachments/assets/7ddc27e2-0778-4b4b-b163-82125b24bbf4" />

**Question 9**
---
Which cities (addresses) in the "customer1" table have an average salary lesser than Rs. 15000

Sample table: customer1
| id | name    | age | address     | salary |
|----|---------|-----|-------------|--------|
| 1  | Ramesh  | 32  | Ahmedabad   | 2000   |
| 2  | Khilan  | 25  | Delhi       | 1500   |
| 3  | Kaushik | 23  | Kota        | 2000   |

```sql
select address, AVG(salary) from customer1 group by address having AVG(salary) < 15000;
```

**Output:**

<img width="874" height="689" alt="image" src="https://github.com/user-attachments/assets/7bd570ac-c2c6-426e-b3d9-28cf3167135d" />

**Question 10**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the average income for each age group, and includes only those age groups where the average income falls between 300,000 and 500,000.

Sample table: employee
| id  | name   | age | city       | income   |
|-----|--------|-----|------------|----------|
| 101 | Peter  | 32  | NewYork    | 200000   |
| 102 | Mark   | 32  | California | 300000   |
| 103 | Donald | 40  | Arizona    | 1000000  |
| 104 | Obama  | 35  | Florida    | 5000000  |

```sql
select age, AVG(income) from employee group by age having AVG(income) >= 300000 and AVG(income)<=500000;
```

**Output:**

<img width="878" height="424" alt="image" src="https://github.com/user-attachments/assets/b5cdb198-267b-4540-a068-a563dd4e0c04" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
