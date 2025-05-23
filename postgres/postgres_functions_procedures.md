
# PostgreSQL Cheat Sheet: Functions and Stored Procedures

---

## 📘 User-Defined Functions (UDF)

### 1. Simple Function (Returns a scalar)
```sql
CREATE FUNCTION get_discount(price NUMERIC) RETURNS NUMERIC AS $$
BEGIN
  RETURN price * 0.10;
END;
$$ LANGUAGE plpgsql;

-- Usage
SELECT get_discount(100);
```

### 2. Function with Parameters and Logic
```sql
CREATE FUNCTION get_tax(price NUMERIC, rate NUMERIC DEFAULT 0.05) RETURNS NUMERIC AS $$
BEGIN
  RETURN price * rate;
END;
$$ LANGUAGE plpgsql;
```

### 3. SQL Function (Shorter Syntax)
```sql
CREATE FUNCTION add_numbers(a INT, b INT) RETURNS INT AS $$
  SELECT a + b;
$$ LANGUAGE SQL;
```

---

## 🔄 Stored Procedures

### 1. Create a Procedure
```sql
CREATE PROCEDURE log_activity(user_id INT, action TEXT)
LANGUAGE plpgsql
AS $$
BEGIN
  INSERT INTO activity_log(user_id, action, action_time)
  VALUES (user_id, action, NOW());
END;
$$;
```

### 2. Call a Procedure
```sql
CALL log_activity(1, 'login');
```

---

## 🔁 Control Flow in Functions/Procedures

### IF Statement
```sql
IF quantity > 10 THEN
  RETURN 'Bulk';
ELSE
  RETURN 'Standard';
END IF;
```

### LOOP / WHILE / FOR
```sql
-- WHILE loop
WHILE i <= 10 LOOP
  total := total + i;
  i := i + 1;
END LOOP;

-- FOR loop
FOR rec IN SELECT * FROM my_table LOOP
  RAISE NOTICE 'ID: %', rec.id;
END LOOP;
```

---

## 🧪 Return Types

### 1. Returning TABLE
```sql
CREATE FUNCTION get_users() RETURNS TABLE(id INT, name TEXT) AS $$
BEGIN
  RETURN QUERY SELECT id, name FROM users;
END;
$$ LANGUAGE plpgsql;
```

### 2. Returning SETOF
```sql
CREATE FUNCTION get_sales_above(min_value NUMERIC) RETURNS SETOF sales AS $$
BEGIN
  RETURN QUERY SELECT * FROM sales WHERE amount > min_value;
END;
$$ LANGUAGE plpgsql;
```

---

## 🧰 Utility Functions

### 1. Check Function Definition
```sql
\df+ function_name
```

### 2. Drop Function or Procedure
```sql
DROP FUNCTION get_discount(NUMERIC);
DROP PROCEDURE log_activity(INT, TEXT);
```

---

## 🛠 Performance and Tips
- Keep functions immutable where possible for caching:
```sql
CREATE FUNCTION now_plus_days(days INT) RETURNS TIMESTAMP AS $$
  SELECT NOW() + (days || ' days')::INTERVAL;
$$ LANGUAGE SQL IMMUTABLE;
```
- Use `EXCEPTION` blocks for error handling.
- Test functions using `SELECT`, procedures with `CALL`.

