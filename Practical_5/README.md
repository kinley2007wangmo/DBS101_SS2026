# Practical 5: Database Normalization

## Aim

To normalize a database by identifying functional dependencies and converting unnormalized data into First Normal Form (1NF), Second Normal Form (2NF), and Third Normal Form (3NF).

---

## Software Requirements

* macOS
* Visual Studio Code (for documentation)
* MySQL Community Server
* Terminal

---

## Theory

Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It divides large tables into smaller related tables while maintaining relationships among them.

The normal forms are:

* **First Normal Form (1NF):** Eliminates repeating groups and ensures each column contains atomic values.
* **Second Normal Form (2NF):** Removes partial dependencies by ensuring that non-key attributes depend on the entire primary key.
* **Third Normal Form (3NF):** Removes transitive dependencies so that non-key attributes depend only on the primary key.

Normalization helps minimize duplicate data and improves database efficiency.

---

## Implementation Steps

### Step 1: Create an Unnormalized Table

Log in to MySQL.

```bash
mysql -u root -p
```

Select the database.

```sql
USE student_db;
```

Create an unnormalized table.

```sql
CREATE TABLE student_records (
    student_id INT,
    student_name VARCHAR(50),
    department_name VARCHAR(50),
    department_head VARCHAR(50)
);
```

![Create an Unnormalized Table](assets/create-table.png)

---

### Step 2: Insert Sample Data

```sql
INSERT INTO student_records
VALUES
(1, 'Kinley', 'Engineering', 'Mr. Dorji'),
(2, 'Sonam', 'IT', 'Mrs. Choden'),
(3, 'Pema', 'Engineering', 'Mr. Dorji');
```

Display the table.

```sql
SELECT * FROM student_records;
```

![Insert Sample Data](assets/insert-sample-data.png)

---

### Step 3: Identify Functional Dependencies

Functional dependencies:

```text
student_id → student_name, department_name

department_name → department_head
```

This indicates that `department_head` depends on `department_name` rather than directly on `student_id`, creating a transitive dependency.

---

### Step 4: Convert to First Normal Form (1NF)

The table already satisfies 1NF because:

* Each row is unique.
* Each column contains atomic values.
* No repeating groups exist.

![Convert to First Normal Form](assets/1NF.png)

---

### Step 5: Convert to Second Normal Form (2NF)

Since the table has a single-column primary key (`student_id`), there are no partial dependencies.

Therefore, it satisfies 2NF.


---

### Step 6: Convert to Third Normal Form (3NF)

Create separate tables.

- Create Students Table

```sql
CREATE TABLE students_normalized (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50),
    department_name VARCHAR(50)
);
```

- Create Departments Table

```sql
CREATE TABLE departments_normalized (
    department_name VARCHAR(50) PRIMARY KEY,
    department_head VARCHAR(50)
);
```

![Create separate tables](assets/create-3NF-table.png)

Insert sample records.

```sql
INSERT INTO students_normalized
VALUES
(1, 'Kinley', 'Engineering'),
(2, 'Sonam', 'IT'),
(3, 'Pema', 'Engineering');

INSERT INTO departments_normalized
VALUES
('Engineering', 'Mr. Dorji'),
('IT', 'Mrs. Choden');
```

![Insert sample records](assets/inseret-3NF-data.png)

Display both tables.

```sql
SELECT * FROM students_normalized;

SELECT * FROM departments_normalized;
```

![Display both tables](assets/display-3NF-table.png)

---

## SQL Commands Used

```sql
USE student_db;

CREATE TABLE student_records (
    student_id INT,
    student_name VARCHAR(50),
    department_name VARCHAR(50),
    department_head VARCHAR(50)
);

INSERT INTO student_records
VALUES
(1, 'Kinley', 'Engineering', 'Mr. Dorji'),
(2, 'Sonam', 'IT', 'Mrs. Choden'),
(3, 'Pema', 'Engineering', 'Mr. Dorji');

SELECT * FROM student_records;

CREATE TABLE students_normalized (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50),
    department_name VARCHAR(50)
);

CREATE TABLE departments_normalized (
    department_name VARCHAR(50) PRIMARY KEY,
    department_head VARCHAR(50)
);

INSERT INTO students_normalized
VALUES
(1, 'Kinley', 'Engineering'),
(2, 'Sonam', 'IT'),
(3, 'Pema', 'Engineering');

INSERT INTO departments_normalized
VALUES
('Engineering', 'Mr. Dorji'),
('IT', 'Mrs. Choden');

SELECT * FROM students_normalized;

SELECT * FROM departments_normalized;
```

---

## Result

The unnormalized table was analyzed, functional dependencies were identified, and the data was successfully reorganized into normalized tables satisfying Third Normal Form (3NF).

---

# Conclusion

This practical demonstrated the process of database normalization by reducing redundancy and eliminating transitive dependencies. The normalized design improves consistency, minimizes duplication, and makes the database easier to maintain and update.
