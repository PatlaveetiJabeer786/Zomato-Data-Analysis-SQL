# 🍴 Zomato Data Analysis (SQL Case Study)

## 📌 Project Overview
This project involves a deep-dive analysis of Zomato's customer behavior and sales data. Using advanced SQL techniques, I answered 12 critical business questions to derive insights into customer loyalty, product performance, and membership impact.

## 🛠️ Database Schema
The analysis is performed across four primary tables:
* **Gold Users:** Membership signup details.
* **Users:** General user signup dates.
* **Sales:** Transactional data including purchase dates and product IDs.
* **Product:** Menu details with pricing.

---

## 🔍 Business Questions Answered

### **Phase 1: Sales & Customer Behavior**
1. **Total Spending:** What is the total amount each customer spent on Zomato?
2. **Visit Frequency:** How many days has each customer visited Zomato?
3. **First Purchase:** What was the first product purchased by each customer?
4. **Popularity:** What is the most purchased item on the menu and how many times was it purchased by all customers?
5. **Customer Favorites:** Which item was the most popular for each individual customer?

### **Phase 2: Gold Membership Insights**
6. **Member Onboarding:** Which item was purchased by the customer immediately after they became a Gold member?
7. **Pre-Member Behavior:** Which item was purchased by the customer just before they became a member?
8. **Pre-Member Totals:** What were the total orders and amount spent for each member before they joined the Gold program?
9. **Loyalty Points System:** * Calculate points collected by each customer based on product-specific rules (e.g., P1: 5rs = 1pt, P2: 10rs = 5pts).
    * Which product has generated the most points so far?
10. **Bonus Period Analysis:** In the first year of Gold membership, users earn 5 points for every 10rs spent. Who earned the most during this "bonus" year?

### **Phase 3: Transactional Ranking**
11. **Standard Ranking:** Rank all transactions for every customer based on date.
12. **Member-Only Ranking:** Rank transactions for Gold members specifically, while marking non-member transactions as 'NA'.

---

## 🚀 Technical Skills Demonstrated
* **Joins:** Inner and Left Joins to connect sales with user and product data.
* **Window Functions:** `RANK()` and `DENSE_RANK()` for transaction sequencing.
* **Aggregations:** `SUM()`, `COUNT()`, and `GROUP BY` for financial reporting.
* **Conditional Logic:** `CASE WHEN` statements for custom loyalty point calculations.
* **CTEs & Subqueries:** Organizing complex multi-step queries for better readability.
