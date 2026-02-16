# Retail Sales Analysis Using SQL

## 📌 Project Overview

**Project Name**: Retail Sales Analysis Using SQL  
**Difficulty Level**: Beginner  
**Database Name**: `sql_project_p2`

This project demonstrates how SQL can be used to analyze retail sales data effectively. It focuses on database creation, data cleaning, exploratory data analysis (EDA), and answering business-oriented questions using SQL queries. The project is ideal for beginners aiming to strengthen their SQL fundamentals through hands-on practice.

---

## 🎯 Project Objectives

- Build and structure a retail sales database  
- Clean and validate raw transactional data  
- Perform exploratory data analysis using SQL  
- Extract meaningful business insights from sales data  

---

## 🗂 Project Structure

### 1️⃣ Database Setup

- A database named **`sql_project_p2`** is created.
- A table **`retail_sales`** is designed to store transaction-level information such as customer details, product category, quantity sold, pricing, and sales value.

```sql
CREATE DATABASE sql_project_p2;

CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

---

### 2️⃣ Data Exploration & Cleaning

```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;
```

---

## 📊 SQL Analysis & Queries

(Queries included in project)

---

## ✅ Conclusion

This project offers a complete beginner-level SQL analytics workflow, covering database design, data cleaning, exploratory analysis, and business-focused querying.
