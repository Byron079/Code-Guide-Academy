# Python Cheat Sheet

A condensed, at-a-glance reference for everyday Python syntax. Keep this open while you code.

---

## 1. Variables & Data Types

```python
name = "Byron"        # str
age = 21               # int
height = 1.78          # float
is_student = True      # bool
nothing = None         # NoneType

print(type(name))      # check a variable's type
```

| Type | Example | Notes |
|---|---|---|
| `int` | `42` | Whole numbers |
| `float` | `3.14` | Decimal numbers |
| `str` | `"hello"` | Text |
| `bool` | `True` / `False` | Logical value |
| `list` | `[1, 2, 3]` | Ordered, changeable |
| `tuple` | `(1, 2, 3)` | Ordered, unchangeable |
| `dict` | `{"a": 1}` | Key-value pairs |
| `set` | `{1, 2, 3}` | Unique, unordered |

**Type conversion:** `int("5")`, `float("3.5")`, `str(42)`, `bool(1)`

---

## 2. Operators

| Category | Operators |
|---|---|
| Arithmetic | `+  -  *  /  //  %  **` |
| Comparison | `==  !=  >  <  >=  <=` |
| Logical | `and  or  not` |
| Assignment | `=  +=  -=  *=  /=  //=  %=  **=` |
| Membership | `in  not in` |
| Identity | `is  is not` |

```python
17 // 4   # 4   (floor division)
17 % 4    # 1   (remainder)
2 ** 5    # 32  (exponent)
```

---

## 3. Strings

```python
s = "Hello, World!"
s.lower(); s.upper(); s.strip()
s.replace("World", "Python")
s.split(",")            # -> list
"-".join(["a", "b"])    # -> "a-b"
len(s)
s[0]          # indexing
s[7:12]       # slicing
s[::-1]       # reverse

name, age = "Byron", 21
f"{name} is {age} years old"   # f-string (preferred)
```

---

## 4. Control Flow

```python
if score >= 90:
    grade = "A"
elif score >= 70:
    grade = "B"
else:
    grade = "F"

# Ternary (inline if)
status = "Pass" if score >= 50 else "Fail"
```

---

## 5. Loops

```python
for i in range(5):          # 0 1 2 3 4
    print(i)

for item in [1, 2, 3]:
    print(item)

for i, item in enumerate(["a", "b"]):
    print(i, item)

while condition:
    ...
    break       # exit loop
    continue    # skip to next iteration
```

---

## 6. Functions

```python
def greet(name, greeting="Hello"):
    """Docstring: describe what this function does."""
    return f"{greeting}, {name}!"

def add_all(*args):        # variable positional args -> tuple
    return sum(args)

def info(**kwargs):        # variable keyword args -> dict
    return kwargs

square = lambda x: x ** 2  # anonymous one-line function
```

---

## 7. Data Structures

```python
# List
lst = [3, 1, 2]
lst.append(4); lst.insert(0, 99); lst.remove(1); lst.sort()
squares = [x**2 for x in lst]              # comprehension

# Tuple (immutable)
point = (10, 20)
x, y = point

# Set
s1, s2 = {1, 2}, {2, 3}
s1 | s2   # union
s1 & s2   # intersection
s1 - s2   # difference

# Dictionary
d = {"name": "Byron", "age": 21}
d["age"] = 22
d.get("email", "N/A")
for k, v in d.items():
    print(k, v)
squares_dict = {x: x**2 for x in range(5)} # comprehension
```

---

## 8. Error Handling

```python
try:
    risky()
except ValueError:
    print("Bad value")
except (TypeError, KeyError) as e:
    print(f"Error: {e}")
else:
    print("No errors")
finally:
    print("Always runs")

raise ValueError("Custom error message")
```

| Exception | Cause |
|---|---|
| `ValueError` | Right type, wrong value |
| `TypeError` | Wrong/incompatible type |
| `ZeroDivisionError` | Division by zero |
| `IndexError` | Bad list/tuple index |
| `KeyError` | Missing dict key |
| `FileNotFoundError` | Missing file |

---

## 9. Files

```python
with open("file.txt", "w") as f:
    f.write("line\n")

with open("file.txt", "r") as f:
    content = f.read()
    # or: for line in f: ...

# JSON
import json
json.dump(data, open("data.json", "w"), indent=4)
data = json.load(open("data.json"))

# CSV
import csv
csv.writer(open("f.csv", "w", newline="")).writerow(["a", "b"])
```

File modes: `"r"` read · `"w"` overwrite · `"a"` append · `"x"` create (fails if exists)

---

## 10. Object-Oriented Programming

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "..."

    def __str__(self):
        return f"Animal({self.name})"

class Dog(Animal):              # inheritance
    def speak(self):            # overriding (polymorphism)
        return f"{self.name} says Woof!"

d = Dog("Rex")
print(d.speak())
```

- `__init__` — constructor, runs on object creation
- `super().__init__(...)` — call the parent's constructor
- `self.__attr` — "private" attribute (name-mangled)
- `@staticmethod`, `@classmethod`, `@property` — common decorators
- `from abc import ABC, abstractmethod` — for abstract base classes

---

## 11. Comprehensions & Functional Tools

```python
[x**2 for x in range(10) if x % 2 == 0]     # list comprehension
{x: x**2 for x in range(5)}                  # dict comprehension
{x for x in [1,1,2,3]}                       # set comprehension

list(map(lambda x: x*2, nums))
list(filter(lambda x: x > 5, nums))
sorted(people, key=lambda p: p[1], reverse=True)
```

---

## 12. Useful Standard Library Modules

| Module | Purpose |
|---|---|
| `math` | sqrt, floor, ceil, pi |
| `random` | randint, choice, shuffle |
| `datetime` | dates and times |
| `os` | filesystem, paths, env vars |
| `sys` | interpreter/argv access |
| `re` | regular expressions |
| `collections` | Counter, defaultdict, namedtuple |
| `json` | JSON encode/decode |
| `sqlite3` | embedded database |
| `logging` | structured application logging |

---

## 13. Regex Quick Reference

| Symbol | Meaning |
|---|---|
| `\d` | digit | `\w` | word character | `\s` | whitespace |
| `.` | any character | `*` | 0 or more | `+` | 1 or more |
| `^` `$` | start / end of string | `{n}` | exactly n times |

```python
import re
re.findall(r"[\w.-]+@[\w.-]+\.\w+", text)   # find emails
re.sub(r"\d", "*", text)                     # replace digits
re.match(r"^\d{3}-\d{4}$", text)             # validate format
```

---

## 14. Virtual Environments & pip

```bash
python -m venv venv              # create
source venv/bin/activate         # activate (Mac/Linux)
venv\Scripts\activate            # activate (Windows)
pip install package_name
pip freeze > requirements.txt
pip install -r requirements.txt
deactivate
```

---

## 15. Common Built-in Functions

`len()` `type()` `range()` `sorted()` `enumerate()` `zip()` `sum()` `min()` `max()`
`isinstance()` `input()` `print()` `open()` `map()` `filter()` `abs()` `round()`

---

## 16. PEP 8 Essentials

- 4 spaces per indent, never tabs
- `snake_case` for variables/functions, `PascalCase` for classes
- 2 blank lines between top-level functions/classes
- Docstrings on public functions and classes
- Keep lines under ~99 characters
- Let **Black** (formatter) and **Ruff** (linter) enforce style automatically
