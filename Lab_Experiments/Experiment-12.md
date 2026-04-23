# SQL Lab – Experiment 12

## Aim
To practice complex hierarchical queries, data integrity maintenance (DELETE with NOT IN), existence checks (NOT EXISTS), and advanced string/set comparisons.

---

## Question 1
Display those employees whose salary is less than their manager but more than the salary of any other managers.

### Query
```sql
SELECT E.ENAME, E.SAL, M.ENAME AS MGR_NAME, M.SAL AS MGR_SAL
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL < M.SAL
AND E.SAL > ANY (SELECT SAL FROM EMPLOYEE WHERE JOB = 'MANAGER' AND EMPNO <> E.MGR);
```

### Output
| ENAME | SAL | MGR_NAME | MGR_SAL |
|-------|-----|----------|---------|
| CLARK | 2450 | KING | 5000 |

---

## Question 2
Find out the number of employees whose salary is greater than their manager's salary.

### Query
```sql
SELECT COUNT(*) AS COUNT_SAL_GT_MGR
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

### Output
| COUNT_SAL_GT_MGR |
|------------------|
| 2 |

---

## Question 3
Display those managers who are not working under the President but are working under any other manager.

### Query
```sql
SELECT ENAME, JOB
FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND MGR IS NOT NULL
AND MGR NOT IN (SELECT EMPNO FROM EMPLOYEE WHERE JOB = 'PRESIDENT');
```

### Output
| ENAME | JOB |
|-------|-----|
| BLAKE | MANAGER |
| CLARK | MANAGER |

---

## Question 4
Delete those departments where no employee is working.

### Query
```sql
DELETE FROM DEPT
WHERE DEPTNO NOT IN (SELECT DISTINCT DEPTNO FROM EMPLOYEE WHERE DEPTNO IS NOT NULL);
```

### Output
| Result |
|--------|
| 1 row deleted |

**Note:** Typically deletes Dept 40 (OPERATIONS) if no one is assigned.

---

## Question 5
Delete those records from the employee table whose deptno is not available in the dept table.

### Query
```sql
DELETE FROM EMPLOYEE
WHERE DEPTNO NOT IN (SELECT DEPTNO FROM DEPT);
```

### Output
| Result |
|--------|
| 0 rows deleted |

**Note:** Maintains referential integrity by removing orphaned records.

---

## Question 6
Display those earners whose salary is out of the grades available in the salgrade table.

### Query
```sql
SELECT ENAME, SAL
FROM EMPLOYEE E
WHERE NOT EXISTS (
    SELECT 1 FROM SALGRADE S WHERE E.SAL BETWEEN S.LOSAL AND S.HISAL
);
```

### Output
```
No records found.
```

---

## Question 7
Display employee name, salary, commission, and those whose net pay is greater than any other in the company.

### Query
```sql
SELECT ENAME, SAL, COMM, (SAL + NVL(COMM, 0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + NVL(COMM, 0)) = (SELECT MAX(SAL + NVL(COMM, 0)) FROM EMPLOYEE);
```

### Output
| ENAME | SAL | COMM | NET_PAY |
|-------|-----|------|---------|
| KING | 5000 | | 5000 |

---

## Question 8
Display those employees who are working in SALES or RESEARCH.

### Query
```sql
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPT D ON E.DEPTNO = D.DEPTNO
WHERE D.DNAME IN ('SALES', 'RESEARCH');
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
| SCOTT | RESEARCH |
| TURNER | SALES |
| ADAMS | RESEARCH |
| JAMES | SALES |
| FORD | RESEARCH |

---

## Question 9
Display the grade of JONES.

### Query
```sql
SELECT S.GRADE
FROM EMPLOYEE E
JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
WHERE E.ENAME = 'JONES';
```

### Output
| GRADE |
|-------|
| 4 |

---

## Question 10
Display the department name, the number of characters of which is equal to the number of employees in any other department.

### Query
```sql
SELECT D.DNAME, LENGTH(D.DNAME) AS NAME_LEN
FROM DEPT D
WHERE LENGTH(D.DNAME) IN (
    SELECT COUNT(*) 
    FROM EMPLOYEE 
    WHERE DEPTNO <> D.DEPTNO 
    GROUP BY DEPTNO
);
```

### Output
| DNAME | NAME_LEN |
|-------|----------|
| SALES | 5 |

**Note:** 'SALES' has 5 chars, matching a department (e.g., RESEARCH) having 5 employees.

---

## Summary

| Query # | Technique | SQL Mechanism | Key Goal |
|---------|-----------|---------------|----------|
| 1 | Double Comparison | Join + ANY | Multi-tier salary check |
| 2 | Aggregate Count | Self-Join | Count outliers |
| 3 | Filtered Hierarchy | NOT IN Presidente | Specific reporting lines |
| 4 | Cleanup | NOT IN | Remove empty departments |
| 5 | Data Integrity | NOT IN | Remove orphaned employees |
| 6 | Existence | NOT EXISTS | Find data outside ranges |
| 7 | Global Max | Subquery (MAX) | Top net pay identification |
| 8 | Multi-Value | Join + IN | Group-based lookup |
| 9 | Grade Lookup | Join + Between | Specific data point retrieval |
| 10 | Meta-Comparison | LENGTH + GROUP BY | Inter-departmental logic |
