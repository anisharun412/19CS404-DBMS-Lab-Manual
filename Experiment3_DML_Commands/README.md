# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'

| Employees Table   |
|------------------|
| employee_id      |
| first_name       |
| last_name        |
| email            |
| phone_number     |
| hire_date        |
| job_id           |
| salary           |
| commission_pct   |
| manager_id       |
| department_id    |

```sql
update Employees set salary = salary*2 where department_id = 20 and job_id like "%MAN" ;
```

**Output:**

<img width="1243" height="450" alt="image" src="https://github.com/user-attachments/assets/f97b0485-cfb7-4c1e-bc35-b6b805700351" />

**Question 2**
---
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.

PRODUCTS TABLE

| name          | type            |
|---------------|-----------------|
| product_id    | INT             |
| product_name  | VARCHAR(100)    |
| category      | VARCHAR(50)     |
| cost_price    | DECIMAL(10,2)   |
| sell_price    | DECIMAL(10,2)   |
| reorder_lvl   | INT             |
| quantity      | INT             |
| supplier_id   | INT             |

```sql
update PRODUCTS set reorder_lvl = 40 where category = "Grocery";
```

**Output:**

<img width="1242" height="498" alt="image" src="https://github.com/user-attachments/assets/81c6ec15-e1c6-41e2-9353-229739ee3b8b" />

**Question 3**
---
Increase the reorder level by 30% for products from 'Food' category having quantity in stock less than 50% of existing reorder level in the products table

| name          | type          |
|---------------|---------------|
| product_id    | INT           |
| product_name  | VARCHAR(10)   |
| category      | VARCHAR(50)   |
| cost_price    | DECIMAL(10)   |
| sell_price    | DECIMAL(10)   |
| reorder_lvl   | INT           |
| quantity      | INT           |
| supplier_id   | INT           |


```sql
update products set reorder_lvl = reorder_lvl+(reorder_lvl*0.3) where category = "Food" and quantity < reorder_lvl/2;
```

**Output:**

<img width="1237" height="492" alt="image" src="https://github.com/user-attachments/assets/e679fc47-8840-4384-9306-d738e67bbdbf" />

**Question 4**
---
For products with a profit % less than 30% of selling price, update the selling price to provide a profit margin of 35% over cost price of the product in the products table.

PRODUCTS TABLE

| name          | type            |
|---------------|-----------------|
| product_id    | INT             |
| product_name  | VARCHAR(100)    |
| category      | VARCHAR(50)     |
| cost_price    | DECIMAL(10,2)   |
| sell_price    | DECIMAL(10,2)   |
| reorder_lvl   | INT             |
| quantity      | INT             |
| supplier_id   | INT             |


```sql
update products
set sell_price = cast(cost_price *1.35 as INT) where ((sell_price - cost_price) / sell_price)<0.30;
```

**Output:**

<img width="1238" height="586" alt="image" src="https://github.com/user-attachments/assets/996672e5-9eee-4148-b575-5d3afb5e4a7f" />

**Question 5**
---
Write a SQL statement to Increase the salary by 500 and email as 'updated' for employees with job ID 'SA_REP' and commission percentage greater than 0.15

Employees Table

| Column Name       |
|-------------------|
| employee_id       |
| first_name        |
| last_name         |
| email             |
| phone_number      |
| hire_date         |
| job_id            |
| salary            |
| commission_pct    |
| manager_id        |
| department_id     |


```sql
update Employees 
set salary = salary + 500, email = 'updated'
where job_id = 'SA_REP' and commission_pct > 0.15;
```

**Output:**

<img width="1242" height="616" alt="image" src="https://github.com/user-attachments/assets/28ed56ee-89e7-4eec-914c-cf664b7156ca" />

**Question 6**
---
Write a SQL query to Delete customers with 'GRADE' 3 and whose 'CUST_NAME' contains the substring 'BBB', and 'PAYMENT_AMT' is greater than 2000

Sample table: Customer

| CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT | OUTSTANDING_AMT | PHONE_NO | AGENT_CODE |
|-----------|-----------|-----------|--------------|--------------|-------|-------------|-------------|-------------|------------------|----------|------------|
| C00013    | Holmes    | London    | London       | UK           | 2     | 6000.00     | 5000.00     | 7000.00     | 4000.00          | BBBBBBB  | A003       |
| C00001    | Micheal   | New York  | New York     | USA          | 2     | 3000.00     | 5000.00     | 2000.00     | 6000.00          | CCCCCCC  | A008       |
| C00020    | Albert    | New York  | New York     | USA          | 3     | 5000.00     | 7000.00     | 6000.00     | 6000.00          | BBBBSBB  | A008       |

```sql
delete from Customer where GRADE = 3 and CUST_NAME like "%BBB%" and PAYMENT_AMT > 2000;
```

**Output:**

<img width="1242" height="591" alt="image" src="https://github.com/user-attachments/assets/59ffe012-6aa6-4c42-96ba-94051b5c62a9" />

**Question 7**
---
Write a SQL query to Delete All Doctors with a NULL Last Name

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
delete from doctors where last_name is NULL;
```

**Output:**

<img width="1233" height="817" alt="image" src="https://github.com/user-attachments/assets/3e110b2a-79ed-4d62-9166-be524dd8dfd1" />

**Question 8**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_CITY' is not 'New York' and 'OUTSTANDING_AMT' is greater than 5000.

Sample table: Customer
| CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT | OUTSTANDING_AMT | PHONE_NO | AGENT_CODE |
|-----------|-----------|-----------|--------------|--------------|-------|-------------|-------------|-------------|------------------|----------|------------|
| C00013    | Holmes    | London    | London       | UK           | 2     | 6000.00     | 5000.00     | 7000.00     | 4000.00          | BBBBBBB  | A003       |
| C00001    | Micheal   | New York  | New York     | USA          | 2     | 3000.00     | 5000.00     | 2000.00     | 6000.00          | CCCCCCC  | A008       |
| C00020    | Albert    | New York  | New York     | USA          | 3     | 5000.00     | 7000.00     | 6000.00     | 6000.00          | BBBBSBB  | A008       |


```sql
delete from Customer where CUST_CITY != 'New York' and OUTSTANDING_AMT > 5000;
```

**Output:**

<img width="1239" height="698" alt="image" src="https://github.com/user-attachments/assets/4884ec42-5e9c-4a2c-8610-9067a7a2580a" />

**Question 9**
---
Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
delete from Doctors where doctor_id >=2 and doctor_id<=4;
```

**Output:**

<img width="1243" height="959" alt="image" src="https://github.com/user-attachments/assets/642c321e-fea8-4b55-95dc-f2039b975480" />

**Question 10**
---
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
delete from Doctors where specialization is null;
```

**Output:**

<img width="1251" height="1127" alt="image" src="https://github.com/user-attachments/assets/a795d6d6-d526-4ca1-a162-dcdeb4af1679" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
