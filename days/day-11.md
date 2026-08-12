# Day 11 – Error handling and validation

## Exercise 1: Safe division

**Question**  
Write a function `safe_divide(a, b)` that returns the result of a / b. If b is zero, return the string `"undefined"` instead of raising an exception.

**Solution**
```python
def safe_divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return "undefined"
```

---

## Exercise 2: Validate email (simple)

**Question**  
Write a function `is_valid_email(s)` that performs a basic check: the string must contain exactly one `@`, the local part and domain must be non-empty, and the domain must contain at least one dot. This is not a full RFC check, just a practical filter.

**Solution**
```python
def is_valid_email(s):
    if s.count('@') != 1:
        return False
    local, domain = s.split('@')
    if not local or not domain:
        return False
    if '.' not in domain:
        return False
    return True
```

---

## Exercise 3: Parse integer with default

**Question**  
Write a function `parse_int(value, default=0)` that tries to convert `value` to an integer. If conversion fails, return the provided default.

**Solution**
```python
def parse_int(value, default=0):
    try:
        return int(value)
    except (ValueError, TypeError):
        return default
```

---

## Exercise 4: Retry on failure

**Question**  
Write a decorator `retry(times=3)` that retries a function up to `times` times if it raises any exception. If all attempts fail, re-raise the last exception.

**Solution**
```python
def retry(times=3):
    def decorator(func):
        def wrapper(*args, **kwargs):
            last_exception = None
            for _ in range(times):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    last_exception = e
            raise last_exception
        return wrapper
    return decorator
```
