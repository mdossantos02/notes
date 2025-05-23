
# PostgreSQL Cheat Sheet: Subqueries, Temp Tables, and In-Memory Tables

---

## 🔄 Subqueries

### 1. Scalar Subquery (Returns a single value)
```sql
SELECT name FROM employees WHERE department_id = (
    SELECT id FROM departments WHERE name = 'Sales'
);
```

### 2. Row Subquery
```sql
SELECT * FROM employees WHERE (department_id, job_id) = (
    SELECT department_id, job_id FROM job_assignments WHERE id = 10
);
```

### 3. Table Subquery
```sql
SELECT * FROM (
    SELECT name, salary FROM employees WHERE salary > 50000
) AS high_earners
WHERE name LIKE 'A%';
```

### 4. Correlated Subquery
```sql
SELECT name FROM employees e WHERE salary > (
    SELECT AVG(salary) FROM employees WHERE department_id = e.department_id
);
```

### 5. EXISTS vs IN
```sql
-- EXISTS
SELECT name FROM employees e
WHERE EXISTS (
    SELECT 1 FROM departments d WHERE d.id = e.department_id
);

-- IN
SELECT name FROM employees
WHERE department_id IN (SELECT id FROM departments WHERE location = 'NY');
```

---

## 🧪 Temporary Tables

### 1. Create and Use a Temp Table
```sql
CREATE TEMP TABLE temp_sales (
    product_id INT,
    quantity INT
);

INSERT INTO temp_sales VALUES (1, 100), (2, 200);

SELECT * FROM temp_sales;
```

### 2. Behavior
- Temporary tables are only visible within the session.
- Automatically dropped at the end of the session.
- Use `ON COMMIT DELETE ROWS` for truncation on commit:
```sql
CREATE TEMP TABLE temp_session_data (
    user_id INT,
    token TEXT
) ON COMMIT DELETE ROWS;
```

---

## ⚡ In-Memory Optimization (Simulated)

PostgreSQL does not have dedicated "in-memory" tables like some databases, but you can optimize for memory usage:

### 1. Unlogged Tables (Skip WAL for performance)
```sql
CREATE UNLOGGED TABLE fast_temp_data (
    id SERIAL,
    value TEXT
);
```

### 2. Increase Work Memory (Session Scope)
```sql
SET work_mem = '64MB';
```

### 3. Use CTEs (Common Table Expressions)
```sql
WITH recent_orders AS (
    SELECT * FROM orders WHERE order_date > now() - INTERVAL '7 days'
)
SELECT * FROM recent_orders WHERE total > 100;
```

---

## 🛠 Performance Tips
- Use indexes even in subqueries.
- Prefer `EXISTS` over `IN` when dealing with large result sets.
- For performance testing, use `EXPLAIN ANALYZE`.

