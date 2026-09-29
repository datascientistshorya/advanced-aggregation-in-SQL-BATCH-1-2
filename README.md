# SQL Advanced Aggregation — Business Analysis Practice

A structured SQL practice project focused on **Advanced Aggregation and Business Analytics** using MySQL.

This project contains 10 business-oriented SQL problems designed to strengthen the ability to transform transactional data into meaningful customer, product, city, and category-level insights.

The exercises emphasize not just writing SQL syntax, but understanding **aggregation levels, business metrics, conditional aggregation, benchmarks, contribution analysis, and performance segmentation**.

## Author

**Shorya Dev Bisht**
https://www.linkedin.com/in/shorya-bisht-a20144349/


## Project Focus

**SQL | MySQL | Data Analysis | Business Analytics | Advanced Aggregation**

The primary objective of this project is to develop strong SQL problem-solving skills from an analyst's perspective.

Rather than focusing only on syntax, the questions simulate common analytical tasks such as:

* Measuring revenue and order performance
* Comparing customers and products
* Calculating completion and contribution rates
* Evaluating category-level performance
* Segmenting customers based on business metrics
* Comparing individual performance against an overall benchmark

---

# Database Schema

The exercises use three related tables.

### Customers

| Column          | Description                |
| --------------- | -------------------------- |
| `customer_id`   | Unique customer identifier |
| `customer_name` | Customer name              |
| `city`          | Customer city              |

### Orders

| Column        | Description                                 |
| ------------- | ------------------------------------------- |
| `order_id`    | Unique order identifier                     |
| `customer_id` | Customer reference                          |
| `product_id`  | Product reference                           |
| `amount`      | Order amount                                |
| `status`      | Order status such as Completed or Cancelled |
| `order_date`  | Order date                                  |

### Products

| Column         | Description               |
| -------------- | ------------------------- |
| `product_id`   | Unique product identifier |
| `product_name` | Product name              |
| `category`     | Product category          |
| `price`        | Product price             |

### Relationships

```text
customers
    |
    | customer_id
    |
orders
    |
    | product_id
    |
products
```

---

# Topics Covered

The 10 questions across the two batches cover the following SQL and analytical concepts:

* `GROUP BY`
* `COUNT()`
* `SUM()`
* `CASE`
* Conditional aggregation
* Multiple aggregations in a single query
* Common Table Expressions (`WITH`)
* Joining aggregated datasets
* Revenue analysis
* Order analysis
* Customer segmentation
* Product contribution analysis
* Category-level benchmarking
* Completion rate
* Revenue share
* AOV
* Business performance classification
* Multi-level aggregation

---

# Batch 1 — Advanced Aggregation

## Question 1 — Category Performance

Analyzed each product category using:

* Total orders
* Total revenue
* Average Order Value (AOV)

Only categories meeting a minimum order threshold were included.

### Business Objective

Identify categories generating meaningful order volume and evaluate their revenue efficiency.

---

## Question 2 — Customer Revenue Contribution

Calculated:

* Customer total spending
* Percentage contribution to overall completed-order revenue

### Business Objective

Understand how individual customers contribute to the overall revenue base.

This introduces the concept of comparing **individual-level metrics against a global benchmark**.

---

## Question 3 — City-Level Performance

Calculated city-level:

* Unique customers
* Completed orders
* Completed revenue
* Average completed order value

### Business Objective

Compare geographical performance using both volume and value metrics.

This helps distinguish between cities generating high order volume and cities generating higher-value transactions.

---

## Question 4 — Product Performance vs Category

Compared individual product performance against its category.

Calculated:

* Product name
* Category
* Product completed revenue
* Category completed revenue
* Product contribution to category revenue

### Business Objective

Identify how strongly each product contributes to the financial performance of its category.

This question introduced an important analytical pattern:

```text
Product Level
     ↓
Category Benchmark
     ↓
Product Contribution
```

---

## Question 5 — Customer Completion Segmentation

Calculated:

* Total customer spending
* Completed spending
* Completed spending percentage

Customers were then segmented into:

* High
* Medium
* Low

based on their completed-spending percentage.

### Business Objective

Identify customers whose spending is predominantly completed versus customers with a relatively large share of cancelled transactions.

---

# Batch 2 — Advanced Business Aggregation

## Question 1 — Customer Order Behavior

Calculated for each customer:

* Total orders
* Completed orders
* Cancelled orders
* Total spending
* Completed revenue

Results were ordered by completed revenue.

### Business Objective

Create a customer-level performance profile combining order volume, cancellations, and revenue.

---

## Question 2 — Product Revenue & Order Mix

Calculated for every product:

* Total orders
* Completed orders
* Cancelled orders
* Completed revenue
* Cancelled revenue

### Business Objective

Understand product-level order behavior and identify products generating revenue versus products experiencing cancellation-related losses.

---

## Question 3 — Category Completion Rate

Calculated for every category:

* Total orders
* Completed orders
* Cancelled orders
* Total revenue
* Completed revenue
* Completion rate

The completion rate was calculated as:

```text
Completed Orders
---------------- × 100
Total Orders
```

### Business Objective

Compare categories based on the proportion of orders successfully completed.

---

## Question 4 — Customer Revenue Share

Calculated:

* Total spending
* Completed spending
* Completed spending percentage
* Performance segment

Customers were classified as:

```text
≥ 80%       → Strong
50%–79%     → Moderate
< 50%       → Weak
```

### Business Objective

Identify customers whose spending is more or less exposed to cancelled orders.

This combines **conditional aggregation, percentage calculations, and business segmentation**.

---

## Question 5 — Product Performance Within Category

Calculated:

* Product completed revenue
* Category completed revenue
* Product contribution to category revenue
* Performance classification

Products were classified as:

```text
≥ 50%       → Dominant
25%–49%     → Significant
< 25%       → Minor
```

### Business Objective

Determine the relative importance of each product within its own category.

The analytical structure was:

```text
Orders
   ↓
Product-Level Completed Revenue
   ↓
Category-Level Completed Revenue
   ↓
Product Contribution %
   ↓
Business Classification
```

This question reinforced the importance of choosing the **correct aggregation level for the denominator**.

---

# Key SQL Patterns Practiced

## 1. Conditional Aggregation

```sql
SUM(
    CASE
        WHEN status = 'Completed'
        THEN amount
        ELSE 0
    END
)
```

Used extensively to calculate completed and cancelled revenue separately.

---

## 2. Conditional Order Counting

```sql
SUM(
    CASE
        WHEN status = 'Completed'
        THEN 1
        ELSE 0
    END
)
```

Used to calculate completed and cancelled order counts.

---

## 3. Percentage Metrics

```sql
completed_orders * 100.0 / total_orders
```

Used for completion-rate calculations.

---

## 4. Common Table Expressions

```sql
WITH customer_data AS (
    ...
)
SELECT ...
FROM customer_data;
```

CTEs were used to make complex analytical queries easier to structure, read, and validate.

---

## 5. Benchmark-Based Analysis

A major pattern practiced in this project was comparing one aggregation level against another.

For example:

```text
Product Revenue
      ↓
Category Revenue
      ↓
Product Contribution %
```

This is particularly important in real-world analytics because the denominator must match the business question.

---

# Key Analytical Learnings

### Aggregation level matters

A percentage is only meaningful when its numerator and denominator represent the correct comparison.

For example:

```text
Product Completed Revenue
-------------------------
Product Total Revenue
```

answers a different question from:

```text
Product Completed Revenue
-------------------------
Category Completed Revenue
```

The first measures the product's completion share.

The second measures the product's contribution to its category.

Understanding this distinction is critical in business analytics.

### Business metrics require context

Revenue alone does not provide a complete picture.

A stronger analysis can combine:

* Order volume
* Revenue
* AOV
* Completion rate
* Cancellation rate
* Customer contribution
* Product mix
* Category contribution

### CTEs improve analytical structure

Complex business questions can often be broken into logical stages:

```text
Raw Data
   ↓
First-Level Aggregation
   ↓
Benchmark Aggregation
   ↓
Comparison
   ↓
Business Classification
```

This approach makes analytical SQL easier to debug and explain.

---

# Analyst Perspective

These exercises are designed around questions that a Data Analyst, Business Analyst, or Web Analyst may encounter in real-world datasets.

Instead of asking only:

> "How do I write this SQL query?"

the focus is on asking:

> "What business question am I trying to answer, and what should the correct denominator and aggregation level be?"

Examples include:

* Which categories generate the most revenue?
* Which customers contribute the most completed revenue?
* Which cities have stronger order performance?
* Which products dominate their categories?
* Where are cancellations affecting revenue?
* Which customers have a high proportion of completed spending?
* Which categories have stronger completion rates?

---

# Skills Demonstrated

Through these 10 exercises, this project demonstrates practical experience with:

**SQL**

* MySQL
* Aggregation
* Conditional aggregation
* CTEs
* Joins
* CASE statements
* Percentage calculations
* Multi-level aggregation

**Data Analysis**

* Customer analysis
* Product analysis
* Category analysis
* Revenue analysis
* Cancellation analysis
* Contribution analysis
* Performance segmentation

**Business Thinking**

* Metric selection
* Benchmark selection
* Denominator validation
* Performance comparison
* Business classification
* Translating SQL output into analytical insights

---

# Project Progress

| Phase   | Topic                   | Status      |
| ------- | ----------------------- | ----------- |
| Phase 1 | Muscle-Memory Refresh   | Completed   |
| Phase 2 | Aggregation Mastery     | Completed   |
| Phase 3 | CASE + Business Metrics | Completed   |
| Phase 4 | JOIN Mastery            | Completed   |
| Phase 5 | Subqueries + CTEs       | Completed   |
| Phase 6 | Advanced Aggregation    | In Progress |
| Batch 1 | Advanced Aggregation    | Completed   |
| Batch 2 | Advanced Aggregation    | In Progress |

**Questions completed across Batch 1 and Batch 2: 10**

---

# Next Step

The next stage of this SQL learning roadmap will continue with **Phase 6 — Advanced Aggregation**, progressing toward more complex analytical SQL problems while maintaining a strong business-analysis perspective.

The objective is to move from simply producing correct queries toward being able to:

```text
Understand the business problem
        ↓
Identify the correct grain
        ↓
Choose the right aggregation
        ↓
Build the SQL
        ↓
Validate the denominator
        ↓
Interpret the result
        ↓
Translate it into business insight
```

---

## Repository Purpose

This repository documents a structured SQL learning journey focused on developing **practical, business-oriented SQL skills** rather than memorizing isolated SQL syntax.

The goal is to build the ability to take transactional data and turn it into reliable analytical outputs that can support real business decisions.

**Author:** Shorya Dev Bisht
