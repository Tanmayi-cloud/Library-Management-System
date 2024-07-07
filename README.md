# Library-Management-System
A Library Management System (LMS) is a software application designed to help libraries manage their collections and interactions with patrons efficiently
CREATE DATABASE IF NOT EXISTS books;
USE books;

CREATE TABLE Books (
  Book_ID varchar(10) PRIMARY KEY,
  Title varchar(100),
  Author VARCHAR(100),
  ISBN varchar(100),
  Genre VARCHAR(50),
  Publisher VARCHAR(50),
  Publication_Date DATE
);

CREATE TABLE Branch (
  Branch_ID varchar(10) PRIMARY KEY,
  Branch_Name VARCHAR(50),
  House_No VARCHAR(10),
  Lane VARCHAR(50),
  Address1 VARCHAR(50),
  Address2 VARCHAR(50),
  City VARCHAR(50),
  State VARCHAR(50),
  Pincode VARCHAR(10),
  Phone_Number VARCHAR(20),
  Email VARCHAR(50)
);

CREATE TABLE Book_Copies (
  Copy_ID varchar(10) PRIMARY KEY,
  Book_ID varchar(10),
  Branch_ID varchar(10),
  Status VARCHAR(20),
  Due_Date DATE,
  FOREIGN KEY (Book_ID) REFERENCES Books(Book_ID),
  FOREIGN KEY (Branch_ID) REFERENCES Branch(Branch_ID)
);

CREATE TABLE Members (
  Member_ID varchar(10) PRIMARY KEY,
  First_Name VARCHAR(50),
  Last_Name VARCHAR(50),
  Phone_Number VARCHAR(20),
  Email VARCHAR(50),
  House_No VARCHAR(10),
  Lane VARCHAR(50),
  Address1 VARCHAR(50),
  Address2 VARCHAR(50),
  City VARCHAR(50),
  State VARCHAR(50),
  Pincode VARCHAR(10),
  Membership_Expiration_Date DATE
);

CREATE TABLE Checkout (
  Checkout_ID varchar(10) PRIMARY KEY,
  Member_ID varchar(10),
  Copy_ID varchar(10),
  Checkout_Date DATE,
  Due_Date DATE,
  Return_Date DATE,
  FOREIGN KEY (Member_ID) REFERENCES Members(Member_ID),
  FOREIGN KEY (Copy_ID) REFERENCES Book_Copies(Copy_ID)
);

CREATE TABLE Fine (
  Fine_ID varchar(10) PRIMARY KEY,
  Member_ID varchar(10),
  Copy_ID varchar(10),
  Fine_Amount DECIMAL(10, 2),
  Fine_Date DATE,
  Status VARCHAR(20),
  FOREIGN KEY (Member_ID) REFERENCES Members(Member_ID),
  FOREIGN KEY (Copy_ID) REFERENCES Book_Copies(Copy_ID)
);


CREATE TABLE Inventory (
  Inventory_ID varchar(10) PRIMARY KEY,
  Branch_ID varchar(10),
  Book_ID varchar(10),
  Quantity INT,
  Date_Added DATE,
  Date_Modified DATE,
  FOREIGN KEY (Branch_ID) REFERENCES Branch(Branch_ID),
  FOREIGN KEY (Book_ID) REFERENCES Books(Book_ID)
);

CREATE TABLE Job_Roles (
  Role_ID varchar(10) PRIMARY KEY,
  Role_Name VARCHAR(50),
  Salary DECIMAL(10, 2)
);
-- Insert data into Books table
INSERT INTO Books (Book_ID, Title, Author, ISBN, Genre, Publisher, Publication_Date)
VALUES ('B001', 'The Great Gatsby', 'F. Scott Fitzgerald', '9780743273565', 'Classic', 'Scribner', '1925-04-10'),
       ('B002', 'To Kill a Mockingbird', 'Harper Lee', '9780061120084', 'Fiction', 'Harper Perennial Modern Classics', '1960-07-11'),
       ('B003', '1984', 'George Orwell', '9780451524935', 'Dystopian', 'Signet Classic', '1949-06-08');

-- Insert data into Branch table
INSERT INTO Branch (Branch_ID, Branch_Name, House_No, Lane, Address1, Address2, City, State, Pincode, Phone_Number, Email)
VALUES ('BR001', 'Main Branch', '123', 'Main Street', 'Central Plaza', '', 'Metropolis', 'Metro', '12345', '123-456-7890', 'info@mainbranch.com'),
       ('BR002', 'West Branch', '456', 'West Avenue', 'West Plaza', '', 'West City', 'Western', '54321', '987-654-3210', 'info@westbranch.com');

-- Insert data into Book_Copies table
INSERT INTO Book_Copies (Copy_ID, Book_ID, Branch_ID, Status, Due_Date)
VALUES ('C001', 'B001', 'BR001', 'Available', NULL),
       ('C002', 'B001', 'BR002', 'Checked Out', '2024-05-05'),
       ('C003', 'B002', 'BR001', 'Available', NULL),
       ('C004', 'B003', 'BR002', 'Available', NULL);

-- Insert data into Members table
INSERT INTO Members (Member_ID, First_Name, Last_Name, Phone_Number, Email, House_No, Lane, Address1, Address2, City, State, Pincode, Membership_Expiration_Date)
VALUES ('M001', 'John', 'Doe', '123-456-7890', 'john.doe@example.com', '101', 'Elm Street', '', '', 'Springfield', 'SP', '12345', '2025-01-01'),
       ('M002', 'Jane', 'Smith', '987-654-3210', 'jane.smith@example.com', '202', 'Oak Avenue', '', '', 'Riverside', 'RS', '54321', '2024-12-31');

-- Insert data into Checkout table
INSERT INTO Checkout (Checkout_ID, Member_ID, Copy_ID, Checkout_Date, Due_Date, Return_Date)
VALUES ('CH001', 'M001', 'C001', '2024-04-28', '2024-05-05', NULL),
       ('CH002', 'M002', 'C003', '2024-04-29', '2024-05-06', NULL);

-- Insert data into Fine table
INSERT INTO Fine (Fine_ID, Member_ID, Copy_ID, Fine_Amount, Fine_Date, Status)
VALUES ('F001', 'M001', 'C002', 5.00, '2024-05-01', 'Unpaid'),
       ('F002', 'M002', 'C003', 0.00, NULL, 'Paid');

-- Insert data into Inventory table
INSERT INTO Inventory (Inventory_ID, Branch_ID, Book_ID, Quantity, Date_Added, Date_Modified)
VALUES ('INV001', 'BR001', 'B001', 5, '2024-04-28', '2024-04-28'),
       ('INV002', 'BR001', 'B002', 3, '2024-04-29', '2024-04-29'),
       ('INV003', 'BR002', 'B001', 2, '2024-04-30', '2024-04-30');

-- Insert data into Job_Roles table
INSERT INTO Job_Roles (Role_ID, Role_Name, Salary)
VALUES ('R001', 'Librarian', 50000.00),
       ('R002', 'Clerk', 35000.00);
SELECT * FROM Books;
SELECT Author,Title, ISBN,Genre, Publisher FROM Books where Author="Harper Lee";
SELECT Book_ID,Title,ISBN,Genre,Publisher,Publication where Genre="Classic";
SELECT * FROM Branch;
SELECT * FROM Book_Copies;
SELECT * FROM Members;
SELECT * FROM Checkout;
SELECT * FROM Fine;
SELECT * FROM Inventory;
SELECT * FROM Job_Roles;
