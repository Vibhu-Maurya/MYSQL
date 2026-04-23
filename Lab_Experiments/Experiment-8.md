# SQL Lab – Experiment 8

## Aim
To practice various types of Joins (Equi-join, Self-join, Outer-join), multi-table queries involving EMPLOYEE, DEPT, and SALGRADE tables, and sorting/filtering joined data.

---

## Question 1
Display all employees with their dept name.

### Query
```sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

### Output
| ENAME | DNAME |
|-------|-------|
| SMITH | RESEARCH |
| ALLEN | SALES |
| WARD | SALES |
| JONES | RESEARCH |
| MARTIN | SALES |
| BLAKE | SALES |
| CLARK | ACCOUNTING |
| SCOTT | RESEARCH |
| KING | ACCOUNTING |
| TURNER | SALES |
| ADAMS | RESEARCH |
| JAMES | SALES |
| FORD | RESEARCH |
| MILLER | ACCOUNTING |

---

## Question 2
Display those employees whose manager names is jones, and also display their manager name.

### Query
```sql
SELECT E.ENAME, M.ENAME AS MANAGER_NAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

### Output
| ENAME | MANAGER_NAME |
|-------|--------------|
| SCOTT | JONES |
| FORD | JONES |

---

## Question 3
Display employee name, his job, his dept name, his manager name, his grade and make out of an under department wise.

### Query
```sql
SELECT E.ENAME, E.JOB, D.DNAME, M.ENAME AS MGR_NAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
ORDER BY D.DNAME;
```

### Output
| ENAME | JOB | DNAME | MGR_NAME | GRADE |
|-------|-----|-------|----------|-------|
| CLARK | MANAGER | ACCOUNTING | KING | 4 |
| KING | PRESIDENT | ACCOUNTING | | 5 |
| MILLER | CLERK | ACCOUNTING | CLARK | 2 |
| SMITH | CLERK | RESEARCH | FORD | 1 |
| JONES | MANAGER | RESEARCH | KING | 4 |
| SCOTT | ANALYST | RESEARCH | JONES | 4 |
| ADAMS | CLERK | RESEARCH | SCOTT | 1 |
| FORD | ANALYST | RESEARCH | JONES | 4 |
| ALLEN | SALESMAN | SALES | BLAKE | 3 |
| WARD | SALESMAN | SALES | BLAKE | 2 |
| MARTIN | SALESMAN | SALES | BLAKE | 2 |
| BLAKE | MANAGER | SALES | KING | 4 |
| TURNER | SALESMAN | SALES | BLAKE | 3 |
| JAMES | CLERK | SALES | BLAKE | 1 |

---

## Question 4
List out all the employees name, job, and salary grade and department name for everyone in the company except ‘clerk’. Sort on salary display the highest salary.

### Query
```sql
SELECT E.ENAME, E.JOB, S.GRADE, D.DNAME, E.SAL
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.JOB <> 'CLERK'
ORDER BY E.SAL DESC;
```

### Output
| ENAME | JOB | GRADE | DNAME | SAL |
|-------|-----|-------|-------|-----|
| KING | PRESIDENT | 5 | ACCOUNTING | 5000 |
| SCOTT | ANALYST | 4 | RESEARCH | 3000 |
| FORD | ANALYST | 4 | RESEARCH | 3000 |
| JONES | MANAGER | 4 | RESEARCH | 2975 |
| BLAKE | MANAGER | 4 | SALES | 2850 |
| CLARK | MANAGER | 4 | ACCOUNTING | 2450 |
| ALLEN | SALESMAN | 3 | SALES | 1600 |
| TURNER | SALESMAN | 3 | SALES | 1500 |
| WARD | SALESMAN | 2 | SALES | 1250 |
| MARTIN | SALESMAN | 2 | SALES | 1250 |

---

## Question 5
Display employee name, his job and his manager. Display also employees who are without manager.

### Query
```sql
SELECT E.ENAME, E.JOB, M.ENAME AS MANAGER
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```

### Output
| ENAME | JOB | MANAGER |
|-------|-----|---------|
| SMITH | CLERK | FORD |
| ALLEN | SALESMAN | BLAKE |
| WARD | SALESMAN | BLAKE |
| JONES | MANAGER | KING |
| MARTIN | SALESMAN | BLAKE |
| BLAKE | MANAGER | KING |
| CLARK | MANAGER | KING |
| SCOTT | ANALYST | JONES |
| KING | PRESIDENT | |
| TURNER | SALESMAN | BLAKE |
| ADAMS | CLERK | SCOTT |
| JAMES | CLERK | BLAKE |
| FORD | ANALYST | JONES |
| MILLER | CLERK | CLARK |

---

## Question 6
List the employee name, job, annual salary, deptno, dept name and grade who earn 36000 a year or who are not clerks.

### Query
```sql
SELECT E.ENAME, E.JOB, E.SAL * 12 AS ANNUAL_SALARY, E.DEPTNO, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE (E.SAL * 12) = 36000 OR E.JOB <> 'CLERK';
```

### Output
| ENAME | JOB | ANNUAL_SALARY | DEPTNO | DNAME | GRADE |
|-------|-----|---------------|--------|-------|-------|
| ALLEN | SALESMAN | 19200 | 30 | SALES | 3 |
| WARD | SALESMAN | 15000 | 30 | SALES | 2 |
| JONES | MANAGER | 35700 | 20 | RESEARCH | 4 |
| MARTIN | SALESMAN | 15000 | 30 | SALES | 2 |
| BLAKE | MANAGER | 34200 | 30 | SALES | 4 |
| CLARK | MANAGER | 29400 | 10 | ACCOUNTING | 4 |
| SCOTT | ANALYST | 36000 | 20 | RESEARCH | 4 |
| KING | PRESIDENT | 60000 | 10 | ACCOUNTING | 5 |
| TURNER | SALESMAN | 18000 | 30 | SALES | 3 |
| FORD | ANALYST | 36000 | 20 | RESEARCH | 4 |

---

## Question 7
List ename, job, annual sal, deptno, dname and grade who earn 30000 per year and who are not clerks.

### Query
```sql
SELECT E.ENAME, E.JOB, E.SAL * 12 AS ANNUAL_SALARY, E.DEPTNO, D.DNAME, S.GRADE
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE (E.SAL * 12) = 30000 AND E.JOB <> 'CLERK';
```

### Output
```
No records found.
```

**Note:** No non-clerk employee has an annual salary exactly matching 30000 (2500 monthly).

---

## Question 8
List out all employees by name and number along with their manager’s name and number also display ‘no manager’ who has no manager.

### Query
```sql
SELECT E.ENAME, E.EMPNO, 
       NVL(M.ENAME, 'no manager') AS MGR_NAME, 
       NVL(TO_CHAR(M.EMPNO), 'no manager') AS MGR_NO
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```

### Output
| ENAME | EMPNO | MGR_NAME | MGR_NO |
|-------|-------|----------|--------|
| SMITH | 7369 | FORD | 7902 |
| ALLEN | 7499 | BLAKE | 7698 |
| WARD | 7521 | BLAKE | 7698 |
| JONES | 7566 | KING | 7839 |
| MARTIN | 7654 | BLAKE | 7698 |
| BLAKE | 7698 | KING | 7839 |
| CLARK | 7782 | KING | 7839 |
| SCOTT | 7788 | JONES | 7566 |
| KING | 7839 | no manager | no manager |
| TURNER | 7844 | BLAKE | 7698 |
| ADAMS | 7876 | SCOTT | 7788 |
| JAMES | 7900 | BLAKE | 7698 |
| FORD | 7902 | JONES | 7566 |
| MILLER | 7934 | CLARK | 7782 |

---

## Question 9
Select dept name, dept no and sum of sal.

### Query
```sql
SELECT D.DNAME, D.DEPTNO, SUM(E.SAL) AS TOTAL_SALARY
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
GROUP BY D.DNAME, D.DEPTNO;
```

### Output
| DNAME | DEPTNO | TOTAL_SALARY |
|-------|--------|--------------|
| ACCOUNTING | 10 | 8750 |
| RESEARCH | 20 | 10875 |
| SALES | 30 | 9400 |

---

## Question 10
Display employee number, name and location of the department in which he is working.

### Query
```sql
SELECT E.EMPNO, E.ENAME, D.LOC
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

### Output
| EMPNO | ENAME | LOC |
|-------|-------|-----|
| 7369 | SMITH | DALLAS |
| 7499 | ALLEN | CHICAGO |
| 7521 | WARD | CHICAGO |
| 7566 | JONES | DALLAS |
| 7654 | MARTIN | CHICAGO |
| 7698 | BLAKE | CHICAGO |
| 7782 | CLARK | NEW YORK |
| 7788 | SCOTT | DALLAS |
| 7839 | KING | NEW YORK |
| 7844 | TURNER | CHICAGO |
| 7876 | ADAMS | DALLAS |
| 7900 | JAMES | CHICAGO |
| 7902 | FORD | DALLAS |
| 7934 | MILLER | NEW YORK |

---

## Question 11
Display employee name and department name for each employee.

### Query
```sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO;
```

### Output
| ENAME | DNAME |
|-------|-------|
| SMITH | RESEARCH |
| ALLEN | SALES |
| WARD | SALES |
| JONES | RESEARCH |
| MARTIN | SALES |
| BLAKE | SALES |
| CLARK | ACCOUNTING |
| SCOTT | RESEARCH |
| KING | ACCOUNTING |
| TURNER | SALES |
| ADAMS | RESEARCH |
| JAMES | SALES |
| FORD | RESEARCH |
| MILLER | ACCOUNTING |

---

## Summary

| Query # | Focus | Join Type | Key Features |
|---------|-------|-----------|--------------|
| 1 | Dept Info | Equi-Join | Basic join between EMP and DEPT |
| 2 | Management | Self-Join | Joining EMP table to itself via MGR field |
| 3 | Comprehensive | Multi-Table | Join 3 tables + Left Outer join for Mgr |
| 4 | Filtering | Multi-Table | Exclusion filter (NOT CLERK) + DESC Sort |
| 5 | Connectivity | Left Join | Displaying employees even without managers |
| 6 | Complex OR | Multi-Table | Filters on annual sal OR job type |
| 7 | Complex AND | Multi-Table | Filters on annual sal AND job type |
| 8 | Null Handling | Left Join | Using NVL to display 'no manager' |
| 9 | Aggregation | Equi-Join | Grouping and Summing by department |
| 10 | Location | Equi-Join | Displaying LOC field from DEPT table |
| 11 | Department | Equi-Join | Simple lookup of DNAME |
