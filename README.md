RDBMS Concepts Repository

This repository contains all fundamental concepts of Relational Database Management Systems (RDBMS) along with their SQL implementations. It serves as a comprehensive reference for learning and practicing RDBMS concepts.

📌 Topics Covered

Introduction to RDBMS

Data Types in SQL

Constraints (Primary Key, Foreign Key, Unique, Not Null, Check, Default)

SQL Queries (SELECT, INSERT, UPDATE, DELETE)

Joins (INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN, SELF JOIN, CROSS JOIN)

Aggregation Functions (COUNT, SUM, AVG, MIN, MAX, GROUP BY, HAVING)

Subqueries

Views

Stored Procedures

Triggers

Indexes

Transactions & ACID Properties

Normalization (1NF, 2NF, 3NF, BCNF, 4NF, 5NF)

Denormalization

ER Model & Relational Schema

SQL Functions (String, Date, Numeric)

User Management & Permissions

Backup & Restore

🔥 SQL Implementations for Each Concept

-- 1. Create a Sample Table
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Age INT CHECK (Age > 0),
    City VARCHAR(50),
    AdmissionDate DATE DEFAULT CURRENT_DATE
);

-- 2. Insert Sample Data
INSERT INTO Students (StudentID, Name, Age, City) VALUES
(1, 'Alice', 22, 'New York'),
(2, 'Bob', 25, 'Los Angeles'),
(3, 'Charlie', 20, 'Chicago');

-- 3. Select Data
SELECT * FROM Students;

-- 4. Using Aggregate Functions
SELECT City, COUNT(StudentID) AS TotalStudents
FROM Students
GROUP BY City;

-- 5. Using Joins (Example with Courses Table)
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(100),
    StudentID INT,
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID)
);

INSERT INTO Courses (CourseID, CourseName, StudentID) VALUES
(101, 'Database Systems', 1),
(102, 'Web Development', 2),
(103, 'Machine Learning', 3);

SELECT Students.Name, Courses.CourseName 
FROM Students 
INNER JOIN Courses ON Students.StudentID = Courses.StudentID;

-- 6. Creating a View
CREATE VIEW StudentCourses AS
SELECT Students.Name, Courses.CourseName 
FROM Students 
JOIN Courses ON Students.StudentID = Courses.StudentID;

-- 7. Creating a Stored Procedure
DELIMITER $$
CREATE PROCEDURE GetStudentCourses()
BEGIN
    SELECT * FROM StudentCourses;
END $$
DELIMITER ;

CALL GetStudentCourses();

-- 8. Creating a Trigger
DELIMITER $$
CREATE TRIGGER BeforeInsertStudent
BEFORE INSERT ON Students
FOR EACH ROW
BEGIN
    IF NEW.Age < 18 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Age must be at least 18';
    END IF;
END $$
DELIMITER ;

-- 9. Creating an Index
CREATE INDEX idx_city ON Students(City);

-- 10. Implementing Transactions
START TRANSACTION;
UPDATE Students SET Age = 23 WHERE StudentID = 1;
ROLLBACK; -- To revert the changes
COMMIT; -- To save the changes

📂 How to Use

Clone the repository:

git clone https://github.com/yourusername/rdbms-concepts.git

Navigate to the directory:

cd rdbms-concepts

Open the SQL scripts in your preferred database client.

Run the queries and explor
