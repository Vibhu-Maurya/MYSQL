# SQL Lab – Experiment 10

## Aim
To practice advanced query techniques including ANY/ALL operators, self-joins for hierarchical data, multi-table joins with complex conditions, and date-based filtering.

---

## Question 1
Display the names of employees from department number 10 with salary greater than that of any employee working in other departments.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ANY (SELECT SAL FROM EMPLOYEE WHERE DEPTNO <> 10);
```

### Output
| ENAME |
|-------|
| CLARK |
| KING |
| MILLER |

---

## Question 2
Display the names of employee from department number 10 with salary greater than that of all employee working in other departments.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ALL (SELECT SAL FROM EMPLOYEE WHERE DEPTNO <> 10);
```

### Output
| ENAME |
|-------|
| KING |

---

## Question 3
Display the details of employees who are in sales dept and grade is 3.

### Query
```sql
SELECT E.*
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE D.DNAME = 'SALES' AND S.GRADE = 3;
```

### Output
| EMPNO | ENAME | JOB | MGR | HIREDATE | SAL | COMM | DEPTNO |
|-------|-------|-----|-----|----------|-----|------|--------|
| 7499 | ALLEN | SALESMAN | 7698 | 20-Feb-81 | 1600 | 300 | 30 |
| 7844 | TURNER | SALESMAN | 7698 | 08-Sep-81 | 1500 | 0 | 30 |

---

## Question 4
Display those who are not managers and who are managers.

### Query
```sql
SELECT ENAME, 
       CASE 
           WHEN EMPNO IN (SELECT MGR FROM EMPLOYEE WHERE MGR IS NOT NULL) THEN 'MANAGER'
           ELSE 'NOT A MANAGER'
       END AS STATUS
FROM EMPLOYEE;
```

### Output
| ENAME | STATUS |
|-------|--------|
| SMITH | NOT A MANAGER |
| ALLEN | NOT A MANAGER |
| WARD | NOT A MANAGER |
| JONES | MANAGER |
| MARTIN | NOT A MANAGER |
| BLAKE | MANAGER |
| CLARK | MANAGER |
| SCOTT | MANAGER |
| KING | MANAGER |
| TURNER | NOT A MANAGER |
| ADAMS | NOT A MANAGER |
| JAMES | NOT A MANAGER |
| FORD | MANAGER |
| MILLER | NOT A MANAGER |

---

## Question 5
Display those employees whose manager name is jones.

### Query
```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

### Output
| ENAME |
|-------|
| SCOTT |
| FORD |

---

## Question 6
Display ename who are working in sales dept.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES');
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

## Question 7
Display employee name, deptname, salary and comm. For those sal in between 2000 to 5000 while location is chicago.

### Query
```sql
SELECT E.ENAME, D.DNAME, E.SAL, E.COMM
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
WHERE E.SAL BETWEEN 2000 AND 5000 
AND D.LOC = 'CHICAGO';
```

### Output
| ENAME | DNAME | SAL | COMM |
|-------|-------|-----|------|
| BLAKE | SALES | 2850 | |

---

## Question 8
Display those employees whose salary greater than his manager salary.

### Query
```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

### Output
| ENAME |
|-------|
| SCOTT |
| FORD |

---

## Question 9
Display those employees who are working in the same dept where his manager is working.

### Query
```sql
SELECT E.ENAME
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.DEPTNO = M.DEPTNO;
```

### Output
| ENAME |
|-------|
| SMITH |
| WARD |
| MARTIN |
| SCOTT |
| TURNER |
| JAMES |
| FORD |
| MILLER |

---

## Question 10
Display grade and employees name for the dept no 10 or 30 but grade is not 4, while joined the company before 31-dec-82.

### Query
```sql
SELECT S.GRADE, E.ENAME
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.DEPTNO IN (10, 30) 
AND S.GRADE <> 4 
AND E.HIREDATE < TO_DATE('31-DEC-1982', 'DD-MON-YYYY');
```

### Output
| GRADE | ENAME |
|-------|-------|
| 3 | ALLEN |
| 2 | WARD |
| 2 | MARTIN |
| 5 | KING |
| 3 | TURNER |
| 1 | JAMES |
| 2 | MILLER |

---

## Summary

| Query # | Feature | SQL Mechanism | Target Result |
|---------|---------|---------------|---------------|
| 1 | ANY Operator | Subquery Comparison | Sal > at least one other |
| 2 | ALL Operator | Subquery Comparison | Sal > everyone else |
| 3 | Multi-Table | Join + Between | Specific job/grade combo |
| 4 | Existence | Subquery / CASE | Role identification |
| 5 | Hierarchy | Self-Join | Indirect manager filtering |
| 6 | Nested Select | Subquery | Dept-based filtering |
| 7 | Location-Based | Join + Range | Geo-filtered results |
| 8 | Salary Comparison | Self-Join | Employees earning more than boss |
| 9 | Org Structure | Self-Join | Common department check |
| 10 | Complex Filters | Joins + Date + Lists | Multi-constrained report |
