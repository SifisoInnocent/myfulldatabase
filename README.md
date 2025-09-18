
# Library Management System Database

## Overview
This project implements a **relational database** for a Library Management System using **MySQL**.  
The database is designed to store information about library members, books, and borrowing records while ensuring data integrity and reducing redundancy.

---

## Database Design

### Tables

1. **Members**
   - `memberID` (INT, PRIMARY KEY, AUTO_INCREMENT)
   - `firstName` (VARCHAR, NOT NULL)
   - `lastName` (VARCHAR, NOT NULL)
   - `email` (VARCHAR, UNIQUE, NOT NULL)
   - `phone` (VARCHAR)

2. **Books**
   - `bookID` (INT, PRIMARY KEY, AUTO_INCREMENT)
   - `title` (VARCHAR, NOT NULL)
   - `author` (VARCHAR, NOT NULL)
   - `isbn` (VARCHAR, UNIQUE, NOT NULL)
   - `publishedYear` (INT)

3. **BorrowRecords**
   - `borrowID` (INT, PRIMARY KEY, AUTO_INCREMENT)
   - `memberID` (INT, FOREIGN KEY → Members.memberID)
   - `bookID` (INT, FOREIGN KEY → Books.bookID)
   - `borrowDate` (DATE, NOT NULL)
   - `returnDate` (DATE, NULL)
   - UNIQUE constraint on (`memberID`, `bookID`, `borrowDate`) to prevent duplicate borrowing on the same day

4. **Optional: BookAuthors** (for Many-to-Many relationships)
   - `bookID` (INT, FOREIGN KEY → Books.bookID)
   - `authorID` (INT, FOREIGN KEY → Authors.authorID)
   - PRIMARY KEY (`bookID`, `authorID`)

---

## Features

- **Primary and Foreign Keys** enforce data integrity.
- **One-to-Many relationships**:
  - Members → BorrowRecords
  - Books → BorrowRecords
- Optional **Many-to-Many relationships** for books and authors.
- **Constraints**:
  - NOT NULL: ensures required fields are always provided.
  - UNIQUE: prevents duplicate emails or ISBN numbers.

---

## How to Use

1. **Open MySQL Workbench** (or another MySQL environment).  
2. **Create the database and tables** by running the `answers.sql` file:

```sql
SOURCE /path/to/answers.sql;
