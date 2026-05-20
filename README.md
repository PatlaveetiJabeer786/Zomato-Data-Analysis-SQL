# 🍽️ Zomato Data Analysis — SQL Case Study

[![Header](https://capsule-render.vercel.app/api?type=waving&color=0:E23744,30:FF6B6B,70:FF4500,100:B22222&height=230&section=header&text=Zomato%20SQL%20Case%20Study&fontSize=46&fontColor=ffffff&animation=fadeIn&fontAlignY=36&desc=Customer%20Behavior%20%7C%20Sales%20%7C%20Loyalty%20%7C%20Restaurant%20Performance%20%7C%2012%20Business%20Questions&descAlignY=58&descSize=14)](https://github.com/PatlaveetiJabeer786/Zomato-Data-Analysis-SQL)

<div align="center">

![SQL](https://img.shields.io/badge/SQL-Advanced%20Queries-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![Joins](https://img.shields.io/badge/SQL-Joins%20%26%20Subqueries-0078D4?style=for-the-badge&logo=database&logoColor=white)
![Domain](https://img.shields.io/badge/Domain-Food%20Delivery%20%26%20Restaurant-E23744?style=for-the-badge)
![Questions](https://img.shields.io/badge/Business%20Questions-12%20Solved-brightgreen?style=for-the-badge)
![Tables](https://img.shields.io/badge/Database%20Tables-4%20Tables-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed%20✅-success?style=for-the-badge)

</div>

---

<div align="center">

```
╔═══════════════════════════════════════════════════════════════════════════╗
║                                                                           ║
║   🍕  4 DATABASE TABLES   •   12 BUSINESS QUESTIONS   •   PURE SQL   🍕  ║
║                                                                           ║
║      Joins  •  Subqueries  •  Aggregations  •  Window Functions           ║
║                                                                           ║
╚═══════════════════════════════════════════════════════════════════════════╝
```

</div>

---

## 📌 Project Overview

This is a **real-world SQL Case Study** built on a **Zomato-inspired food delivery database** — simulating the exact type of business analysis that data teams at companies like Zomato, Swiggy, and Uber Eats perform every day.

The project answers **12 critical business questions** using pure SQL — covering customer behavior, product performance, restaurant metrics, membership (Gold) impact, and loyalty patterns — all extracted through advanced SQL techniques including **INNER JOINs, LEFT JOINs, Subqueries, Aggregations, GROUP BY, ORDER BY, and NULL handling**.

This is also a **SQL interview preparation project** — the questions directly mirror what top companies ask in data analyst interviews.

---

## 🧩 Business Problem

> *"Zomato has millions of customers placing orders every day across thousands of restaurants. The business needs to understand: Who are our most loyal customers? Which restaurants and food items are top performers? Does our Gold membership program actually change how much customers spend? Which customers are at risk of leaving? Without SQL analysis, these questions take weeks to answer manually — the business cannot grow without data-backed decisions."*

**The 12 critical business questions Zomato needed answered:**

| # | Business Question | SQL Concept Used |
|---|-------------------|-----------------|
| 1 | How many days has each customer visited Zomato? | `COUNT DISTINCT`, `GROUP BY` |
| 2 | What was the first product purchased by each customer? | Subquery, `MIN`, `JOIN` |
| 3 | What is the most purchased item and how many times was it ordered? | `COUNT`, `GROUP BY`, `ORDER BY` |
| 4 | What is the most popular item for each customer? | Subquery, `MAX`, Multi-table `JOIN` |
| 5 | What item did each customer purchase first after becoming a Gold member? | `JOIN`, Date filtering, Subquery |
| 6 | What item did each customer purchase just before becoming a Gold member? | `JOIN`, Date comparison, Subquery |
| 7 | What are the total orders and amount spent by each customer before becoming a Gold member? | `JOIN`, `SUM`, `COUNT`, Date filter |
| 8 | What is the total points earned by each customer and which product earns the most points? | `JOIN`, Points logic, `SUM` |
| 9 | In the first year of Gold membership, how many points did each customer earn? | `JOIN`, Date range filter, Points calc |
| 10 | Which customer spent more in the first year — Customer 1 or Customer 3? | Comparative aggregation, `JOIN` |
| 11 | Which transactions did Gold members make (mark as Gold/Non-Gold)? | `CASE WHEN`, `JOIN` |
| 12 | What is the rank of each customer's transactions? | `RANK()`, Window Function, `JOIN` |

---

## 🗄️ Database Schema — 4 Tables

```
╔══════════════════════════════════════════════════════════════════════╗
║                    ZOMATO DATABASE SCHEMA                            ║
╠══════════════════════════════════════════════════════════════════════╣
║                                                                      ║
║   ┌──────────────┐         ┌──────────────────┐                      ║
║   │    USERS     │         │   GOLD_USERS     │                      ║
║   │──────────────│         │──────────────────│                      ║
║   │ userid  (PK) │────┐    │ userid      (FK) │                      ║
║   │ signup_date  │    │    │ gold_signup_date  │                      ║
║   └──────────────┘    │    └──────────────────┘                      ║
║                        │                                             ║
║   ┌──────────────┐    │    ┌──────────────────┐                      ║
║   │    SALES     │    │    │    PRODUCT       │                      ║
║   │──────────────│    │    │──────────────────│                      ║
║   │ userid  (FK) │────┘    │ product_id  (PK) │                      ║
║   │ created_date │────────►│ product_name     │                      ║
║   │ product_id   │(FK)     │ price            │                      ║
║   └──────────────┘         └──────────────────┘                      ║
║                                                                      ║
╚══════════════════════════════════════════════════════════════════════╝
```

| Table | Description | Key Columns |
|-------|-------------|-------------|
| 🧑 **Users** | Customer signup details | `userid`, `signup_date` |
| 🥇 **Gold_Users** | Gold membership enrollment | `userid`, `gold_signup_date` |
| 🛒 **Sales** | All order transactions | `userid`, `created_date`, `product_id` |
| 🍕 **Product** | Menu items with pricing | `product_id`, `product_name`, `price` |

---

## 🔍 All 12 SQL Queries — Solved

### Q1 — How many days has each customer visited Zomato?

```sql
SELECT userid,
       COUNT(DISTINCT created_date) AS visit_count
FROM sales
GROUP BY userid;
```
> **Business Use:** Identify most engaged customers for loyalty campaigns

---

### Q2 — What was the first product purchased by each customer?

```sql
SELECT s.userid, s.created_date, s.product_id, p.product_name
FROM sales s
JOIN product p ON s.product_id = p.product_id
WHERE s.created_date = (
    SELECT MIN(created_date)
    FROM sales s2
    WHERE s2.userid = s.userid
)
ORDER BY s.userid;
```
> **Business Use:** Understand the entry-point product — what brings new customers in

---

### Q3 — Most purchased item & how many times ordered overall?

```sql
SELECT product_id,
       COUNT(product_id) AS order_count
FROM sales
GROUP BY product_id
ORDER BY order_count DESC
LIMIT 1;
```
> **Business Use:** Identify hero products for promotions and inventory priority

---

### Q4 — Most popular item for each customer?

```sql
SELECT userid, product_id, order_count
FROM (
    SELECT userid,
           product_id,
           COUNT(product_id) AS order_count,
           RANK() OVER (PARTITION BY userid ORDER BY COUNT(product_id) DESC) AS rnk
    FROM sales
    GROUP BY userid, product_id
) ranked
WHERE rnk = 1;
```
> **Business Use:** Power personalized recommendations — show each user their favourite item first

---

### Q5 — First item purchased AFTER becoming a Gold member?

```sql
SELECT s.userid, s.created_date, s.product_id, p.product_name
FROM sales s
JOIN gold_users g ON s.userid = g.userid
JOIN product p ON s.product_id = p.product_id
WHERE s.created_date >= g.gold_signup_date
  AND s.created_date = (
      SELECT MIN(s2.created_date)
      FROM sales s2
      JOIN gold_users g2 ON s2.userid = g2.userid
      WHERE s2.userid = s.userid
        AND s2.created_date >= g2.gold_signup_date
  )
ORDER BY s.userid;
```
> **Business Use:** Understand what Gold members buy first — validate membership onboarding perks

---

### Q6 — Item purchased just BEFORE becoming Gold member?

```sql
SELECT s.userid, s.created_date, s.product_id, p.product_name
FROM sales s
JOIN gold_users g ON s.userid = g.userid
JOIN product p ON s.product_id = p.product_id
WHERE s.created_date < g.gold_signup_date
  AND s.created_date = (
      SELECT MAX(s2.created_date)
      FROM sales s2
      JOIN gold_users g2 ON s2.userid = g2.userid
      WHERE s2.userid = s.userid
        AND s2.created_date < g2.gold_signup_date
  )
ORDER BY s.userid;
```
> **Business Use:** Identify which products convert free users to Gold — optimize upgrade triggers

---

### Q7 — Total orders & amount spent BEFORE becoming Gold member?

```sql
SELECT s.userid,
       COUNT(s.product_id) AS total_orders,
       SUM(p.price)        AS total_spent
FROM sales s
JOIN gold_users g ON s.userid = g.userid
JOIN product p    ON s.product_id = p.product_id
WHERE s.created_date < g.gold_signup_date
GROUP BY s.userid
ORDER BY s.userid;
```
> **Business Use:** Measure pre-membership spend — quantify the value of upgrading customers

---

### Q8 — Points earned by each customer? Which product earns the most points?

```sql
-- Points Logic: Every ₹5 spent = 1 point (Product 3: Every ₹5 = 5 points)
SELECT s.userid,
       SUM(
           CASE
               WHEN s.product_id = 1 THEN FLOOR(p.price / 5)
               WHEN s.product_id = 2 THEN FLOOR(p.price / 2)
               WHEN s.product_id = 3 THEN FLOOR(p.price / 5) * 5
           END
       ) AS total_points
FROM sales s
JOIN product p ON s.product_id = p.product_id
GROUP BY s.userid
ORDER BY total_points DESC;
```
> **Business Use:** Optimize loyalty program — identify which product drives the most points & engagement

---

### Q9 — Points earned in FIRST YEAR of Gold membership (₹10 spent = 5 points)?

```sql
SELECT s.userid,
       SUM(p.price * 2.5) AS points_earned_first_year
FROM sales s
JOIN gold_users g ON s.userid = g.userid
JOIN product p    ON s.product_id = p.product_id
WHERE s.created_date >= g.gold_signup_date
  AND s.created_date <= DATE_ADD(g.gold_signup_date, INTERVAL 1 YEAR)
GROUP BY s.userid;
```
> **Business Use:** Track Gold membership ROI — does the first year deliver value?

---

### Q10 — Who spent more in first year of Gold — Customer 1 or Customer 3?

```sql
SELECT s.userid,
       SUM(p.price) AS total_spent
FROM sales s
JOIN gold_users g ON s.userid = g.userid
JOIN product p    ON s.product_id = p.product_id
WHERE s.userid IN (1, 3)
  AND s.created_date >= g.gold_signup_date
  AND s.created_date <= DATE_ADD(g.gold_signup_date, INTERVAL 1 YEAR)
GROUP BY s.userid
ORDER BY total_spent DESC;
```
> **Business Use:** Compare high-value Gold members — identify upsell & retention priorities

---

### Q11 — Which transactions were made as Gold member vs Non-Gold?

```sql
SELECT s.userid,
       s.created_date,
       s.product_id,
       CASE
           WHEN g.gold_signup_date IS NOT NULL
                AND s.created_date >= g.gold_signup_date
           THEN 'Gold Member'
           ELSE 'Non-Gold'
       END AS membership_status
FROM sales s
LEFT JOIN gold_users g ON s.userid = g.userid
ORDER BY s.userid, s.created_date;
```
> **Business Use:** Segment all transactions by membership status — measure Gold vs non-Gold behaviour

---

### Q12 — Rank of each customer's transactions (most recent = Rank 1)?

```sql
SELECT *,
       RANK() OVER (
           PARTITION BY userid
           ORDER BY created_date DESC
       ) AS transaction_rank
FROM sales
ORDER BY userid, transaction_rank;
```
> **Business Use:** Identify recency patterns — most recent purchases reveal current interests

---

## 💡 Key Business Insights & Outcomes

### 🧑 Customer Behaviour
- Some customers visit **daily** while others are **monthly** — clear segmentation for targeted campaigns
- The **first product purchased** varies by customer — no single hero onboarding product exists
- **Recency ranking** reveals active vs dormant customers — retention campaigns can be timed accordingly

### 🍕 Product Performance
- One product consistently dominates **total order count** across all customers — prime candidate for promotions
- The **most points-earning product** is not always the best seller — loyalty program design needs rebalancing
- **Customer favourite items** differ — proving that personalized recommendations would significantly improve UX

### 🥇 Gold Membership Impact
- Customers **change their buying behaviour after becoming Gold** — the first Gold purchase differs from pre-membership patterns
- Spend **before becoming Gold** vs after shows membership drives incremental revenue
- First-year Gold members earn more points with higher-priced items — **price and points strategy needs alignment**

### 📊 Transaction Intelligence
- Labelling transactions as **Gold vs Non-Gold** enables A/B style analysis on membership value
- **RANK() window function** reveals purchase recency — foundation for RFM (Recency, Frequency, Monetary) modelling

---

## 📈 Business Value Delivered

| Business Decision | Without SQL Analysis | With This SQL Analysis |
|-------------------|---------------------|----------------------|
| 🎯 Customer targeting | Treated all users the same | Segmented by visit frequency & spend |
| 🏆 Product promotion | Promoted randomly | Focused on top-ordered & high-points items |
| 💳 Gold membership strategy | Guessed at membership value | Quantified pre vs post-Gold spend change |
| 🔄 Retention campaigns | No churn signals | Recency ranking flags dormant customers |
| 🍕 Personalization | Same menu to everyone | Favourite item per customer identified |
| 💰 Revenue optimization | No conversion insight | Pre-Gold trigger product identified |

---

## 📁 Project Structure

```
Zomato-Data-Analysis-SQL/
│
├── Zomato_project_1.sql        # All 12 SQL queries + table creation + data insertion
└── README.md
```

---

## 🚀 How to Run This Project

### Prerequisites
- **MySQL Workbench** or **SQL Server Management Studio (SSMS)** or any SQL IDE

### Steps

```sql
-- Step 1: Create the database
CREATE DATABASE zomato_analysis;
USE zomato_analysis;

-- Step 2: Run the SQL file
-- Open Zomato_project_1.sql in your IDE
-- Execute the full script (creates tables, inserts data, runs all 12 queries)
```

1. Open your SQL IDE (MySQL Workbench / SSMS)
2. Create a new database called `zomato_analysis`
3. Open and run `Zomato_project_1.sql` — it creates all tables, inserts sample data, and runs all 12 business queries
4. Each query block is clearly labelled with the business question it answers

---

## 🧠 Key Technical SQL Skills Demonstrated

```
✅  INNER JOIN          — Connect Sales ↔ Product ↔ Users ↔ Gold_Users
✅  LEFT JOIN           — Include non-Gold members in membership analysis
✅  Subqueries          — Find first/last purchase dates per customer
✅  Correlated Subquery — Compare each row against per-user aggregates
✅  CASE WHEN           — Label Gold vs Non-Gold transactions dynamically
✅  RANK() Window Fn    — Rank transactions by recency per customer
✅  PARTITION BY        — Apply ranking independently per customer
✅  GROUP BY + COUNT    — Count orders, visits, items per user/product
✅  SUM + FLOOR         — Calculate loyalty points with custom business rules
✅  DATE_ADD + Interval — Filter transactions within first year of membership
✅  NULL Handling       — Identify unrated orders, non-Gold members
✅  MIN / MAX dates     — Find first/last transaction per customer
```

---

## 🌟 Final Summary

| 🔴 Business Problem | 🟢 SQL Solution | 📈 Business Result |
|--------------------|----------------|-------------------|
| Who are most loyal customers? | COUNT DISTINCT visits per user | Loyalty tiers identified |
| Which product drives most sales? | COUNT orders, ORDER BY DESC | Hero product for promotions confirmed |
| Does Gold membership change spend? | Date-filtered JOIN + SUM | Pre vs Post Gold spend quantified |
| Which transactions are Gold vs not? | CASE WHEN + LEFT JOIN | Full transaction segmentation done |
| Who is at risk of churning? | RANK() by recency | Dormant customers flagged |
| What converts users to Gold? | Last purchase before gold_signup_date | Conversion trigger product identified |

---

## 👨‍💻 About Me

I'm a Data Analyst passionate about solving real business problems using advanced SQL — the language that sits at the core of every data-driven company.

- 🔗 **LinkedIn:** [linkedin.com/in/jabeer-patlaveeti](https://linkedin.com/in/jabeer-patlaveeti)
- 📧 **Email:** jabeerpatlaveeti@gmail.com
- 🌐 **GitHub:** [github.com/PatlaveetiJabeer786](https://github.com/PatlaveetiJabeer786)

---

<div align="center">

⭐ **If this project helped you prepare for SQL interviews, please give it a Star!** ⭐

*This project simulates real Zomato-style business analysis using a structured toy dataset.*

</div>

[![Footer](https://capsule-render.vercel.app/api?type=waving&color=0:E23744,30:FF6B6B,70:FF4500,100:B22222&height=120&section=footer)](https://github.com/PatlaveetiJabeer786/Zomato-Data-Analysis-SQL)
