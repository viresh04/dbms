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
# 4th one
```py

-- Create DEPART table first (since EMPLOYEE has foreign key reference to it)
CREATE TABLE d12 (
    dept_no INT PRIMARY KEY,
    dept_name VARCHAR(50) NOT NULL UNIQUE,
    total_employees INT DEFAULT 0 CHECK (total_employees >= 0),
    location VARCHAR(100)
);

-- Create EMPLOYEE table with constraints
CREATE TABLE e12 (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50) NOT NULL,
    birth_date DATE NOT NULL,
    gender CHAR(1) CHECK (gender IN ('M', 'F')),
    dept_no INT,
    address VARCHAR(200),
    designation VARCHAR(50) NOT NULL,
    salary DECIMAL(10, 2) CHECK (salary > 0),
    experience INT CHECK (experience >= 0),
    email VARCHAR(100) UNIQUE,
    FOREIGN KEY (dept_no) REFERENCES DEPART(dept_no)
);

-- Create PROJECT table with constraints
CREATE TABLE p12 (
    proj_id INT PRIMARY KEY,
    type_of_project VARCHAR(50) NOT NULL,
    status VARCHAR(20) CHECK (status IN ('In Progress', 'Completed', 'On Hold')),
    start_date DATE NOT NULL,
    emp_id INT,
    FOREIGN KEY (emp_id) REFERENCES EMPLOYEE(emp_id)
);

-- Insert data into DEPART table
INSERT INTO d12 VALUES(101, 'HR', 3, 'Building A, Floor 1'),
 INSERT INTO d12 VALUES(102, 'FINANCE', 2, 'Building A, Floor 2');
INSERT INTO d12 VALUES(103, 'CIVIL', 2, 'Building B, Floor 1');
INSERT INTO d12 VALUES(104, 'MCA', 3, 'Building C, Floor 3');
INSERT INTO d12 VALUES(105, 'SALES', 0, 'Building D, Floor 1');

-- Insert data into EMPLOYEE table
INSERT INTO e12 VALUES  (1001, 'John Smith', '1990-05-15', 'M', 101, '123 Main St', 'HR Manager', 75000.00, 8, 'john.smith@company.com');
(1002, 'Maria Garcia', '1985-10-20', 'F', 102, '456 Oak Ave', 'Financial Analyst', 65000.00, 10, 'maria.garcia@company.com'),
(1003, 'Amanda Roberts', '1992-03-08', 'F', 103, '789 Pine Rd', 'Civil Engineer', 70000.00, 6, 'amanda.roberts@company.com'),
(1004, 'Robert Johnson', '1988-07-12', 'M', 104, '321 Elm St', 'Systems Analyst', 72000.00, 9, 'robert.johnson@company.com'),
(1005, 'Sarah Williams', '1995-11-30', 'F', 101, '654 Cedar Ln', 'HR Assistant', 45000.00, 3, 'sarah.williams@company.com'),
(1006, 'Michael Brown', '1987-04-22', 'M', 104, '987 Birch Blvd', 'Database Admin', 78000.00, 11, 'michael.brown@company.com'),
(1007, 'Angela Davis', '1993-05-18', 'F', 103, '159 Maple Dr', 'Project Engineer', 68000.00, 5, 'angela.davis@company.com'),
(1008, 'James Wilson', '1991-08-05', 'M', 102, '753 Spruce Pl', 'Accountant', 60000
.00, 7, 'james.wilson@company.com'),
(1009, 'Lisa Taylor', '1989-01-15', 'F', 101, '852 Walnut St', 'Recruiter', 55000.00, 6, 'lisa.taylor@company.com'),
(1010, 'David Miller', '1994-09-10', 'M', 104, '426 Cherry Ave', 'Software Developer', 71000.00, 4, 'david.miller@company.com');

-- Insert data into PROJECT table
INSERT INTO PROJECT VALUES
(501, 'Website Redesign', 'In Progress', '2024-01-15', 1006),
(502, 'Budget Planning', 'Completed', '2023-11-01', 1002),
(503, 'Office Renovation', 'In Progress', '2024-02-20', 1003),
(504, 'Recruitment Drive', 'On Hold', '2023-12-05', 1001),
(505, 'Database Migration', 'In Progress', '2024-03-10', 1004),
(506, 'Bridge Construction', 'In Progress', '2024-01-05', 1007),
(507, 'Financial Audit', 'Completed', '2023-10-15', 1008),
(508, 'Employee Training', 'On Hold', '2024-02-01', 1009);

-- 1. 
DELETE FROM DEPART WHERE total_employees < 1;

-- 2.
SELECT emp_name, designation 
FROM EMPLOYEE 
WHERE gender = 'F' 
ORDER BY emp_name DESC;

-- 3.
SELECT emp_name 
FROM EMPLOYEE 
WHERE emp_name LIKE 'A%A';

-- 4. 
SELECT emp_name, salary 
FROM EMPLOYEE 
WHERE salary = (SELECT MIN(salary) FROM EMPLOYEE);

-- 5. 
UPDATE EMPLOYEE
SET salary = salary * 1.10
WHERE dept_no = (SELECT dept_no FROM DEPART WHERE dept_name = 'CIVIL');

-- 6. 
SELECT COUNT(*) AS total_mca_employees
FROM EMPLOYEE
WHERE dept_no = (SELECT dept_no FROM DEPART WHERE dept_name = 'MCA');

-- 7.
SELECT emp_name, birth_date
FROM EMPLOYEE
WHERE MONTH(birth_date) = MONTH(CURRENT_DATE());
8
SELECT * FROM EMPLOYEE;
```
