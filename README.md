# 📚 Smart Library Management System

> A comprehensive SQL database project for managing library operations including books, authors, members, and transactions with advanced queries and analytics.

---

## 🎯 Table of Contents

- [📋 Project Overview](#-project-overview)
- [🏗️ Database Architecture](#️-database-architecture)
- [📊 Schema & Tables](#-schema--tables)
- [🔧 CRUD Operations](#-crud-operations)
- [📈 Advanced Queries](#-advanced-queries)
- [🛠️ Setup Instructions](#️-setup-instructions)
- [📝 Query Examples](#-query-examples)

---

## 📋 Project Overview

The **Smart Library Management System** is a robust SQL database designed to manage:
- 📚 Books inventory and availability
- ✍️ Author information and management
- 👥 Member registration and membership tracking
- 📑 Book borrowing and transaction history
- 💰 Fine calculation and management

### Key Features
✅ Complete CRUD operations  
✅ Advanced SQL joins and relationships  
✅ Complex queries with subqueries  
✅ Date and time manipulation  
✅ Window functions and analytics  
✅ String manipulation functions  
✅ Case expressions for conditional logic  

---

## 🏗️ Database Architecture

```
┌─────────────────────────────────────────────────┐
│              Database: practical_pr             │
├─────────────────────────────────────────────────┤
│                                                 │
│  ┌──────────┐      ┌──────────┐                 │
│  │  Books   │◄─────┤ Authors  │                 │
│  └──────────┘      └──────────┘                 │
│       ▲                                         │
│       │                                         │
│       └─────────┬─────────────────────┐         │
│                 │                     │         │
│          ┌──────────────┐      ┌──────────┐     │
│          │ Transactions │      │ Members  │     │
│          └──────────────┘      └──────────┘     │
│                                                 │
└─────────────────────────────────────────────────┘
```

---

## 📊 Schema & Tables

### 1️⃣ **Books Table**

| Column | Type | Constraint | Description |
|--------|------|-----------|-------------|
| `book_ID` | INT | PRIMARY KEY | Unique identifier for books |
| `title` | VARCHAR(50) | - | Name of the book |
| `author_ID` | INT | FOREIGN KEY | Reference to Authors table |
| `category` | VARCHAR(50) | - | Book category (Fantasy, Horror, etc.) |
| `isbn` | VARCHAR(50) | - | International Standard Book Number |
| `published_Date` | DATE | - | Publication date of the book |
| `price` | INT | - | Book price in currency units |
| `available_copies` | INT | - | Number of copies available |

**Sample Data:**
| book_ID | title | author_ID | category | isbn | published_Date | price | available_copies |
|---------|-------|-----------|----------|------|----------------|-------|------------------|
| 101 | Harry Potter and the Sorcerers Stone | 1 | Fantasy | 978-0590353427 | 1997-06-26 | 20 | 10 |
| 102 | The Shining | 2 | Horror | 978-0345806789 | 1977-01-28 | 15 | 0 |
| 103 | A Game of Thrones | 3 | Fantasy | 978-0553103540 | 1996-08-01 | 25 | 0 |
| 104 | Murder on the Orient Express | 4 | Mystery | 978-0062073495 | 2016-01-01 | 12 | 11 |
| 105 | The Old Man and the Sea | 5 | Fiction | 978-0684801223 | 1952-09-01 | 10 | 0 |

---

### 2️⃣ **Authors Table**

| Column | Type | Constraint | Description |
|--------|------|-----------|-------------|
| `author_ID` | INT | PRIMARY KEY | Unique identifier for authors |
| `name` | VARCHAR(50) | - | Author's full name |
| `email` | VARCHAR(50) | - | Author's email address |

**Sample Data:**
| author_ID | name | email |
|-----------|------|-------|
| 1 | J.K. Rowling | jk.rowling@example.com |
| 2 | Stephen King | stephen.king@example.com |
| 3 | George R.R. Martin | grrmartin@example.com |
| 4 | Agatha Christie | a.christie@example.com |
| 5 | Ernest Hemingway | e.hemingway@example.com |

---

### 3️⃣ **Members Table**

| Column | Type | Constraint | Description |
|--------|------|-----------|-------------|
| `member_ID` | INT | PRIMARY KEY | Unique identifier for members |
| `name` | VARCHAR(50) | - | Member's full name |
| `email` | VARCHAR(50) | - | Member's email address |
| `phone_number` | INT | - | Contact number |
| `membership_date` | DATE | - | Date when member joined |

**Sample Data:**
| member_ID | name | email | phone_number | membership_date |
|-----------|------|-------|--------------|-----------------|
| 1 | Alice Johnson | alice.j@example.com | 1234567890 | 2021-01-15 |
| 2 | Bob Smith | bob.smith@example.com | 2147483647 | 2023-03-22 |
| 3 | Charlie Brown | charlie.b@example.com | 5551234 | 2023-06-10 |
| 4 | Diana Prince | diana.p@example.com | 9998887 | 2023-08-05 |
| 5 | Ethan Hunt | ethan.h@example.com | 1112223 | 2024-01-12 |

---

### 4️⃣ **Transactions Table**

| Column | Type | Constraint | Description |
|--------|------|-----------|-------------|
| `transaction_ID` | INT | PRIMARY KEY | Unique transaction identifier |
| `member_ID` | INT | FOREIGN KEY | Reference to Members table |
| `book_ID` | INT | FOREIGN KEY | Reference to Books table |
| `borrow_date` | DATE | - | Date when book was borrowed |
| `return_date` | DATE | - | Date when book was returned (NULL if not returned) |
| `fine_amount` | INT | - | Fine charged for late return |

**Sample Data:**
| transaction_ID | member_ID | book_ID | borrow_date | return_date | fine_amount |
|-----------------|-----------|---------|-------------|------------|-------------|
| 501 | 1 | 101 | 2026-01-15 | 2026-02-17 | 0 |
| 502 | 2 | 103 | 2025-05-05 | 2025-12-19 | 2 |
| 503 | 3 | 105 | 2024-02-10 | NULL | 0 |
| 504 | 4 | 102 | 2024-02-12 | NULL | 0 |
| 505 | 5 | 104 | 2024-02-15 | 2024-02-16 | 0 |

---

## 🔧 CRUD Operations

### ➕ **CREATE (Insert)**

#### Insert into Books Table:
```sql
INSERT INTO books VALUES
(106, 'The Shining', 2, 'Science','988-0590353427', '1999-06-26', 200, 1);
```

#### Insert into Authors Table:
```sql
INSERT INTO authors VALUES
(106, 'Alice', 'a06@gmail.com');
```

#### Insert into Members Table:
```sql
INSERT INTO members VALUES
(6, 'David', 'dp@gmail.com', 1245678200, '2024-01-01');
```

---

### ✏️ **UPDATE**

#### Update Available Copies (Decrease):
```sql
UPDATE books
SET available_copies = available_copies - 1
WHERE book_ID = 101;
```
**Explanation:** Decreases available copies when a book is borrowed.

#### Update Available Copies (Increase):
```sql
UPDATE books
SET available_copies = available_copies + 1
WHERE book_ID = 104;
```
**Explanation:** Increases available copies when a book is returned.

---

### 🗑️ **DELETE**

#### Delete Old Transactions:
```sql
DELETE FROM transactions
WHERE borrow_date <= '2024-02-01';
```
**Explanation:** Removes transaction records older than February 2024.

---

### 📖 **READ (Retrieve)**

#### Get Available Books:
```sql
SELECT * 
FROM books
WHERE available_copies > 0;
```
**Explanation:** Displays all books that have at least one copy available.

---

## 📈 Advanced Queries

### 1️⃣ **SQL WHERE Clause with Conditions**

| Query | Purpose | Formula |
|-------|---------|---------|
| `WHERE YEAR(published_date) > 2015` | Books published after 2015 | Extracts year from date |
| `WHERE available_copies > 0` | Available books only | Simple comparison |
| `WHERE membership_date < '2022-01-01'` | Members joined before 2022 | Date comparison |

---

### 2️⃣ **Sorting & Limiting Results**

#### Top 5 Most Expensive Books:
```sql
SELECT * FROM books
ORDER BY price DESC
LIMIT 5;
```

| ORDER BY | LIMIT | Result |
|----------|-------|--------|
| `price DESC` | 5 | Highest 5 prices, descending |
| `title ASC` | 10 | First 10 alphabetically |

---

### 3️⃣ **Logical Operators (AND, OR, NOT)**

#### Using AND:
```sql
SELECT * FROM books
WHERE category = 'science' AND price < 500;
```
✅ Returns books that are BOTH science category AND less than 500 price.

#### Using NOT:
```sql
SELECT * FROM books
WHERE NOT available_copies > 0;
```
✅ Returns books with NO available copies.

#### Using OR:
```sql
SELECT * FROM members
WHERE YEAR(membership_date) > '2020-01-01'
OR member_ID IN(
    SELECT member_ID
    FROM transactions
    GROUP BY member_ID
    HAVING COUNT(*) > 3
);
```
✅ Returns members who joined after 2020 OR borrowed more than 3 books.

---

### 4️⃣ **Grouping & Aggregation**

#### Books Borrowed by Member:
```sql
SELECT member_ID, COUNT(book_ID) AS total_borrow
FROM transactions
GROUP BY member_ID;
```

| member_ID | total_borrow |
|-----------|--------------|
| 1 | 1 |
| 2 | 1 |
| 3 | 1 |

#### Books by Category:
```sql
SELECT category, COUNT(*) AS total_books
FROM books
GROUP BY category;
```

| category | total_books |
|----------|-------------|
| Fantasy | 2 |
| Horror | 1 |
| Mystery | 1 |
| Fiction | 1 |

---

### 5️⃣ **Aggregate Functions**

| Function | Query | Purpose | Example Output |
|----------|-------|---------|-----------------|
| **COUNT** | `SELECT COUNT(*) AS total_books FROM books;` | Count total records | 5 |
| **AVG** | `SELECT AVG(price) AS AVG_price FROM books;` | Calculate average | 16.4 |
| **SUM** | `SELECT SUM(fine_amount) AS total_fines FROM transactions;` | Sum values | 2 |
| **MAX** | `SELECT MAX(price) AS max_price FROM books;` | Find maximum | 25 |
| **MIN** | `SELECT MIN(price) AS min_price FROM books;` | Find minimum | 10 |

#### Most Borrowed Book:
```sql
SELECT book_ID, COUNT(*) AS borrow_count
FROM transactions
GROUP BY book_ID
ORDER BY borrow_count DESC
LIMIT 1;
```

---

### 6️⃣ **JOIN Operations**

#### INNER JOIN (Match records in both tables):
```sql
SELECT books.title, authors.name
FROM books
INNER JOIN authors 
ON books.author_ID = authors.author_ID;
```

| title | name |
|-------|------|
| Harry Potter and the Sorcerers Stone | J.K. Rowling |
| The Shining | Stephen King |

---

#### LEFT JOIN (All from left, matching from right):
```sql
SELECT m.name, t.book_ID
FROM members m
LEFT JOIN transactions t
ON m.member_ID = t.member_ID;
```

---

#### RIGHT JOIN (All from right, matching from left):
```sql
SELECT b.title
FROM transactions t
RIGHT JOIN books b
ON t.book_ID = b.book_ID
WHERE t.book_ID IS NULL;
```

---

#### FULL OUTER JOIN (All records from both tables):
```sql
SELECT m.name, t.book_ID
FROM members m
LEFT JOIN transactions t
ON m.member_ID = t.member_ID
WHERE t.book_ID IS NULL

UNION

SELECT m.name, t.book_ID
FROM members m
RIGHT JOIN transactions t
ON m.member_ID = t.member_ID
WHERE t.book_ID IS NULL;
```

---

### 7️⃣ **Subqueries**

#### Books borrowed by members who joined after 2022:
```sql
SELECT * FROM books
WHERE book_ID IN(
    SELECT book_ID
    FROM transactions
    WHERE member_ID IN(
        SELECT member_ID
        FROM members
        WHERE YEAR(membership_date) > 2022
    )
);
```

#### Members who never borrowed a book:
```sql
SELECT * FROM members
WHERE member_ID NOT IN(
    SELECT DISTINCT member_ID FROM transactions
);
```

---

### 8️⃣ **Date & Time Functions**

| Function | Query | Result | Explanation |
|----------|-------|--------|-------------|
| **YEAR()** | `SELECT YEAR(published_date) FROM books;` | 1997, 1977, 1996... | Extracts year from date |
| **MONTH()** | `SELECT MONTH(borrow_date) FROM transactions;` | 1-12 | Extracts month number |
| **DATEDIFF()** | `SELECT DATEDIFF(return_date, borrow_date)` | Number of days | Calculates days between dates |
| **DATE_FORMAT()** | `SELECT DATE_FORMAT(borrow_date, '%d-%m-%y')` | 15-01-26 | Formats date as string |
| **CURDATE()** | `SELECT CURDATE()` | 2026-06-19 | Gets current date |

#### Extract Year from Published Date:
```sql
SELECT published_date,
YEAR(published_date) AS year_of_published
FROM books;
```

#### Date Difference Between Borrow and Return:
```sql
SELECT transaction_ID,
DATEDIFF(return_date, borrow_date) AS difference_in_days
FROM transactions;
```

#### Format Borrow Date as DD-MM-YYYY:
```sql
SELECT borrow_date,
DATE_FORMAT(borrow_date, '%d-%m-%y') AS formatted_date
FROM transactions;
```

---

### 9️⃣ **String Manipulation Functions**

| Function | Query | Purpose | Example |
|----------|-------|---------|---------|
| **UPPER()** | `SELECT UPPER(title) FROM books;` | Convert to uppercase | HARRY POTTER |
| **LOWER()** | `SELECT LOWER(name) FROM authors;` | Convert to lowercase | j.k. rowling |
| **TRIM()** | `SELECT TRIM(name) FROM authors;` | Remove spaces | JK Rowling |
| **LENGTH()** | `SELECT LENGTH(title) FROM books;` | Get string length | 42 |
| **REPLACE()** | `SELECT REPLACE(email, '@', '[AT]')` | Replace characters | user[AT]example.com |
| **SUBSTRING()** | `SELECT SUBSTRING(title, 1, 10)` | Extract portion | Harry Pott |

#### Replace NULL with 'Not Provided':
```sql
SELECT 
    member_ID, 
    email, 
    REPLACE(email, 'NULL', 'Not Provided') AS replace_email
FROM members;
```

---

### 🔟 **Window Functions**

#### Rank Books by ID:
```sql
SELECT book_ID,
RANK() OVER (ORDER BY book_ID DESC) AS rank_position
FROM transactions
GROUP BY book_id;
```

| book_ID | rank_position |
|---------|--------------|
| 105 | 1 |
| 104 | 2 |
| 103 | 3 |

#### Cumulative Borrow Count:
```sql
SELECT member_id,
borrow_date,
COUNT(*) OVER (PARTITION BY member_id 
ORDER BY borrow_date) AS cumulative_borrow
FROM transactions;
```

---

### 1️⃣1️⃣ **CASE Expressions**

#### Assign Membership Status:
```sql
SELECT member_id,
CASE
    WHEN MAX(borrow_date) >= DATE_SUB(CURDATE(), INTERVAL 6 MONTH)
    THEN 'Active'
    ELSE 'Inactive'
END AS Membership_Status
FROM transactions
GROUP BY member_id;
```

| member_id | Membership_Status |
|-----------|------------------|
| 1 | Active |
| 2 | Active |
| 3 | Inactive |

#### Categorize Books by Publication Date:
```sql
SELECT title,
CASE
    WHEN published_date > 2020 THEN 'New Arrival'
    WHEN published_date < 2000 THEN 'Classic'
    ELSE 'Regular'
END AS Book_Category
FROM books;
```

| title | Book_Category |
|-------|--------------|
| Harry Potter and the Sorcerers Stone | Classic |
| The Shining | Classic |
| A Game of Thrones | Regular |

---

## 🛠️ Setup Instructions

### Step 1: Create Database
```sql
CREATE DATABASE practical_pr;
USE practical_pr;
```

### Step 2: Create Tables
Execute the table creation scripts from the project file in the following order:
1. Authors Table (no dependencies)
2. Books Table (depends on Authors)
3. Members Table (no dependencies)
4. Transactions Table (depends on Books and Members)

### Step 3: Insert Sample Data
Insert the provided sample data into each table.

### Step 4: Run Queries
Test all queries provided in the project documentation.

---

## 📝 Query Examples

### Quick Reference

<details>
<summary><strong>🔍 Find All Available Books</strong></summary>

```sql
SELECT * FROM books
WHERE available_copies > 0;
```
</details>

<details>
<summary><strong>📊 Count Total Books by Category</strong></summary>

```sql
SELECT category, COUNT(*) AS total_books
FROM books
GROUP BY category;
```
</details>

<details>
<summary><strong>💰 Calculate Average Book Price</strong></summary>

```sql
SELECT AVG(price) AS average_price
FROM books;
```
</details>

<details>
<summary><strong>📚 Get Book Details with Author Names</strong></summary>

```sql
SELECT b.title, a.name, b.price
FROM books b
INNER JOIN authors a 
ON b.author_ID = a.author_ID;
```
</details>

<details>
<summary><strong>🚫 Find Members Who Never Borrowed</strong></summary>

```sql
SELECT * FROM members
WHERE member_ID NOT IN(
    SELECT DISTINCT member_ID FROM transactions
);
```
</details>

<details>
<summary><strong>⏰ Check Books Not Returned</strong></summary>

```sql
SELECT * FROM transactions
WHERE return_date IS NULL;
```
</details>

---

## 📌 Key Relationships

```
Books ──┬── author_ID ──→ Authors
        │
        └── book_ID ──→ Transactions ──member_ID──→ Members
```

- **Books → Authors**: One-to-Many (One author can write many books)
- **Books → Transactions**: One-to-Many (One book can have multiple transactions)
- **Members → Transactions**: One-to-Many (One member can borrow multiple books)

---

## 🎓 Learning Outcomes

After working with this project, you'll understand:
- ✅ Database design with proper normalization
- ✅ Creating and managing relationships with primary/foreign keys
- ✅ CRUD operations in SQL
- ✅ Complex JOIN operations
- ✅ Aggregate functions and grouping
- ✅ Subqueries and nested queries
- ✅ Date/Time and String functions
- ✅ Window functions for analytics
- ✅ Conditional logic with CASE statements
- ✅ Real-world database scenarios

---

## 📄 File Reference

📁 **Project File:** `smart_library_management_system.txt`

---

## 🤝 Contributing

Feel free to extend this project by adding:
- Additional tables (Reviews, Ratings, Reservations)
- More complex queries
- Stored procedures
- Triggers for automation
- Views for common queries
- 
---


