# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
| student_id | student_name | subject | grade |
|------------|--------------|---------|-------|
| 1          | Alice        | Math    | 90    |
| 2          | Bob          | Math    | 85    |
| 3          | Charlie      | Math    | 95    |
| 4          | David        | Science | 88    |
| 5          | Emma         | Science | 92    |
| 6          | Frank        | Science | 85    |
| 7          | John         | Social  | 85    |

```sql
select * from GRADES g where g.grade = ( select max(g2.grade) from GRADES g2 where g2.subject = g.subject);
```

**Output:**

<img width="1299" height="541" alt="image" src="https://github.com/user-attachments/assets/4384bc4f-d6d1-4f78-a577-494f00520405" />

**Question 2**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

Sample table: CUSTOMERS

| ID | Name     | Age | Address     | Salary |
|----|----------|-----|-------------|--------|
| 1  | Ramesh   | 32  | Ahmedabad   | 2000   |
| 2  | Khilan   | 25  | Delhi       | 1500   |
| 3  | Kaushik  | 23  | Kota        | 2000   |
| 4  | Chaitali | 25  | Mumbai      | 6500   |
| 5  | Hardik   | 27  | Bhopal      | 8500   |
| 6  | Komal    | 22  | Hyderabad   | 4500   |
| 7  | Muffy    | 24  | Indore      | 10000  |


```sql
select * from CUSTOMERS where ADDRESS = 'Delhi';
```

**Output:**

<img width="1298" height="430" alt="image" src="https://github.com/user-attachments/assets/606201ae-bed1-4119-a9d3-f7e46fced6eb" />

**Question 3**
---
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)
| name             | type           |
|------------------|----------------|
| medication_id    | INT            |
| medication_name  | VARCHAR(50)    |
| dosage           | VARCHAR(20)    |

```sql
SELECT *
FROM Medications m
WHERE m.dosage = (
    SELECT MIN(m2.dosage)
    FROM Medications m2
);
```

**Output:**

<img width="1295" height="496" alt="image" src="https://github.com/user-attachments/assets/a7581786-21fd-4fee-b572-3f15ba6c8d89" />


**Question 4**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

| name | type     |
|------|----------|
| id   | INTEGER  |
| name | TEXT     |
| city | TEXT     |
| email| TEXT     |
| phone| INTEGER  |

```sql
SELECT *
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (
        SELECT MAX(id)
        FROM customer
    )
);
```

**Output:**

<img width="1293" height="601" alt="image" src="https://github.com/user-attachments/assets/46949eff-81b0-4abf-926c-539be791ab36" />

**Question 5**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

Sample table: CUSTOMERS
| ID | Name     | Age | Address     | Salary |
|----|----------|-----|-------------|--------|
| 1  | Ramesh   | 32  | Ahmedabad   | 2000   |
| 2  | Khilan   | 25  | Delhi       | 1500   |
| 3  | Kaushik  | 23  | Kota        | 2000   |
| 4  | Chaitali | 25  | Mumbai      | 6500   |
| 5  | Hardik   | 27  | Bhopal      | 8500   |
| 6  | Komal    | 22  | Hyderabad   | 4500   |
| 7  | Muffy    | 24  | Indore      | 10000  |

```sql
SELECT *
FROM CUSTOMERS
WHERE AGE < 30;
```

**Output:**

<img width="1287" height="674" alt="image" src="https://github.com/user-attachments/assets/3c074123-5eea-4c9c-84dd-776ada7bcb03" />


**Question 6**
---
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)
| student_id | student_name | subject  | grade |
|------------|--------------|---------|-------|
| 1          | Alice        | Math    | 90    |
| 2          | Bob          | Math    | 85    |
| 3          | Charlie      | Math    | 95    |
| 4          | David        | Science | 88    |
| 5          | Emma         | Science | 92    |
| 6          | Frank        | Science | 85    |
| 7          | John         | Social  | 85    |

```sql
SELECT *
FROM Grades g
WHERE g.grade = (
    SELECT MIN(g2.grade)
    FROM Grades g2
    WHERE g2.subject = g.subject
);
```

**Output:**

<img width="1292" height="545" alt="image" src="https://github.com/user-attachments/assets/6f030663-251b-4104-98d1-ccf3e93c6291" />


**Question 7**
---
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

salesman table
| name        | type           |
|------------|----------------|
| salesman_id | numeric(5)     |
| name        | varchar(30)    |
| city        | varchar(15)    |
| commission  | decimal(5,2)   |

customer table
| name         | type  |
|-------------|-------|
| customer_id  | int   |
| cust_name    | text  |
| city         | text  |
| grade        | int   |
| salesman_id  | int   |


```sql
SELECT s.salesman_id, s.name
FROM salesman s
WHERE s.salesman_id IN (
    SELECT c.salesman_id
    FROM customer c
    GROUP BY c.salesman_id
    HAVING COUNT(c.customer_id) > 1
);
```

**Output:**

<img width="1292" height="563" alt="image" src="https://github.com/user-attachments/assets/2fcefa1c-073e-453a-8a2f-da73ef08f81b" />

**Question 8**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

Sample table: CUSTOMERS
| ID | NAME      | AGE | ADDRESS     | SALARY  |
|----|-----------|-----|------------|--------|
| 1  | Ramesh    | 32  | Ahmedabad  | 2000   |
| 2  | Khilan    | 25  | Delhi      | 1500   |
| 3  | Kaushik   | 23  | Kota       | 2000   |
| 4  | Chaitali  | 25  | Mumbai     | 6500   |
| 5  | Hardik    | 27  | Bhopal     | 8500   |
| 6  | Komal     | 22  | Hyderabad  | 4500   |
| 7  | Muffy     | 24  | Indore     | 10000  |


```sql
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi'
  AND AGE <= 30 order by ID ;

```

**Output:**

<img width="1286" height="451" alt="image" src="https://github.com/user-attachments/assets/167b77c1-6807-4dd3-8790-9b9c476e9671" />

**Question 9**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer
| name  | type    |
|-------|---------|
| id    | INTEGER |
| name  | TEXT    |
| city  | TEXT    |
| email | TEXT    |
| phone | INTEGER |

```sql
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(phone) = 1
);
```

**Output:**

<img width="1294" height="561" alt="image" src="https://github.com/user-attachments/assets/069c518f-08f0-4f3e-ae3a-60bdc59b80f9" />

**Question 10**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)
| name            | type        |
|-----------------|------------|
| medication_id   | INT        |
| medication_name | VARCHAR(50)|
| dosage          | VARCHAR(20)|

```
SELECT *
FROM Medications m
WHERE m.dosage = (
    SELECT MAX(m2.dosage)
    FROM Medications m2
);
```

**Output:**

<img width="1285" height="494" alt="image" src="https://github.com/user-attachments/assets/a6973fd5-8428-4c25-8438-c120d6c39cd5" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
