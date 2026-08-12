# Day 09 – Sets and uniqueness

## Exercise 1: Intersection of multiple lists

**Question**  
Write a function `common_elements(*lists)` that returns a set of elements that appear in every provided list.

Example:
```
common_elements([1, 2, 3], [2, 3, 4], [3, 2, 5])  → {2, 3}
```

**Hints**  
Convert the first list to a set and successively intersect.

**Solution**
```python
def common_elements(*lists):
    if not lists:
        return set()
    result = set(lists[0])
    for lst in lists[1:]:
        result &= set(lst)
    return result
```

---

## Exercise 2: Unique in order

**Question**  
Write a function `unique_in_order(iterable)` that returns a list of unique elements while preserving the original order of first appearance.

Example:
```
unique_in_order("AABBCCcAa")  → ['A', 'B', 'C', 'c', 'A', 'a']
```

**Hints**  
Use a set to track seen items while building the result list.

**Solution**
```python
def unique_in_order(iterable):
    seen = set()
    result = []
    for item in iterable:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return result
```

---

## Exercise 3: Symmetric difference of lists

**Question**  
Write a function `symmetric_diff(a, b)` that returns a sorted list of elements that are in either list but not in both.

**Hints**  
Convert to sets and use the `^` operator or combination of differences.

**Solution**
```python
def symmetric_diff(a, b):
    return sorted(set(a) ^ set(b))
```

---

## Exercise 4: First missing positive

**Question**  
Write a function `first_missing_positive(nums)` that finds the smallest missing positive integer in a list of integers (which may contain negatives and zeros). The solution should run in linear time and constant extra space if possible, but a simple approach using a set is acceptable for this exercise.

Example:
```
first_missing_positive([3, 4, -1, 1])  → 2
```

**Hints**  
Put the numbers into a set and check from 1 upward.

**Solution**
```python
def first_missing_positive(nums):
    s = set(nums)
    candidate = 1
    while candidate in s:
        candidate += 1
    return candidate
```
