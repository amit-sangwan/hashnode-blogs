---
title: "Python Basics"
seoTitle: "Brushing up on python core concepts"
seoDescription: "Learn Python basics, from variables and data types to loops, functions, OOP, and more essential concepts and syntax in programming"
datePublished: Mon May 26 2025 11:41:31 GMT+0000 (Coordinated Universal Time)
cuid: cmb50ojik001g09lehxnb1bgi
slug: python-basics
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/D9Zow2REm8U/upload/342c69df93d8649db6d4f057b7b7d158.jpeg
tags: python, python-beginner, revision, ai-testing-tools

---

## 1\. Variables

Variables store data in memory that can be referenced later.

```plaintext
name = "Amit"
age = 33
```

---

## 2\. Data Types

Python has several built-in data types:

* `int`: Integer numbers
    
* `float`: Decimal numbers
    
* `str`: Strings (text)
    
* `bool`: Boolean (True/False)
    
* `list`, `tuple`, `dict`, `set`: Collections
    

```plaintext
x = 10           # int
y = 3.14         # float
text = "Hello"   # str
flag = True      # bool
```

---

## 3\. Naming Conventions

Follow PEP8 guidelines:

* Variables/functions: `snake_case`
    
* Classes: `CamelCase`
    

```plaintext
user_name = "john_doe"
class PersonInfo:
    pass
```

---

## 4\. Operators

* Arithmetic: `+`, `-`, `*`, `/`, `%`, `**`, `//` – perform math operations
    
* Comparison: `==`, `!=`, `>`, `<`, `>=`, `<=` – compare values
    
* Logical: `and`, `or`, `not` – combine Boolean expressions
    
* Assignment: `=`, `+=`, `-=` etc. – assign and update values
    
* Identity: `is`, `is not` – check object identity
    
* Membership: `in`, `not in` – check element existence
    
* Bitwise: `&`, `|`, `^`, `~`, `<<`, `>>` – operate on bits
    

```plaintext
x, y = 5, 2
print(x + y)       # 7
print(x > y)       # True
print(x and y)     # 2
```

---

## 5\. Type Casting

Convert between data types using constructors.

```plaintext
int("5")        # 5
float("3.14")   # 3.14
str(10)         # "10"
```

---

## 6\. type() Function

Returns the data type of the object.

```plaintext
type(42)        # <class 'int'>
type("abc")    # <class 'str'>
```

---

## 7\. Strings and Methods

Strings are immutable and have many useful methods.

```plaintext
msg = "  python programming  "
print(msg.upper())          # Convert to uppercase
print(msg.lower())          # Convert to lowercase
print(msg.strip())          # Remove leading/trailing whitespace
print(msg.capitalize())     # Capitalize first letter
print(msg.title())          # Capitalize each word
print(msg.replace("python", "java"))  # Replace substring
print(msg.startswith(" ")) # Check prefix
print(msg.endswith("g  ")) # Check suffix
print(msg.find("pro"))     # Find index of substring
print(msg.count("m"))       # Count occurrences
print(msg.isalpha())        # Check if all chars are letters
print(msg.isdigit())        # Check if all chars are digits
print(msg.split())          # Split by whitespace
print("-".join(["code", "with", "amit"]))  # Join with delimiter
print(msg.islower())        # Check if all lowercase
print(msg.isupper())        # Check if all uppercase
print(msg.isspace())        # Check if all whitespace
print(msg.center(30, "-"))  # Center the string
print(msg.ljust(25, "."))   # Left justify with padding
print(msg.rjust(25, "."))   # Right justify with padding
```

---

## 8\. Conditional Statements

Control flow using `if`, `elif`, and `else`.

```plaintext
if age < 18:
    print("Minor")
elif age == 18:
    print("Just Adult")
else:
    print("Adult")
```

---

## 9\. Collections

* `list`: Ordered, mutable
    
* `tuple`: Ordered, immutable
    
* `set`: Unordered, unique
    
* `dict`: Key-value pairs
    

```plaintext
lst = [1, 2, 3]
tpl = (1, 2)
st = {1, 2, 2}
dct = {"a": 1, "b": 2}
```

### Common Methods:

**List**:

```plaintext
lst.append(4)        # Add to end
lst.extend([5, 6])   # Extend list
lst.insert(1, 9)     # Insert at index
lst.remove(2)        # Remove value
lst.pop()            # Remove last item
lst.index(3)         # Get index of value
lst.count(1)         # Count occurrences
lst.sort()           # Sort list
lst.reverse()        # Reverse list
lst.clear()          # Clear list
lst.copy()           # Copy list
lst[1:4]             # Slice list
```

**Tuple**:

```plaintext
tpl.count(1)         # Count occurrences
tpl.index(2)         # Get index of value
```

**Set**:

```plaintext
st.add(3)                  # Add element
st.remove(1)               # Remove element
st.discard(10)             # Discard safely
st.update([4, 5])          # Add multiple
st.union({6, 7})           # Union sets
st.intersection({2, 3})    # Common elements
st.difference({2})         # Unique elements
st.symmetric_difference({3})  # Non-common elements
print(len(st))             # Size of set
print(2 in st)             # Membership check
st.pop()                   # Remove arbitrary item
```

**Dict**:

```plaintext
dct.keys()               # Get all keys
dct.values()             # Get all values
dct.items()              # Get key-value pairs
dct.get("a")              # Get value safely
dct.update({"c": 3})     # Add/update entries
dct.pop("b")              # Remove key
dct.popitem()            # Remove last inserted
dct.setdefault("d", 4)   # Set default if not present
dct.clear()              # Clear dictionary
print("a" in dct)         # Check key existence
```

---

## 10\. Loops

Use loops to iterate over sequences.

```plaintext
# For loop using range
for i in range(3):
    print(i)

# For loop over list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# Using enumerate
for index, fruit in enumerate(fruits):
    print(index, fruit)

# While loop
i = 0
while i < 3:
    print(i)
    i += 1
```

---

## 11\. Slice Operator

Extract parts of a sequence using `start:stop:step` syntax.

```plaintext
text = "Python"
print(text[1:4])     # 'yth' from index 1 to 3
print(text[:3])      # 'Pyt' from start to index 2
print(text[::2])     # 'Pto' with step 2
print(text[::-1])    # 'nohtyP' (reverse string)
nums = list(range(10))
print(nums[2:8:2])   # [2, 4, 6] from index 2 to 7, step 2
```

---

## 12\. range() and len()

* `range()`: Generates a sequence of numbers
    
* `len()`: Returns the length
    

```plaintext
for i in range(5): print(i)
print(len("hello"))  # 5
```

---

## 13\. List Comprehension

Concise way to build lists.

```plaintext
squares = [x*x for x in range(5)]  # [0, 1, 4, 9, 16]
evens = [x for x in range(10) if x%2 == 0]
```

---

## 14\. Functions

Reusable blocks of code.

```plaintext
def greet(name):
    return f"Hello, {name}"

print(greet("Amit"))
```

---

## 15\. None Keyword

Represents the absence of a value.

```plaintext
value = None
```

---

## 16\. Unpacking Operators (\* and \*\*)

* `*` unpacks lists/tuples
    
* `**` unpacks dictionaries
    

```plaintext
a, *b = [1, 2, 3, 4]
def func(a, b, c): pass
func(**{'a':1, 'b':2, 'c':3})
```

---

## 17\. global Keyword

Modify a global variable inside a function.

```plaintext
count = 0

def increment():
    global count
    count += 1
```

---

## 18\. raise Exception

Used to raise user-defined exceptions.

```plaintext
if age < 0:
    raise ValueError("Age cannot be negative")
```

---

## 19\. Lambda Functions

Anonymous single-expression functions.

```plaintext
square = lambda x: x * x
print(square(5))  # 25
```

---

## 20\. map() and filter()

Apply functions to sequences.

```plaintext
nums = [1, 2, 3, 4]
print(list(map(lambda x: x*2, nums)))      # [2, 4, 6, 8]
print(list(map(str, nums)))               # ['1', '2', '3', '4']
print(list(filter(lambda x: x%2 == 0, nums)))  # [2, 4]
print(list(filter(lambda x: x > 2, nums)))     # [3, 4]

names = ["Anna", "Ben", "Amy", "Tom"]
print(list(filter(lambda name: name.startswith("A"), names)))  # ['Anna', 'Amy']
print(list(map(lambda name: name.upper(), names)))  # ['ANNA', 'BEN', 'AMY', 'TOM']
```

---

## 21\. f-Strings

Modern way to format strings.

```plaintext
name = "Amit"
age = 33
print(f"Hello, {name}. You are {age} years old.")
```

---

## 22\. Exception Handling – try, except, finally, else

```plaintext
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Cannot divide by zero")
else:
    print("No exceptions occurred")
finally:
    print("This block always runs")
```

---

## 23\. File Handling – open(), read(), write(), with

```plaintext
# Writing to a file
with open("test.txt", "w") as file:
    file.write("Hello World")

# Reading from a file
with open("test.txt", "r") as file:
    content = file.read()
    print(content)

# JSON file handling
import json

data = {"name": "Amit", "age": 33}

with open("data.json", "w") as json_file:
    json.dump(data, json_file)

with open("data.json", "r") as json_file:
    loaded = json.load(json_file)
    print(loaded)

# Excel file handling using pandas
import pandas as pd

# Reading Excel file
df = pd.read_excel("sample.xlsx")
print(df.head())

# Writing to Excel file
df.to_excel("output.xlsx", index=False)
```

---

## 24\. Modules & Imports – import, from, built-in modules

```plaintext
import math
from datetime import datetime
print(math.sqrt(16))
print(datetime.now())
```

### Commonly Used Libraries

* `os` – for interacting with the operating system (e.g., `os.listdir()`)
    
* `sys` – for command line args and system-level ops (e.g., `sys.argv`)
    
* `json` – for working with JSON data (e.g., `json.load()`)
    
* `re` – for regular expressions (e.g., `re.match()`)
    
* `collections` – for specialized containers (e.g., `Counter`, `defaultdict`)
    
* `datetime` – for manipulating dates and times
    
* `random` – for generating random numbers
    
* `pandas` – for data analysis and manipulation (e.g., `pd.read_csv()`)
    
* `numpy` – for numerical operations
    
* `matplotlib.pyplot` – for data visualization (e.g., `plt.plot()`)
    

---

## 25\. Classes & OOP Basics – class, **init**(), self, inheritance

Object-Oriented Programming (OOP) in Python allows modeling real-world entities as classes.

* `class`: Defines the blueprint
    
* `__init__`: Constructor to initialize object state
    
* `self`: Refers to instance of the class
    
* Inheritance: One class inherits properties of another
    

```plaintext
class Animal:
    def __init__(self, name):
        self.name = name
    def speak(self):
        return f"{self.name} makes a sound"

class Dog(Animal):
    def speak(self):
        return f"{self.name} barks"

d = Dog("Rex")
print(d.speak())
```

---

## 26\. isinstance() and issubclass()

* `isinstance(obj, Class)`: Checks if an object is an instance of a class or its subclass
    
* `issubclass(SubClass, Class)`: Checks if a class is derived from another class
    

```plaintext
print(isinstance(5, int))           # True
print(isinstance("abc", str))      # True
print(issubclass(Dog, Animal))      # True
print(issubclass(Animal, object))   # True
```

---

## 27\. Pass, Break, Continue – loop control keywords

```plaintext
for i in range(5):
    if i == 2:
        continue  # Skip iteration
    elif i == 4:
        break     # Exit loop
    print(i)

# Placeholder function

def future_feature():
    pass
```

---