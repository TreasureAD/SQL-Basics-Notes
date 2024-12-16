## **Chapter 1: Introduction to Databases and SQL**

### Key Points:
- **What is SQL**: SQL (Structured Query Language) is used to interact with relational databases.
- **Relational Databases**: Organize data into tables (rows and columns).
- **Basic SQL Commands**:
  - `CREATE DATABASE`
  - `CREATE TABLE`
  - `INSERT INTO`
  - `SELECT`

### Example:
1. Create a database and a table:
   ```sql
   CREATE DATABASE LibraryDB;

   USE LibraryDB;

   CREATE TABLE Books (
       BookID INT AUTO_INCREMENT PRIMARY KEY,
       Title VARCHAR(255),
       Author VARCHAR(255),
       PublishedYear INT
   );
   ```

2. Insert data into the table:
   ```sql
   INSERT INTO Books (Title, Author, PublishedYear) VALUES 
   ('The Great Gatsby', 'F. Scott Fitzgerald', 1925),
   ('1984', 'George Orwell', 1949);
   ```

3. Retrieve data:
   ```sql
   SELECT * FROM Books;
   ```

---

## **Chapter 2: Querying Data**

### Key Points:
- **SELECT Statements**:
  - Retrieve specific columns using `SELECT column_name`.
  - Filter rows using `WHERE` conditions.
- **Logical Operators**: `AND`, `OR`, `NOT`.
- **Comparison Operators**: `=`, `>`, `<`, `>=`, `<=`, `<>`.

### Example:
1. Retrieve books published after 1930:
   ```sql
   SELECT Title, Author FROM Books 
   WHERE PublishedYear > 1930;
   ```

2. Use `AND` to add more conditions:
   ```sql
   SELECT * FROM Books 
   WHERE PublishedYear > 1930 AND Author = 'George Orwell';
   ```

---

## **Chapter 3: Filtering and Sorting Data**

### Key Points:
- **ORDER BY**: Sort results (ascending `ASC` or descending `DESC`).
- **LIMIT**: Restrict the number of rows returned.
- **LIKE**: Use wildcard `%` for pattern matching.

### Example:
1. Sort books alphabetically:
   ```sql
   SELECT * FROM Books 
   ORDER BY Title ASC;
   ```

2. Find books with titles starting with 'The':
   ```sql
   SELECT * FROM Books 
   WHERE Title LIKE 'The%';
   ```

3. Retrieve only the top 2 rows:
   ```sql
   SELECT * FROM Books 
   LIMIT 2;
   ```

---

## **Chapter 4: Aggregate Functions and Grouping Data**

### Key Points:
- **Aggregate Functions**:
  - `COUNT()`: Count rows.
  - `SUM()`: Calculate total.
  - `AVG()`: Calculate average.
  - `MAX()`, `MIN()`: Find max and min values.
- **GROUP BY**: Group results by a column.
- **HAVING**: Filter grouped results.

### Example:
1. Count total books:
   ```sql
   SELECT COUNT(*) AS TotalBooks FROM Books;
   ```

2. Find the earliest and latest published years:
   ```sql
   SELECT MIN(PublishedYear) AS Earliest, MAX(PublishedYear) AS Latest 
   FROM Books;
   ```

3. Group by author and count books:
   ```sql
   SELECT Author, COUNT(*) AS BookCount 
   FROM Books 
   GROUP BY Author;
   ```

---

## **Chapter 5: Modifying Data**

### Key Points:
- **UPDATE**: Modify existing rows.
- **DELETE**: Remove rows.
- **TRUNCATE**: Remove all rows but keep the table.

### Example:
1. Update a book's published year:
   ```sql
   UPDATE Books 
   SET PublishedYear = 1926 
   WHERE Title = 'The Great Gatsby';
   ```

2. Delete a specific row:
   ```sql
   DELETE FROM Books 
   WHERE Title = '1984';
   ```

3. Delete all data in the table:
   ```sql
   TRUNCATE TABLE Books;
   ```

---

## **Chapter 6: Relationships and Joins**

### Key Points:
- **Primary Key**: A unique identifier for each record in a table.
- **Foreign Key**: Links two tables together.
- **Joins**:
  - `INNER JOIN`: Matches rows in both tables.
  - `LEFT JOIN`: Returns all rows from the left table, matching rows from the right.
  - `RIGHT JOIN`: Returns all rows from the right table.

### Example:
1. Create two tables with a relationship:
   ```sql
   CREATE TABLE Authors (
       AuthorID INT AUTO_INCREMENT PRIMARY KEY,
       AuthorName VARCHAR(255)
   );

   CREATE TABLE Books (
       BookID INT AUTO_INCREMENT PRIMARY KEY,
       Title VARCHAR(255),
       AuthorID INT,
       FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID)
   );
   ```

2. Insert data into the tables:
   ```sql
   INSERT INTO Authors (AuthorName) VALUES 
   ('F. Scott Fitzgerald'), 
   ('George Orwell');

   INSERT INTO Books (Title, AuthorID) VALUES 
   ('The Great Gatsby', 1),
   ('1984', 2);
   ```

3. Use an `INNER JOIN` to display books with their authors:
   ```sql
   SELECT Books.Title, Authors.AuthorName 
   FROM Books
   INNER JOIN Authors ON Books.AuthorID = Authors.AuthorID;
   ```

4. Use a `LEFT JOIN` to show all authors, even those without books:
   ```sql
   SELECT Authors.AuthorName, Books.Title 
   FROM Authors
   LEFT JOIN Books ON Books.AuthorID = Authors.AuthorID;
   ```
