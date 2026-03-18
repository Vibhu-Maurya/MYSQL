# SQL Lab – Experiment 1

## Aim
To practice Data Definition Language (DDL) and Data Manipulation Language (DML) operations including table creation, data insertion, deletion, updates, and structural modifications.

---

## Question 1
Create Employee_master table with data using Employee table.

### Query
```sql
CREATE TABLE Employee_master AS
SELECT * FROM EMPLOYEE;
```

### Output
```
Table created successfully.
Records copied: 14 rows
```

---

## Question 2
Delete all records from Employee_master whose DeptNo is 10.

### Query
```sql
DELETE FROM Employee_master
WHERE DEPTNO = 10;
```

### Output
```
1 row deleted.
```

| DEPTNO | Department |
|--------|------------|
| 10     | RESEARCH   |

**Note:** Employee MILLER (EMPNO 7934) from DEPTNO 10 has been deleted.

---

## Question 3
Update 10% salary increase for employees in DEPTNO 20 in Employee_master.

### Query
```sql
UPDATE Employee_master
SET SAL = SAL + (SAL * 0.10)
WHERE DEPTNO = 20;
```

### Output
```
5 rows updated.
```

| EMPNO | ENAME | JOB | SAL (Before) | SAL (After) | DEPTNO |
|-------|-------|-----|-------------|------------|--------|
| 7369  | SMITH | CLERK | 800 | 880 | 20 |
| 7566  | JONES | MANAGER | 2975 | 3272.50 | 20 |
| 7782  | CLARK | MANAGER | 2450 | 2695 | 20 |
| 7839  | KING | PRESIDENT | 5000 | 5500 | 20 |
| 7876  | ADAMS | CLERK | 1100 | 1210 | 20 |

---

## Question 4
Alter SAL column with size 10,2 (NUMBER datatype with 10 digits, 2 decimal places) in Employee_master.

### Query
```sql
ALTER TABLE Employee_master
MODIFY SAL NUMBER(10, 2);
```

### Output
```
Table altered successfully.
Column SAL modified to NUMBER(10, 2)
```

---

## Question 5
Drop Employee_master table.

### Query
```sql
DROP TABLE Employee_master;
```

### Output
```
Table dropped.
```

---

## Summary

| Operation | Records Affected | Status |
|-----------|------------------|--------|
| CREATE TABLE (Employee_master) | 14 rows | ✓ Success |
| DELETE (DEPTNO = 10) | 1 row | ✓ Success |
| UPDATE (10% SAL for DEPTNO 20) | 5 rows | ✓ Success |
| ALTER TABLE (SAL column) | - | ✓ Success |
| DROP TABLE | - | ✓ Success |

