# Day 03 – Lists and simple data structures

## Exercise 1: Rotate list

**Question**  
Write a function `rotate(lst, k)` that rotates a list to the right by `k` positions. `k` can be larger than the length of the list.

Example:
```
rotate([1, 2, 3, 4, 5], 2)  → [4, 5, 1, 2, 3]
```

**Hints**  
Use modulo to normalize k, then slice.

**Solution**
```python
def rotate(lst, k):
    if not lst:
        return []
    k = k % len(lst)
    return lst[-k:] + lst[:-k]
```

---

## Exercise 2: Flatten nested list (one level)

**Question**  
Write a function `flatten(lst)` that flattens a list that may contain nested lists one level deep. Assume nested items are either numbers or lists of numbers.

Example:
```
flatten([1, [2, 3], 4, [5]])  → [1, 2, 3, 4, 5]
```

**Hints**  
Iterate and extend when you encounter a list.

**Solution**
```python
def flatten(lst):
    result = []
    for item in lst:
        if isinstance(item, list):
            result.extend(item)
        else:
            result.append(item)
    return result
```

---

## Exercise 3: Second largest unique

**Question**  
Write a function `second_largest(lst)` that returns the second largest unique number in a list of integers. If there is no second largest, return `None`.

Example:
```
second_largest([5, 1, 5, 3, 2])  → 3
second_largest([7, 7, 7])        → None
```

**Hints**  
You can use a set or keep track of the two largest values carefully.

**Solution**
```python
def second_largest(lst):
    unique = sorted(set(lst), reverse=True)
    return unique[1] if len(unique) >= 2 else None
```

---

## Exercise 4: Chunk list

**Question**  
Write a function `chunk(lst, size)` that splits a list into sublists of length `size`. The last chunk may be shorter.

Example:
```
chunk([1, 2, 3, 4, 5, 6, 7], 3)  → [[1, 2, 3], [4, 5, 6], [7]]
```

**Hints**  
Use slicing in a loop or list comprehension with range.

**Solution**
```python
def chunk(lst, size):
    return [lst[i:i + size] for i in range(0, len(lst), size)]
```
