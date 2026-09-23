
# 📚 Library Management System — PostgreSQL

<img src="https://socialify.git.ci/Samukelokhathi/Code-Tribe-Library-Management-System-PostgreSQL-/image?language=1&owner=1&name=1&stargazers=1&theme=Light" alt="Code-Tribe-Library-Management-System-PostgreSQL-" width="640" height="320" />

This project focuses on understanding how databases work, creating tables, inserting records, retrieving information, updating data, deleting records, and performing advanced SQL queries.
---

## 🚀 Project Overview

The Library Management System is a database application designed to manage a library's collection of books, authors, and patrons.

The system allows users to:

- Add new books and authors.
- View existing records.
- Update book availability.
- Manage patron borrowing records.
- Delete records.
- Perform advanced SQL queries.

The project uses PostgreSQL as the database management system and pgAdmin 4 to execute and manage SQL queries.

---

## 🎯 Use-Case Scenario

Imagine a library that needs to keep track of its books, authors, and patrons.

A librarian should be able to:

- Add new books to the library.
- Register authors.
- View available books.
- Search for books by title or author.
- Mark books as borrowed or returned.
- Update patron borrowing records.
- Remove outdated records.
- Run SQL queries to analyze library information.

## 🚀 Getting Started

### Clone the Repository

```bash
git clone https://github.com/Samukelokhathi/Code-Tribe-Library-Management-System-PostgreSQL-
```

### Navigate into the Project

```bash
cd Code-Tribe-Library-Management-System-PostgreSQL-
```
# 💻 Installation and Setup

## 1. Install PostgreSQL

Download PostgreSQL from the official website:

🔗 https://www.postgresql.org/download/

### Windows Installation

1. Open the PostgreSQL download page.
2. Select Windows.
3. Download the PostgreSQL installer.
4. Run the installer.
5. Follow the installation instructions.
6. Select the PostgreSQL Server and pgAdmin 4 components if offered.
7. Set a password for the PostgreSQL database superuser.
8. Keep note of the password you create.
9. Complete the installation.

### 🔐 Create a PostgreSQL Password

During installation, PostgreSQL asks you to create a password for the database superuser, commonly named `postgres`.

Example:

```text
Username: postgres
Password: YOUR_OWN_PASSWORD
Port: 5432
```

## 2. Open pgAdmin 4

After installing PostgreSQL:

1. Open pgAdmin 4.
2. Find the PostgreSQL server in the Browser panel.
3. Click on the server.
4. Enter the password you created during installation.
5. Connect to the PostgreSQL server.

If the server is not connected, ensure that the PostgreSQL service is running.

---

## 3. Open Query Tool

1. Expand the PostgreSQL server.
2. Right-click on the Databases section.
3. Select **Query Tool** after connecting to a suitable database.
4. Use the SQL editor to execute your commands.

---

## 🗄️ Database Setup Using pgAdmin 4

### 1. Create a Database

Open pgAdmin 4 and create a new database named `LibraryDB`.

Alternatively, run the following SQL command:

```sql
CREATE DATABASE LibraryDB;
```

Connect to the `LibraryDB` database and open the Query Tool.

### 2. Create Database Tables

The system uses three main tables:

- Authors
- Books
- Patrons

#### Authors Table

```sql
CREATE TABLE IF NOT EXISTS Authors(
    id SERIAL PRIMARY KEY,
    name VARCHAR(255),
    nationality VARCHAR(255),
    birth_year INT,
    death_year INT
);
```

#### Books Table

```sql
CREATE TABLE IF NOT EXISTS Books(
    id SERIAL PRIMARY KEY,
    title VARCHAR(255),
    genres TEXT[],
    published_year INT,
    available BOOL,
    author_id INT REFERENCES Authors(id)
);
```

#### Patrons Table

```sql
CREATE TABLE IF NOT EXISTS Patrons(
    id SERIAL PRIMARY KEY,
    name VARCHAR(255),
    email VARCHAR(255),
    borrowed_books INT[] DEFAULT ARRAY[]::INT[]
);
```

## 📚 Database Relationships

```text
Authors
   │
   │ author_id
   ▼
Books

Patrons
   │
   │ borrowed_books
   ▼
Books (IDs)
```

> The `Books.author_id` column references `Authors.id`. The `Patrons.borrowed_books` column stores book IDs in an integer array.

## 🏃‍♂️ Project Sprints

### Sprint 1: Project Setup

- Create the PostgreSQL database.
- Open the database in pgAdmin 4.
- Create the Authors, Books, and Patrons tables.
- Define primary keys and foreign key relationships.


# 📥 Sprint 2: Insert Data

## 1. Insert Authors

```sql
INSERT INTO authors
(id, name, nationality, birth_year, death_year)
VALUES
(1, 'George Orwell', 'British', 1903, 1950),
(2, 'Harper Lee', 'American', 1926, 2016),
(3, 'F. Scott Fitzgerald', 'American', 1896, 1940),
(4, 'Aldous Huxley', 'British', 1894, 1963),
(5, 'J.D. Salinger', 'American', 1919, 2010),
(6, 'Herman Melville', 'American', 1819, 1891),
(7, 'Jane Austen', 'British', 1775, 1817),
(8, 'Leo Tolstoy', 'Russian', 1828, 1910),
(9, 'Fyodor Dostoevsky', 'Russian', 1821, 1881),
(10, 'J.R.R. Tolkien', 'British', 1892, 1973);
```

## 2. Insert Books

```sql
INSERT INTO books
(id, title, author_id, genres, published_year, available)
VALUES
(1, '1984', 1, ARRAY['Dystopian', 'Political Fiction'], 1949, TRUE),
(2, 'To Kill a Mockingbird', 2, ARRAY['Southern Gothic', 'Bildungsroman'], 1960, TRUE),
(3, 'The Great Gatsby', 3, ARRAY['Tragedy'], 1925, TRUE),
(4, 'Brave New World', 4, ARRAY['Dystopian', 'Science Fiction'], 1932, TRUE),
(5, 'The Catcher in the Rye', 5, ARRAY['Realist Novel', 'Bildungsroman'], 1951, TRUE),
(6, 'Moby-Dick', 6, ARRAY['Adventure Fiction'], 1851, TRUE),
(7, 'Pride and Prejudice', 7, ARRAY['Romantic Novel'], 1813, TRUE),
(8, 'War and Peace', 8, ARRAY['Historical Novel'], 1869, TRUE),
(9, 'Crime and Punishment', 9, ARRAY['Philosophical Novel'], 1866, TRUE),
(10, 'The Hobbit', 10, ARRAY['Fantasy'], 1937, TRUE);
```

## 3. Insert Patrons

```sql
INSERT INTO patrons
(id, name, email, borrowed_books)
VALUES
(1, 'Alice Johnson', 'alice@example.com', ARRAY[]::INT[]),
(2, 'Bob Smith', 'bob@example.com', ARRAY[1, 2]),
(3, 'Carol White', 'carol@example.com', ARRAY[]::INT[]),
(4, 'David Brown', 'david@example.com', ARRAY[3]),
(5, 'Eve Davis', 'eve@example.com', ARRAY[]::INT[]),
(6, 'Frank Moore', 'frank@example.com', ARRAY[4, 5]),
(7, 'Grace Miller', 'grace@example.com', ARRAY[]::INT[]),
(8, 'Hank Wilson', 'hank@example.com', ARRAY[6]),
(9, 'Ivy Taylor', 'ivy@example.com', ARRAY[]::INT[]),
(10, 'Jack Anderson', 'jack@example.com', ARRAY[7, 8]);
```

---

# 🔍 Sprint 3: Read Operations (Queries)

## 1. Get All Books

```sql
SELECT * FROM Books;
```

## 2. Get a Book by Title

```sql
SELECT * FROM Books
WHERE title = 'Brave New World';
```

## 3. Get a Book by ID

```sql
SELECT * FROM Books
WHERE id = 4;
```

## 4. Get All Books by a Specific Author

```sql
SELECT * FROM Books
WHERE author_id = 2;
```

## 5. Get All Available Books

```sql
SELECT * FROM Books
WHERE available = TRUE;
```

## 6. View All Authors

```sql
SELECT * FROM Authors;
```

## 7. View All Patrons

```sql
SELECT * FROM Patrons;
```

---

# ✏️ Sprint 4: Update Operations

## 1. Mark a Book as Borrowed

Set the book's availability to false.

```sql
UPDATE Books
SET available = FALSE
WHERE id = 2;
```

## 2. Mark a Book as Returned

Set the book's availability to true.

```sql
UPDATE Books
SET available = TRUE
WHERE id = 2;
```

## 3. Add a New Genre

Add a new genre to an existing book.

```sql
UPDATE Books
SET genres = array_append(genres, 'Fiction')
WHERE id = 3;
```

## 4. Add a Borrowed Book to a Patron

```sql
UPDATE Patrons
SET borrowed_books = array_append(borrowed_books, 2)
WHERE id = 1;
```

## 5. View the Updated Record

```sql
SELECT * FROM Patrons
WHERE id = 1;
```

---

# 🗑️ Sprint 5: Delete Operations

## 1. Delete a Book by Title

```sql
DELETE FROM Books
WHERE title = '1984';
```

## 2. Delete an Author by ID

```sql
DELETE FROM Authors
WHERE id = 2;
```

> **Important:** An author referenced by a book cannot normally be deleted while the foreign key relationship is still present. Handle dependent book records first or use an appropriate foreign key deletion strategy.

---

# 🧠 Sprint 6: Advanced Queries

## 1. Find Books Published After 1950

```sql
SELECT * FROM Books
WHERE published_year > 1950;
```

## 2. Find All American Authors

```sql
SELECT * FROM Authors
WHERE nationality = 'American';
```

## 3. Set All Books as Available

```sql
UPDATE Books
SET available = TRUE;
```

## 4. Find Available Books Published After 1950

```sql
SELECT * FROM Books
WHERE available = TRUE
AND published_year > 1950;
```

## 5. Find Authors Whose Names Contain "George"

```sql
SELECT * FROM Authors
WHERE name ILIKE '%George%';
```

## 6. Increment the Published Year 1869 by 1

```sql
UPDATE Books
SET published_year = 1870
WHERE published_year = 1869;
```

---


## 🛠️ Technologies Used

- PostgreSQL
- SQL
- pgAdmin 4
- Relational Database Management
- Git & GitHub


# 📚 What I Learned

During this project, I practiced:

- Installing PostgreSQL and using pgAdmin 4.
- Creating and managing databases.
- Creating relational tables.
- Understanding primary keys and foreign keys.
- Inserting records using SQL.
- Retrieving data using SELECT queries.
- Updating and deleting records.
- Working with PostgreSQL arrays.
- Filtering data using WHERE conditions.
- Searching text using ILIKE.
- Using logical operators such as AND.
- Understanding database relationships.
- Working with SQL CRUD operations.
- Managing database data integrity.
- Building a foundation for backend development.

---

# 🎯 Project Goals

The main goals of this project are to:

- Strengthen my SQL and PostgreSQL knowledge.
- Understand relational database management.
- Practice creating and manipulating tables.
- Learn how foreign keys work.
- Improve my database querying skills.
- Understand CRUD operations.
- Connect database knowledge with backend API development.
- Build a foundation for full-stack development.

---

# 📖 My Learning Journey

This project forms part of my transition from frontend development into backend and database development.

```text
JavaScript
    ↓
TypeScript
    ↓
Node.js
    ↓
REST APIs
    ↓
SQL
    ↓
PostgreSQL
    ↓
Database Management
    ↓
Backend Development
    ↓
Full-Stack Development 🚀
```

---

# 🔗 Project Links

- 🔗 **GitHub Repository:** https://github.com/Samukelokhathi/Code-Tribe-Library-Management-System-PostgreSQL-
- 🔗 **GitHub Profile:** https://github.com/Samukelokhathi
- 🔗 **PostgreSQL:** https://www.postgresql.org/
- 🔗 **pgAdmin 4:** https://www.pgadmin.org/

---


<div align="center">

### 💻 Keep Learning. Keep Building. Keep Improving. 🚀

Built with ❤️ by **Samukelo Khathi**

</div>
