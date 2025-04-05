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
CREATE TABLE DP (
    dept_no INT PRIMARY KEY,
    dept_name VARCHAR(50) UNIQUE,
    location VARCHAR(100)
);

CREATE TABLE EY  (
 emp_id INT PRIMARY KEY,
    emp_name VARCHAR2(50) NOT NULL,
    birth_date DATE NOT NULL,
    gender VARCHAR2(10) CHECK (gender IN ('Male', 'Female')) NOT NULL,
    dept_no INT,
    address VARCHAR2(255),
designation VARCHAR2(20) CHECK (designation IN ('Manager', 'Clerk', 'Leader', 'Analyst', 'Designer', 'Coder', 'Tester')) NOT NULL,   
 salary DECIMAL(10,2) CHECK (salary > 0),
    experience INT CHECK (experience >= 0),
    email VARCHAR(100) NOT NULL CHECK (email LIKE '%@%.%'),
    FOREIGN KEY (dept_no) REFERENCES DP(dept_no)
);

INSERT INTO  DP VALUES (10, 'Accounts', 'NY');
INSERT INTO  DP VALUES(20, 'HR', 'NY');
INSERT INTO  DP VALUES(30, 'Production', 'DL');
INSERT INTO  DP VALUES(40, 'Sales', 'NY');
INSERT INTO  DP VALUES(50, 'IT', 'MU');

INSERT INTO EY VALUES(101, 'Alice', TO_DATE('12-MAY-1990', 'Female', 10, '123 Main St', 'Manager', 60000, 10, 'alice@example.com');
INSERT INTO EY VALUES(102, 'Bob', '23-SEP-1995', 'Male', 20, '456 Elm St', 'Clerk', 35000, 5, 'bob@example.com');
INSERT INTO EY VALUES(103, 'Charlie', TO_DATE('11-FEB-1998', 'DD-MON-YYYY'), 'Male', 30, '789 Oak St', 'Analyst', 45000, 3, 'charlie@example.com');
INSERT INTO EY VALUES(104, 'David', TO_DATE('30-JUL-2000', 'DD-MON-YYYY'), 'Male', 40, '321 Maple St', 'Coder', 40000, 2, 'david@example.com');
INSERT INTO EY VALUES(105, 'Eve', TO_DATE('15-OCT-1992', 'DD-MON-YYYY'), 'Female', 50, '654 Pine St', 'Designer', 50000, 8, 'eve@example.com');


DESC DP;
DESC EY;

SELECT * FROM EY ORDER BY emp_name ASC;
SELECT * FROM DP ORDER BY dept_name ASC; 


DELETE FROM DP WHERE location = 'Ahmedabad';

SELECT * FROM EY WHERE gender = 'Female';

SELECT d.dept_name, e.emp_name FROM EY e
JOIN DP d ON e.dept_no = d.dept_no ORDER BY d.dept_name;

SELECT emp_name FROM EY WHERE salary BETWEEN 20000 AND 50000;

SELECT emp_name, designation FROM EY WHERE gender = 'Female' ORDER BY emp_name DESC;

SELECT emp_name FROM EY WHERE emp_name LIKE 'A%A';

SELECT emp_name, salary FROM EY
WHERE salary = (SELECT MIN(salary) FROM EY);

UPDATE EY
SET salary = salary * 1.10
WHERE dept_no = (SELECT dept_no FROM DP WHERE dept_name = 'IT');
    
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
##3RD PRG 
```py
CREATE TABLE STUDENT (
rollno INT PRIMARY KEY,
name VARCHAR(100) NOT NULL,
class VARCHAR(20) NOT NULL,
birthdate DATE NOT NULL
);


CREATE TABLE COURSE (
courseno INT PRIMARY KEY, coursename VARCHAR(100) NOT NULL,
max_marks INT CHECK (max_marks > 0), pass_marks INT,
CHECK (pass_marks > 0 AND pass_marks <= max_marks)
);

CREATE TABLE SC (
rollno INT,
courseno INT,
marks INT CHECK (marks BETWEEN 0 AND 100),
PRIMARY KEY (rollno, courseno),
FOREIGN KEY (rollno) REFERENCES STUDENT(rollno) ON DELETE CASCADE,
FOREIGN KEY (courseno) REFERENCES COURSE(courseno) ON DELETE CASCAD ); 

insert into STUDENT values (1, 'Alice', 'MCA', '10-MAY-1998');
insert into STUDENT values (2, 'Bob', 'MCA', '15-AUG-1997');
insert into STUDENT values (3, 'Charlie', 'BSc', '20-FEB-1999');
insert into STUDENT values (4, 'viresh', 'BCA', '21-nov-2010');
insert into STUDENT values (5,'satu','msc','24-dec-2011');

insert into COURSE values(101, 'dbms',100,45);
insert into COURSE values(102, 'os',100,35);
insert into COURSE values(103, 'ds',100,75);
insert into COURSE values(104, 'python',100,60);
insert into COURSE values(105, 'se',100,50);

insert into SC values (1,	101,	85);
insert into SC values(1,	102,	72);
insert into SC values (2,101,66);
insert into SC values (3,104,77);
insert into SC values (3,105,81);
insert into SC values (4,103,81);

3//

(Already added in the SC table using CHECK (marks BETWEEN 0 AND 100))

4**
SELECT s.rollno, s.name, s.class, s.birthdate, c.coursename, sc.marks
FROM STUDENT s
JOIN SC sc ON s.rollno = sc.rollno
JOIN COURSE c ON sc.courseno = c.courseno
WHERE c.coursename = '  DBMS'

5**
SELECT s.rollno, s.name FROM STUDENT s
JOIN SC sc ON s.rollno = sc.rollno
JOIN COURSE c ON sc.courseno = c.courseno
 
WHERE c.coursename = 'Computer Networks' AND sc.marks > (c.max_marks * 0.7)
AND s.rollno NOT IN (
SELECT sc.rollno FROM SC sc
JOIN COURSE c ON sc.courseno = c.courseno WHERE sc.marks < c.pass_marks
);

8th
SELECT s.rollno, s.name, AVG(sc.marks) AS avg_marks FROM STUDENT s
JOIN SC sc ON s.rollno = sc.rollno GROUP BY s.rollno, s.name;

9th
SELECT * FROM COURSE WHERE pass_marks > (max_marks * 0.3);

```
