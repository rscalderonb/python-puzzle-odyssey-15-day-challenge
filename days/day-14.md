# Day 14 – Classes and basic OOP

## Exercise 1: Simple Counter class

**Question**  
Implement a `Counter` class with methods `increment()`, `decrement()`, and `value()` (a property or method that returns the current count). The counter starts at 0 and should never go below 0.

**Solution**
```python
class Counter:
    def __init__(self):
        self._count = 0

    def increment(self):
        self._count += 1

    def decrement(self):
        if self._count > 0:
            self._count -= 1

    @property
    def value(self):
        return self._count
```

---

## Exercise 2: Bank account

**Question**  
Implement a `BankAccount` class with `deposit(amount)`, `withdraw(amount)`, and a `balance` property. Withdrawals that would make the balance negative should be ignored (or raise an exception – your choice, document it).

**Solution**
```python
class BankAccount:
    def __init__(self, initial=0):
        self._balance = initial

    def deposit(self, amount):
        if amount > 0:
            self._balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance -= amount

    @property
    def balance(self):
        return self._balance
```

---

## Exercise 3: Stack class

**Question**  
Implement a `Stack` class with `push(item)`, `pop()`, `peek()`, and `is_empty()` methods. `pop` and `peek` on an empty stack should raise an appropriate exception or return a sentinel – choose one and stay consistent.

**Solution**
```python
class Stack:
    def __init__(self):
        self._items = []

    def push(self, item):
        self._items.append(item)

    def pop(self):
        if not self._items:
            raise IndexError("pop from empty stack")
        return self._items.pop()

    def peek(self):
        if not self._items:
            raise IndexError("peek from empty stack")
        return self._items[-1]

    def is_empty(self):
        return len(self._items) == 0
```

---

## Exercise 4: Rectangle and area comparison

**Question**  
Implement a `Rectangle` class with width and height. Add an `area` property and a method `can_fit_inside(other)` that returns True if the current rectangle can fit inside another rectangle (considering rotation is not allowed).

**Solution**
```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    @property
    def area(self):
        return self.width * self.height

    def can_fit_inside(self, other):
        return self.width <= other.width and self.height <= other.height
```
