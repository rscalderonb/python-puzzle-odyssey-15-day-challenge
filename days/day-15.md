# Day 15 – Putting it together (mini projects)

## Exercise 1: Simple TODO list manager

**Question**  
Write a small command-line style TODO manager as a class or set of functions that supports:
- adding a task
- listing all tasks
- marking a task as done
- removing a task

Store the tasks in memory (a list of dictionaries is fine).

**Solution** (illustrative)
```python
class TodoList:
    def __init__(self):
        self.tasks = []

    def add(self, description):
        self.tasks.append({"description": description, "done": False})

    def list(self):
        for i, task in enumerate(self.tasks, 1):
            status = "[x]" if task["done"] else "[ ]"
            print(f"{i}. {status} {task['description']}")

    def complete(self, index):
        if 0 <= index < len(self.tasks):
            self.tasks[index]["done"] = True

    def remove(self, index):
        if 0 <= index < len(self.tasks):
            self.tasks.pop(index)
```

---

## Exercise 2: CSV summary

**Question**  
Write a function that reads a simple CSV file (header + rows of numbers) and returns a dictionary with the sum and average of each numeric column.

**Solution** (illustrative)
```python
import csv

def csv_summary(path):
    with open(path, newline='', encoding='utf-8') as f:
        reader = csv.DictReader(f)
        columns = {name: [] for name in reader.fieldnames}
        for row in reader:
            for name, value in row.items():
                try:
                    columns[name].append(float(value))
                except ValueError:
                    pass
    summary = {}
    for name, values in columns.items():
        if values:
            summary[name] = {
                "sum": sum(values),
                "avg": sum(values) / len(values)
            }
    return summary
```

---

## Exercise 3: Simple password strength checker

**Question**  
Write a function `password_strength(password)` that returns a score from 0 to 5 based on length, presence of upper/lower case, digits, and special characters. Document the scoring rules in a docstring.

**Solution**
```python
def password_strength(password):
    """
    Score 0-5:
    +1 if length >= 8
    +1 if length >= 12
    +1 if has both upper and lower case
    +1 if has at least one digit
    +1 if has at least one special character
    """
    score = 0
    if len(password) >= 8:
        score += 1
    if len(password) >= 12:
        score += 1
    if any(c.isupper() for c in password) and any(c.islower() for c in password):
        score += 1
    if any(c.isdigit() for c in password):
        score += 1
    if any(not c.isalnum() for c in password):
        score += 1
    return score
```

---

## Exercise 4: Mini contact book

**Question**  
Implement a simple contact book that stores name → phone mappings. Support adding, looking up, deleting, and listing all contacts. Persist the data to a JSON file so it survives program restarts.

**Solution** (illustrative)
```python
import json
import os

class ContactBook:
    def __init__(self, path="contacts.json"):
        self.path = path
        self.contacts = {}
        if os.path.exists(path):
            with open(path, 'r', encoding='utf-8') as f:
                self.contacts = json.load(f)

    def save(self):
        with open(self.path, 'w', encoding='utf-8') as f:
            json.dump(self.contacts, f, indent=2)

    def add(self, name, phone):
        self.contacts[name] = phone
        self.save()

    def lookup(self, name):
        return self.contacts.get(name)

    def delete(self, name):
        if name in self.contacts:
            del self.contacts[name]
            self.save()

    def list_all(self):
        return dict(self.contacts)
```
