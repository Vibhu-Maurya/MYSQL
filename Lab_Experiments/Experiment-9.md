# SQL Lab – Experiment 9

## Aim
To practice subqueries (Single-row and Multi-row), correlated subqueries, and advanced filtering using results from nested queries across EMPLOYEE and DEPT tables.

---

## Question 1
Display the name of employee who earns highest salary.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

### Output
| ENAME |
|-------|
| KING |

---

## Question 2
Display the employee number and name of employee working as clerk and earning highest salary among clerks.

### Query
```sql
SELECT EMPNO, ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```

### Output
| EMPNO | ENAME |
|-------|-------|
| 7934 | MILLER |

---

## Question 3
Display the names of the salesman who earns a salary more than the highest salary of any clerk.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'SALESMAN'
AND SAL > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```

### Output
| ENAME |
|-------|
| ALLEN |
| TURNER |

---

## Question 4
Display the names of clerks who earn salary more than that of james and salary lesser than that of scott.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
AND SAL < (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

### Output
| ENAME |
|-------|
| ADAMS |
| MILLER |

---

## Question 5
Display the names of employees who earn a salary more than that of james or a salary greater than that of scott.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
OR SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

### Output
| ENAME |
|-------|
| ALLEN |
| WARD |
| JONES |
| MARTIN |
| BLAKE |
| CLARK |
| SCOTT |
| KING |
| TURNER |
| ADAMS |
| FORD |
| MILLER |

---

## Question 6
Display the names of the employees who earn highest salary in their respective departments.

### Query
```sql
SELECT ENAME, DEPTNO, SAL
FROM EMPLOYEE
WHERE (DEPTNO, SAL) IN (SELECT DEPTNO, MAX(SAL) FROM EMPLOYEE GROUP BY DEPTNO);
```

### Output
| ENAME | DEPTNO | SAL |
|-------|--------|-----|
| BLAKE | 30 | 2850 |
| SCOTT | 20 | 3000 |
| KING | 10 | 5000 |
| FORD | 20 | 3000 |

---

## Question 7
Display the names of employees who earn highest salaries in their respective job groups.

### Query
```sql
SELECT ENAME, JOB, SAL
FROM EMPLOYEE
WHERE (JOB, SAL) IN (SELECT JOB, MAX(SAL) FROM EMPLOYEE GROUP BY JOB);
```

### Output
| ENAME | JOB | SAL |
|-------|-----|-----|
| JONES | MANAGER | 2975 |
| SCOTT | ANALYST | 3000 |
| KING | PRESIDENT | 5000 |
| ALLEN | SALESMAN | 1600 |
| FORD | ANALYST | 3000 |
| MILLER | CLERK | 1300 |

---

## Question 8
Display the employee names who are working in accounting dept.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'ACCOUNTING');
```

### Output
| ENAME |
|-------|
| CLARK |
| KING |
| MILLER |

---

## Question 9
Display the employee names who are working in chicago.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE LOC = 'CHICAGO');
```

### Output
| ENAME |
|-------|
| ALLEN |
| WARD |
| MARTIN |
| BLAKE |
| TURNER |
| JAMES |

---

## Question 10
Display the job groups having total salary greater than the maximum salary for managers.

### Query
```sql
SELECT JOB, SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY JOB
HAVING SUM(SAL) > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'MANAGER');
```

### Output
| JOB | TOTAL_SALARY |
|-----|--------------|
| ANALYST | 6000 |
| CLERK | 4150 |
| MANAGER | 8275 |
| PRESIDENT | 5000 |
| SALESMAN | 5600 |

---

## Summary

| Query # | Technique | Function/Operator | Objective |
|---------|-----------|-------------------|-----------|
| 1 | Single-Row Subquery | MAX, = | Overall highest salary |
| 2 | Filtered Subquery | MAX, = | Highest salary in group |
| 3 | Comparison Subquery | MAX, > | Comparison across jobs |
| 4 | Range Subquery | Double Subquery | Salary between two people |
| 5 | Logical OR Subquery | OR, > | Multiple conditions |
| 6 | Multi-Column Subquery | IN (Dept, MaxSal) | Dept-wise winners |
| 7 | Multi-Column Subquery | IN (Job, MaxSal) | Job-wise winners |
| 8 | Table-Link Subquery | = (Select DeptNo) | Filtering by DNAME |
| 9 | Table-Link Subquery | = (Select DeptNo) | Filtering by LOC |
| 10 | Group-Filtering Subquery | HAVING, SUM, MAX | Aggregated group comparison |
