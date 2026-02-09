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
Part 1: Basic & Intermediate Queries
Total Spending: What is the total amount each customer has spent on Zomato?

Visit Frequency: How many distinct days has each customer visited the platform?

First Purchase: What was the very first product purchased by each customer?

Most Popular Menu Item: What is the most purchased item on the entire menu, and how many times was it bought by all customers?

Customer Preference: Which specific item was the most popular for each individual customer?

Part 2: Advanced Member Analysis
Post-Membership Activity: Which item was the first one purchased by a customer after they became a Gold member?

Pre-Membership Activity: Which item was the last one purchased by a customer just before they became a Gold member?

Pre-Membership Totals: What were the total orders and total amount spent for each member before they joined the Gold program?

Reward Points System: * Calculate the total points collected by each customer based on specific product rules (e.g., P1: 5rs = 1pt, P2: 10rs = 5pts, P3: 5rs = 1pt).

Identify which specific product has yielded the most total points so far.

First-Year Gold Bonus: In their first year after joining Gold, members earn 5 points for every 10rs spent. Who earned the most in their first year, and what was that total?

Transaction Ranking: Rank all transactions for every customer based on their purchase date.

Member Transaction Logic: Rank all transactions for each member, but for any transactions made by non-gold members (or before gold signup), mark the rank as "NA."
