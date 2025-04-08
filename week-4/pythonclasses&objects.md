# 🐍 Python OOP & Exception Handling - Explained Simply

---

## 🔹 1. Constructors (`__init__`)
Constructors are special methods in Python that are automatically triggered when a new object is created. Their job is to initialize object properties.

### ✅ Example
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return f"{self.name} makes a sound."

lion = Animal("Lion")
print(lion.speak())  # Lion makes a sound.
```

### ⚠️ Common Mistakes
- Using `_init_` instead of `__init__`
- Forgetting the `self` parameter in method definitions

---

## 🔹 2. Destructors (`__del__`)
Destructors are automatically invoked when an object is deleted or goes out of scope, often used for cleanup.

### ✅ Example
```python
class Person:
    def __init__(self, name):
        self.name = name
        print(f"{self.name} is created.")

    def __del__(self):
        print(f"{self.name} is destroyed.")

p = Person("Alice")
del p  # Triggers destructor
```

### ⚠️ Common Mistakes
- Writing `_del_` instead of `__del__`

---

## 🔹 3. Shallow vs Deep Copy
The `copy` module in Python lets you duplicate objects.

### 🧪 Shallow Copy (`copy.copy()`)
Only top-level objects are copied. Nested objects remain shared.

```python
import copy

class Address:
    def __init__(self, city, country):
        self.city = city
        self.country = country

class Person:
    def __init__(self, name, address):
        self.name = name
        self.address = address

original = Person("John", Address("NY", "USA"))
shallow = copy.copy(original)

original.address.city = "Boston"
print(shallow.address.city)  # Boston - shared reference
```

### 🧪 Deep Copy (`copy.deepcopy()`)
Everything, including nested objects, gets duplicated.

```python
import copy

deep = copy.deepcopy(original)
original.address.city = "Chicago"
print(deep.address.city)  # Still Boston - separate copy
```

### ⚠️ Mistakes
- Using `=` instead of `copy.copy()` or `copy.deepcopy()` will only copy the reference.
- Use `deepcopy()` for fully independent objects.

---

## 🔹 4. Common Method Mistakes in OOP
| Mistake | Fix |
|--------|-----|
| `_init_` instead of `__init__` | Use `__init__` |
| `_str_` instead of `__str__` | Use `__str__` |
| Overriding methods improperly | Use `*args` for flexibility |
| `if _name_ == "_main_"` | Use `if __name__ == "__main__"` |

---

## 🔹 5. Exception Handling in Python

### ✅ Structure
- `try`: Code that may raise an exception
- `except`: Catch errors
- `finally`: Always runs, even if there’s an error

### 🔸 Basic Example
```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print("Error:", e)
finally:
    print("Cleanup happens here.")
```

### 🔸 Multiple Exceptions
```python
try:
    num = int(input("Enter a number: "))
    result = 10 / num
except ZeroDivisionError:
    print("You can't divide by zero.")
except ValueError:
    print("Please enter a valid number.")
finally:
    print("Execution done.")
```

---

## 🔹 6. Custom Exceptions
You can create your own exceptions by inheriting from `Exception`.

```python
class CustomException(Exception):
    def __init__(self, message):
        self.message = message
        super().__init__(self.message)

try:
    raise CustomException("Something went wrong!")
except CustomException as e:
    print("Caught:", e)
finally:
    print("End of custom exception block.")
```

---

## 🔹 7. Common Exceptions in Python

| Exception | Trigger Example |
|----------|-----------------|
| `ZeroDivisionError` | `10 / 0` |
| `ValueError` | `int("abc")` |
| `TypeError` | `"str" + 5` |
| `IndexError` | `list[10]` |
| `KeyError` | `dict["missing"]` |
| `AttributeError` | `"str".fake()` |
| `FileNotFoundError` | `open("notfound.txt")` |

---

## 🔹 8. Using `else` in `try-except`

```python
try:
    num = int(input("Number: "))
    result = 10 / num
except ZeroDivisionError:
    print("Division by zero!")
else:
    print("Result is", result)
finally:
    print("Always runs.")
```

---

## ✅ Summary
- Use `__init__` and `__del__` correctly for object lifecycle management.
- Understand the difference between shallow and deep copies.
- Handle exceptions with `try-except-finally` and optionally `else`.
- Create custom exceptions when built-in ones don’t fit.

---

🚀 Mastering OOP and exceptions makes your Python code robust and scalable!
