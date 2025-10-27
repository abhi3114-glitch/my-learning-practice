# MySQL

## Overview
MySQL is one of the most popular open-source relational database management systems.

## Basic Operations
```sql
-- Database
CREATE DATABASE myapp;
USE myapp;

-- Table
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(255) UNIQUE,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- CRUD
INSERT INTO users (name, email) VALUES ('John', 'john@example.com');
SELECT * FROM users WHERE id = 1;
UPDATE users SET name = 'Jane' WHERE id = 1;
DELETE FROM users WHERE id = 1;
```

## Joins & Aggregations
```sql
SELECT u.name, COUNT(o.id) as order_count
FROM users u
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id
HAVING order_count > 5
ORDER BY order_count DESC;
```

## Indexes
```sql
CREATE INDEX idx_email ON users(email);
CREATE FULLTEXT INDEX idx_content ON posts(title, content);
```

## Best Practices
1. Use **InnoDB** engine for transactions
2. Index **foreign keys**
3. Use **prepared statements** to prevent SQL injection

## Resources
- MySQL Documentation
