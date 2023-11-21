# Group 6 University DB Documentation

## Initial Setup

### MySQL

#### Table Creation

```
CREATE TABLE Departments ( 
    id VARCHAR(10) PRIMARY KEY, 
    DeptName VARCHAR(50), 
    HeadProfessorID INT 
); 
CREATE TABLE Professors ( 
    id INT PRIMARY KEY AUTO_INCREMENT, 
    FirstName NVARCHAR(100), 
    LastName NVARCHAR(100), 
    Department_ID VARCHAR(10), 
    FOREIGN KEY (Department_ID) REFERENCES Departments(id) 
); 
CREATE TABLE Students ( 
    id INT PRIMARY KEY AUTO_INCREMENT, 
    FirstName NVARCHAR(100), 
    LastName NVARCHAR(100), 
    DoB DATE, 
    EnrolmentYear INT 
); 
CREATE TABLE Courses ( 
    id INT PRIMARY KEY AUTO_INCREMENT, 
    CourseName VARCHAR(50), 
    Department_ID VARCHAR(10), 
    FOREIGN KEY (Department_ID) REFERENCES Departments(id) 
); 
CREATE TABLE StudentEnrollments ( 
    StudentID INT, 
    CourseID INT, 
    FOREIGN KEY (StudentID) REFERENCES Students(id), 
    FOREIGN KEY (CourseID) REFERENCES Courses(id), 
    PRIMARY KEY (StudentID, CourseID) 
);
```

#### Altering Foreign Key

Foreign key connecting tables **Departments (Department Head)** with **Professors (ID)** had to be added subsequently to avoid conflicts with circular references:

```
ALTER TABLE Departments
ADD FOREIGN KEY (HeadProfessorID) REFERENCES Professors(id);
```

#### Database Population

The following queries populates our demo database with students, courses, departments and professors. It then fills the junction table (representing a *MANY-TO-MANY* relationship between Students and Courses) **StudentEnrollments** with data, making sure several students are enrolled in several courses.

```
INSERT INTO Students (FirstName, LastName, DoB, EnrolmentYear)
VALUES 
    ('John', 'Doe', '1990-01-15', 2010),
    ('Jane', 'Smith', '1992-05-20', 2012),
    ('Bob', 'Johnson', '1991-08-10', 2011),
    ('Alice', 'Williams', '1993-03-25', 2013),
    ('Eva', 'Brown', '1994-09-12', 2014),
    ('Michael', 'Miller', '1990-07-03', 2010),
    ('Sophia', 'Davis', '1995-11-18', 2015),
    ('Daniel', 'Taylor', '1993-02-08', 2013),
    ('Olivia', 'Moore', '1992-12-01', 2012),
    ('William', 'Wilson', '1994-06-30', 2014),
    ('Emily', 'Clark', '1991-04-17', 2011),
    ('Matthew', 'Jones', '1993-10-22', 2013),
    ('Ava', 'Anderson', '1990-08-09', 2010),
    ('Christopher', 'White', '1994-01-28', 2014),
    ('Sophie', 'Walker', '1992-06-15', 2012),
    ('David', 'Harris', '1991-09-05', 2011),
    ('Emma', 'Evans', '1993-04-14', 2013),
    ('Ryan', 'Martin', '1995-12-10', 2015),
    ('Grace', 'Thomas', '1990-03-20', 2010),
    ('Jackson', 'Wright', '1992-07-25', 2012);

-- TO AVOID CONFLICT (PROFESSORID NULL) --
SET FOREIGN_KEY_CHECKS = 0;

INSERT INTO Departments (id, DeptName, HeadProfessorID)
VALUES
    ('MATH20', 'Mathematics', 1),
    ('BIO12', 'Biology', 2),
    ('CHEM15', 'Chemistry', 3),
    ('PHYS10', 'Physics', 4),
    ('ENG05', 'English', 5);

INSERT INTO Professors (FirstName, LastName, Department_ID)
VALUES
    ('Karen', 'Blanchard', 'MATH20'),
    ('August', 'Severus', 'BIO12'),
    ('Carl', 'Jokerson', 'CHEM15'),
    ('Pamela', 'Svensson', 'PHYS10'),
    ('Joel', 'Simonsen', 'ENG05'),
    ('Gary', 'Tatchet', 'MATH20'),
    ('Paulie', 'Brooke', 'BIO12'),
    ('James', 'Ferrell', 'CHEM15'),
    ('Nelson', 'Schweinhund', 'PHYS10'),
    ('Niels', 'Abrahamsson', 'ENG05');

-- CHECKS FOREIGN KEYS AGAIN --
SET FOREIGN_KEY_CHECKS = 1;

INSERT INTO Courses (CourseName, Department_ID)
VALUES
    ('Calculus I', 'MATH20'),
    ('Biology 101', 'BIO12'),
    ('Chemistry 101', 'CHEM15'),
    ('Physics 201', 'PHYS10'),
    ('English Composition', 'ENG05'),
    ('Linear Algebra', 'MATH20'),
    ('Calculus II', 'MATH20'),
    ('Biology 201', 'BIO12'),
    ('Organic Chemistry', 'CHEM15'),
    ('Shakespearean Literature', 'ENG05');

INSERT INTO StudentEnrollments (StudentID, CourseID)
VALUES
    (1, 1), (1, 2), (1, 3), (1, 4), (1, 5),
    (2, 1), (2, 2), (2, 3), (2, 4),
    (3, 1), (3, 2), (3, 3), (3, 4),
    (4, 1), (4, 2), (4, 3), (4, 4), (4, 5),
    (5, 1), (5, 2), (5, 3), (5, 4), (5, 5),
    (6, 1), (6, 2), (6, 3),
    (7, 1), (7, 2), (7, 3),
    (8, 1), (8, 2), (8, 3),
    (9, 1), (9, 2),
    (10, 1), (10, 2), (10, 3), (10, 4), (10, 5),
    (11, 1), (11, 2), (11, 3), (11, 4),
    (12, 1), (12, 2), (12, 3), (12, 4), (12, 5),
    (13, 1), (13, 2), (13, 3), (13, 4),
    (14, 1), (14, 2), (14, 3), (14, 4), (14, 5),
    (15, 1), (15, 2), (15, 3), (15, 4),
    (16, 1), (16, 2), (16, 3), (16, 4), (16, 5),
    (17, 1), (17, 2), (17, 3),
    (18, 1), (18, 2), (18, 3),
    (19, 1), (19, 2), (19, 3),
    (20, 1), (20, 2), (20, 3), (20, 4), (20, 5);
```
