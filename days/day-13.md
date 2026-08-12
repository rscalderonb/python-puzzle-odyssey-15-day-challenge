# Day 13 – Simple algorithms

## Exercise 1: Sieve of Eratosthenes

**Question**  
Write a function `primes_up_to(n)` that returns a list of all prime numbers less than or equal to `n` using the Sieve of Eratosthenes.

**Solution**
```python
def primes_up_to(n):
    if n < 2:
        return []
    sieve = [True] * (n + 1)
    sieve[0] = sieve[1] = False
    for i in range(2, int(n ** 0.5) + 1):
        if sieve[i]:
            for j in range(i * i, n + 1, i):
                sieve[j] = False
    return [i for i, is_prime in enumerate(sieve) if is_prime]
```

---

## Exercise 2: Greatest common divisor

**Question**  
Implement Euclid's algorithm in a function `gcd(a, b)` that returns the greatest common divisor of two non-negative integers.

**Solution**
```python
def gcd(a, b):
    while b:
        a, b = b, a % b
    return a
```

---

## Exercise 3: Least common multiple

**Question**  
Write a function `lcm(a, b)` that returns the least common multiple of two positive integers. You may use the GCD function from the previous exercise.

**Solution**
```python
def lcm(a, b):
    return abs(a * b) // gcd(a, b) if a and b else 0

def gcd(a, b):
    while b:
        a, b = b, a % b
    return a
```

---

## Exercise 4: Matrix transpose

**Question**  
Write a function `transpose(matrix)` that returns the transpose of a rectangular list-of-lists matrix.

Example:
```
transpose([[1, 2, 3], [4, 5, 6]])  → [[1, 4], [2, 5], [3, 6]]
```

**Solution**
```python
def transpose(matrix):
    if not matrix:
        return []
    return [list(row) for row in zip(*matrix)]
```
