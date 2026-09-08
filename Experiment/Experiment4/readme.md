# Experiment 4: SQL JOIN Operations

**Name:** Satyam Singh  
**UID:** 24BCS12662

## Aim

Practice SQL JOIN operations across multiple tables and display the required results.

## Problem Statements

1. List `customer_name` and `order_date` for all customers who have placed orders.
2. List all customer names and their corresponding `product_name`, including customers who have not placed any orders.
3. Display `product_name` and `order_date` for all products that are ordered.
4. Perform a `FULL OUTER JOIN` on `student` and `course` tables using `Course_id`.

## SQL Queries

### 1) Customers and Order Dates

```sql
SELECT cust.customer_name, od.order_date
FROM customers AS cust
INNER JOIN orders AS od
ON cust.customer_id = od.customer_id;
```

### 2) All Customers with Products (Including Customers with No Orders)

```sql
SELECT cust.customer_name, p.product_name
FROM customers AS cust
LEFT JOIN orders AS od
ON cust.customer_id = od.customer_id
LEFT JOIN products AS p
ON od.product_name = p.product_name;
```

### 3) Products and Their Order Dates

```sql
SELECT p.product_name, od.order_date
FROM products AS p
INNER JOIN orders AS od
ON p.product_name = od.product_name;
```

### 4) FULL OUTER JOIN on Student and Course

```sql
SELECT *
FROM student
FULL OUTER JOIN course
ON student.Course_id = course.Course_id;
```

## Additional Practice Queries

### 5) Employee-Manager and Customer-Product Combinations

```sql
SELECT e1.employee_name AS Employee, e2.employee_name AS Manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.employee_id;

SELECT customer_name, product_name
FROM customers
CROSS JOIN products;
```

### 6) Self JOIN on Student Table

```sql
SELECT s1.st_id, s1.st_name, s1.department, s2.st_id, s2.st_name, s2.department
FROM student s1
JOIN student s2
ON s1.department = s2.department
AND s1.st_id <> s2.st_id;

SELECT DISTINCT s1.st_id, s1.st_name, s1.course_id
FROM student s1
JOIN student s2
ON s1.course_id = s2.course_id
AND s1.st_id <> s2.st_id
ORDER BY s1.course_id;
```

## Output Screenshots

### Output 4.1
![Output 4.1](4.1.png)

### Output 4.2
![Output 4.2](4.2.png)

### Output 4.3
![Output 4.3](4.3.png)

### Output 4.4
![Output 4.4](4.4.png)

### Output 4.5
![Output 4.5](4.5.png)

### Output 4.6
![Output 4.6](4.6.png)

## Result

All required JOIN queries were executed successfully, and the outputs matched the expected results.
