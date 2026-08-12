# Day 01 – Numbers and basic control flow

## Exercise 1: Digit product

**Question**  
Write a function `digit_product(n)` that returns the product of all non-zero digits of a positive integer `n`. If the number contains only zeros, return 0.

Example:
```
digit_product(1205)  → 10   # 1 * 2 * 5
digit_product(1000)  → 0
```

**Hints**  
Convert the number to a string or repeatedly use modulo and integer division. Skip zeros.

**Solution**
```python
def digit_product(n):
    if n == 0:
        return 0
    product = 1
    has_nonzero = False
    while n > 0:
        digit = n % 10
        if digit != 0:
            product *= digit
            has_nonzero = True
        n //= 10
    return product if has_nonzero else 0
```

---

## Exercise 2: Collatz length

**Question**  
The Collatz sequence works as follows: start with any positive integer. If it is even, divide by 2; if odd, multiply by 3 and add 1. Repeat until you reach 1.  
Write a function `collatz_length(n)` that returns how many steps are needed to reach 1.

Example:
```
collatz_length(6)  → 8   # 6 → 3 → 10 → 5 → 16 → 8 → 4 → 2 → 1
```

**Hints**  
A simple loop is enough. Be careful with the order of operations.

**Solution**
```python
def collatz_length(n):
    steps = 0
    while n != 1:
        if n % 2 == 0:
            n //= 2
        else:
            n = 3 * n + 1
        steps += 1
    return steps
```

---

## Exercise 3: Perfect number check

**Question**  
A perfect number is a positive integer that is equal to the sum of its proper divisors (excluding itself).  
Write a function `is_perfect(n)` that returns `True` if `n` is perfect, otherwise `False`.

Example:
```
is_perfect(28)  → True   # 1 + 2 + 4 + 7 + 14 = 28
is_perfect(12)  → False
```

**Hints**  
You only need to check divisors up to the square root of n for efficiency, but a simple loop is fine for this exercise.

**Solution**
```python
def is_perfect(n):
    if n <= 1:
        return False
    total = 1
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            total += i
            if i != n // i and n // i != n:
                total += n // i
    return total == n
```

---

## Exercise 4: Sum of multiples with exclusion

**Question**  
Write a function `sum_multiples(limit, a, b)` that returns the sum of all positive integers below `limit` that are multiples of `a` or `b`, but not both.

Example:
```
sum_multiples(20, 3, 5)  → 63
# multiples of 3 or 5 below 20, excluding those divisible by both (15)
```

**Hints**  
Use the principle of inclusion-exclusion or simply check the conditions carefully.

**Solution**
```python
def sum_multiples(limit, a, b):
    total = 0
    for i in range(1, limit):
        if (i % a == 0) ^ (i % b == 0):  # XOR: one or the other, not both
            total += i
    return total
```
