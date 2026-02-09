# Zomato-Data-Analysis-SQL
SQL-based analysis of Zomato data focusing on customer behavior, sales performance, and restaurant trends using advanced Joins and Subqueries.

# 🍴 Zomato Data Analysis (SQL)

## 📌 Project Objective
To extract meaningful insights from Zomato's restaurant and delivery data to understand customer ordering habits and business growth.

## 🛠️ SQL Techniques Used
* **Joins:** Combining customer, orders, and restaurant tables.
* **Window Functions:** Calculating running totals and customer ranking.
* **Aggregations:** Analyzing average order value and total revenue.
* **CTEs & Subqueries:** Organizing complex logic for multi-step analysis.

## 🔍 Key Business Questions Answered
1. What is the total amount each customer spent on Zomato?
2. How many days has each customer visited the platform?
3. What was the first product purchased by each customer?
4. What is the most purchased item on the menu?

## 📊 Sample Query Preview
```sql
-- Example: Finding total sales per customer
SELECT userid, SUM(price) as total_spent
FROM sales s
JOIN product p ON s.product_id = p.product_id
GROUP BY userid;
