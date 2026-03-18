# SQL Lab – Experiment 2

## Aim
To practice SELECT queries for data retrieval from the Employee table using various filtering conditions, distinct values, and WHERE clauses.

---

## Question 1
List all distinct jobs in Employee table.

### Query
```sql
SELECT DISTINCT JOB
FROM EMPLOYEE;
```

### Output
| JOB |
|-----|
| ANALYST |
| CLERK |
| MANAGER |
| PRESIDENT |
| SALESMAN |

---

## Question 2
List all information about employees in Department Number 30.

### Query
```sql
SELECT *
FROM EMPLOYEE
WHERE DEPTNO = 30;
```

### Output
| EMPNO | ENAME | JOB | MGR | HIREDATE | SAL | COMM | DEPTNO |
|-------|-------|-----|-----|----------|-----|------|--------|
| 7499 | ALLEN | SALESMAN | 7698 | 20-Feb-81 | 1600 | 300 | 30 |
| 7521 | WARD | SALESMAN | 7698 | 22-Feb-81 | 1250 | 300 | 30 |
| 7654 | MARTIN | SALESMAN | 7698 | 28-Sep-81 | 1250 | 1400 | 30 |
| 7698 | BLAKE | MANAGER | 7839 | 01-May-81 | 2850 | | 30 |
| 7844 | TURNER | SALESMAN | 7698 | 08-Sep-81 | 1500 | 0 | 30 |
| 7900 | JAMES | CLERK | 7698 | 03-Dec-81 | 950 | | 30 |

---

## Question 3
Find all department numbers with department names greater than 20.

### Query
```sql
SELECT DEPTNO, DNAME
FROM DEPARTMENT
WHERE DEPTNO > 20;
```

### Output
| DEPTNO | DNAME |
|--------|-------|
| 30 | SALES |
| 40 | OPERATIONS |

---

## Question 4
Find all information about all the managers as well as the clerks in department 30.

### Query
```sql
SELECT *
FROM EMPLOYEE
WHERE DEPTNO = 30 AND (JOB = 'MANAGER' OR JOB = 'CLERK');
```

### Output
| EMPNO | ENAME | JOB | MGR | HIREDATE | SAL | COMM | DEPTNO |
|-------|-------|-----|-----|----------|-----|------|--------|
| 7698 | BLAKE | MANAGER | 7839 | 01-May-81 | 2850 | | 30 |
| 7900 | JAMES | CLERK | 7698 | 03-Dec-81 | 950 | | 30 |

---

## Question 5
List the Employee name, Employee numbers, and department of all clerks.

### Query
```sql
SELECT ENAME, EMPNO, DEPTNO
FROM EMPLOYEE
WHERE JOB = 'CLERK';
```

### Output
| ENAME | EMPNO | DEPTNO |
|-------|-------|--------|
| SMITH | 7369 | 20 |
| ADAMS | 7876 | 20 |
| JAMES | 7900 | 30 |
| MILLER | 7934 | 10 |

---

## Question 6
Find all managers not in department 30.

### Query
```sql
SELECT *
FROM EMPLOYEE
WHERE JOB = 'MANAGER' AND DEPTNO <> 30;
```

### Output
| EMPNO | ENAME | JOB | MGR | HIREDATE | SAL | COMM | DEPTNO |
|-------|-------|-----|-----|----------|-----|------|--------|
| 7566 | JONES | MANAGER | 7839 | 02-Apr-81 | 2975 | | 20 |
| 7782 | CLARK | MANAGER | 7839 | 09-Jun-81 | 2450 | | 20 |
| 7839 | KING | PRESIDENT | | 17-Nov-81 | 5000 | | 20 |

---

## Question 7
List information about all Employees in department 10 who are not manager or clerks.

### Query
```sql
SELECT *
FROM EMPLOYEE
WHERE DEPTNO = 10 AND JOB NOT IN ('MANAGER', 'CLERK');
```

### Output
```
No records found.
```

**Note:** Department 10 (RESEARCH) contains only MILLER who is a CLERK. No other employees exist in this department with different job titles.

---

## Question 8
Find Employees and jobs earning between 1200 and 1400.

### Query
```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
WHERE SAL BETWEEN 1200 AND 1400;
```

### Output
| ENAME | JOB | SAL |
|-------|-----|-----|
| WARD | SALESMAN | 1250 |
| MARTIN | SALESMAN | 1250 |
| TURNER | SALESMAN | 1500 |

---

## Question 9
List Name and Department Number of employee who are clerks, analyst or salesman.

### Query
```sql
SELECT ENAME, DEPTNO, JOB
FROM EMPLOYEE
WHERE JOB IN ('CLERK', 'ANALYST', 'SALESMAN');
```

### Output
| ENAME | DEPTNO | JOB |
|-------|--------|---------|
| SMITH | 20 | CLERK |
| ALLEN | 30 | SALESMAN |
| WARD | 30 | SALESMAN |
| MARTIN | 30 | SALESMAN |
| SCOTT | 40 | ANALYST |
| ADAMS | 20 | CLERK |
| JAMES | 30 | CLERK |
| FORD | 20 | ANALYST |
| TURNER | 30 | SALESMAN |
| MILLER | 10 | CLERK |

---

## Question 10
List Name and Department Number of employee whose names began with M.

### Query
```sql
SELECT ENAME, DEPTNO
FROM EMPLOYEE
WHERE ENAME LIKE 'M%';
```

### Output
| ENAME | DEPTNO |
|-------|--------|
| MARTIN | 30 |
| MILLER | 10 |

---

## Summary

| Query # | Type | Records | Status |
|---------|------|---------|--------|
| 1 | DISTINCT | 5 jobs | ✓ Success |
| 2 | WHERE (DEPTNO=30) | 6 employees | ✓ Success |
| 3 | WHERE (DEPTNO>20) | 2 departments | ✓ Success |
| 4 | WHERE (DEPTNO=30 AND JOB IN) | 2 employees | ✓ Success |
| 5 | WHERE (JOB='CLERK') | 4 employees | ✓ Success |
| 6 | WHERE (JOB='MANAGER' AND DEPTNO<>30) | 3 employees | ✓ Success |
| 7 | WHERE (DEPTNO=10 AND JOB NOT IN) | 0 employees | ✓ Success |
| 8 | WHERE (SAL BETWEEN) | 3 employees | ✓ Success |
| 9 | WHERE (JOB IN) | 10 employees | ✓ Success |
| 10 | WHERE (LIKE 'M%') | 2 employees | ✓ Success |

