# task01-23-06-2025
Using MySQL WORKBENCH , I have worked on database creation, table creation, and relationship definitions for a Library Management

## Library Database Management

### Database Creation

```
CREATE DATABASE LibraryDB;
USE LibraryDB;
```

### Table Creation

#### Books Table

-Stores information about each book. <br>
-Fields: BookID, Title, ISBN, Publisher, YearPublished, Genre, CopiesAvailable.

<code>
CREATE TABLE Books (
    BookID INT PRIMARY KEY AUTO_INCREMENT,
    Title VARCHAR(255) NOT NULL,
    ISBN VARCHAR(20) UNIQUE,
    Publisher VARCHAR(100),
    YearPublished INT,
    Genre VARCHAR(50),
    CopiesAvailable INT DEFAULT 0
);
</code>
