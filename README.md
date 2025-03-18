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
