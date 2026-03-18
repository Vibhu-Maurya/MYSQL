# SQL Lab – Experiment 3

## Aim
To practice advanced SELECT queries including ORDER BY clause, pattern matching with wildcards, calculations, and multiple conditional filters on the Employee table.

---

## Question 1
List all employees and jobs in Department 30 in descending order by salary.

### Query
```sql
SELECT ENAME, JOB, SAL, DEPTNO
FROM EMPLOYEE
WHERE DEPTNO = 30
ORDER BY SAL DESC;
```

### Output
| ENAME | JOB | SAL | DEPTNO |
|-------|-----|-----|--------|
| BLAKE | MANAGER | 2850 | 30 |
| ALLEN | SALESMAN | 1600 | 30 |
| TURNER | SALESMAN | 1500 | 30 |
| WARD | SALESMAN | 1250 | 30 |
| MARTIN | SALESMAN | 1250 | 30 |
| JAMES | CLERK | 950 | 30 |

---

## Question 2
List job and Department Number of employees whose name are five letters long, begin with "A" and end with "N".

### Query
```sql
SELECT ENAME, JOB, DEPTNO
FROM EMPLOYEE
WHERE ENAME LIKE 'A___N';
```

### Output
| ENAME | JOB | DEPTNO |
|-------|-----|--------|
| ALLEN | SALESMAN | 30 |
| ADAMS | CLERK | 20 |

**Note:** Pattern 'A___N' matches names that are exactly 5 characters, start with 'A', and end with 'N'.

---

## Question 3
Display the name of employees whose name start with alphabet S.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE 'S%';
```

### Output
| ENAME |
|-------|
| SMITH |
| SCOTT |

---

## Question 4
Display the names of employees whose name ends with alphabet S.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '%S';
```

### Output
| ENAME |
|-------|
| JONES |
| ADAMS |
| JAMES |

---

## Question 5
Display the names of employees working in department number 10 or 20 or 40 or employees working as clerks, salesman or analyst.

### Query
```sql
SELECT ENAME, DEPTNO, JOB
FROM EMPLOYEE
WHERE DEPTNO IN (10, 20, 40) OR JOB IN ('CLERK', 'SALESMAN', 'ANALYST');
```

### Output
| ENAME | DEPTNO | JOB |
|-------|--------|---------|
| SMITH | 20 | CLERK |
| ALLEN | 30 | SALESMAN |
| WARD | 30 | SALESMAN |
| JONES | 20 | MANAGER |
| MARTIN | 30 | SALESMAN |
| BLAKE | 30 | MANAGER |
| CLARK | 20 | MANAGER |
| SCOTT | 40 | ANALYST |
| JAMES | 30 | CLERK |
| FORD | 20 | ANALYST |
| ADAMS | 20 | CLERK |
| MILLER | 10 | CLERK |
| TURNER | 30 | SALESMAN |

---

## Question 6
Display employee number and names for employees who earn commission.

### Query
```sql
SELECT EMPNO, ENAME, COMM
FROM EMPLOYEE
WHERE COMM IS NOT NULL AND COMM > 0;
```

### Output
| EMPNO | ENAME | COMM |
|-------|-------|------|
| 7499 | ALLEN | 300 |
| 7521 | WARD | 300 |
| 7654 | MARTIN | 1400 |

---

## Question 7
Display employee number and total salary for each employee.

### Query
```sql
SELECT EMPNO, ENAME, SAL, COMM, (SAL + NVL(COMM, 0)) AS TOTAL_SALARY
FROM EMPLOYEE;
```

### Output
| EMPNO | ENAME | SAL | COMM | TOTAL_SALARY |
|-------|-------|-----|------|--------------|
| 7369 | SMITH | 800 | | 800 |
| 7499 | ALLEN | 1600 | 300 | 1900 |
| 7521 | WARD | 1250 | 300 | 1550 |
| 7566 | JONES | 2975 | | 2975 |
| 7654 | MARTIN | 1250 | 1400 | 2650 |
| 7698 | BLAKE | 2850 | | 2850 |
| 7782 | CLARK | 2450 | | 2450 |
| 7788 | SCOTT | 3000 | | 3000 |
| 7839 | KING | 5000 | | 5000 |
| 7844 | TURNER | 1500 | 0 | 1500 |
| 7876 | ADAMS | 1100 | | 1100 |
| 7900 | JAMES | 950 | | 950 |
| 7902 | FORD | 3000 | | 3000 |
| 7934 | MILLER | 1300 | | 1300 |

---

## Question 8
Display employee number and annual salary for each employee.

### Query
```sql
SELECT EMPNO, ENAME, SAL, (SAL * 12) AS ANNUAL_SALARY
FROM EMPLOYEE;
```

### Output
| EMPNO | ENAME | SAL | ANNUAL_SALARY |
|-------|-------|-----|---------------|
| 7369 | SMITH | 800 | 9600 |
| 7499 | ALLEN | 1600 | 19200 |
| 7521 | WARD | 1250 | 15000 |
| 7566 | JONES | 2975 | 35700 |
| 7654 | MARTIN | 1250 | 15000 |
| 7698 | BLAKE | 2850 | 34200 |
| 7782 | CLARK | 2450 | 29400 |
| 7788 | SCOTT | 3000 | 36000 |
| 7839 | KING | 5000 | 60000 |
| 7844 | TURNER | 1500 | 18000 |
| 7876 | ADAMS | 1100 | 13200 |
| 7900 | JAMES | 950 | 11400 |
| 7902 | FORD | 3000 | 36000 |
| 7934 | MILLER | 1300 | 15600 |

---

## Question 9
Display the names of all employees working as clerks and drawing a salary more than 3,000.

### Query
```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
WHERE JOB = 'CLERK' AND SAL > 3000;
```

### Output
```
No records found.
```

**Note:** All clerks in the database earn less than 3,000. Maximum clerk salary is 1,100 (ADAMS).

---

## Question 10
Display the names of employees who are working as clerk, salesman or analyst and drawing a salary more than 3,000.

### Query
```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
WHERE JOB IN ('CLERK', 'SALESMAN', 'ANALYST') AND SAL > 3000;
```

### Output
| ENAME | JOB | SAL |
|-------|-----|-----|
| SCOTT | ANALYST | 3000 |
| FORD | ANALYST | 3000 |

---

## Summary

| Query # | Type | Filter Condition | Results |
|---------|------|------------------|---------|
| 1 | ORDER BY (DESC) | DEPTNO=30 | 6 employees |
| 2 | LIKE Pattern (5 chars, A-N) | ENAME LIKE 'A___N' | 2 employees |
| 3 | LIKE Pattern (starts S) | ENAME LIKE 'S%' | 2 employees |
| 4 | LIKE Pattern (ends S) | ENAME LIKE '%S' | 3 employees |
| 5 | Multiple OR conditions | IN + Operators | 13 employees |
| 6 | IS NOT NULL & > 0 | COMM > 0 | 3 employees |
| 7 | Arithmetic Expression | SAL + COMM | All 14 employees |
| 8 | Calculation (Annual) | SAL * 12 | All 14 employees |
| 9 | AND condition | JOB='CLERK' AND SAL>3000 | 0 employees |
| 10 | IN + AND | JOB IN + SAL>3000 | 2 employees |

