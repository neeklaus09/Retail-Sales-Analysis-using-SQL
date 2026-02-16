# Retail Sales Analysis Using SQL

## 📌 Project Overview

**Project Name**: Retail Sales Analysis Using SQL  
**Level**: Beginner  
**Database Name**: `sql_project_p2`

This project demonstrates the use of SQL to perform end-to-end analysis on retail sales data. It includes database creation, data cleaning, exploratory data analysis (EDA), and solving real-world business problems using SQL queries. The project is designed for beginners who want practical exposure to SQL in data analytics.

---

## 🎯 Objectives

- Create and structure a retail sales database  
- Clean the dataset by identifying and removing null values  
- Perform exploratory data analysis using SQL  
- Answer business-driven questions using SQL queries  

---

## 🗂 Project Structure

### 1️⃣ Database Setup

The database **`sql_project_p2`** is created along with a table **`retail_sales`** to store transaction-level data.

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

Basic checks are performed to understand the dataset and remove incomplete records.

```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

SELECT *
FROM retail_sales
WHERE sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL
   OR gender IS NULL OR age IS NULL OR category IS NULL
   OR quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

DELETE
FROM retail_sales
WHERE sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL
   OR gender IS NULL OR age IS NULL OR category IS NULL
   OR quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```

---

## 📊 Business Questions Solved Using SQL

### 1. Retrieve all sales made on a specific date
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```

---

### 2. Transactions for Clothing category with quantity ≥ 4 in Nov 2022
```sql
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
  AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
  AND quantity >= 4;
```

---

### 3. Total sales and total orders for each category
```sql
SELECT 
    category,
    SUM(total_sale) AS net_sale,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
```

---

### 4. Average age of customers purchasing Beauty products
```sql
SELECT
    ROUND(AVG(age), 2) AS avg_age
FROM retail_sales
WHERE category = 'Beauty';
```

---

### 5. Transactions with total sale value greater than 1000
```sql
SELECT *
FROM retail_sales
WHERE total_sale > 1000;
```

---

### 6. Total transactions by gender for each category
```sql
SELECT
    category,
    gender,
    COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
```

---

### 7. Best selling month (based on average sales) for each year
```sql
SELECT year, month, avg_sale
FROM (
    SELECT
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER (
            PARTITION BY EXTRACT(YEAR FROM sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rank
    FROM retail_sales
    GROUP BY 1, 2
) t
WHERE rank = 1;
```

---

### 8. Top 5 customers based on highest total sales
```sql
SELECT
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```

---

### 9. Number of unique customers per category
```sql
SELECT
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
```

---

### 10. Order distribution by time-based shifts
```sql
WITH sales_shift AS (
    SELECT *,
        CASE
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)
SELECT
    shift,
    COUNT(*) AS total_orders
FROM sales_shift
GROUP BY shift;
```

---

## 🔍 Key Insights

- Customers belong to diverse age groups with varying purchasing behavior  
- Clothing and Beauty categories contribute significantly to total sales  
- Presence of high-value transactions indicates premium buying trends  
- Monthly analysis highlights seasonal demand patterns  
- A small group of customers generates a major portion of revenue  

---

## ✅ Conclusion

This project provides a complete beginner-friendly SQL workflow, covering database creation, data cleaning, exploratory data analysis, and business-oriented querying. It serves as a strong foundation project for aspiring data analysts and can be extended further with advanced SQL techniques.
