# Day 05 – Functions and modular design

## Exercise 1: Compose functions

**Question**  
Write a function `compose(f, g)` that returns a new function which applies `g` first and then `f` to its argument.

Example:
```
def double(x): return x * 2
def increment(x): return x + 1
h = compose(double, increment)
h(5)  → 12   # double(increment(5))
```

**Hints**  
Return a lambda or a nested function.

**Solution**
```python
def compose(f, g):
    def composed(x):
        return f(g(x))
    return composed
```

---

## Exercise 2: Memoize simple function

**Question**  
Write a decorator `memoize` that caches the results of a function that takes a single hashable argument. Subsequent calls with the same argument should return the cached value.

Example:
```
@memoize
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)
```

**Hints**  
Use a dictionary to store previously computed results.

**Solution**
```python
def memoize(func):
    cache = {}
    def wrapper(n):
        if n not in cache:
            cache[n] = func(n)
        return cache[n]
    return wrapper
```

---

## Exercise 3: Partial application

**Question**  
Write a function `partial(func, *fixed_args)` that returns a new function with some arguments already filled in.

Example:
```
def add(a, b, c):
    return a + b + c
add5 = partial(add, 5)
add5(3, 2)  → 10
```

**Hints**  
Return a function that combines the fixed arguments with the new ones.

**Solution**
```python
def partial(func, *fixed_args):
    def wrapper(*args):
        return func(*(fixed_args + args))
    return wrapper
```

---

## Exercise 4: Once only

**Question**  
Write a decorator `once` that ensures a function can be executed only once. Subsequent calls should return the result of the first call without re-executing the function.

**Hints**  
Keep a flag and the cached result inside the decorator.

**Solution**
```python
def once(func):
    result = None
    called = False
    def wrapper(*args, **kwargs):
        nonlocal result, called
        if not called:
            result = func(*args, **kwargs)
            called = True
        return result
    return wrapper
```
