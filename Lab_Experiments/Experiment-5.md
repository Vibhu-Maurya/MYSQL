# SQL Lab – Experiment 5

## Aim
To practice aggregate functions (COUNT, SUM, MAX, MIN, AVG) and string manipulation functions (UPPER, LOWER, INITCAP, LENGTH) for data analysis and text processing on the Employee table.

---

## Question 1
Display the total number of employees working in the company.

### Query
```sql
SELECT COUNT(*) AS TOTAL_EMPLOYEES
FROM EMPLOYEE;
```

### Output
| TOTAL_EMPLOYEES |
|-----------------|
| 14 |

---

## Question 2
Display the total salary being paid to all employees.

### Query
```sql
SELECT SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE;
```

### Output
| TOTAL_SALARY |
|--------------|
| 29025 |

---

## Question 3
Display the maximum salary from employee table.

### Query
```sql
SELECT MAX(SAL) AS MAXIMUM_SALARY
FROM EMPLOYEE;
```

### Output
| MAXIMUM_SALARY |
|----------------|
| 5000 |

---

## Question 4
Display the minimum salary from employee table.

### Query
```sql
SELECT MIN(SAL) AS MINIMUM_SALARY
FROM EMPLOYEE;
```

### Output
| MINIMUM_SALARY |
|----------------|
| 800 |

---

## Question 5
Display the average salary from employee table.

### Query
```sql
SELECT AVG(SAL) AS AVERAGE_SALARY
FROM EMPLOYEE;
```

### Output
| AVERAGE_SALARY |
|----------------|
| 2073.21 |

---

## Question 6
Display the maximum salary being paid to clerk.

### Query
```sql
SELECT MAX(SAL) AS MAX_CLERK_SALARY
FROM EMPLOYEE
WHERE JOB = 'CLERK';
```

### Output
| MAX_CLERK_SALARY |
|------------------|
| 1100 |

**Note:** Employee ADAMS (EMPNO 7876) is the clerk with highest salary.

---

## Question 7
Display the maximum salary being paid in department number 20.

### Query
```sql
SELECT MAX(SAL) AS MAX_DEPT20_SALARY
FROM EMPLOYEE
WHERE DEPTNO = 20;
```

### Output
| MAX_DEPT20_SALARY |
|-------------------|
| 5000 |

**Note:** Employee KING (EMPNO 7839) from DEPTNO 20 has the highest salary in the department.

---

## Question 8
Display the minimum salary paid to any salesman.

### Query
```sql
SELECT MIN(SAL) AS MIN_SALESMAN_SALARY
FROM EMPLOYEE
WHERE JOB = 'SALESMAN';
```

### Output
| MIN_SALESMAN_SALARY |
|---------------------|
| 1250 |

**Note:** Employees WARD and MARTIN have the minimum salesman salary of 1250.

---

## Question 9
Display the average salary drawn by managers.

### Query
```sql
SELECT AVG(SAL) AS AVG_MANAGER_SALARY
FROM EMPLOYEE
WHERE JOB = 'MANAGER';
```

### Output
| AVG_MANAGER_SALARY |
|--------------------|
| 2758.33 |

**Note:** Average of managers: (2975 + 2850 + 2450) / 3 = 2758.33

---

## Question 10
Display the total salary drawn by analysts working in department number 40.

### Query
```sql
SELECT SUM(SAL) AS TOTAL_ANALYST_SALARY
FROM EMPLOYEE
WHERE JOB = 'ANALYST' AND DEPTNO = 40;
```

### Output
| TOTAL_ANALYST_SALARY |
|----------------------|
| 3000 |

**Note:** Only SCOTT (EMPNO 7788) is an analyst in DEPTNO 40.

---

## Question 11
Display the names of the employee in Uppercase.

### Query
```sql
SELECT EMPNO, ENAME, UPPER(ENAME) AS ENAME_UPPERCASE
FROM EMPLOYEE;
```

### Output
| EMPNO | ENAME | ENAME_UPPERCASE |
|-------|-------|-----------------|
| 7369 | SMITH | SMITH |
| 7499 | ALLEN | ALLEN |
| 7521 | WARD | WARD |
| 7566 | JONES | JONES |
| 7654 | MARTIN | MARTIN |
| 7698 | BLAKE | BLAKE |
| 7782 | CLARK | CLARK |
| 7788 | SCOTT | SCOTT |
| 7839 | KING | KING |
| 7844 | TURNER | TURNER |
| 7876 | ADAMS | ADAMS |
| 7900 | JAMES | JAMES |
| 7902 | FORD | FORD |
| 7934 | MILLER | MILLER |

---

## Question 12
Display the names of the employee in Lowercase.

### Query
```sql
SELECT EMPNO, ENAME, LOWER(ENAME) AS ENAME_LOWERCASE
FROM EMPLOYEE;
```

### Output
| EMPNO | ENAME | ENAME_LOWERCASE |
|-------|-------|-----------------|
| 7369 | SMITH | smith |
| 7499 | ALLEN | allen |
| 7521 | WARD | ward |
| 7566 | JONES | jones |
| 7654 | MARTIN | martin |
| 7698 | BLAKE | blake |
| 7782 | CLARK | clark |
| 7788 | SCOTT | scott |
| 7839 | KING | king |
| 7844 | TURNER | turner |
| 7876 | ADAMS | adams |
| 7900 | JAMES | james |
| 7902 | FORD | ford |
| 7934 | MILLER | miller |

---

## Question 13
Display the names of the employee in Proper case.

### Query
```sql
SELECT EMPNO, ENAME, INITCAP(LOWER(ENAME)) AS ENAME_PROPER_CASE
FROM EMPLOYEE;
```

### Output
| EMPNO | ENAME | ENAME_PROPER_CASE |
|-------|-------|-------------------|
| 7369 | SMITH | Smith |
| 7499 | ALLEN | Allen |
| 7521 | WARD | Ward |
| 7566 | JONES | Jones |
| 7654 | MARTIN | Martin |
| 7698 | BLAKE | Blake |
| 7782 | CLARK | Clark |
| 7788 | SCOTT | Scott |
| 7839 | KING | King |
| 7844 | TURNER | Turner |
| 7876 | ADAMS | Adams |
| 7900 | JAMES | James |
| 7902 | FORD | Ford |
| 7934 | MILLER | Miller |

---

## Question 14
Display the length of Your name using appropriate function.

### Query
```sql
SELECT LENGTH('VIBHU-KAVI') AS NAME_LENGTH;
```

### Output
| NAME_LENGTH |
|-------------|
| 10 |

**Note:** The name 'VIBHU-KAVI' has 10 characters including the hyphen.

---

## Question 15
Display the length of all the employee names.

### Query
```sql
SELECT EMPNO, ENAME, LENGTH(ENAME) AS NAME_LENGTH
FROM EMPLOYEE;
```

### Output
| EMPNO | ENAME | NAME_LENGTH |
|-------|-------|-------------|
| 7369 | SMITH | 5 |
| 7499 | ALLEN | 5 |
| 7521 | WARD | 4 |
| 7566 | JONES | 5 |
| 7654 | MARTIN | 6 |
| 7698 | BLAKE | 5 |
| 7782 | CLARK | 5 |
| 7788 | SCOTT | 5 |
| 7839 | KING | 4 |
| 7844 | TURNER | 6 |
| 7876 | ADAMS | 5 |
| 7900 | JAMES | 5 |
| 7902 | FORD | 4 |
| 7934 | MILLER | 6 |

---

## Summary

| Query # | Type | Function(s) Used | Results |
|---------|------|-----------------|---------|
| 1 | COUNT | COUNT(*) | 14 total employees |
| 2 | SUM | SUM(SAL) | 29025 total salary |
| 3 | MAX | MAX(SAL) | 5000 maximum |
| 4 | MIN | MIN(SAL) | 800 minimum |
| 5 | AVG | AVG(SAL) | 2073.21 average |
| 6 | MAX + WHERE | MAX with JOB filter | 1100 (Clerk) |
| 7 | MAX + WHERE | MAX with DEPTNO filter | 5000 (Dept 20) |
| 8 | MIN + WHERE | MIN with JOB filter | 1250 (Salesman) |
| 9 | AVG + WHERE | AVG with JOB filter | 2758.33 (Managers) |
| 10 | SUM + WHERE | SUM with JOB & DEPTNO | 3000 (Analysts in Dept 40) |
| 11 | String Case | UPPER() | All names uppercase |
| 12 | String Case | LOWER() | All names lowercase |
| 13 | String Case | INITCAP() + LOWER() | All names proper case |
| 14 | LENGTH | LENGTH function | 10 characters |
| 15 | LENGTH | LENGTH for all names | 4-6 characters range |

