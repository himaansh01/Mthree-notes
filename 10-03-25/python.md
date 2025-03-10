# Documentation for NumPy, Pandas, and SQLAlchemy Code

## 1. NumPy and Pandas Operations

### 1.1 Importing Required Libraries
```python
import numpy as np
import pandas as pd
```
This imports NumPy and Pandas, which are essential libraries for numerical and data analysis in Python.

### 1.2 Creating Arrays with NumPy
- **Random Array:** `np.random.rand(3, 4)`
  - Creates a 3x4 matrix with random values between 0 and 1.
- **Zeros Array:** `np.zeros((3, 4))`
  - Generates a 3x4 matrix filled with zeros.
- **Ones Array:** `np.ones((3, 4))`
  - Generates a 3x4 matrix filled with ones.
- **Full Array:** `np.full((3, 4), 10)`
  - Generates a 3x4 matrix filled with the number 10.

### 1.3 Creating a Range of Numbers
- `np.arange(10, 20, 0.5)`
  - Creates an array of numbers from 10 to 20 with a step of 0.5.

### 1.4 Matrix Operations
```python
matrix_1 = np.array([[1, 2, 3], [4, 5, 6]])
matrix_2 = np.array([[1, 2, 3], [4, 5, 6]])
```

- **Addition:** `matrix_1 + matrix_2`
  - Performs element-wise addition.
- **Subtraction:** `matrix_1 - matrix_2`
  - Performs element-wise subtraction.
- **Multiplication:** `matrix_1 * matrix_2`
  - Performs element-wise multiplication.
- **Division:** `matrix_1 / matrix_2`
  - Performs element-wise division.
- **Power:** `matrix_1 ** matrix_2`
  - Raises elements of `matrix_1` to the power of `matrix_2`.
- **Transpose:** `matrix_1.T`
  - Computes the transpose of `matrix_1`.
- **Dot Product:**
```python
matrix_3 = np.array([[1, 2], [3, 4], [5, 6]])  # 3x2 matrix
matrix_4 = np.array([[7, 8, 9], [10, 11, 12]])  # 2x3 matrix
matrix_dot_product = np.dot(matrix_3, matrix_4)
```
  - Performs a dot product between two matrices.

### 1.5 Statistical Operations
- **Mean:** `np.mean(arr_range)`
  - Computes the mean of the array.
- **Median:** `np.median(arr_range)`
  - Computes the median of the array.
- **Standard Deviation:** `np.std(arr_range)`
  - Computes the standard deviation.
- **Variance:** `np.var(arr_range)`
  - Computes the variance.

### 1.6 Pandas Series and DataFrame
```python
series = pd.Series([1, 2, 3, 4, 5])
series_2 = pd.Series([1, 2, 3, 4, 5], index=['a', 'b', 'c', 'd', 'e'])
```
- **Pandas Series**: A one-dimensional labeled array.

```python
data = {
    'Name': ['John', 'Jane', 'Jim', 'Jill'],
    'Age': [20, 21, 22, 23],
    'City': ['New York', 'Los Angeles', 'Chicago', 'Houston']
}
df = pd.DataFrame(data)
```
- **Pandas DataFrame**: A two-dimensional labeled data structure.

```python
df_csv = pd.read_csv('data.csv')
```
- **Reading CSV Files**: Loads data from a CSV file into a Pandas DataFrame.

---

## 2. SQLAlchemy Database Operations

### 2.1 Importing Required Libraries
```python
from sqlalchemy import create_engine, MetaData, Table, Column, Integer, String, ForeignKey, insert, select
```

### 2.2 Database Connection
```python
engine = create_engine('sqlite:///D:/backup/python3/basic-module/src/basic_module/datastructure/data.db', echo=True)
```
- Establishes a connection to the SQLite database.
- `echo=True` enables logging of SQL statements.

### 2.3 Defining Database Tables
```python
metadata = MetaData()

users = Table('users', metadata,
    Column('id', Integer, primary_key=True),
    Column('name', String),
    Column('age', Integer),
    Column('city', String),
)

posts = Table('posts', metadata,
    Column('id', Integer, primary_key=True),
    Column('title', String),
    Column('content', String),
    Column('user_id', Integer, ForeignKey('users.id')),
)
```
- **Users Table:** Contains `id`, `name`, `age`, `city`.
- **Posts Table:** Contains `id`, `title`, `content`, `user_id` (ForeignKey to users table).

### 2.4 Creating Tables
```python
metadata.create_all(engine)
```
- Creates tables if they do not already exist.

### 2.5 Inserting Data
```python
with engine.begin() as con:
    insert_stmt = insert(users).values(name='John', age=20, city='New York')
    result = con.execute(insert_stmt)
    print(f"Inserted {result.rowcount} user(s).")

    insert_stmt = insert(posts).values(title='Post 1', content='Content 1', user_id=1)
    result = con.execute(insert_stmt)
    print(f"Inserted {result.rowcount} post(s).")
```
- Inserts a user and a post into their respective tables.

### 2.6 Querying Data
```python
with engine.connect() as con:
    select_stmt = select(users)
    result = con.execute(select_stmt)
    print("\nUsers Table:")
    for row in result:
        print(row)
```
- Retrieves all records from the `users` table.

```python
with engine.connect() as con:
    select_stmt = select(posts)
    result = con.execute(select_stmt)
    print("\nPosts Table:")
    for row in result:
        print(row)
```
- Retrieves all records from the `posts` table.

### 2.7 SQLite Version and Debugging
```python
import os
from sqlalchemy import create_engine

db_path = os.getenv("SQLITE_DB_PATH", "sqlite:///default.db")
engine = create_engine(f"sqlite:///{db_path}")
print(engine.url.database)
```
- Fetches the database path from an environment variable or defaults to `default.db`.

```python
import sqlite3
print("SQLAlchemy Version:", create_engine('sqlite://').dialect.dbapi.sqlite_version)
print("Python SQLite Version:", sqlite3.sqlite_version)
```
- Prints the SQLite version used by SQLAlchemy.

```python
print(sqlite3.connect(':memory:').execute('select sqlite_version()').fetchone())
```
- Runs an in-memory SQLite query to check the SQLite version.

```python
import os
print(os.getcwd())
```
- Prints the current working directory.


