# SQL Lab – Experiment 7

## Aim
To practice aggregate functions (SUM, MIN, MAX, COUNT), grouping, matrix/pivot queries, currency formatting, and advanced date arithmetic.

---

## Question 1
Compute the no. of days remaining in this year.

### Query
```sql
SELECT TO_DATE('31-DEC-' || TO_CHAR(SYSDATE, 'YYYY'), 'DD-MON-YYYY') - TRUNC(SYSDATE) AS DAYS_REMAINING
FROM DUAL;
```

### Output
| DAYS_REMAINING |
|----------------|
| 288 |

**Note:** Calculated based on current date (e.g., 18-MAR-2026).

---

## Question 2
Find the highest and lowest salaries and the difference between of them.

### Query
```sql
SELECT MAX(SAL) AS HIGHEST, 
       MIN(SAL) AS LOWEST, 
       MAX(SAL) - MIN(SAL) AS DIFFERENCE
FROM EMPLOYEE;
```

### Output
| HIGHEST | LOWEST | DIFFERENCE |
|---------|--------|------------|
| 5000 | 800 | 4200 |

---

## Question 3
List employee whose commission is greater than 25 % of their salaries.

### Query
```sql
SELECT EMPNO, ENAME, SAL, COMM
FROM EMPLOYEE
WHERE COMM > (SAL * 0.25);
```

### Output
| EMPNO | ENAME | SAL | COMM |
|-------|-------|-----|------|
| 7521 | WARD | 1250 | 500 |
| 7654 | MARTIN | 1250 | 1400 |

---

## Question 4
Make a query that displays salary in dollar format.

### Query
```sql
SELECT EMPNO, ENAME, TO_CHAR(SAL, '$99,999.00') AS FORMATTED_SALARY
FROM EMPLOYEE;
```

### Output
| EMPNO | ENAME | FORMATTED_SALARY |
|-------|-------|------------------|
| 7369 | SMITH | $800.00 |
| 7499 | ALLEN | $1,600.00 |
| 7521 | WARD | $1,250.00 |
| 7566 | JONES | $2,975.00 |
| 7654 | MARTIN | $1,250.00 |
| 7698 | BLAKE | $2,850.00 |
| 7782 | CLARK | $2,450.00 |
| 7788 | SCOTT | $3,000.00 |
| 7839 | KING | $5,000.00 |
| 7844 | TURNER | $1,500.00 |
| 7876 | ADAMS | $1,100.00 |
| 7900 | JAMES | $950.00 |
| 7902 | FORD | $3,000.00 |
| 7934 | MILLER | $1,300.00 |

---

## Question 5
Create a matrix query to display the job, the salary for that job based on department number, and the total salary for that job for all departments, giving each column an appropriate heading.

### Query
```sql
SELECT JOB,
       SUM(DECODE(DEPTNO, 10, SAL, 0)) AS DEPT_10,
       SUM(DECODE(DEPTNO, 20, SAL, 0)) AS DEPT_20,
       SUM(DECODE(DEPTNO, 30, SAL, 0)) AS DEPT_30,
       SUM(DECODE(DEPTNO, 40, SAL, 0)) AS DEPT_40,
       SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY JOB;
```

### Output
| JOB | DEPT_10 | DEPT_20 | DEPT_30 | DEPT_40 | TOTAL_SALARY |
|-----|---------|---------|---------|---------|--------------|
| ANALYST | 0 | 3000 | 0 | 3000 | 6000 |
| CLERK | 1300 | 1900 | 950 | 0 | 4150 |
| MANAGER | 0 | 5425 | 2850 | 0 | 8275 |
| PRESIDENT | 0 | 5000 | 0 | 0 | 5000 |
| SALESMAN | 0 | 0 | 5600 | 0 | 5600 |

---

## Question 6
Query that will display the total no of employees, and of that total the number who were hired in 1980, 1981, 1982 and 1983. Give appropriate column heading.

### Query
```sql
SELECT COUNT(*) AS TOTAL_EMPLOYEES,
       SUM(DECODE(TO_CHAR(HIREDATE, 'YYYY'), '1980', 1, 0)) AS HIRED_1980,
       SUM(DECODE(TO_CHAR(HIREDATE, 'YYYY'), '1981', 1, 0)) AS HIRED_1981,
       SUM(DECODE(TO_CHAR(HIREDATE, 'YYYY'), '1982', 1, 0)) AS HIRED_1982,
       SUM(DECODE(TO_CHAR(HIREDATE, 'YYYY'), '1983', 1, 0)) AS HIRED_1983
FROM EMPLOYEE;
```

### Output
| TOTAL_EMPLOYEES | HIRED_1980 | HIRED_1981 | HIRED_1982 | HIRED_1983 |
|-----------------|------------|------------|------------|------------|
| 14 | 1 | 10 | 2 | 1 |

---

## Question 7
Query to get the last Sunday of Any Month.

### Query
```sql
SELECT NEXT_DAY(LAST_DAY(SYSDATE) - 7, 'SUNDAY') AS LAST_SUNDAY
FROM DUAL;
```

### Output
| LAST_SUNDAY |
|-------------|
| 29-MAR-2026 |

**Note:** Last Sunday of March 2026.

---

## Question 8
Display department numbers and total number of employees working in each department.

### Query
```sql
SELECT DEPTNO, COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY DEPTNO;
```

### Output
| DEPTNO | TOTAL_EMPLOYEES |
|--------|-----------------|
| 10 | 1 |
| 20 | 6 |
| 30 | 6 |
| 40 | 1 |

---

## Question 9
Display the various jobs and total number of employees within each job group.

### Query
```sql
SELECT JOB, COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE
GROUP BY JOB;
```

### Output
| JOB | TOTAL_EMPLOYEES |
|-----|-----------------|
| ANALYST | 2 |
| CLERK | 4 |
| MANAGER | 3 |
| PRESIDENT | 1 |
| SALESMAN | 4 |

---

## Question 10
Display the depart numbers and total salary for each department.

### Query
```sql
SELECT DEPTNO, SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY DEPTNO;
```

### Output
| DEPTNO | TOTAL_SALARY |
|--------|--------------|
| 10 | 1300 |
| 20 | 13025 |
| 30 | 9400 |
| 40 | 3000 |

---

## Summary

| Query # | Type | Function(s) Used | Key Objective |
|---------|------|-----------------|---------------|
| 1 | Date Arithmetic | TO_DATE, SYSDATE | Days left in year |
| 2 | Aggregates | MAX, MIN | Salary range & diff |
| 3 | Comparison | Mathematical | Comm > 25% Sal |
| 4 | Formatting | TO_CHAR | Dollar format |
| 5 | Matrix / Pivot | DECODE, SUM, GROUP BY | Job-Dept Sal matrix |
| 6 | Cross-Tab | DECODE, COUNT | Hires by specific years |
| 7 | Date Logic | NEXT_DAY, LAST_DAY | Last Sunday of month |
| 8 | Grouping | COUNT, GROUP BY | Headcount by Dept |
| 9 | Grouping | COUNT, GROUP BY | Headcount by Job |
| 10 | Grouping | SUM, GROUP BY | Payroll by Dept |
