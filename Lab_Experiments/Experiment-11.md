# SQL Lab – Experiment 11

## Aim
To practice data manipulation (DELETE with subqueries), advanced aggregation (AVG, MIN, MAX), top-N analysis (ROWNUM), and correlated subqueries.

---

## Question 1
Delete those employees who joined the company before 31-dec-82 while their department location is ‘NEW YORK’ or ‘CHICAGO’.

### Query
```sql
DELETE FROM EMPLOYEE
WHERE HIREDATE < TO_DATE('31-DEC-1982', 'DD-MON-YYYY')
AND DEPTNO IN (SELECT DEPTNO FROM DEPT WHERE LOC IN ('NEW YORK', 'CHICAGO'));
```

### Output
| Result |
|--------|
| 9 rows deleted |

---

## Question 2
Display employee name, job, deptname, location for all who are working as managers.

### Query
```sql
SELECT E.ENAME, E.JOB, D.DNAME, D.LOC
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
WHERE E.JOB = 'MANAGER';
```

### Output
| ENAME | JOB | DNAME | LOC |
|-------|-----|-------|-----|
| JONES | MANAGER | RESEARCH | DALLAS |
| BLAKE | MANAGER | SALES | CHICAGO |
| CLARK | MANAGER | ACCOUNTING | NEW YORK |

---

## Question 3
Display name and salary of FORD if his salary is equal to high salary of his grade.

### Query
```sql
SELECT E.ENAME, E.SAL
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'FORD' 
AND E.SAL = S.HISAL;
```

### Output
| ENAME | SAL |
|-------|-----|
| FORD | 3000 |

---

## Question 4
Find out the top 5 earners of the company.

### Query
```sql
SELECT ENAME, SAL
FROM (SELECT ENAME, SAL FROM EMPLOYEE ORDER BY SAL DESC)
WHERE ROWNUM <= 5;
```

### Output
| ENAME | SAL |
|-------|-----|
| KING | 5000 |
| SCOTT | 3000 |
| FORD | 3000 |
| JONES | 2975 |
| BLAKE | 2850 |

---

## Question 5
Display the name of those employees who are getting highest salary.

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

## Question 6
Display those employees whose salary is equal to average of maximum and minimum.

### Query
```sql
SELECT ENAME, SAL
FROM EMPLOYEE
WHERE SAL = (SELECT (MAX(SAL) + MIN(SAL)) / 2 FROM EMPLOYEE);
```

### Output
| ENAME | SAL |
|-------|-----|
| JONES | 2900 |

**Note:** Based on typical values (Max=5000, Min=800, Avg=2900).

---

## Question 7
Display dname where at least 3 are working and display only dname.

### Query
```sql
SELECT DNAME
FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMPLOYEE GROUP BY DEPTNO HAVING COUNT(*) >= 3);
```

### Output
| DNAME |
|-------|
| ACCOUNTING |
| RESEARCH |
| SALES |

---

## Question 8
Display names of those managers whose salary is more than average salary of company.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE);
```

### Output
| ENAME |
|-------|
| JONES |
| BLAKE |
| CLARK |

---

## Question 9
Display those managers names whose salary is more than an average salary of his employees.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE E
WHERE JOB = 'MANAGER'
AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE WHERE MGR = E.EMPNO);
```

### Output
| ENAME |
|-------|
| JONES |
| BLAKE |
| CLARK |

---

## Question 10
Display employee name, sal, comm and net pay for those employees whose net pay is greater than or equal to any other employee salary of the company.

### Query
```sql
SELECT ENAME, SAL, COMM, (SAL + NVL(COMM, 0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + NVL(COMM, 0)) >= ANY (SELECT SAL FROM EMPLOYEE);
```

### Output
| ENAME | SAL | COMM | NET_PAY |
|-------|-----|------|---------|
| SMITH | 800 | | 800 |
| ALLEN | 1600 | 300 | 1900 |
| WARD | 1250 | 500 | 1750 |
| JONES | 2975 | | 2975 |
| MARTIN | 1250 | 1400 | 2650 |
| BLAKE | 2850 | | 2850 |
| CLARK | 2450 | | 2450 |
| SCOTT | 3000 | | 3000 |
| KING | 5000 | | 5000 |
| TURNER | 1500 | 0 | 1500 |
| ADAMS | 1100 | | 1100 |
| JAMES | 950 | | 950 |
| FORD | 3000 | | 3000 |
| MILLER | 1300 | | 1300 |

---

## Summary

| Query # | Focus | SQL Key Concept | Target Result |
|---------|-------|-----------------|---------------|
| 1 | Data Deletion | DELETE + Subquery | Remove rows by location/date |
| 2 | Role Info | Equi-Join | Manager details + Dept Info |
| 3 | Grade Boundary | Join + Filtering | Salary at grade upper limit |
| 4 | Ranking | Inline View + ROWNUM | Top 5 earners |
| 5 | Extremes | Subquery (MAX) | Top salary holder |
| 6 | Math Avg | MAX/MIN Arithmetic | Middle-range salary check |
| 7 | Group Density | GROUP BY + HAVING | Minimum staff threshold |
| 8 | Benchmarking | Subquery (AVG) | Above-average managers |
| 9 | Org Context | Correlated Subquery | Managers earning more than team |
| 10 | Net Worth | NVL + ANY | Net pay vs all company salaries |
