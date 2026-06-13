# Practical 4: Creating Database Users and Granting Permissions

## Aim

To create new database users in MySQL and assign different levels of permissions on databases and tables using the `GRANT` statement.

---

## Software Requirements

* macOS
* Terminal
* MySQL Community Server

---

## Theory

MySQL provides a user management system that allows database administrators to create multiple user accounts and control their privileges. Permissions can be granted at different levels, such as the entire database, specific tables, or specific operations.

Some commonly used privileges include:

* `SELECT` – Allows reading data from tables.
* `INSERT` – Allows inserting new records.
* `UPDATE` – Allows modifying existing records.
* `DELETE` – Allows removing records.
* `ALL PRIVILEGES` – Grants full control over the database.

Using proper permissions improves database security by ensuring that users can only perform authorized operations.

---

## Implementation Steps

### Step 1: Log in as Root User

Open Terminal and log in to MySQL.

```bash
mysql -u root -p
```

Enter the root password.

![login mySQl](assets/login-mySQL.png)

---

### Step 2: Display Existing Users

Execute the following query:

```sql
SELECT User, Host
FROM mysql.user;
```

This displays all existing MySQL users.

![Display Existing Users](assets/display-existing-users.png)

---

### Step 3: Create a New User

Create a new user named `student1`.

```sql
CREATE USER 'student1'@'localhost'
IDENTIFIED BY 'password123';
```

Verify that the user has been created.

```sql
SELECT User, Host
FROM mysql.user;
```
![Create a New User](assets/create-new-user.png)

---

### Step 4: Grant All Privileges on student_db

```sql
GRANT ALL PRIVILEGES
ON student_db.*
TO 'student1'@'localhost';
```

Apply the changes.

```sql
FLUSH PRIVILEGES;
```

![Grant All Privileges on student_db](assets/GRANT-output.png)

---

### Step 5: Verify Granted Permissions

Execute:

```sql
SHOW GRANTS FOR 'student1'@'localhost';
```

This displays all privileges assigned to the user.

![Verify Granted Permissions](assets/verify-GRANT-permission.png)

---

### Step 6: Grant SELECT Permission Only

Create another user.

```sql
CREATE USER 'viewer'@'localhost'
IDENTIFIED BY 'viewer123';
```

Grant only read permission.

```sql
GRANT SELECT
ON student_db.students
TO 'viewer'@'localhost';

FLUSH PRIVILEGES;
```

Check the assigned privileges.

```sql
SHOW GRANTS FOR 'viewer'@'localhost';
```

![Grant SELECT Permission Only](assets/GRANT-SELECT-permission.png)

---

### Step 7: Revoke a Permission

Remove the `SELECT` privilege from `viewer`.

```sql
REVOKE SELECT
ON student_db.students
FROM 'viewer'@'localhost';

FLUSH PRIVILEGES;
```

Verify the updated permissions.

```sql
SHOW GRANTS FOR 'viewer'@'localhost';
```

![Revoke a Permission](assets/revoke-permission.png)

---

## SQL Commands Used

```sql
SELECT User, Host
FROM mysql.user;

CREATE USER 'student1'@'localhost'
IDENTIFIED BY 'password123';

GRANT ALL PRIVILEGES
ON student_db.*
TO 'student1'@'localhost';

FLUSH PRIVILEGES;

SHOW GRANTS FOR 'student1'@'localhost';

CREATE USER 'viewer'@'localhost'
IDENTIFIED BY 'viewer123';

GRANT SELECT
ON student_db.students
TO 'viewer'@'localhost';

FLUSH PRIVILEGES;

SHOW GRANTS FOR 'viewer'@'localhost';

REVOKE SELECT
ON student_db.students
FROM 'viewer'@'localhost';

FLUSH PRIVILEGES;

SHOW GRANTS FOR 'viewer'@'localhost';
```

---

## Result

Two MySQL users were successfully created. Different access permissions were assigned using the `GRANT` statement, verified using `SHOW GRANTS`, and modified using the `REVOKE` statement.

---

## Conclusion

This practical demonstrated how to create MySQL user accounts and manage their access privileges. Proper permission management helps improve database security by restricting users to only the operations they are authorized to perform.
