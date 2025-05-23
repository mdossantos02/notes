
# PostgreSQL Essential Cheat Sheet with Performance Tuning

## 1. Connecting to PostgreSQL
```bash
psql -h host -U user -d dbname
```

## 2. Basic SQL Operations
```sql
-- Create
CREATE TABLE table_name (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL
);

-- Read
SELECT * FROM table_name;

-- Update
UPDATE table_name SET name = 'new name' WHERE id = 1;

-- Delete
DELETE FROM table_name WHERE id = 1;
```

## 3. Indexing
```sql
-- Create index
CREATE INDEX idx_name ON table_name(column_name);

-- Unique index
CREATE UNIQUE INDEX idx_unique_name ON table_name(column_name);

-- Composite index
CREATE INDEX idx_multi ON table_name(col1, col2);

-- Index on expressions
CREATE INDEX idx_lower_name ON table_name(LOWER(name));
```

## 4. Performance Tuning Tips

### 4.1 EXPLAIN ANALYZE
```sql
EXPLAIN ANALYZE SELECT * FROM table_name WHERE id = 1;
```

### 4.2 Vacuum and Analyze
```bash
VACUUM ANALYZE;
```

### 4.3 Query Optimization Tips
- Use `EXISTS` instead of `IN` for subqueries
- Avoid `SELECT *` in production
- Use LIMIT with OFFSET wisely
- Consider materialized views for expensive queries

### 4.4 Connection Settings
```conf
# postgresql.conf
max_connections = 100
work_mem = 4MB
shared_buffers = 128MB
effective_cache_size = 512MB
```

### 4.5 Autovacuum Tuning
```conf
# postgresql.conf
autovacuum = on
autovacuum_naptime = 1min
autovacuum_vacuum_threshold = 50
```

### 4.6 Parallel Queries
```sql
-- Enable parallel execution
SET max_parallel_workers_per_gather = 4;
```

### 4.7 Partitioning
```sql
CREATE TABLE measurement (
    city_id         int,
    logdate         date,
    peaktemp        int,
    unitsales       int
) PARTITION BY RANGE (logdate);
```

### 4.8 Monitoring
```sql
SELECT * FROM pg_stat_activity;
SELECT * FROM pg_stat_user_tables;
```

## 5. Useful Meta-Commands in `psql`
```bash
\dt         -- list tables
\d table    -- describe table
\l          -- list databases
\c dbname   -- connect to database
\x          -- expanded display
```
