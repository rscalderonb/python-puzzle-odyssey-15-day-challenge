# Day 08 – Sorting and searching

## Exercise 1: Insertion sort

**Question**  
Implement the insertion sort algorithm in a function `insertion_sort(lst)` that sorts a list in place and also returns it.

**Hints**  
Classic insertion sort: for each element, insert it into the correct position in the already-sorted portion.

**Solution**
```python
def insertion_sort(lst):
    for i in range(1, len(lst)):
        key = lst[i]
        j = i - 1
        while j >= 0 and lst[j] > key:
            lst[j + 1] = lst[j]
            j -= 1
        lst[j + 1] = key
    return lst
```

---

## Exercise 2: Binary search

**Question**  
Write a function `binary_search(lst, target)` that returns the index of `target` in a sorted list, or `-1` if it is not present. Do not use the built-in `in` or `index` methods.

**Hints**  
Maintain low and high indices and repeatedly examine the middle.

**Solution**
```python
def binary_search(lst, target):
    low, high = 0, len(lst) - 1
    while low <= high:
        mid = (low + high) // 2
        if lst[mid] == target:
            return mid
        elif lst[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1
```

---

## Exercise 3: Merge two sorted lists

**Question**  
Write a function `merge_sorted(a, b)` that merges two already sorted lists into a new sorted list.

**Hints**  
Two-pointer technique.

**Solution**
```python
def merge_sorted(a, b):
    result = []
    i = j = 0
    while i < len(a) and j < len(b):
        if a[i] <= b[j]:
            result.append(a[i])
            i += 1
        else:
            result.append(b[j])
            j += 1
    result.extend(a[i:])
    result.extend(b[j:])
    return result
```

---

## Exercise 4: Find peak element

**Question**  
A peak element in a list is greater than or equal to its neighbors. Write a function `find_peak(lst)` that returns the index of any peak element. Assume the list is non-empty and edges are considered peaks if they are greater than their single neighbor.

**Hints**  
A linear scan is acceptable for this exercise.

**Solution**
```python
def find_peak(lst):
    n = len(lst)
    if n == 1:
        return 0
    if lst[0] >= lst[1]:
        return 0
    if lst[n-1] >= lst[n-2]:
        return n - 1
    for i in range(1, n-1):
        if lst[i] >= lst[i-1] and lst[i] >= lst[i+1]:
            return i
    return 0
```
