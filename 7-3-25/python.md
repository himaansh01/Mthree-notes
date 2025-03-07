# OOPS Documentation

## Overview
This Python script demonstrates several concepts including:
- Object-Oriented Programming (OOP) with inheritance, method overloading, and overriding.
- Copying objects using shallow and deep copy.
- File system operations including creating, writing, reading, appending, deleting files, checking file existence, retrieving file information, and directory management.

---

## Class Definitions

### Animal Class
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"Animal {self.name}"

    def speak(self):
        print(f"Animal {self.name} is speaking")
```
**Description**: 
- The base class for all animals.
- Contains a `speak` method and `__str__` method.

### Dog Class (Inheritance, Method Overloading & Overriding)
```python
class Dog(Animal):
    def __str__(self):
        return f"Dog {self.name}"

    def speak(self, age=None):
        if age is None:
            print(f"Dog {self.name} is barking")
        else:
            print(f"Dog {self.name} is barking and {age} years old coming from Method Overloading")

    def speaks(self, age, name):
        return f"Dog {name} is barking and {age} years old"
```
**Description**: 
- Inherits from `Animal`.
- Overrides `speak` method to demonstrate method overloading using default parameters.
- Adds a `speaks` method that requires both `age` and `name`.

### Cat and Bird Classes
```python
class Cat(Animal):
    def speak(self):
        print(f"Cat {self.name} is meowing")

class Bird(Animal):
    def speak(self):
        print(f"Bird {self.name} is chirping")
```
**Description**:
- Both `Cat` and `Bird` inherit from `Animal` and override the `speak` method.

---

## Object Copying (Shallow vs Deep Copy)
```python
import copy

class Person:
    def __init__(self, name, address):
        self.name = name
        self.address = address

    def __repr__(self):
        return f"Person(name={self.name}, address={self.address})"

class Address:
    def __init__(self, city, country):
        self.city = city
        self.country = country

    def __repr__(self):
        return f"Address(city={self.city}, country={self.country})"
```
**Description**:
- Demonstrates object copying in Python.
- Uses `copy.copy()` for shallow copy and `copy.deepcopy()` for deep copy.

**Example Execution**:
```python
# Create a person with an address
address = Address("New York", "USA")
person = Person("John", address)

# Create copies
shallow_person = copy.copy(person)
deep_person = copy.deepcopy(person)
```

---

## File System Operations
```python
import os

def create_file():
    with open("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py", "w") as file:
        file.write("Hello, World!")

def write_to_file():
    with open("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py", "w") as file:
        file.write("Hello, Python!")

def read_from_file():
    with open("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py", "r") as file:
        print(file.read())

def append_to_file():
    with open("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py", "a") as file:
        file.write("\nAppending some text!")

def delete_file():
    if os.path.exists("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py"):
        os.remove("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py")
    else:
        print("File does not exist.")

def check_if_file_exists():
    if os.path.exists("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py"):
        print("File exists")
    else:
        print("File does not exist")

def get_current_working_directory():
    print("Current Working Directory:", os.getcwd())

def list_files_in_directory():
    print("Files in directory:", os.listdir("."))

def get_size_of_file():
    if os.path.exists("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py"):
        print("File Size:", os.path.getsize("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py"), "bytes")
    else:
        print("File does not exist.")

def get_last_modified_time_of_file():
    if os.path.exists("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py"):
        print("Last Modified Time:", os.path.getmtime("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py"))
    else:
        print("File does not exist.")

def get_file_name():
    print("File Name:", os.path.basename("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py"))

def get_file_extension():
    print("File Extension:", os.path.splitext("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py")[1])

def get_file_path():
    print("File Path:", os.path.abspath("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py"))

def get_file_directory():
    print("File Directory:", os.path.dirname("D:\\backup\\python3\\basic-module\\src\\basic_module\\datastructure\\oops3.py"))
```

---

## Conclusion

- This script demonstrates various Python programming concepts, including OOP, object copying, and file operations.
- It provides practical examples of how to manage objects, their copies, and file handling in Python.

This documentation is ready to be pushed into GitHub along with the script.

