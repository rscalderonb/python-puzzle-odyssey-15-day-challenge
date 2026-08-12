# Day 10 – Generators and iterators

## Exercise 1: Infinite Fibonacci generator

**Question**  
Write a generator function `fibonacci()` that yields the Fibonacci sequence indefinitely (0, 1, 1, 2, 3, 5, ...).

**Hints**  
Use a simple loop with two variables and `yield`.

**Solution**
```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b
```

---

## Exercise 2: Chunked iterator

**Question**  
Write a generator `chunked(iterable, size)` that yields successive chunks (as lists) of the given size from the iterable.

Example:
```
list(chunked(range(10), 3))  → [[0, 1, 2], [3, 4, 5], [6, 7, 8], [9]]
```

**Hints**  
Accumulate items until you reach the size, then yield and reset.

**Solution**
```python
def chunked(iterable, size):
    chunk = []
    for item in iterable:
        chunk.append(item)
        if len(chunk) == size:
            yield chunk
            chunk = []
    if chunk:
        yield chunk
```

---

## Exercise 3: Running average

**Question**  
Write a generator `running_average(iterable)` that yields the running average after each new number is seen.

Example:
```
list(running_average([10, 20, 30]))  → [10.0, 15.0, 20.0]
```

**Hints**  
Keep a running total and a count.

**Solution**
```python
def running_average(iterable):
    total = 0
    count = 0
    for value in iterable:
        total += value
        count += 1
        yield total / count
```

---

## Exercise 4: Take while condition

**Question**  
Write a generator `takewhile(predicate, iterable)` that yields items from the iterable as long as the predicate returns True, then stops.

**Hints**  
This is similar to the behavior of `itertools.takewhile`.

**Solution**
```python
def takewhile(predicate, iterable):
    for item in iterable:
        if not predicate(item):
            break
        yield item
```
