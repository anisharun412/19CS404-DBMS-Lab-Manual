# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

Sample table:
Customer
| customer_id | cust_name       | city       | grade | salesman_id |
|------------|----------------|------------|-------|-------------|
| 3002       | Nick Rimando   | New York   | 100   | 5001        |
| 3007       | Brad Davis     | New York   | 200   | 5001        |
| 3005       | Graham Zusi    | California | 200   | 5002        |
| 3008       | Julian Green   | London     | 300   | 5002        |
| 3004       | Fabian Johnson | Paris      | 300   | 5006        |
| 3009       | Geoff Cameron  | Berlin     | 100   | 5003        |
| 3003       | Jozy Altidor   | Moscow     | 200   | 5007        |
| 3001       | Brad Guzan     | London     |       | 5005        |

Salesman Table
| salesman_id | name        | city      | commission |
|------------|------------|-----------|------------|
| 5001       | James Hoog | New York  | 0.15       |
| 5002       | Nail Knite | Paris     | 0.13       |
| 5005       | Pit Alex   | London    | 0.11       |
| 5006       | Mc Lyon    | Paris     | 0.14       |
| 5007       | Paul Adam  | Rome      | 0.13       |
| 5003       | Lauson Hen | San Jose  | 0.12       |

```sql
SELECT 
    c.cust_name,
    c.city,
    c.grade,
    s.name as Salesman,
    s.city
FROM customer c
JOIN salesman s
    ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;

```

**Output:**

<img width="1292" height="1029" alt="image" src="https://github.com/user-attachments/assets/1c3afba4-ec7b-41c3-8b30-779d61122da7" />


**Question 2**
---
Write the SQL query that achieves the selection of all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
| patient_id | doctor_id | first_name | last_name | date_of_birth | admission_date | discharge_date |
|------------|-----------|------------|-----------|---------------|----------------|----------------|
| 1          | 1         | Alice      | Williams  | 1980-05-12    | 2024-01-10     | NULL           |
| 2          | 2         | Bob        | Miller    | 1995-08-23    | 2024-02-15     | 2024-03-01     |
| 3          | 3         | Charlie    | Davis     | 1972-11-30    | 2024-03-10     | NULL           |

TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date
| result_id | patient_id | test_name      | result                  | test_date   |
|-----------|------------|----------------|------------------------|------------|
| 1         | 1          | Blood Pressure | 120/80                 | 2024-01-20 |
| 2         | 2          | X-Ray          | Normal                 | 2024-03-05 |
| 3         | 3          | Blood Test     | Within Normal Range    | 2024-04-01 |


```sql
SELECT 
    t.*
FROM test_results AS t
INNER JOIN patients AS p
    ON t.patient_id = p.patient_id
WHERE p.first_name = 'Alice';
```

**Output:**

<img width="1287" height="506" alt="image" src="https://github.com/user-attachments/assets/c7592c39-39f4-47c8-b30f-c4d93ff87017" />


**Question 3**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

Sample table:
Orders Table

| ord_no | purch_amt | ord_date   | customer_id | salesman_id |
|--------|-----------|------------|-------------|-------------|
| 70001  | 150.5     | 2012-10-05 | 3005        | 5002        |
| 70009  | 270.65    | 2012-09-10 | 3001        | 5005        |
| 70002  | 65.26     | 2012-10-05 | 3002        | 5001        |
| 70004  | 110.5     | 2012-08-17 | 3009        | 5003        |
| 70007  | 948.5     | 2012-09-10 | 3005        | 5002        |
| 70005  | 2400.6    | 2012-07-27 | 3007        | 5001        |
| 70008  | 5760      | 2012-09-10 | 3002        | 5001        |
| 70010  | 1983.43   | 2012-10-10 | 3004        | 5006        |
| 70003  | 2480.4    | 2012-10-10 | 3009        | 5003        |
| 70012  | 250.45    | 2012-06-27 | 3008        | 5002        |
| 70011  | 75.29     | 2012-08-17 | 3003        | 5007        |
| 70013  | 3045.6    | 2012-04-25 | 3002        | 5001        |


Customer Table

| customer_id | cust_name       | city       | grade | salesman_id |
|-------------|----------------|------------|-------|-------------|
| 3002        | Nick Rimando   | New York   | 100   | 5001        |
| 3007        | Brad Davis     | New York   | 200   | 5001        |
| 3005        | Graham Zusi    | California | 200   | 5002        |
| 3008        | Julian Green   | London     | 300   | 5002        |
| 3004        | Fabian Johnson | Paris      | 300   | 5006        |
| 3009        | Geoff Cameron  | Berlin     | 100   | 5003        |
| 3003        | Jozy Altidor   | Moscow     | 200   | 5007        |
| 3001        | Brad Guzan     | London     |       | 5005        |


Salesman Table

| salesman_id | name        | city      | commission |
|------------|------------|-----------|------------|
| 5001       | James Hoog | New York  | 0.15       |
| 5002       | Nail Knite | Paris     | 0.13       |
| 5005       | Pit Alex   | London    | 0.11       |
| 5006       | Mc Lyon    | Paris     | 0.14       |
| 5007       | Paul Adam  | Rome      | 0.13       |
| 5003       | Lauson Hen | San Jose  | 0.12       |

```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM orders o
INNER JOIN customer c
       ON o.customer_id = c.customer_id
INNER JOIN salesman s
       ON o.salesman_id = s.salesman_id;
       
```

**Output:**

<img width="1496" height="1187" alt="image" src="https://github.com/user-attachments/assets/54108b35-1ac4-48cd-ba11-968c6af98bea" />

**Question 4**
---
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

NURSES TABLE:

ATTRIBUTES - nurse_id, first_name, last_name, department_id
| nurse_id | department_id | first_name | last_name |
|----------|---------------|------------|-----------|
| 1        | 1             | Emma       | Taylor    |
| 2        | 2             | David      | Moore     |
| 3        | 3             | Sophia     | Clark     |

DEPARTMENTS TABLE:

ATTRIBUTES - department_id, department_name
| department_id | department_name |
|---------------|----------------|
| 1             | Cardiology     |
| 2             | Orthopedics    |
| 3             | Pediatrics     |


```sql
SELECT 
    n.*, 
    d.department_name
FROM nurses AS n
INNER JOIN departments AS d
    ON n.department_id = d.department_id;
    
```

**Output:**

<img width="1294" height="663" alt="image" src="https://github.com/user-attachments/assets/3c7480a3-86b8-409c-99ab-38293a0b0d9f" />

**Question 5**
---
From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

Sample table: 
Customer Table

| customer_id | cust_name       | city       | grade | salesman_id |
|-------------|----------------|------------|-------|-------------|
| 3002        | Nick Rimando   | New York   | 100   | 5001        |
| 3007        | Brad Davis     | New York   | 200   | 5001        |
| 3005        | Graham Zusi    | California | 200   | 5002        |
| 3008        | Julian Green   | London     | 300   | 5002        |
| 3004        | Fabian Johnson | Paris      | 300   | 5006        |
| 3009        | Geoff Cameron  | Berlin     | 100   | 5003        |
| 3003        | Jozy Altidor   | Moscow     | 200   | 5007        |
| 3001        | Brad Guzan     | London     |       | 5005        |


Salesman Table

| salesman_id | name        | city      | commission |
|------------|------------|-----------|------------|
| 5001       | James Hoog | New York  | 0.15       |
| 5002       | Nail Knite | Paris     | 0.13       |
| 5005       | Pit Alex   | London    | 0.11       |
| 5006       | Mc Lyon    | Paris     | 0.14       |
| 5007       | Paul Adam  | Rome      | 0.13       |
| 5003       | Lauson Hen | San Jose  | 0.12       |

```sql
SELECT
    c.cust_name AS 'Customer Name',
    c.city AS city,
    s.name AS Salesman,
    s.commission
FROM customer c
JOIN salesman s
    ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;
```

**Output:**

<img width="1298" height="878" alt="image" src="https://github.com/user-attachments/assets/9c55c990-76a3-4d8d-93d2-704d8066e218" />

**Question 6**
---

Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```sql
SELECT
    s.name AS salesman_name,
    c.cust_name AS customer_name
FROM salesman AS s
LEFT JOIN customer AS c
    ON s.salesman_id = c.salesman_id;

```

**Output:**

<img width="1289" height="1004" alt="image" src="https://github.com/user-attachments/assets/4dfb71ee-4571-4b76-8fe6-6976c640e093" />

**Question 7**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  

Sample table:
Customer Table

| customer_id | cust_name       | city       | grade | salesman_id |
|-------------|----------------|------------|-------|-------------|
| 3002        | Nick Rimando   | New York   | 100   | 5001        |
| 3007        | Brad Davis     | New York   | 200   | 5001        |
| 3005        | Graham Zusi    | California | 200   | 5002        |
| 3008        | Julian Green   | London     | 300   | 5002        |
| 3004        | Fabian Johnson | Paris      | 300   | 5006        |
| 3009        | Geoff Cameron  | Berlin     | 100   | 5003        |
| 3003        | Jozy Altidor   | Moscow     | 200   | 5007        |
| 3001        | Brad Guzan     | London     |       | 5005        |


Salesman Table

| salesman_id | name        | city      | commission |
|------------|------------|-----------|------------|
| 5001       | James Hoog | New York  | 0.15       |
| 5002       | Nail Knite | Paris     | 0.13       |
| 5005       | Pit Alex   | London    | 0.11       |
| 5006       | Mc Lyon    | Paris     | 0.14       |
| 5007       | Paul Adam  | Rome      | 0.13       |

```sql
SELECT
    c.cust_name   AS "Customer Name",
    c.city AS "city",
    s.name AS "Salesman",
    s.city AS city,
    s.commission  AS commission
FROM customer AS c
INNER JOIN salesman AS s
    ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12
  AND s.city <> c.city
ORDER BY s.commission DESC;

```

**Output:**

<img width="1292" height="730" alt="image" src="https://github.com/user-attachments/assets/fb111870-bb1c-4d5d-8160-04aa114898dc" />


**Question 8**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
SELECT
    c.cust_name,
    o.ord_no,
    o.ord_date,
    o.purch_amt
FROM customer AS c
LEFT JOIN orders AS o
    ON c.customer_id = o.customer_id;
```

**Output:**

<img width="1338" height="1038" alt="image" src="https://github.com/user-attachments/assets/dcf1c9e6-be04-4c7d-99f5-91feb73ab25f" />

**Question 9**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table:
Salesman Table

| salesman_id | name        | city      | commission |
|------------|------------|-----------|------------|
| 5001       | James Hoog | New York  | 0.15       |
| 5002       | Nail Knite | Paris     | 0.13       |
| 5005       | Pit Alex   | London    | 0.11       |
| 5006       | Mc Lyon    | Paris     | 0.14       |
| 5007       | Paul Adam  | Rome      | 0.13       |
| 5003       | Lauson Hen | San Jose  | 0.12       |


Customer Table

| customer_id | cust_name       | city       | grade | salesman_id |
|-------------|----------------|------------|-------|-------------|
| 3002        | Nick Rimando   | New York   | 100   | 5001        |
| 3007        | Brad Davis     | New York   | 200   | 5001        |
| 3005        | Graham Zusi    | California | 200   | 5002        |
| 3008        | Julian Green   | London     | 300   | 5002        |
| 3004        | Fabian Johnson | Paris      | 300   | 5006        |
| 3009        | Geoff Cameron  | Berlin     | 100   | 5003        |
| 3003        | Jozy Altidor   | Moscow     | 200   | 5007        |
| 3001        | Brad Guzan     | London     |       | 5005        |


```sql
SELECT
    s.name AS Salesman,
    c.cust_name,
    c.city
FROM salesman AS s
JOIN customer AS c
    ON s.city = c.city;
```

**Output:**

<img width="1293" height="787" alt="image" src="https://github.com/user-attachments/assets/42231ea1-3c3f-4914-a8a2-a861450a073e" />


**Question 10**
---
Write the SQL query that achieves the selection of the first name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date of '2024-01-15'.:

Patients Table

| name           | type        |
|----------------|------------|
| patient_id     | INT        |
| first_name     | VARCHAR(50)|
| last_name      | VARCHAR(50)|
| date_of_birth  | DATE       |
| admission_date | DATE       |
| discharge_date | DATE       |
| doctor_id      | INT        |


Surgeries Table

| name         | type |
|--------------|------|
| surgery_id   | INT  |
| patient_id   | INT  |
| surgeon_id   | INT  |
| surgery_date | DATE |

```sql
SELECT 
    p.first_name
FROM patients AS p
INNER JOIN surgeries AS s
    ON p.patient_id = s.patient_id
WHERE s.surgery_date = '2024-01-15';

```

**Output:**

<img width="1302" height="494" alt="image" src="https://github.com/user-attachments/assets/b385c88f-1e44-4f3c-9ebc-6b6d9b888c8a" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
