# Project Exercise: Implementing the University Database System

Scenario:
You have designed an ERD for a fictional Swedish university's database system. Now, you are tasked
with bringing this design to life by creating the actual database, populating it with data, and
performing various operations.

## Requirements:

1. Create the Database from the ERD:
- Transform the entities from your ERD into SQL `CREATE TABLE` statements. These entities include
  Students, Courses, Professors, Departments, and the junction table StudentEnrollments.
- Make sure to define the proper constraints (e.g., `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`) as
  per your ERD.
2. Populate the Database:
- Write SQL `INSERT` statements to add data to your tables, reflecting the attributes outlined in the
  ERD exercise:
- Students should have ID, name, date of birth, and enrollment year.
- Courses need a course code, name, credits, and associated department.
- Professors require an ID, name, date of hire, and associated department.
- Departments demand a department code, name, and department head.
- Include enough sample data to make the subsequent tasks meaningful (at least 10 students, 5
  professors, 3 departments, and 10 courses).
3. Querying the Database:
- Write SQL `SELECT` statements that:
- Retrieve all courses a particular student is enrolled in.
- Count how many professors belong to each department.
- List all courses offered by a department.
- Show the department head for each department.
4. Modifying Data:
- Write SQL statements that simulate operational changes, such as:
- Adding a new professor to a department.
- Assigning a new department head.
- Registering a student for a course (hint: this will involve the StudentEnrollments junction table).
- Adding a new course to a department.
5. Data Integrity Challenge:
- Show examples of how your database handles attempts to:
- Enroll a student in a non-existent course.
- Assign a non-existent professor as a department head.
- Add a course without associating it with a department.
- Discuss what constraints were triggered in these cases and why.
  Presentation:

Each group will present their SQL implementations, demonstrate their queries in action, and discuss their data integrity challenges and (if tackled) the bonus challenge.

Discussion:
Conclude with a discussion on the challenges faced during implementation, insights gained about the importance of database design, and reflections on how database constraints ensure data integrity.
