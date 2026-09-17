# Experiment 7

**Name:** Satyam Singh  
**UID:** 24BCS12662

## Aim

Practice procedural SQL using cursors and stored procedures.

## Problem Statements

1. Use a cursor to iterate through orders and print high-value orders.  
2. Create and call a stored procedure to insert employee records with a validation rule.

## SQL Queries

### 1) Cursor on Orders ([7.1.sql](7.1.sql))

```sql
DECLARE
    CURSOR c_orders IS
        SELECT order_id, amount
        FROM orders;

BEGIN
    FOR ord IN c_orders LOOP
        IF ord.amount > 10000 THEN
            dbms_output.put_line(
                'order id: ' || ord.order_id || ', high value'
            );
        END IF;
    END LOOP;
END;
/
```

### 2) Procedure with Validation ([7.2.sql](7.2.sql))

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100),
    emp_salary NUMERIC(10,2),
    department VARCHAR(100)
);

INSERT INTO employees VALUES
(1, 'amit', 50000, 'it'),
(3, 'rahul', 60000, 'hr'),
(5, 'priya', 55000, 'finance');

CREATE OR REPLACE PROCEDURE add_emp(
    p_emp_id INT,
    p_emp_name VARCHAR(256),
    p_emp_salary NUMERIC(10,2),
    p_department VARCHAR(256)
)
LANGUAGE plpgsql
AS $$
BEGIN
    IF p_emp_id % 2 = 0 THEN
        RAISE EXCEPTION 'even not allowed';
    END IF;

    INSERT INTO employees (emp_id, emp_name, emp_salary, department)
    VALUES (p_emp_id, p_emp_name, p_emp_salary, p_department);

    RAISE NOTICE 'Employee added successfully';
END;
$$;

CALL add_emp(101, 'amit', 50000, 'it');
CALL add_emp(102, 'rahul', 60000, 'hr');

SELECT * FROM employees;
```

## Result

Cursor and procedure-based SQL tasks were implemented successfully.
