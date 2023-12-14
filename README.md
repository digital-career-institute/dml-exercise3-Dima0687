# DML exercise3
Exercise Set:
Exercise Set:
create student table , add columns such as maths,chemistry,physics, and age.

```SQL
CREATE TABLE students(id INT PRIMARY KEY, name VARCHAR(50), age INT, maths DECIMAL(5,2), chemistry DECIMAL(5,2), physics DECIMAL(5,2));

+-----------+--------------+------+-----+---------+-------+
| Field     | Type         | Null | Key | Default | Extra |
+-----------+--------------+------+-----+---------+-------+
| id        | int          | NO   | PRI | NULL    |       |
| name      | varchar(50)  | YES  |     | NULL    |       |
| age       | int          | YES  |     | NULL    |       |
| maths     | decimal(5,2) | YES  |     | NULL    |       |
| chemistry | decimal(5,2) | YES  |     | NULL    |       |
| physics   | decimal(5,2) | YES  |     | NULL    |       |
+-----------+--------------+------+-----+---------+-------+
```

add entries of studnets who have scored more than 75 in physics.add entry for the studnet whose name is alice and bob.

add some students who scored less than 70.

```SQL
INSERT INTO students VALUES
   (1, "Alice", 23, 90, 75, 80),
   (2, "Bob", 21, 65, 68, 70),
   (3, "John", 25, 82, 88, 84),
   (4, "Jane", 24, 67, 65, 76);

+----+-------+------+-------+-----------+---------+
| id | name  | age  | maths | chemistry | physics |
+----+-------+------+-------+-----------+---------+
|  1 | Alice |   23 | 90.00 |     75.00 |   80.00 |
|  2 | Bob   |   21 | 65.00 |     68.00 |   70.00 |
|  3 | John  |   25 | 82.00 |     88.00 |   84.00 |
|  4 | Jane  |   24 | 67.00 |     65.00 |   76.00 |
+----+-------+------+-------+-----------+---------+
```

Task 1: SELECT Queries

1.Retrieve all information from the "Students" table:
```SQL
SELECT * FROM students;

+----+-------+------+-------+-----------+---------+
| id | name  | age  | maths | chemistry | physics |
+----+-------+------+-------+-----------+---------+
|  1 | Alice |   23 | 90.00 |     75.00 |   80.00 |
|  2 | Bob   |   21 | 65.00 |     68.00 |   70.00 |
|  3 | John  |   25 | 82.00 |     88.00 |   84.00 |
|  4 | Jane  |   24 | 67.00 |     65.00 |   76.00 |
+----+-------+------+-------+-----------+---------+
```

2.Fetch only the names and ages of students:
```SQL
SELECT name, age FROM students;

+-------+------+
| name  | age  |
+-------+------+
| Alice |   23 |
| Bob   |   21 |
| John  |   25 |
| Jane  |   24 |
+-------+------+
```

3.Get the details of students who scored above 75 in the "Physics" subject:
```SQL
SELECT * FROM students WHERE physics > 75;
+----+-------+------+-------+-----------+---------+
| id | name  | age  | maths | chemistry | physics |
+----+-------+------+-------+-----------+---------+
|  1 | Alice |   23 | 90.00 |     75.00 |   80.00 |
|  3 | John  |   25 | 82.00 |     88.00 |   84.00 |
|  4 | Jane  |   24 | 67.00 |     65.00 |   76.00 |
+----+-------+------+-------+-----------+---------+
```

4.Insert a new student into the "Students" table:
```SQL
INSERT INTO students VALUES
    (5, "Dilan", 22, 90, 60, 77);

+----+-------+------+-------+-----------+---------+
| id | name  | age  | maths | chemistry | physics |
+----+-------+------+-------+-----------+---------+
|  1 | Alice |   23 | 90.00 |     75.00 |   80.00 |
|  2 | Bob   |   21 | 65.00 |     68.00 |   70.00 |
|  3 | John  |   25 | 82.00 |     88.00 |   84.00 |
|  4 | Jane  |   24 | 67.00 |     65.00 |   76.00 |
|  5 | Dilan |   22 | 90.00 |     60.00 |   77.00 |
+----+-------+------+-------+-----------+---------+
```

5.Add a student who excelled only in Mathematics and Chemistry:
```SQL
// What does excelled means? I left physics out
INSERT INTO students(id, name, age, maths, chemistry) VALUES (6, "Drake", 18, 98, 95);

+----+-------+------+-------+-----------+---------+
| id | name  | age  | maths | chemistry | physics |
+----+-------+------+-------+-----------+---------+
|  1 | Alice |   23 | 90.00 |     75.00 |   80.00 |
|  2 | Bob   |   21 | 65.00 |     68.00 |   70.00 |
|  3 | John  |   25 | 82.00 |     88.00 |   84.00 |
|  4 | Jane  |   24 | 67.00 |     65.00 |   76.00 |
|  5 | Dilan |   22 | 90.00 |     60.00 |   77.00 |
|  6 | Drake |   18 | 98.00 |     95.00 |    NULL |
+----+-------+------+-------+-----------+---------+
```

6.Update the age of a student named "Alice" to 23 years:
```SQL
// "My" Alice was already 23 years old, so i increased to 24y now.
UPDATE students SET age = 24 WHERE name = "Alice";

// But this query can make trouble, what if there is more than one Alice in the table?
UPDATE students SET age = 24 WHERE name = "Alice" AND id = 1;
// OR JUST
UPDATE students SET age = 24 WHERE id = 1;

+----+-------+------+-------+-----------+---------+
| id | name  | age  | maths | chemistry | physics |
+----+-------+------+-------+-----------+---------+
|  1 | Alice |   24 | 90.00 |     75.00 |   80.00 |
|  2 | Bob   |   21 | 65.00 |     68.00 |   70.00 |
|  3 | John  |   25 | 82.00 |     88.00 |   84.00 |
|  4 | Jane  |   24 | 67.00 |     65.00 |   76.00 |
|  5 | Dilan |   22 | 90.00 |     60.00 |   77.00 |
|  6 | Drake |   18 | 98.00 |     95.00 |    NULL |
+----+-------+------+-------+-----------+---------+
```

7.Increase the Chemistry score of all students by 5 points:
```SQL
UPDATE students SET chemistry = chemistry + 5;

+----+-------+------+-------+-----------+---------+
| id | name  | age  | maths | chemistry | physics |
+----+-------+------+-------+-----------+---------+
|  1 | Alice |   24 | 90.00 |     80.00 |   80.00 |
|  2 | Bob   |   21 | 65.00 |     73.00 |   70.00 |
|  3 | John  |   25 | 82.00 |     93.00 |   84.00 |
|  4 | Jane  |   24 | 67.00 |     70.00 |   76.00 |
|  5 | Dilan |   22 | 90.00 |     65.00 |   77.00 |
|  6 | Drake |   18 | 98.00 |    100.00 |    NULL |
+----+-------+------+-------+-----------+---------+
```

8.Delete a student named "Bob" from the "Students" table:
```SQL
DELETE FROM students WHERE name = "Bob";
// same problem as with task 6, but i'm to lazy now =)
+----+-------+------+-------+-----------+---------+
| id | name  | age  | maths | chemistry | physics |
+----+-------+------+-------+-----------+---------+
|  1 | Alice |   24 | 90.00 |     80.00 |   80.00 |
|  3 | John  |   25 | 82.00 |     93.00 |   84.00 |
|  4 | Jane  |   24 | 67.00 |     70.00 |   76.00 |
|  5 | Dilan |   22 | 90.00 |     65.00 |   77.00 |
|  6 | Drake |   18 | 98.00 |    100.00 |    NULL |
+----+-------+------+-------+-----------+---------+
```

9.Remove all students who scored below 70 in Mathematics:
```SQL
DELETE FROM students WHERE maths < 70;

+----+-------+------+-------+-----------+---------+
| id | name  | age  | maths | chemistry | physics |
+----+-------+------+-------+-----------+---------+
|  1 | Alice |   24 | 90.00 |     80.00 |   80.00 |
|  3 | John  |   25 | 82.00 |     93.00 |   84.00 |
|  5 | Dilan |   22 | 90.00 |     65.00 |   77.00 |
|  6 | Drake |   18 | 98.00 |    100.00 |    NULL |
+----+-------+------+-------+-----------+---------+
```
