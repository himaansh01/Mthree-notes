# 📘 Git and SQL Documentation

---

## 🚀 Introduction to Git

### Overview

Git is a **distributed version control system** designed to manage code changes, facilitate team collaboration, and maintain a reliable history of modifications. It allows developers to efficiently track progress and revert to previous versions when necessary.

### Advantages of Using Git

- Cross-platform support: **Windows, macOS, and Linux**
- **Free and open-source**
- Enables **branching**, concurrent development, and large-scale project management

---

## ⚙️ Initial Git Setup

### Installing Git

- Visit [git-scm.com](https://git-scm.com) to download and install Git
- Use **Git Bash** on Windows and **Terminal** on macOS or Linux

### Configuring User Identity

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

This ensures commits are linked to your identity across all repositories.

---

## 🔧 Common Git Commands

### Stage Changes

```bash
git add --all
```

Stages all changes (new files, updates, deletions) for the next commit.

### Commit Changes

```bash
git commit -m "Descriptive commit message"
```

Creates a commit with a message describing the changes.

### Push to Remote Repository

```bash
git push origin main
```

Sends local commits to the `main` branch of the remote repository.

### Pull from Remote Repository

```bash
git pull origin main
```

Fetches and merges changes from the remote repository into your local branch.

---

## 🌿 Branching in Git

### Create a New Branch

```bash
git branch feature-name
```

### Create and Switch to a New Branch

```bash
git checkout -b feature-name
```

This command both creates and switches to the new branch.

### View All Branches

```bash
git branch
```

### Delete a Local Branch

```bash
git branch -d branch-name     # Safely deletes merged branch
git branch -D branch-name     # Force deletes unmerged branch
```

### Delete a Remote Branch

```bash
git push origin --delete branch-name
```

---

## 🔗 Remote Tracking (Upstream Branches)

- Tracks a local branch against a remote counterpart to simplify pushing and pulling.

### Set Upstream

```bash
git push -u origin branch-name
```

### Check Upstream Info

```bash
git branch -vv
```

### Change Upstream Tracking

```bash
git branch --set-upstream-to=origin/branch-name
```

---

## 📄 Additional Git Utilities

### View Current Status

```bash
git status
```

Shows the current state of the working directory and staging area.

### View Commit History

```bash
git log
git log --oneline -n 2  # Shows the last 2 commits in compact format
```

### View File Differences

```bash
git diff              # All unstaged changes
git diff --staged     # Staged but uncommitted changes
git diff filename     # Differences in a specific file
```

### Reset to Remote State

```bash
git reset --hard origin/branch-name
```

Overwrites local changes to match the remote repository.

### Fetch Without Merge

```bash
git fetch --all
```

Downloads changes from the remote without merging them.

---

# 🧠 SQL Documentation

---

## 🏗️ Database Creation

```sql
CREATE DATABASE database_name;
USE database_name;
```

---

## 🧱 Table Creation

```sql
CREATE TABLE employees (
  emp_id INT PRIMARY KEY,
  name VARCHAR(50),
  salary DECIMAL(10,2),
  department VARCHAR(50)
);
```

---

## ➕ Inserting Records

```sql
INSERT INTO employees VALUES (1, 'John Doe', 50000.00, 'IT');
```

---

## 🔍 Retrieving Data

```sql
SELECT * FROM employees;
```

---

## 🔗 SQL Joins

### LEFT JOIN Example

```sql
SELECT e.emp_id, e.name, e.salary,
COALESCE(d.department_name, 'No Department') AS department
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id
WHERE d.department_id IS NULL;
```

This query returns employees who are not associated with any department.

---

## ⚠️ Foreign Key Constraints

### Table with ON DELETE and ON UPDATE

```sql
CREATE TABLE enrollments (
  enrollment_id INT PRIMARY KEY,
  student_id INT,
  course_id INT DEFAULT 999,
  enrollment_date DATE,
  FOREIGN KEY (student_id) REFERENCES students(student_id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  FOREIGN KEY (course_id) REFERENCES courses(course_id)
    ON DELETE SET NULL ON UPDATE SET DEFAULT
);
```

**Constraint Behavior:**

- `ON DELETE CASCADE`: Deletes related enrollments when a student is deleted
- `ON DELETE SET NULL`: Sets `course_id` to NULL when a course is deleted
- `ON UPDATE CASCADE`: Propagates student ID updates
- `ON UPDATE SET DEFAULT`: Resets course ID to default when updated

---

## ⚙️ SQL Triggers

### Create a Logging Trigger Before Deleting a Course

```sql
CREATE TABLE enrollment_logging (
  enrollment_id INT PRIMARY KEY,
  action VARCHAR(200),
  change_date DATE
);

CREATE TRIGGER before_course_deletion
BEFORE DELETE ON courses
FOR EACH ROW
INSERT INTO enrollment_logging (enrollment_id, action, change_date)
VALUES (OLD.course_id, 'DELETE BASED ON DELETION FROM COURSE', NOW());
```

Triggers automatically perform actions in response to certain events.

---

## ❌ Deleting Data

### Deleting with Cascading Effect

```sql
DELETE FROM courses WHERE course_id = 1;
```

Deletes a course and automatically removes related records (if cascading is enabled).

### Verify Deletions

```sql
SELECT * FROM enrollments;
SELECT * FROM courses;
```
