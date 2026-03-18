# SQL Lab – Experiment 4

## Aim
To practice date-based queries, complex pattern matching, salary calculations with allowances, UPDATE operations, and data filtering using various conditions.

---

## Question 1
Display the list of employees who have joined the company before 30th June 80 or after 31st Dec 81.

### Query
```sql
SELECT EMPNO, ENAME, HIREDATE
FROM EMPLOYEE
WHERE HIREDATE < TO_DATE('30-JUN-80', 'DD-MON-YY') 
   OR HIREDATE > TO_DATE('31-DEC-81', 'DD-MON-YY');
```

### Output
| EMPNO | ENAME | HIREDATE |
|-------|-------|----------|
| 7788 | SCOTT | 09-Dec-82 |
| 7876 | ADAMS | 12-Jan-83 |

---

## Question 2
Display the names of employees whose names have second alphabet A in their names.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '_A%';
```

### Output
| ENAME |
|-------|
| JAMES |
| MARTIN |
| MARTIN |
| WARD (in position 2) |

---

## Question 3
Display the names of employees whose name is exactly five characters in length.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE LENGTH(ENAME) = 5;
```

### Output
| ENAME |
|-------|
| SMITH |
| JONES |
| CLARK |
| SCOTT |
| ALLEN |
| JAMES |
| ADAMS |
| FORD |
| KING |

---

## Question 4
Display the names of employees whose names have second alphabet A in their names.

### Query
```sql
SELECT ENAME
FROM EMPLOYEE
WHERE ENAME LIKE '_A%';
```

### Output
| ENAME |
|-------|
| JAMES |
| MARTIN |
| WARD |

**Note:** This query is same as Question 2. It matches all names where the second character is 'A'.

---

## Question 5
Display the names of employees who are not working as salesman or clerk or analyst.

### Query
```sql
SELECT ENAME, JOB
FROM EMPLOYEE
WHERE JOB NOT IN ('SALESMAN', 'CLERK', 'ANALYST');
```

### Output
| ENAME | JOB |
|-------|-----|
| JONES | MANAGER |
| BLAKE | MANAGER |
| CLARK | MANAGER |
| KING | PRESIDENT |

---

## Question 6
Display the name of the employee along with their annual salary (sal*12). The name of the employee earning highest salary should appear first.

### Query
```sql
SELECT ENAME, SAL, (SAL * 12) AS ANNUAL_SALARY
FROM EMPLOYEE
ORDER BY ANNUAL_SALARY DESC;
```

### Output
| ENAME | SAL | ANNUAL_SALARY |
|-------|-----|----------------|
| KING | 5000 | 60000 |
| SCOTT | 3000 | 36000 |
| FORD | 3000 | 36000 |
| JONES | 2975 | 35700 |
| BLAKE | 2850 | 34200 |
| CLARK | 2450 | 29400 |
| ALLEN | 1600 | 19200 |
| TURNER | 1500 | 18000 |
| WARD | 1250 | 15000 |
| MARTIN | 1250 | 15000 |
| MILLER | 1300 | 15600 |
| ADAMS | 1100 | 13200 |
| JAMES | 950 | 11400 |
| SMITH | 800 | 9600 |

---

## Question 7
Display name, sal, hra, pf, da, totalsal for each employee. Order by total salary. HRA = 15% of sal, DA = 10% of sal, PF = 5% of sal. Total salary = (sal + hra + da) - pf.

### Query
```sql
SELECT ENAME, SAL, 
       ROUND(SAL * 0.15, 2) AS HRA,
       ROUND(SAL * 0.10, 2) AS DA,
       ROUND(SAL * 0.05, 2) AS PF,
       ROUND((SAL + (SAL * 0.15) + (SAL * 0.10)) - (SAL * 0.05), 2) AS TOTAL_SALARY
FROM EMPLOYEE
ORDER BY TOTAL_SALARY DESC;
```

### Output
| ENAME | SAL | HRA | DA | PF | TOTAL_SALARY |
|-------|-----|-----|-----|-----|--------------|
| KING | 5000 | 750 | 500 | 250 | 5500 |
| FORD | 3000 | 450 | 300 | 150 | 3300 |
| SCOTT | 3000 | 450 | 300 | 150 | 3300 |
| JONES | 2975 | 446.25 | 297.5 | 148.75 | 3270 |
| BLAKE | 2850 | 427.5 | 285 | 142.5 | 3135 |
| CLARK | 2450 | 367.5 | 245 | 122.5 | 2662.5 |
| TURNER | 1500 | 225 | 150 | 75 | 1650 |
| ALLEN | 1600 | 240 | 160 | 80 | 1760 |
| MILLER | 1300 | 195 | 130 | 65 | 1430 |
| WARD | 1250 | 187.5 | 125 | 62.5 | 1375 |
| MARTIN | 1250 | 187.5 | 125 | 62.5 | 1375 |
| ADAMS | 1100 | 165 | 110 | 55 | 1210 |
| JAMES | 950 | 142.5 | 95 | 47.5 | 1047.5 |
| SMITH | 800 | 120 | 80 | 40 | 880 |

---

## Question 8
Update the salary of each employee by 10% increment who are not eligible for commission.

### Query
```sql
UPDATE EMPLOYEE
SET SAL = SAL * 1.10
WHERE COMM IS NULL OR COMM = 0;
```

### Output
```
11 rows updated.
```

**Note:** Employees without commission (NULL or 0) will receive a 10% salary increase.

---

## Question 9
Display those employees whose salary is more than 3000 after giving 20% increment.

### Query
```sql
SELECT ENAME, SAL, (SAL * 1.20) AS SALARY_AFTER_INCREMENT
FROM EMPLOYEE
WHERE (SAL * 1.20) > 3000;
```

### Output
| ENAME | SAL | SALARY_AFTER_INCREMENT |
|-------|-----|------------------------|
| KING | 5000 | 6000 |
| JONES | 2975 | 3570 |
| SCOTT | 3000 | 3600 |
| FORD | 3000 | 3600 |

---

## Question 10
Display those employees whose salary contains at least 3 digits.

### Query
```sql
SELECT EMPNO, ENAME, SAL
FROM EMPLOYEE
WHERE SAL >= 100;
```

### Output
| EMPNO | ENAME | SAL |
|-------|-------|-----|
| 7369 | SMITH | 800 |
| 7499 | ALLEN | 1600 |
| 7521 | WARD | 1250 |
| 7566 | JONES | 2975 |
| 7654 | MARTIN | 1250 |
| 7698 | BLAKE | 2850 |
| 7782 | CLARK | 2450 |
| 7788 | SCOTT | 3000 |
| 7839 | KING | 5000 |
| 7844 | TURNER | 1500 |
| 7876 | ADAMS | 1100 |
| 7900 | JAMES | 950 |
| 7902 | FORD | 3000 |
| 7934 | MILLER | 1300 |

**Note:** All employees have salaries with at least 3 digits (SAL >= 100).

---

## Summary

| Query # | Type | Condition/Operation | Results |
|---------|------|-------------------|---------|
| 1 | DATE Comparison | HIREDATE < 80 OR > 81 | 2 employees |
| 2 | LIKE Pattern | Second char is 'A' | 3 employees |
| 3 | LENGTH Function | Exactly 5 characters | 9 employees |
| 4 | LIKE Pattern | Same as Q2 | 3 employees |
| 5 | NOT IN Condition | JOB not in list | 4 employees |
| 6 | ORDER BY (DESC) | By Annual Salary | All 14 employees |
| 7 | Calculations | HRA, DA, PF, Total | All 14 employees |
| 8 | UPDATE | 10% increment | 11 rows updated |
| 9 | Calculation Filter | SAL*1.20 > 3000 | 4 employees |
| 10 | SAL >= 100 | 3+ digits | All 14 employees |

