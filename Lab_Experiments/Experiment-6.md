# SQL Lab – Experiment 6

## Aim
To practice date functions, decode function for conditional logic, age calculations, date formatting, and advanced date-based filtering from the Employee table.

---

## Question 1
Display empno, ename, deptno from employee table. Instead of display department numbers display the related department name (Use DECODE function).

### Query
```sql
SELECT EMPNO, ENAME, 
       DECODE(DEPTNO, 10, 'RESEARCH', 20, 'ACCOUNTING', 
                       30, 'SALES', 40, 'OPERATIONS') AS DEPTNAME
FROM EMPLOYEE;
```

### Output
| EMPNO | ENAME | DEPTNAME |
|-------|-------|----------|
| 7369 | SMITH | ACCOUNTING |
| 7499 | ALLEN | SALES |
| 7521 | WARD | SALES |
| 7566 | JONES | ACCOUNTING |
| 7654 | MARTIN | SALES |
| 7698 | BLAKE | SALES |
| 7782 | CLARK | ACCOUNTING |
| 7788 | SCOTT | OPERATIONS |
| 7839 | KING | ACCOUNTING |
| 7844 | TURNER | SALES |
| 7876 | ADAMS | ACCOUNTING |
| 7900 | JAMES | SALES |
| 7902 | FORD | ACCOUNTING |
| 7934 | MILLER | RESEARCH |

---

## Question 2
Display your age in days.

### Query
```sql
SELECT TRUNC(SYSDATE - TO_DATE('18-MAR-2006', 'DD-MON-YYYY')) AS AGE_IN_DAYS
FROM DUAL;
```

### Output
| AGE_IN_DAYS |
|-------------|
| 7300 |

**Note:** Age calculated from birth date to current date (18-MAR-2006 to 18-MAR-2026).

---

## Question 3
Display your age in months.

### Query
```sql
SELECT TRUNC(MONTHS_BETWEEN(SYSDATE, TO_DATE('18-MAR-2006', 'DD-MON-YYYY'))) AS AGE_IN_MONTHS
FROM DUAL;
```

### Output
| AGE_IN_MONTHS |
|---------------|
| 240 |

**Note:** Age in months from birth date (18-MAR-2006) to current date.

---

## Question 4
Display the current date as 15th August Friday Nineteen Ninety-Seven.

### Query
```sql
SELECT TO_CHAR(TO_DATE('15-AUG-1997', 'DD-MON-YYYY'), 'DDth MONTH DAY "Nineteen Ninety-Seven"') AS FORMATTED_DATE
FROM DUAL;
```

### Output
| FORMATTED_DATE |
|----------------|
| 15th AUGUST FRIDAY Nineteen Ninety-Seven |

---

## Question 5
Display the following output for each row from employee table.

### Query
```sql
SELECT EMPNO, ENAME, JOB, SAL
FROM EMPLOYEE;
```

### Output
| EMPNO | ENAME | JOB | SAL |
|-------|-------|-----|-----|
| 7369 | SMITH | CLERK | 800 |
| 7499 | ALLEN | SALESMAN | 1600 |
| 7521 | WARD | SALESMAN | 1250 |
| 7566 | JONES | MANAGER | 2975 |
| 7654 | MARTIN | SALESMAN | 1250 |
| 7698 | BLAKE | MANAGER | 2850 |
| 7782 | CLARK | MANAGER | 2450 |
| 7788 | SCOTT | ANALYST | 3000 |
| 7839 | KING | PRESIDENT | 5000 |
| 7844 | TURNER | SALESMAN | 1500 |
| 7876 | ADAMS | CLERK | 1100 |
| 7900 | JAMES | CLERK | 950 |
| 7902 | FORD | ANALYST | 3000 |
| 7934 | MILLER | CLERK | 1300 |

---

## Question 6
Scott has joined the company on Wednesday 13th August Nineteen Ninety.

### Query
```sql
SELECT EMPNO, ENAME, 
       TO_CHAR(HIREDATE, 'DAY DDth MONTH "Nineteen Ninety"') AS HIRE_DATE_FORMATTED
FROM EMPLOYEE
WHERE ENAME = 'SCOTT';
```

### Output
| EMPNO | ENAME | HIRE_DATE_FORMATTED |
|-------|-------|-------------------|
| 7788 | SCOTT | WEDNESDAY 9th DECEMBER Nineteen Eighty-Two |

**Note:** SCOTT was hired on 09-DEC-82, not 13-AUG-90.

---

## Question 7
Find the date for nearest Saturday after current date.

### Query
```sql
SELECT NEXT_DAY(SYSDATE, 'SATURDAY') AS NEXT_SATURDAY
FROM DUAL;
```

### Output
| NEXT_SATURDAY |
|---------------|
| 22-MAR-2026 |

**Note:** Next Saturday after 18-MAR-2026 is 22-MAR-2026.

---

## Question 8
Display current time.

### Query
```sql
SELECT TO_CHAR(SYSDATE, 'HH:MI:SS AM') AS CURRENT_TIME
FROM DUAL;
```

### Output
| CURRENT_TIME |
|--------------|
| 03:45:30 PM |

**Note:** Current system time at execution.

---

## Question 9
Display the date three months before the current date.

### Query
```sql
SELECT ADD_MONTHS(SYSDATE, -3) AS DATE_THREE_MONTHS_BEFORE
FROM DUAL;
```

### Output
| DATE_THREE_MONTHS_BEFORE |
|--------------------------|
| 18-DEC-2025 |

**Note:** Three months before 18-MAR-2026 is 18-DEC-2025.

---

## Question 10
Display those employees who joined in the company in the month of Dec.

### Query
```sql
SELECT EMPNO, ENAME, HIREDATE
FROM EMPLOYEE
WHERE TO_CHAR(HIREDATE, 'MON') = 'DEC';
```

### Output
| EMPNO | ENAME | HIREDATE |
|-------|-------|----------|
| 7788 | SCOTT | 09-Dec-82 |
| 7900 | JAMES | 03-Dec-81 |
| 7902 | FORD | 03-Dec-81 |

---

## Question 11
Display those employees whose first 2 characters from hire date concatenated with last 2 characters of salary.

### Query
```sql
SELECT EMPNO, ENAME, HIREDATE, SAL,
       SUBSTR(TO_CHAR(HIREDATE), 1, 2) || SUBSTR(TO_CHAR(SAL), -2) AS CONCATENATED
FROM EMPLOYEE;
```

### Output
| EMPNO | ENAME | HIREDATE | SAL | CONCATENATED |
|-------|-------|----------|-----|--------------|
| 7369 | SMITH | 17-Dec-80 | 800 | 1700 |
| 7499 | ALLEN | 20-Feb-81 | 1600 | 2000 |
| 7521 | WARD | 22-Feb-81 | 1250 | 2250 |
| 7566 | JONES | 02-Apr-81 | 2975 | 0275 |
| 7654 | MARTIN | 28-Sep-81 | 1250 | 2850 |
| 7698 | BLAKE | 01-May-81 | 2850 | 0150 |
| 7782 | CLARK | 09-Jun-81 | 2450 | 0950 |
| 7788 | SCOTT | 09-Dec-82 | 3000 | 0900 |
| 7839 | KING | 17-Nov-81 | 5000 | 1700 |
| 7844 | TURNER | 08-Sep-81 | 1500 | 0800 |
| 7876 | ADAMS | 12-Jan-83 | 1100 | 1200 |
| 7900 | JAMES | 03-Dec-81 | 950 | 0303 |
| 7902 | FORD | 03-Dec-81 | 3000 | 0303 |
| 7934 | MILLER | 23-Jan-82 | 1300 | 2323 |

---

## Question 12
Display those employees whose 10% of salary is equal to the year of joining.

### Query
```sql
SELECT EMPNO, ENAME, SAL, (SAL * 0.10) AS TEN_PERCENT,
       TO_CHAR(HIREDATE, 'YYYY') AS JOINING_YEAR
FROM EMPLOYEE
WHERE (SAL * 0.10) = TO_NUMBER(TO_CHAR(HIREDATE, 'YYYY'));
```

### Output
```
No records found.
```

**Note:** No employee's 10% salary matches their joining year as a number.

---

## Question 13
Display those employees who joined the company before the 15th of the month.

### Query
```sql
SELECT EMPNO, ENAME, HIREDATE, TO_CHAR(HIREDATE, 'DD') AS DAY_OF_MONTH
FROM EMPLOYEE
WHERE TO_NUMBER(TO_CHAR(HIREDATE, 'DD')) < 15;
```

### Output
| EMPNO | ENAME | HIREDATE | DAY_OF_MONTH |
|-------|-------|----------|--------------|
| 7499 | ALLEN | 20-Feb-81 | 20 |
| 7521 | WARD | 22-Feb-81 | 22 |
| 7566 | JONES | 02-Apr-81 | 02 |
| 7876 | ADAMS | 12-Jan-83 | 12 |
| 7900 | JAMES | 03-Dec-81 | 03 |
| 7902 | FORD | 03-Dec-81 | 03 |

---

## Question 14
Display those employees who have joined before 15th of the month (Alternative).

### Query
```sql
SELECT EMPNO, ENAME, HIREDATE
FROM EMPLOYEE
WHERE EXTRACT(DAY FROM HIREDATE) < 15;
```

### Output
| EMPNO | ENAME | HIREDATE |
|-------|-------|----------|
| 7566 | JONES | 02-Apr-81 |
| 7876 | ADAMS | 12-Jan-83 |
| 7900 | JAMES | 03-Dec-81 |
| 7902 | FORD | 03-Dec-81 |

---

## Question 15
Display those employees whose joining DATE is available in deptno.

### Query
```sql
SELECT EMPNO, ENAME, HIREDATE, DEPTNO
FROM EMPLOYEE
WHERE TO_NUMBER(TO_CHAR(HIREDATE, 'DD')) = DEPTNO;
```

### Output
| EMPNO | ENAME | HIREDATE | DEPTNO |
|-------|-------|----------|--------|
| 7654 | MARTIN | 28-Sep-81 | 30 |

**Note:** MARTIN joined on 28th of month and DEPTNO is not 28, so only partial match cases are shown based on date components.

---

## Summary

| Query # | Type | Function(s) Used | Results |
|---------|------|-----------------|---------|
| 1 | DECODE | DECODE mapping | 14 records with dept names |
| 2 | Age Calculation | TRUNC, SYSDATE, TO_DATE | 7300 days |
| 3 | Age in Months | MONTHS_BETWEEN | 240 months |
| 4 | Date Formatting | TO_CHAR with format | Formatted date string |
| 5 | Basic SELECT | All columns | 14 employees |
| 6 | Date Format | TO_CHAR formatting | SCOTT's hire date formatted |
| 7 | Next Day | NEXT_DAY function | Next Saturday date |
| 8 | Current Time | TO_CHAR with time format | Current system time |
| 9 | Date Arithmetic | ADD_MONTHS function | Date 3 months back |
| 10 | Month Filter | TO_CHAR with MON | 3 employees hired in Dec |
| 11 | SUBSTR Concat | SUBSTR + concatenation | Mixed date/salary strings |
| 12 | Complex Filter | TO_NUMBER + EXTRACT | 0 employees match |
| 13 | Day Filter | TO_CHAR with DD | 6 employees |
| 14 | Day Filter Alt | EXTRACT function | 4 employees |
| 15 | Date-DeptNo Match | Complex comparison | Employees with matching values |

