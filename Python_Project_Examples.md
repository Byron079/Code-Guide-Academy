# Python Project Examples

Ten projects, ordered from beginner to advanced. Each includes the skills it practises, a brief, step-by-step build guidance, and a stretch goal. Build them in order for the smoothest learning curve — copying code teaches nothing, struggling through your own version does.

---

## Beginner Projects

### 1. Number Guessing Game
**Skills:** loops, conditionals, `random`, input validation

Build a game where the computer picks a random number between 1 and 100, and the player has to guess it, receiving "higher" or "lower" hints.

- Use `random.randint(1, 100)` to pick the secret number.
- Use a `while` loop that keeps asking until the guess is correct.
- Wrap `int(input(...))` in a `try/except` so non-numeric input doesn't crash the game.
- Count and display the number of guesses at the end.

**Stretch goal:** Add a maximum of 7 guesses, and a difficulty setting that changes the number range.

---

### 2. Command-Line To-Do List
**Skills:** lists, dictionaries, functions, JSON file storage

A to-do list you run from the terminal that remembers your tasks between sessions.

- Store tasks as a list of dictionaries: `{"task": "Buy milk", "done": False}`.
- Build a menu loop: Add task / View tasks / Mark complete / Delete task / Quit.
- Save to `tasks.json` after every change, and load it on startup.

**Stretch goal:** Add due dates and sort the list by date before displaying it.

---

### 3. Simple Text-Based Adventure Game
**Skills:** functions, dictionaries, control flow, program structure

A branching story where the player's choices lead to different outcomes.

- Represent each "room" or "scene" as a dictionary with a description and available choices.
- Use a function per scene that returns the name of the next scene based on input.
- Track inventory or health in a dictionary that persists across scenes.

**Stretch goal:** Load the entire story from a JSON file instead of hard-coding it, so non-programmers could write new stories.

---

## Intermediate Projects

### 4. Library Management System
**Skills:** OOP, exception handling, file storage, search/filter logic

Model a small library with borrowable books and registered members.

- `Book` class: `title`, `author`, `isbn`, `is_borrowed`.
- `Member` class: `name`, `member_id`, `borrowed_books` (a list of Book objects).
- Methods to borrow/return a book, raising a custom `BookUnavailableError` if already borrowed.
- Persist the full catalogue to a JSON file between runs.

**Stretch goal:** Add due dates and a method that lists all currently overdue books.

---

### 5. Movie Rental System
**Skills:** OOP, menus, validation, aggregation

Simulate a movie rental store.

- `Movie` class: `title`, `genre`, `available_copies`.
- `Customer` class: `name`, `rented_movies`, `rent()`, `return_movie()`.
- Menu-driven program: list movies, rent, return, view a customer's rental history.
- Validate that a movie can't be rented when `available_copies == 0`.

**Stretch goal:** Add a late-fee calculator based on days overdue, using the `datetime` module.

---

### 6. Expense Tracker with Reports
**Skills:** CSV/JSON, dictionaries, data aggregation, basic charting

Track daily expenses and summarise spending by category.

- Log each expense as `{"date": ..., "category": ..., "amount": ...}` to a CSV file.
- Write a report function that totals spending per category and per month.
- Use `matplotlib` to plot a bar chart of spending by category.

**Stretch goal:** Add a monthly budget per category and flag categories that are over budget.

---

### 7. Weather Dashboard (API Project)
**Skills:** `requests`, JSON parsing, error handling

Fetch and display real weather data for any city the user enters.

- Sign up for a free weather API key.
- Write `get_weather(city)` that calls the API and returns the key details as a dictionary.
- Handle network errors and invalid city names gracefully.
- Loop so the user can check multiple cities without restarting.

**Stretch goal:** Cache each city's result for 10 minutes to avoid repeat API calls.

---

## Advanced Projects

### 8. Notes App with a Real Database
**Skills:** `sqlite3`, CRUD operations, OOP, testing

A persistent notes app backed by an embedded database instead of a flat file.

- Design a `notes` table: `id`, `title`, `content`, `created_at`.
- Write Create/Read/Update/Delete functions using parameterised queries (never string-formatted SQL).
- Wrap the database logic in a `NotesRepository` class, separate from the menu/UI code.
- Write `pytest` tests for each CRUD function against a temporary test database.

**Stretch goal:** Add full-text search across note titles and content.

---

### 9. Mini REST API with Flask
**Skills:** Flask, HTTP methods, JSON, routing

Build a small task-management API that other programs (or a frontend) could talk to.

- `GET /tasks` — list all tasks. `POST /tasks` — add a task. `DELETE /tasks/<id>` — remove one.
- Store tasks in-memory first, then upgrade to SQLite once the basic routes work.
- Return proper HTTP status codes (`201 Created`, `404 Not Found`, etc.).
- Test every route with Postman, curl, or your browser.

**Stretch goal:** Add basic API-key authentication that rejects requests missing a valid `X-API-Key` header.

---

### 10. Inventory Management System (Capstone)
**Skills:** OOP, decorators, file/database storage, custom exceptions, testing — everything combined

A complete small business tool tying together most of what you've learned.

- `Inventory` class storing products (`name`, `price`, `quantity`) internally.
- Methods to add stock, sell stock (raising `OutOfStockError` if insufficient), and calculate total inventory value.
- Apply a `@timer` decorator to the value-calculation method.
- Persist to JSON or SQLite after every change, and reload on startup.
- Write at least 5 `pytest` tests, including the `OutOfStockError` case.

**Stretch goal:** Add a simple Flask front-end so the inventory can be managed from a browser instead of the terminal.

---

## How to Use This List

1. Don't jump straight to advanced projects — the intermediate ones deliberately reuse OOP patterns you'll need later.
2. Before coding, write a short plan: what classes/functions will you need, and what does each one do?
3. Build the smallest working version first (even if ugly), then add features one at a time.
4. Once a project works, go back and add error handling, tests, and comments — this is what turns a script into a proper piece of software.
5. Push every finished project to GitHub. A portfolio of small, real projects is worth far more than tutorials completed.
