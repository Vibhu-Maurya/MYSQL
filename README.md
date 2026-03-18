# SQL Lab Experiments

A comprehensive collection of SQL laboratory experiments demonstrating various database concepts and query techniques using Oracle SQL.

## 📋 Overview

This repository contains 7 SQL experiments that cover fundamental to advanced SQL concepts:

- **Experiment-0**: Database Schema & Sample Data (Foundation)
- **Experiment-1**: DDL & DML Operations (CREATE, DELETE, UPDATE, ALTER, DROP)
- **Experiment-2**: Data Retrieval (DISTINCT, WHERE, IN, LIKE)
- **Experiment-3**: Advanced Queries (ORDER BY, Calculations, Multiple Conditions)
- **Experiment-4**: Date Queries, Salary Calculations & Updates
- **Experiment-5**: Aggregate & String Functions (COUNT, SUM, AVG, UPPER, LOWER, LENGTH)
- **Experiment-6**: Date Functions & DECODE (NEXT_DAY, MONTHS_BETWEEN, EXTRACT)

## 🗂️ Database Schema

### EMPLOYEE Table
- **EMPNO**: Employee Number (Primary Key)
- **ENAME**: Employee Name
- **JOB**: Job Title
- **MGR**: Manager Employee Number
- **HIREDATE**: Date of Joining
- **SAL**: Monthly Salary
- **COMM**: Commission Amount
- **DEPTNO**: Department Number (Foreign Key)

### DEPARTMENT Table
- **DEPTNO**: Department Number (Primary Key)
- **DNAME**: Department Name

## 📊 Sample Data

- **14 Employees** across 4 departments
- **Salary Range**: ₹800 - ₹5,000 per month
- **Departments**: RESEARCH, ACCOUNTING, SALES, OPERATIONS
- **Jobs**: CLERK, SALESMAN, MANAGER, ANALYST, PRESIDENT

## 🛠️ Technologies Used

- **Database**: Oracle SQL
- **Documentation**: Markdown (.md files)
- **Version Control**: Git & GitHub

## 📈 Key Concepts Covered

### DDL (Data Definition Language)
- CREATE TABLE
- ALTER TABLE
- DROP TABLE

### DML (Data Manipulation Language)
- INSERT
- UPDATE
- DELETE

### DQL (Data Query Language)
- SELECT statements
- WHERE clauses
- JOIN operations
- Subqueries

### Functions & Operators
- **Aggregate Functions**: COUNT, SUM, MAX, MIN, AVG
- **String Functions**: UPPER, LOWER, INITCAP, LENGTH, SUBSTR
- **Date Functions**: SYSDATE, TO_DATE, TO_CHAR, MONTHS_BETWEEN, NEXT_DAY, ADD_MONTHS, EXTRACT
- **Conditional Logic**: DECODE, CASE
- **Mathematical Operators**: Arithmetic calculations

### Advanced Concepts
- Pattern matching with LIKE
- Date arithmetic and formatting
- Salary calculations with allowances (HRA, DA, PF)
- Complex filtering conditions
- Data type conversions

## 📁 Repository Structure

```
SQL-Lab/
├── Experiment-0.md    # Database schema & sample data
├── Experiment-1.md    # DDL & DML operations
├── Experiment-2.md    # Basic data retrieval
├── Experiment-3.md    # Advanced SELECT queries
├── Experiment-4.md    # Date functions & updates
├── Experiment-5.md    # Aggregate & string functions
├── Experiment-6.md    # Complex date operations
└── README.md         # This file
```

## 🚀 Getting Started

### Prerequisites
- Oracle Database or compatible SQL environment
- Git for version control
- Text editor (VS Code recommended)

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/lab_experiments.git
   cd lab_experiments
   ```

2. **Create Database Tables**
   - Refer to Experiment-0.md for complete table creation scripts
   - Execute the CREATE TABLE statements in order
   - Insert sample data using provided INSERT statements

3. **Run Experiments**
   - Open each Experiment-X.md file
   - Execute queries in your SQL environment
   - Compare results with expected outputs

## 📊 Statistics

| Metric | Value |
|--------|-------|
| Total Experiments | 7 |
| SQL Queries | 85+ |
| Concepts Covered | 50+ |
| Tables Used | 2 |
| Sample Records | 18 |

## 🎯 Learning Outcomes

By completing these experiments, you will be able to:

- ✅ Design and implement database schemas
- ✅ Perform CRUD operations effectively
- ✅ Write complex SELECT queries with multiple conditions
- ✅ Use aggregate functions for data analysis
- ✅ Manipulate dates and strings in SQL
- ✅ Apply conditional logic in queries
- ✅ Format and present query results professionally

## 📝 Documentation Standards

All experiments follow consistent formatting:
- **SQL Code Blocks**: Properly formatted with syntax highlighting
- **Expected Outputs**: Tables showing query results
- **Explanations**: Clear descriptions of each query's purpose
- **Notes**: Additional insights and observations

## 🤝 Contributing

This is an educational repository. Feel free to:
- Report issues with queries or outputs
- Suggest improvements to documentation
- Add additional experiments
- Share alternative solutions

## 📄 License

This project is for educational purposes. Feel free to use and modify the content for learning SQL.

## 👨‍💻 Author

**Vibhu-Kavi**
- Academic Year: 2025-2026
- Course: Database Management Systems (DBMS)
- Institution: [Your Institution Name]

---

*Happy Learning! 🎓*

*Remember: Practice makes perfect. Execute each query, understand the logic, and experiment with variations.*
