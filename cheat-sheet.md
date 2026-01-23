# 🐍 Cheat Sheet
_Commonly Used Code Snippets_

Bu doküman, Python öğrenirken ve çalışırken en sık kullanılan yapıların **hızlı bir referans (cheat sheet)** halidir.

---

## 1. Basic Python Syntax

### Print to Console
```python
print("Hello, World!")
```

### Variable Assignment
```python
x = 10
```

### Commenting
```python
# This is a comment
```

### Multi-line Comment (Docstring)
```python
"""
This is a multi-line comment
"""
```

### Input from User
```python
name = input("Enter your name: ")
```

### Check Data Type
```python
type(x)
```

### Type Casting
```python
int("10")
float("10.5")
str(100)
```

---

## 2. Data Structures

### List (Array)
```python
my_list = [1, 2, 3, 4, 5]
```

### Access List Item
```python
my_list[0]
```

### List Slicing
```python
my_list[1:4]
```

### Add Item to List
```python
my_list.append(6)
```

### Remove Item from List
```python
my_list.remove(3)
```

### Tuple
```python
my_tuple = (1, 2, 3, 4)
```

### Set
```python
my_set = {1, 2, 3, 4}
```

### Dictionary (HashMap)
```python
my_dict = {
    "key1": "value1",
    "key2": "value2"
}
```

### Access Dictionary Value
```python
my_dict["key1"]
```

### Add Key-Value Pair
```python
my_dict["key3"] = "value3"
```

---

## 3. Control Flow

### If Statement
```python
if x > 10:
    print("x is greater than 10")
```

### If-Else Statement
```python
if x > 10:
    print("x is greater than 10")
else:
    print("x is less than or equal to 10")
```

### Elif Statement
```python
if x > 10:
    print("x is greater")
elif x == 10:
    print("x is 10")
else:
    print("x is smaller")
```

### For Loop
```python
for i in range(5):
    print(i)
```

### While Loop
```python
while x < 10:
    x += 1
```

### Break
```python
for i in range(5):
    if i == 3:
        break
```

### Continue
```python
for i in range(5):
    if i == 3:
        continue
```

---

## 4. Functions

### Define Function
```python
def my_function():
    print("Hello from function!")
```

### Function with Parameters
```python
def greet(name):
    print(f"Hello, {name}!")
```

### Return Value from Function
```python
def add(a, b):
    return a + b
```

### Lambda Function
```python
add = lambda a, b: a + b
```

---

## 5. String Manipulation

### Concatenate Strings
```python
full_name = "John" + " " + "Doe"
```

### String Length
```python
len("Hello")
```

### Convert to Upper Case
```python
"hello".upper()
```

### Convert to Lower Case
```python
"HELLO".lower()
```

### Substring
```python
"Hello, World!"[7:12]
```

### Find Substring
```python
"Hello, World!".find("World")
```

### Replace Substring
```python
"Hello, World!".replace("World", "Python")
```

### Split Substring
```python
"Hello, World!".split(", ")
```

---

## 6. File Handling

### Open a File
```python
file = open("example.txt", "r")
```

### Read File
```python
content = file.read()
```

### Read Line by Line
```python
lines = file.readlines()
```

### Write to File
```python
file = open("example.txt", "w")
file.write("Hello, World!")
```

### Close a File
```python
file.close()
```
> ✅ Best Practice:
```python
with open("example.txt", "r") as file:
    content = file.read()
```

---

## 7. List Comprehension

### Basic List Comprehension
```python
[x**2 for x in range(5)]
```

### With Condition
```python
[x for x in range(10) if x % 2 == 0]
```

---

## 8. Error Handling

### Try-Except
```python
try:
    x = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
```

### Try-Except-Finally
```python
try:
    x = 10 / 0
except ZeroDivisionError:
    print("Error!")
finally:
    print("This runs always")
```

---

## 9. Working with Libraries

### Importing a Library
```python
import math
```

### Using a Library Function
```python
math.sqrt(16)
```

### Install a Library (pip)
```python
pip install pandas
```

### Import Specific Function
```python
from math import sqrt
```

---

## 9. Working with Libraries

### Importing a Library
```python
import math
```

### Using a Library Function
```python
math.sqrt(16)
```

### Install a Library (pip)
```python
pip install pandas
```

### Import Specific Function
```python
from math import sqrt
```

---

## 10. NumPy for Numerical Operations

### Import NumPy
```python
import numpy as np
```

### Create NumPy Array
```python
arr = np.array([1, 2, 3, 4, 5])
```

### Array Reshaping
```python
arr.reshape(5, 1)
```

### Array Operations
```python
arr + 10
arr * 2
```

### Array Slicing
```python
arr[1:4]
```

### Array Operations
```python
np.mean(arr)
np.median(arr)
np.std(arr)
```

---

## 11. Pandas for Data Handling

### Import Pandas
```python
import pandas as pd
```

### Create DataFrame
```python
df = pd.DataFrame({
    "Name": ["Alice", "Bob"],
    "Age": [25, 30]
})
```

### Read CSV File
```python
df = pd.read_csv("data.csv")
```

### View Data
```python
df.head()
```

---

## 12. Matplotlib for Visualization

### Import Matplotlib
```python
import matplotlib.pyplot as plt
```

### Simple Plot
```python
plt.plot([1, 2, 3], [4, 5, 6])
plt.show()
```

### Bar Plot
```python
plt.bar([1, 2, 3], [4, 5, 6])
plt.show()
```

### Histogram
```python
plt.hist([1, 2, 2, 3, 4, 5])
plt.show()
```

### Scatter Plot
```python
plt.scatter([1, 2, 3], [4, 5, 6])
plt.show()
```
