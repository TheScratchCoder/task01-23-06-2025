# task01-23-06-2025
Using MySQL WORKBENCH , I have worked on database creation, table creation, and relationship definitions for a Library Management

## Library Database Management

### Database Creation

```
CREATE DATABASE LibraryDB;
USE LibraryDB;
```

### Table Creation

#### 1. Books Table

-Stores information about each book. <br>
-Fields: BookID, Title, ISBN, Publisher, YearPublished, Genre, CopiesAvailable.

```
CREATE TABLE Books (
    BookID INT PRIMARY KEY AUTO_INCREMENT,
    Title VARCHAR(255) NOT NULL,
    ISBN VARCHAR(20) UNIQUE,
    Publisher VARCHAR(100),
    YearPublished INT,
    Genre VARCHAR(50),
    CopiesAvailable INT DEFAULT 0
);
```

#### 2. Authors

-Stores data of authors. <br>
-Fields: AuthorID, FirstName, LastName.

```
CREATE TABLE Authors (
    AuthorID INT PRIMARY KEY AUTO_INCREMENT,
    FirstName VARCHAR(100),
    LastName VARCHAR(100)
);
```


#### 3. BookAuthors

-Handles many-to-many relationship between Books and Authors. <br>
-Composite Primary Key: BookID, AuthorID.

```
CREATE TABLE BookAuthors (
    BookID INT,
    AuthorID INT,
    PRIMARY KEY (BookID, AuthorID),
    FOREIGN KEY (BookID) REFERENCES Books(BookID),
    FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID)
);
```


#### 4. Members

-Holds member (user) information. <br>
-Fields: MemberID, FullName, Email, Phone, Address, MembershipDate.

```
CREATE TABLE Members (
    MemberID INT PRIMARY KEY AUTO_INCREMENT,
    FullName VARCHAR(100),
    Email VARCHAR(100) UNIQUE,
    Phone VARCHAR(15),
    Address TEXT,
    MembershipDate DATE
);
```


#### 5. Staff

-Staff managing loans, returns, etc. <br>
-Fields: StaffID, FullName, Role, Email.

```
CREATE TABLE Staff (
    StaffID INT PRIMARY KEY AUTO_INCREMENT,
    FullName VARCHAR(100),
    Role VARCHAR(50),
    Email VARCHAR(100) UNIQUE
);
```


#### 6. Loans (Tracks borrowed books)

-Records which book is loaned to which member. <br>
-Fields: LoanID, BookID, MemberID, StaffID, LoanDate, DueDate, ReturnDate.

```
CREATE TABLE Loans (
    LoanID INT PRIMARY KEY AUTO_INCREMENT,
    BookID INT,
    MemberID INT,
    StaffID INT,
    LoanDate DATE,
    DueDate DATE,
    ReturnDate DATE,
    FOREIGN KEY (BookID) REFERENCES Books(BookID),
    FOREIGN KEY (MemberID) REFERENCES Members(MemberID),
    FOREIGN KEY (StaffID) REFERENCES Staff(StaffID)
);
```

#### 7.Fines (Late returns)

-Manages fines for late returns. <br>
-Fields: FineID, LoanID, Amount, Paid.

```
CREATE TABLE Fines (
    FineID INT PRIMARY KEY AUTO_INCREMENT,
    LoanID INT,
    Amount DECIMAL(10, 2),
    Paid BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (LoanID) REFERENCES Loans(LoanID)
);
```

