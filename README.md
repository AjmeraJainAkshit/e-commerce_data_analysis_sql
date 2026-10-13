# 🛒 E-Commerce Sales Analysis using MySQL

A end-to-end **SQL data analysis project** that answers **52 real-world business questions** on an e-commerce dataset, covering revenue, customers, products, retention, churn, and order behaviour.

![MySQL](https://img.shields.io/badge/Database-MySQL-blue)
![SQL](https://img.shields.io/badge/Language-SQL-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📌 Project Overview

An online store wants to understand how its business is performing. This project builds a relational database in MySQL and uses SQL to turn raw order data into business insights: what sells, who buys, where revenue comes from, and which customers are at risk of leaving.

## 🗂️ Dataset

| Table | Rows | Description |
|---|---|---|
| `customers` | 90 | Customer name, city, gender, signup date |
| `products` | 38 | Product name, category, unit price |
| `orders` | 2,000 | Order date and status (Delivered / Pending / Cancelled) |
| `order_items` | 4,967 | Products, quantity and price per order |

**Product categories:** Electronics, Clothing, Home & Kitchen, Beauty, Sports, Books, Grocery
**Order period:** January 2025 – July 2026

### Schema

```
customers (customer_id PK, customer_name, city, gender, signup_date)
products (product_id PK, product_name, category, unit_price)
orders (order_id PK, customer_id FK, order_date, order_status)
order_items (order_item_id PK, order_id FK, product_id FK, quantity, unit_price)
```

```
customers 1 ──── * orders 1 ──── * order_items * ──── 1 products
```

## 🧠 SQL Concepts Used

- **Joins:** INNER JOIN, LEFT JOIN, self join
- **Aggregations:** SUM, COUNT, AVG, GROUP BY, HAVING
- **CTEs** (Common Table Expressions) and **subqueries**
- **Window functions:** `RANK`, `DENSE_RANK`, `ROW_NUMBER`, `LAG`, `LEAD`, running totals, `SUM() OVER()`
- **Conditional logic:** CASE WHEN
- **Date functions:** `DATE_FORMAT`, `DATEDIFF`
- **Analytics techniques:** RFM analysis, retention, churn, cohort-style acquisition, market basket analysis

## ❓ Business Questions Solved (52)

### 1️⃣ Business Overview
Total revenue, total orders, total customers, total products, average order value.

### 2️⃣ Product & Category Performance
Top 5 / top 10 best-selling products, best and worst selling category, highest and lowest revenue product, top-selling product in each category, revenue contribution % of each product and category, most expensive product, average products per order.

### 3️⃣ Customer Analysis
Top 3 / 5 / 10 customers by revenue, customer ranking, customer lifetime value (CLV), highest-value order per customer, average order value per customer, customers buying from multiple categories, revenue split by gender.

### 4️⃣ Sales Trends
Monthly revenue trend, daily sales trend, running total of revenue, month-over-month growth, highest revenue month, fastest-growing category.

### 5️⃣ Geographic Analysis
Revenue by city, top 3 cities by revenue.

### 6️⃣ Customer Behaviour & Retention
Repeat customers, repeat purchase rate, new vs returning customers, monthly active customers, new customers acquired each month, previous / next order date, days between consecutive orders, average days between orders.

### 7️⃣ Churn & Segmentation
Customers who never ordered, inactive customers, customers at risk of churn, churn rate, RFM (Recency, Frequency, Monetary) analysis.

### 8️⃣ Order Operations
Orders above ₹10,000, cancellation rate, delivered vs cancelled orders.

### 9️⃣ Product Affinity
Which two products are most frequently bought together.

## 💡 Sample Query

**Month-over-month revenue growth**

```sql
WITH monthly_sale AS (
    SELECT DATE_FORMAT(o.order_date, '%y-%m') AS month,
           SUM(oi.quantity * oi.unit_price) AS revenue
    FROM orders o
    JOIN order_items oi ON o.order_id = oi.order_id
    GROUP BY month
)
SELECT month,
       revenue,
       LAG(revenue) OVER (ORDER BY month) AS previous_month_revenue,
       ROUND(100 * (revenue - LAG(revenue) OVER (ORDER BY month))
             / LAG(revenue) OVER (ORDER BY month), 2) AS growth_percentage
FROM monthly_sale
ORDER BY month;
```

## 🚀 How to Run

1. Install **MySQL** (8.0 or higher recommended, needed for window functions) and MySQL Workbench.
2. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/ecommerce-sales-analysis-sql.git
   ```
3. Open `E-commerce Analysis Data Analysis project.sql` in MySQL Workbench.
4. Run the script. It will:
   - create the `E_Commerce_Project` database
   - create the 4 tables
   - insert all the sample data
5. Run the queries under the business questions section one by one and explore the results.

## 📁 Repository Structure

```
├── E-commerce Analysis Data Analysis project.sql   # Schema, data and all 52 queries
└── README.md
```

## 🔍 Key Takeaways

- Built a clean 4-table relational model and joined it across multiple levels to answer business questions.
- Used window functions and CTEs to handle ranking, running totals and period-over-period growth.
- Applied RFM, churn and retention logic to understand customer behaviour, not just sales totals.
- Practised translating plain business questions into accurate SQL.

## 🛠️ Tools

- MySQL 8.0
- MySQL Workbench

## 👤 Author

**Your Name**
🔗 [LinkedIn](https://www.linkedin.com/in/akshitjain27/) | 💻 [GitHub]((https://github.com/AjmeraJainAkshit))

---

⭐ If you found this project useful, consider giving it a star!
