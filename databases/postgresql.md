# PostgreSQL

## Overview
PostgreSQL is a powerful, open-source object-relational database system with strong reliability and feature robustness.

## Basic SQL
```sql
-- Create table
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(255) UNIQUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Insert
INSERT INTO users (name, email) VALUES ('John', 'john@example.com');

-- Select
SELECT * FROM users WHERE age >= 18;
SELECT name, email FROM users ORDER BY created_at DESC LIMIT 10;

-- Update
UPDATE users SET name = 'Jane' WHERE id = 1;

-- Delete
DELETE FROM users WHERE id = 1;
```

## Joins
```sql
SELECT u.name, o.total
FROM users u
INNER JOIN orders o ON u.id = o.user_id
WHERE o.status = 'completed';

-- LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN
```

## Indexes
```sql
CREATE INDEX idx_users_email ON users(email);
CREATE UNIQUE INDEX idx_users_email_unique ON users(email);
CREATE INDEX idx_users_name_trgm ON users USING gin(name gin_trgm_ops);
```

## JSON Support
```sql
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  data JSONB
);

INSERT INTO products (data) VALUES ('{"name": "Product", "price": 29.99}');
SELECT data->>'name' FROM products;
SELECT * FROM products WHERE data @> '{"active": true}';
```

## Transactions
```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
-- or ROLLBACK;
```

## Best Practices
1. Always use **transactions** for related operations
2. Create **indexes** on frequently queried columns
3. Use **EXPLAIN ANALYZE** to optimize queries
4. Implement **connection pooling**

## Resources
- PostgreSQL Documentation
