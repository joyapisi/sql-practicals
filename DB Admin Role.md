
# 🗄️ Library Management Database (DBA Project)

This project sets up and manages a **library management system database**.  
It focuses on **database administration tasks** such as schema design, indexing, user roles, permissions, and backups.

---

## 📖 Getting Started

This repository includes files with SQL for database administration tasks:

- `schema.sql` → defines the structure of the database.  
- `data.sql` → inserts sample records into the database.  
- `admin_tasks.sql` → includes DBA-level commands (users, roles, backups, indexing, etc.).  

---

## 🗄️ Schema (`schema.sql`)

```sql
-- Create database
CREATE DATABASE bookstore_db;

-- Switch to database
\c bookstore_db;

-- Create tables
CREATE TABLE books (
    id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    title VARCHAR(200) NOT NULL,
    author VARCHAR(100) NOT NULL,
    published_year INT,
    available BOOLEAN DEFAULT TRUE
);

CREATE TABLE members (
    id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    full_name VARCHAR(150) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    join_date DATE DEFAULT CURRENT_DATE
);

CREATE TABLE borrow_records (
    id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    member_id INT REFERENCES members(id),
    book_id INT REFERENCES books(id),
    borrow_date DATE DEFAULT CURRENT_DATE,
    return_date DATE
);
````

---

## 📚 Sample Data (`data.sql`)

```sql
INSERT INTO books (title, author, published_year) VALUES
('1984', 'George Orwell', 1949),
('To Kill a Mockingbird', 'Harper Lee', 1960),
('The Great Gatsby', 'F. Scott Fitzgerald', 1925);

INSERT INTO members (full_name, email) VALUES
('Alice Johnson', 'alice@example.com'),
('Bob Smith', 'bob@example.com');
```

---

## 🛠 DBA Tasks (`admin_tasks.sql`)

```sql
-- 1. Create roles and users
CREATE ROLE librarian WITH LOGIN PASSWORD 'securePass123';
CREATE ROLE assistant WITH LOGIN PASSWORD 'assistantPass';

-- 2. Grant permissions
GRANT CONNECT ON DATABASE bookstore_db TO librarian;
GRANT USAGE, SELECT ON ALL SEQUENCES IN SCHEMA public TO assistant;
GRANT SELECT, INSERT, UPDATE ON books, members TO assistant;

-- 3. Create indexes for performance
CREATE INDEX idx_books_title ON books(title);
CREATE INDEX idx_members_email ON members(email);

-- 4. Backup (PostgreSQL command line example)
-- pg_dump bookstore_db > library_backup.sql;

-- 5. Restore backup
-- psql bookstore_db < library_backup.sql;

-- 6. Monitor (show current connections)
SELECT * FROM pg_stat_activity;

-- 7. Enforce constraints (no duplicate borrow records)
ALTER TABLE borrow_records ADD CONSTRAINT unique_borrow UNIQUE (member_id, book_id, borrow_date);
```

---

## 🔒 Key DBA Skills Demonstrated

* Database creation & schema design
* User & role management with permissions
* Indexing for performance optimization
* Backup & restore strategies
* Monitoring connections
* Enforcing constraints for data integrity

---

## 📝 License

This project is [MIT](./LICENSE) licensed.


👉 See the difference?  
- The **vet_clinic** (data analyst) project was all about **queries to answer questions**.  
- The **bookstore_db** (DB Admin) project is about **setup, roles, indexing, security, and backups**.  

Would you like me to **add example admin queries** (like checking database size, vacuuming, or analyzing query performance) to make it even more realistic for a DBA role?
```
