# Python Code Samples

A library of ready-to-copy snippets for common tasks. Each one is self-contained — paste it in, adjust the details, and run.

---

## Input Validation Loop

```python
def get_valid_int(prompt, minimum=None, maximum=None):
    while True:
        try:
            value = int(input(prompt))
            if minimum is not None and value < minimum:
                print(f"Must be at least {minimum}.")
                continue
            if maximum is not None and value > maximum:
                print(f"Must be at most {maximum}.")
                continue
            return value
        except ValueError:
            print("Please enter a whole number.")

age = get_valid_int("Enter your age: ", minimum=0, maximum=120)
```

---

## Reading and Writing JSON Safely

```python
import json
import os

def load_json(path, default=None):
    if not os.path.exists(path):
        return default if default is not None else {}
    with open(path, "r") as f:
        return json.load(f)

def save_json(path, data):
    with open(path, "w") as f:
        json.dump(data, f, indent=4)

settings = load_json("settings.json", default={"theme": "dark"})
settings["last_opened"] = "2026-09-08"
save_json("settings.json", settings)
```

---

## Class Template with Encapsulation

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.__balance = balance          # "private" attribute

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        self.__balance += amount

    def withdraw(self, amount):
        if amount > self.__balance:
            raise ValueError("Insufficient funds")
        self.__balance -= amount

    def get_balance(self):
        return self.__balance

    def __str__(self):
        return f"{self.owner}'s account: R{self.__balance:.2f}"

account = BankAccount("Byron", 500)
account.deposit(150)
print(account)
```

---

## Custom Exception

```python
class InsufficientStockError(Exception):
    """Raised when trying to sell more stock than is available."""
    pass

def sell(stock, quantity):
    if quantity > stock:
        raise InsufficientStockError(f"Only {stock} left in stock")
    return stock - quantity

try:
    sell(5, 10)
except InsufficientStockError as e:
    print(f"Sale failed: {e}")
```

---

## Timing Decorator

```python
import time
from functools import wraps

def timer(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print(f"{func.__name__} took {time.time() - start:.4f}s")
        return result
    return wrapper

@timer
def slow_task():
    time.sleep(1)

slow_task()
```

---

## Logging Setup

```python
import logging

logging.basicConfig(
    filename="app.log",
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s",
)

logging.info("Application started")
logging.warning("Config file missing, using defaults")
logging.error("Failed to connect to the database")
```

---

## CSV Read/Write with `csv.DictReader`/`DictWriter`

```python
import csv

# Writing
rows = [{"name": "Byron", "score": 88}, {"name": "Alex", "score": 72}]
with open("scores.csv", "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=["name", "score"])
    writer.writeheader()
    writer.writerows(rows)

# Reading
with open("scores.csv", "r") as f:
    for row in csv.DictReader(f):
        print(row["name"], row["score"])
```

---

## Simple REST API Call with Error Handling

```python
import requests

def get_json(url, params=None):
    try:
        response = requests.get(url, params=params, timeout=5)
        response.raise_for_status()      # raises for 4xx/5xx status codes
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        return None

data = get_json("https://api.github.com/users/python")
if data:
    print(data["name"], data["public_repos"])
```

---

## SQLite CRUD Helper

```python
import sqlite3

def get_connection(db_name="app.db"):
    return sqlite3.connect(db_name)

def create_table():
    with get_connection() as conn:
        conn.execute("""
            CREATE TABLE IF NOT EXISTS notes (
                id INTEGER PRIMARY KEY,
                title TEXT NOT NULL,
                content TEXT
            )
        """)

def add_note(title, content):
    with get_connection() as conn:
        conn.execute(
            "INSERT INTO notes (title, content) VALUES (?, ?)",
            (title, content),
        )

def get_all_notes():
    with get_connection() as conn:
        return conn.execute("SELECT * FROM notes").fetchall()

create_table()
add_note("Shopping", "Milk, eggs, bread")
print(get_all_notes())
```

---

## Basic pytest Test File

```python
# calculator.py
def add(a, b):
    return a + b

def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")
    return a / b

# test_calculator.py
import pytest
from calculator import add, divide

def test_add():
    assert add(2, 3) == 5

def test_divide():
    assert divide(10, 2) == 5

def test_divide_by_zero_raises():
    with pytest.raises(ZeroDivisionError):
        divide(10, 0)

# Run with: pytest
```

---

## Command-Line Argument Parsing

```python
import argparse

parser = argparse.ArgumentParser(description="Greet a user")
parser.add_argument("name", help="Name of the person to greet")
parser.add_argument("--shout", action="store_true", help="Print in uppercase")
args = parser.parse_args()

message = f"Hello, {args.name}!"
print(message.upper() if args.shout else message)

# Run: python script.py Byron --shout
```

---

## Environment Variables (.env pattern)

```python
import os
from dotenv import load_dotenv    # pip install python-dotenv

load_dotenv()   # reads variables from a .env file into the environment

api_key = os.environ.get("API_KEY")
if not api_key:
    raise RuntimeError("API_KEY is not set - check your .env file")
```

```
# .env file (add this filename to .gitignore!)
API_KEY=your-secret-key-here
```

---

## Minimal Flask API

```python
from flask import Flask, jsonify, request

app = Flask(__name__)
tasks = []

@app.route("/tasks", methods=["GET"])
def get_tasks():
    return jsonify(tasks)

@app.route("/tasks", methods=["POST"])
def add_task():
    task = request.json
    tasks.append(task)
    return jsonify(task), 201

if __name__ == "__main__":
    app.run(debug=True)
```

---

## Useful One-Liners

```python
# Remove duplicates while keeping order
list(dict.fromkeys([1, 2, 2, 3, 1]))          # [1, 2, 3]

# Flatten a list of lists
sum([[1, 2], [3, 4]], [])                      # [1, 2, 3, 4]

# Count occurrences
from collections import Counter
Counter("mississippi")                          # Counter({'i': 4, 's': 4, ...})

# Swap two variables
a, b = b, a

# Merge two dictionaries (Python 3.9+)
merged = dict1 | dict2

# Read a file into a list of stripped lines
lines = [line.strip() for line in open("file.txt")]

# Get today's date as a string
from datetime import date
today = date.today().isoformat()               # '2026-09-08'
```
