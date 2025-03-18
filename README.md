# 1st

```py
 CREATE TABLE DP (
 dept_no INT PRIMARY KEY,
 dept_name VARCHAR(50) NOT NULL UNIQUE,
 location VARCHAR(50)
);
```
DESC DP;
```py
INSERT INTO DP VALUES (10, 'Account', 'NY');
INSERT INTO DP  VALUES (20, 'HR', 'NY');
INSERT INTO DP  VALUES (30, 'Production', 'DL');
INSERT INTO DP  VALUES (40, 'Sales', 'NY');
INSERT INTO DP  VALUES (50, 'EDP', 'MU');
INSERT INTO DP  VALUES (60, 'TRG', NULL);
INSERT INTO DP  VALUES (110, 'RND', 'AH');
```
```py
SELECT * FROM DP;
```
```py
SELECT * FROM DP WHERE location = 'NY';
```
```py
SELECT * FROM DP WHERE dept_no = 10;
```
```py
SELECT * FROM DP WHERE dept_name LIKE 'A%';
```
```py
SELECT * FROM DP WHERE dept_no BETWEEN 1 AND 100;
```
```py
DELETE FROM DP WHERE dept_name = 'TRG';
```
```py
UPDATE DP SET dept_name = 'IT' WHERE dept_name = 'EDP';
```
# 2ND PRG
```PY
-- 1. Create the Database
CREATE DATABASE COMPANY;
USE COMPANY;

-- 2. Create the DEPART Table
CREATE TABLE DEPART (
    dept_no INT PRIMARY KEY,
    dept_name VARCHAR(50) NOT NULL,
    total_employees INT CHECK(total_employees >= 0),
    location VARCHAR(50)
);

-- 3. Create the EMPLOYEE Table
CREATE TABLE EMPLOYEE (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50) NOT NULL,
    birth_date DATE,
    gender VARCHAR(10) CHECK(gender IN ('Male', 'Female')),
    dept_no INT,
    address VARCHAR(100),
    designation VARCHAR(50),
    salary DECIMAL(10, 2),
    experience INT,
    email VARCHAR(100) UNIQUE,
    FOREIGN KEY (dept_no) REFERENCES DEPART(dept_no)
);

-- 4. Create the PROJECT Table
CREATE TABLE PROJECT (
    proj_id INT PRIMARY KEY,
    type_of_project VARCHAR(50),
    status VARCHAR(20),
    start_date DATE,
    emp_id INT,
    FOREIGN KEY (emp_id) REFERENCES EMPLOYEE(emp_id)
);

-- 5. Insert Data into DEPART
INSERT INTO DEPART VALUES (101, 'CIVIL', 3, 'Delhi');
INSERT INTO DEPART VALUES (102, 'MCA', 5, 'Mumbai');
INSERT INTO DEPART VALUES (103, 'MECH', 1, 'Chennai');

-- 6. Insert Data into EMPLOYEE
INSERT INTO EMPLOYEE VALUES (1, 'Anita', '1995-03-10', 'Female', 102, 'Delhi', 'Manager', 55000, 5, 'anita@gmail.com');
INSERT INTO EMPLOYEE VALUES (2, 'Akash', '1997-07-15', 'Male', 101, 'Mumbai', 'Engineer', 45000, 3, 'akash@gmail.com');
INSERT INTO EMPLOYEE VALUES (3, 'Asha', '1996-03-22', 'Female', 102, 'Chennai', 'Analyst', 40000, 2, 'asha@gmail.com');
INSERT INTO EMPLOYEE VALUES (4, 'Rahul', '1998-02-12', 'Male', 103, 'Delhi', 'Supervisor', 30000, 1, 'rahul@gmail.com');
INSERT INTO EMPLOYEE VALUES (5, 'Amara', '1994-03-05', 'Female', 101, 'Mumbai', 'Engineer', 47000, 4, 'amara@gmail.com');

-- 7. Insert Data into PROJECT
INSERT INTO PROJECT VALUES (201, 'Bridge Construction', 'Ongoing', '2024-01-10', 1);
INSERT INTO PROJECT VALUES (202, 'Software Development', 'Completed', '2023-09-15', 3);
INSERT INTO PROJECT VALUES (203, 'Road Construction', 'Ongoing', '2024-02-20', 2);

-- 8. Delete the department whose total number of employees is less than 1
DELETE FROM DEPART WHERE total_employees < 1;

-- 9. Display names and designation of all female employees in descending order
SELECT emp_name, designation
FROM EMPLOYEE
WHERE gender = 'Female'
ORDER BY emp_name DESC;

-- 10. Display employees whose name starts with 'A' and ends with 'A'
SELECT emp_name
FROM EMPLOYEE
WHERE emp_name LIKE 'A%A';

-- 11. Find employee with minimum salary
SELECT emp_name, salary
FROM EMPLOYEE
WHERE salary = (SELECT MIN(salary) FROM EMPLOYEE);

-- 12. Increase salary by 10% for employees in the 'CIVIL' department
UPDATE EMPLOYEE
SET salary = salary * 1.10
WHERE dept_no = (SELECT dept_no FROM DEPART WHERE dept_name = 'CIVIL');

-- 13. Count total number of employees in 'MCA' department
SELECT COUNT(*)
FROM EMPLOYEE
WHERE dept_no = (SELECT dept_no FROM DEPART WHERE dept_name = 'MCA');

-- 14. List employees born in the current month
SELECT emp_name, birth_date
FROM EMPLOYEE
WHERE MONTH(birth_date) = MONTH(CURDATE());

```
