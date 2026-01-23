# 🐍 Python Cheat Sheet
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
