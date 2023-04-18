# Database-Systems-Project

Commands to Complete Tasks (Easier to Read in SQL_Code file)

Task 2 (Create tables and insert values into tables)

-- Create Course table
CREATE TABLE Course (
  course_id INT PRIMARY KEY,
  department VARCHAR(255),
  course_number INT,
  course_name VARCHAR(255),
  semester VARCHAR(255),
  year INT
);

-- Create Student table
CREATE TABLE Student (
  student_id INT PRIMARY KEY,
  first_name VARCHAR(255),
  last_name VARCHAR(255),
  course_id INT,
  FOREIGN KEY (course_id) REFERENCES Course(course_id)
);

-- Create Assignment table
CREATE TABLE Assignment (
  assignment_id INT PRIMARY KEY,
  category VARCHAR(255),
  percentage DECIMAL(5,2),
  course_id INT,
  FOREIGN KEY (course_id) REFERENCES Course(course_id)
);

-- Create Grades table
CREATE TABLE Grades (
  grade_id INT PRIMARY KEY,
  assignment_id INT,
  student_id INT,
  score DECIMAL(5,2),
  FOREIGN KEY (assignment_id) REFERENCES Assignment(assignment_id),
  FOREIGN KEY (student_id) REFERENCES Student(student_id)
);

-- Insert values into Course table
INSERT INTO Course (course_id, department, course_number, course_name, semester, year)
VALUES (1, 'Computer Science', 101, 'Database Systems', 'Spring', 2023);

-- Insert values into Student table
INSERT INTO Student (student_id, first_name, last_name, course_id)
VALUES (1, 'Kevin', 'Claiborne, Jr', 1),
       (2, 'Asaad', 'Martin', 1),
       (3, 'Amira', 'Crump', 1);

-- Insert values into Assignment table
INSERT INTO Assignment (assignment_id, category, percentage, course_id)
VALUES (1, 'Participation', 10.0, 1),
       (2, 'Homework', 20.0, 1),
       (3, 'Tests', 50.0, 1),
       (4, 'Projects', 20.0, 1);

-- Insert values into Grades table
INSERT INTO Grades (grade_id, assignment_id, student_id, score)
VALUES (1, 1, 1, 8.5),
       (2, 2, 1, 92.0),
       (3, 3, 1, 75.0),
       (4, 4, 1, 88.0),
       (5, 1, 2, 9.0),
       (6, 2, 2, 88.5),
       (7, 3, 2, 82.0),
       (8, 4, 2, 95.0),
       (9, 1, 3, 7.0),
       (10, 2, 3, 78.0),
       (11, 3, 3, 90.0),
       (12, 4, 3, 91.5);
       
       
       
Task 3 (Show contents of created tables)

SELECT * FROM Course;
SELECT * FROM Student;
SELECT * FROM Assignment;
SELECT * FROM Grades;



Task 4 (Compute average/highest/lowest score of an assignment)

-- Average score
SELECT AVG(score) AS average_score
FROM Grades
WHERE assignment_id = 2;

-- Highest score
SELECT MAX(score) AS highest_score
FROM Grades
WHERE assignment_id = 2;

-- Lowest score
SELECT MIN(score) AS lowest_score
FROM Grades
WHERE assignment_id = 2;



Task 5 (List all of the students in a given course)

SELECT s.* FROM Student s
JOIN Course c ON s.course_id = c.course_id
WHERE c.course_id = 1;



Task 6 (List all of the students in a course and all of their scores on every assignment)
Task 7 (Add an assignment to a course)

INSERT INTO Assignment (assignment_id, category, percentage, course_id)
VALUES (5, 'Final Exam', 30.0, 1);



Task 8 (Change the percentages of the categories for a course)

UPDATE Assignment
SET percentage = 30.0
WHERE category = 'Homework' AND course_id = 1;



Task 9 (Add 2 points to the score of each student on an assignment)

UPDATE Grades
SET score = score + 2
WHERE assignment_id = 3;



Task 10 (Add 2 points just to those students whose last name contains a ‘Q’)
Task 11 (Compute the grade for a student)

SELECT s.first_name, s.last_name, SUM(a.percentage * g.score / 100) AS grade
FROM Student s
JOIN Grades g ON s.student_id = g.student_id
JOIN Assignment a ON g.assignment_id = a.assignment_id
GROUP BY s.first_name, s.last_name
HAVING s.student_id = 1;


Task 12 (Compute the grade for a student, where the lowest score for a given category is dropped)


