# SQL Lab – Experiment 0

## Aim
To understand the database schema, table structures, and sample data used in all SQL lab experiments. This serves as the foundation for all subsequent experiments.

---

## Table 1: EMPLOYEE

### Table Structure (Schema)
```sql
CREATE TABLE EMPLOYEE (
    EMPNO    NUMBER(4)      PRIMARY KEY,
    ENAME    VARCHAR2(20)   NOT NULL,
    JOB      VARCHAR2(20),
    MGR      NUMBER(4),
    HIREDATE DATE,
    SAL      NUMBER(10),
    COMM     NUMBER(7),
    DEPTNO   NUMBER(2)      FOREIGN KEY REFERENCES DEPARTMENT(DEPTNO)
);
```

### Column Description

| Column Name | Data Type | Size | Constraints | Description |
|------------|-----------|------|-------------|-------------|
| EMPNO | NUMBER | 4 | PRIMARY KEY | Employee Number (Unique ID) |
| ENAME | VARCHAR2 | 20 | NOT NULL | Employee Name |
| JOB | VARCHAR2 | 20 | - | Job Title/Designation |
| MGR | NUMBER | 4 | - | Manager Employee Number |
| HIREDATE | DATE | - | - | Date of Hiring |
| SAL | NUMBER | 10 | - | Monthly Salary |
| COMM | NUMBER | 7 | - | Commission Amount |
| DEPTNO | NUMBER | 2 | FOREIGN KEY | Department Number |

### Sample Data Insertion

```sql
INSERT INTO EMPLOYEE VALUES (7369, 'SMITH', 'CLERK', 7902, '17-DEC-80', 800, NULL, 20);
INSERT INTO EMPLOYEE VALUES (7499, 'ALLEN', 'SALESMAN', 7698, '20-FEB-81', 1600, 300, 30);
INSERT INTO EMPLOYEE VALUES (7521, 'WARD', 'SALESMAN', 7698, '22-FEB-81', 1250, 300, 30);
INSERT INTO EMPLOYEE VALUES (7566, 'JONES', 'MANAGER', 7839, '02-APR-81', 2975, NULL, 20);
INSERT INTO EMPLOYEE VALUES (7654, 'MARTIN', 'SALESMAN', 7698, '28-SEP-81', 1250, 1400, 30);
INSERT INTO EMPLOYEE VALUES (7698, 'BLAKE', 'MANAGER', 7839, '01-MAY-81', 2850, NULL, 30);
INSERT INTO EMPLOYEE VALUES (7782, 'CLARK', 'MANAGER', 7839, '09-JUN-81', 2450, NULL, 20);
INSERT INTO EMPLOYEE VALUES (7788, 'SCOTT', 'ANALYST', 7566, '09-DEC-82', 3000, NULL, 40);
INSERT INTO EMPLOYEE VALUES (7839, 'KING', 'PRESIDENT', NULL, '17-NOV-81', 5000, NULL, 20);
INSERT INTO EMPLOYEE VALUES (7844, 'TURNER', 'SALESMAN', 7698, '08-SEP-81', 1500, 0, 30);
INSERT INTO EMPLOYEE VALUES (7876, 'ADAMS', 'CLERK', 7788, '12-JAN-83', 1100, NULL, 20);
INSERT INTO EMPLOYEE VALUES (7900, 'JAMES', 'CLERK', 7698, '03-DEC-81', 950, NULL, 30);
INSERT INTO EMPLOYEE VALUES (7902, 'FORD', 'ANALYST', 7566, '03-DEC-81', 3000, NULL, 20);
INSERT INTO EMPLOYEE VALUES (7934, 'MILLER', 'CLERK', 7782, '23-JAN-82', 1300, NULL, 10);
```

### Employee Table Data

| EMPNO | ENAME | JOB | MGR | HIREDATE | SAL | COMM | DEPTNO |
|-------|-------|-----|-----|----------|-----|------|--------|
| 7369 | SMITH | CLERK | 7902 | 17-Dec-80 | 800 | - | 20 |
| 7499 | ALLEN | SALESMAN | 7698 | 20-Feb-81 | 1600 | 300 | 30 |
| 7521 | WARD | SALESMAN | 7698 | 22-Feb-81 | 1250 | 300 | 30 |
| 7566 | JONES | MANAGER | 7839 | 02-Apr-81 | 2975 | - | 20 |
| 7654 | MARTIN | SALESMAN | 7698 | 28-Sep-81 | 1250 | 1400 | 30 |
| 7698 | BLAKE | MANAGER | 7839 | 01-May-81 | 2850 | - | 30 |
| 7782 | CLARK | MANAGER | 7839 | 09-Jun-81 | 2450 | - | 20 |
| 7788 | SCOTT | ANALYST | 7566 | 09-Dec-82 | 3000 | - | 40 |
| 7839 | KING | PRESIDENT | - | 17-Nov-81 | 5000 | - | 20 |
| 7844 | TURNER | SALESMAN | 7698 | 08-Sep-81 | 1500 | 0 | 30 |
| 7876 | ADAMS | CLERK | 7788 | 12-Jan-83 | 1100 | - | 20 |
| 7900 | JAMES | CLERK | 7698 | 03-Dec-81 | 950 | - | 30 |
| 7902 | FORD | ANALYST | 7566 | 03-Dec-81 | 3000 | - | 20 |
| 7934 | MILLER | CLERK | 7782 | 23-Jan-82 | 1300 | - | 10 |

---

## Table 2: DEPARTMENT

### Table Structure (Schema)
```sql
CREATE TABLE DEPARTMENT (
    DEPTNO   NUMBER(2)      PRIMARY KEY,
    DNAME    VARCHAR2(15)   NOT NULL
);
```

### Column Description

| Column Name | Data Type | Size | Constraints | Description |
|------------|-----------|------|-------------|-------------|
| DEPTNO | NUMBER | 2 | PRIMARY KEY | Department Number (Unique ID) |
| DNAME | VARCHAR2 | 15 | NOT NULL | Department Name |

### Sample Data Insertion

```sql
INSERT INTO DEPARTMENT VALUES (10, 'RESEARCH');
INSERT INTO DEPARTMENT VALUES (20, 'ACCOUNTING');
INSERT INTO DEPARTMENT VALUES (30, 'SALES');
INSERT INTO DEPARTMENT VALUES (40, 'OPERATIONS');
```

### Department Table Data

| DEPTNO | DNAME |
|--------|-------|
| 10 | RESEARCH |
| 20 | ACCOUNTING |
| 30 | SALES |
| 40 | OPERATIONS |

---

## Key Relationships

### Primary Key - Foreign Key Relationship
- **EMPLOYEE.DEPTNO** → **DEPARTMENT.DEPTNO** (Foreign Key)
- **EMPLOYEE.MGR** → **EMPLOYEE.EMPNO** (Self-referencing Foreign Key)

### Hierarchy
- KING (EMPNO 7839) is the PRESIDENT with no manager (MGR = NULL)
- JONES, BLAKE, CLARK report to KING
- SCOTT and FORD report to JONES
- SMITH and ADAMS report to FORD/SCOTT
- Other employees report to BLAKE

---

## Statistics

### Employee Statistics

| Metric | Value |
|--------|-------|
| Total Employees | 14 |
| Total Salary Paid | 29,025 |
| Average Salary | 2,073.21 |
| Highest Salary | 5,000 (KING) |
| Lowest Salary | 800 (SMITH) |

### Department Statistics

| Department | DEPTNO | Employees | Avg Salary |
|------------|--------|-----------|-----------|
| RESEARCH | 10 | 1 | 1,300 |
| ACCOUNTING | 20 | 5 | 2,685 |
| SALES | 30 | 6 | 1,483.33 |
| OPERATIONS | 40 | 1 | 3,000 |

### Job Distribution

| Job | Count | Avg Salary |
|-----|-------|-----------|
| CLERK | 4 | 1,087.50 |
| SALESMAN | 4 | 1,400 |
| MANAGER | 3 | 2,758.33 |
| ANALYST | 2 | 3,000 |
| PRESIDENT | 1 | 5,000 |

---

## Setup Instructions

### Step 1: Create DEPARTMENT table first (No dependencies)
```sql
CREATE TABLE DEPARTMENT (
    DEPTNO   NUMBER(2)      PRIMARY KEY,
    DNAME    VARCHAR2(15)   NOT NULL
);
```

### Step 2: Insert Department Data
```sql
INSERT INTO DEPARTMENT VALUES (10, 'RESEARCH');
INSERT INTO DEPARTMENT VALUES (20, 'ACCOUNTING');
INSERT INTO DEPARTMENT VALUES (30, 'SALES');
INSERT INTO DEPARTMENT VALUES (40, 'OPERATIONS');
COMMIT;
```

### Step 3: Create EMPLOYEE table (After DEPARTMENT)
```sql
CREATE TABLE EMPLOYEE (
    EMPNO    NUMBER(4)      PRIMARY KEY,
    ENAME    VARCHAR2(20)   NOT NULL,
    JOB      VARCHAR2(20),
    MGR      NUMBER(4),
    HIREDATE DATE,
    SAL      NUMBER(10),
    COMM     NUMBER(7),
    DEPTNO   NUMBER(2)      FOREIGN KEY REFERENCES DEPARTMENT(DEPTNO)
);
```

### Step 4: Insert Employee Data
Insert all 14 employee records using the INSERT statements provided above.

```sql
COMMIT;
```

### Step 5: Verify Data
```sql
SELECT COUNT(*) FROM EMPLOYEE;
SELECT COUNT(*) FROM DEPARTMENT;
```

---

## Important Notes

1. **NULL Values**: Some columns contain NULL values which indicate:
   - **NULL in MGR**: Employee is at the top of hierarchy (KING)
   - **NULL in COMM**: Employee does not earn commission (non-sales staff)

2. **Commission**: Only SALESMAN earn commission:
   - ALLEN: 300
   - WARD: 300
   - MARTIN: 1400
   - TURNER: 0 (No commission earned)

3. **Hire Dates**: Range from 17-NOV-80 to 12-JAN-83

4. **Salary Range**: 800 to 5000 per month

5. **Manager Structure**: 
   - KING reports to no one (NULL MGR)
   - 3 Managers (JONES, BLAKE, CLARK) report to KING
   - Other employees report to various managers

---

## Quick Reference Queries

### View all employees with their department names
```sql
SELECT e.EMPNO, e.ENAME, e.JOB, d.DNAME, e.SAL
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
ORDER BY d.DNAME, e.ENAME;
```

### View employee hierarchy
```sql
SELECT e.ENAME, e.JOB, m.ENAME as MANAGER_NAME
FROM EMPLOYEE e
LEFT JOIN EMPLOYEE m ON e.MGR = m.EMPNO
ORDER BY e.ENAME;
```

### View salary summary by department
```sql
SELECT d.DNAME, COUNT(e.EMPNO) as COUNT, 
       AVG(e.SAL) as AVG_SAL, MAX(e.SAL) as MAX_SAL
FROM EMPLOYEE e
JOIN DEPARTMENT d ON e.DEPTNO = d.DEPTNO
GROUP BY d.DNAME
ORDER BY d.DNAME;
```

---

## Summary

**Experiment-0** provides:
- ✓ Complete table schemas (CREATE TABLE)
- ✓ Data dictionary with column descriptions
- ✓ 14 employee records across 4 departments
- ✓ Statistical summaries
- ✓ Setup instructions for database initialization
- ✓ Quick reference queries for common operations

This foundation is essential for all 6 experiments that follow.

