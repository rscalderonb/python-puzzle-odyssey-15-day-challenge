# Day 06 – Recursion and nested structures

## Exercise 1: Deep sum

**Question**  
Write a recursive function `deep_sum(lst)` that sums all numbers in a nested list structure of arbitrary depth.

Example:
```
deep_sum([1, [2, [3, 4], 5], 6])  → 21
```

**Hints**  
Check the type of each element; recurse on lists, add numbers.

**Solution**
```python
def deep_sum(lst):
    total = 0
    for item in lst:
        if isinstance(item, list):
            total += deep_sum(item)
        else:
            total += item
    return total
```

---

## Exercise 2: Nested depth

**Question**  
Write a recursive function `max_depth(lst)` that returns the maximum nesting depth of a list. An empty list or a list of non-lists has depth 1.

Example:
```
max_depth([1, [2, [3]]])  → 3
```

**Hints**  
Recurse and keep the maximum of 1 + depth of children.

**Solution**
```python
def max_depth(lst):
    if not isinstance(lst, list):
        return 0
    if not lst:
        return 1
    return 1 + max((max_depth(item) for item in lst), default=0)
```

---

## Exercise 3: Flatten deeply

**Question**  
Write a recursive function `deep_flatten(lst)` that completely flattens a nested list of arbitrary depth into a single flat list.

Example:
```
deep_flatten([1, [2, [3, 4], 5], 6])  → [1, 2, 3, 4, 5, 6]
```

**Hints**  
Similar to deep_sum but collect values instead of summing.

**Solution**
```python
def deep_flatten(lst):
    result = []
    for item in lst:
        if isinstance(item, list):
            result.extend(deep_flatten(item))
        else:
            result.append(item)
    return result
```

---

## Exercise 4: Binary tree path sum (simple)

**Question**  
Represent a binary tree node as a dictionary: `{'value': x, 'left': node or None, 'right': node or None}`.  
Write a recursive function `has_path_sum(root, target)` that returns `True` if there is a root-to-leaf path whose values sum to `target`.

**Hints**  
Subtract the current value and recurse on children; base case when both children are None.

**Solution**
```python
def has_path_sum(root, target):
    if root is None:
        return False
    remaining = target - root['value']
    if root['left'] is None and root['right'] is None:
        return remaining == 0
    return (has_path_sum(root['left'], remaining) or
            has_path_sum(root['right'], remaining))
```
