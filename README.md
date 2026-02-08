1. **INTRODUCTION**

This project demonstrates the use of SQL JOINs and Window Functions to analyze sales data for a small retail business.
The goal is to extract useful insights from customer, product, and sales information using correct SQL queries.

2. **BUSINESS PROBLEM DEFINITION**
Business Context

The business is a small retail shop that sells electronic products to customers located in different regions of Rwanda.

**DATA CHALLENGE**

Although the shop records customers, products, and sales, it is difficult to clearly understand customer behavior, product performance, and sales trends over time using simple queries.

**EXPECTED OUTCOME**

By using SQL JOINs and Window Functions, the business expects to identify active customers, best-selling products, and sales trends to support better business decisions.

3.**SUCCESS CRITERIA**

The analysis aims to achieve the following measurable goals:

Identify top products per region using RANK()

Calculate running total of sales over time using SUM() OVER()

Compare current sales with previous sales periods using LAG()

Segment customers into four spending groups using NTILE(4)

Calculate three-period moving averages using AVG() OVER()

4.**DATABASE SCHEMA DESIGN**

The database consists of three related tables:

customers: stores customer details

products: stores product information

sales: stores sales transactions

Each sale links one customer to one product.
The sales table contains foreign keys referencing both customers and products.

(Insert ER Diagram screenshot here)

5. Part A – SQL JOINs Implementation
5.1 **INNER JOIN**

Purpose: Retrieve sales that have valid customers and products.

SELECT s.sale_id, c.customer_name, p.product_name, s.sale_date, s.total_amount
FROM sales s
INNER JOIN customers c ON s.customer_id = c.customer_id
INNER JOIN products p ON s.product_id = p.product_id;


**BUSINESS INTERPRETATION**:
This query displays all valid sales transactions.
It ensures that only sales linked to existing customers and products are analyzed.

5.2 **LEFT JOIN**

Purpose: Identify customers who have never made a purchase.

SELECT c.customer_id, c.customer_name
FROM customers c
LEFT JOIN sales s ON c.customer_id = s.customer_id
WHERE s.sale_id IS NULL;


**BUSINESS INTERPRETATION**:
This query helps identify inactive customers.
The business can target these customers with promotions to encourage purchases.

5.3 **RIGHT JOIN**

Purpose: Detect products that have not been sold.

SELECT p.product_id, p.product_name
FROM sales s
RIGHT JOIN products p ON s.product_id = p.product_id
WHERE s.sale_id IS NULL;


**BUSINESS INTERPRETATION**:
This query shows products with no sales activity.
Such products may need marketing attention or reconsideration.

5.4 **FULL OUTER JOIN**

Purpose: Display all customers and products, including unmatched records.

SELECT c.customer_name, p.product_name
FROM customers c
FULL OUTER JOIN products p
ON c.customer_id = p.product_id;


**BUSINESS INTERPRETATION**:
This query provides a complete overview of customers and products.
It includes records even when no sales relationship exists.

5.5 **SELF JOIN**

Purpose: Compare customers located in the same region.

SELECT a.customer_name AS customer_1, b.customer_name AS customer_2, a.region
FROM customers a
JOIN customers b
ON a.region = b.region
AND a.customer_id < b.customer_id;


**BUSINESS INTERPRETATION**:
This query identifies customers from the same region.
It helps analyze regional customer distribution.

6. **RUSLUTS ANALYSIS**
**DESCRIPTIVE ANALYSIS**

The analysis shows which customers and products are active and how sales are distributed.

**DIGNOSTIC ANALYSIS**

Some customers and products have no sales records, indicating low engagement or poor performance.

**PRESCRIPTIVE ANALYSIS**

The business should promote inactive products and target customers who have never made purchases.

7. **CONCLUSION**

This project successfully demonstrated the use of SQL JOINs to analyze relational data.
The results provide meaningful insights that can help improve sales and customer engagement.

8. **REFERENCES**

Oracle SQL Documentation

PostgreSQL Official Documentation

Lecture Notes – INSY 8311

