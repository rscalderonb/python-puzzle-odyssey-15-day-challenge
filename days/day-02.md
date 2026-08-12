# Day 02 – Strings and character processing

## Exercise 1: Alternating case

**Question**  
Write a function `alternating_case(s)` that returns a new string where letters alternate between uppercase and lowercase, starting with uppercase. Non-letter characters stay unchanged and do not affect the alternation.

Example:
```
alternating_case("hello world!")  → "HeLlO wOrLd!"
```

**Hints**  
Keep a separate counter for letters only.

**Solution**
```python
def alternating_case(s):
    result = []
    upper = True
    for char in s:
        if char.isalpha():
            result.append(char.upper() if upper else char.lower())
            upper = not upper
        else:
            result.append(char)
    return ''.join(result)
```

---

## Exercise 2: Longest consecutive characters

**Question**  
Write a function `longest_run(s)` that returns a tuple `(char, length)` representing the character that appears in the longest consecutive run and the length of that run. If there are ties, return the one that appears first.

Example:
```
longest_run("aaabbccccdda")  → ('c', 4)
```

**Hints**  
A single pass keeping track of the current run is sufficient.

**Solution**
```python
def longest_run(s):
    if not s:
        return (None, 0)
    max_char = s[0]
    max_len = 1
    current_char = s[0]
    current_len = 1
    for char in s[1:]:
        if char == current_char:
            current_len += 1
            if current_len > max_len:
                max_len = current_len
                max_char = current_char
        else:
            current_char = char
            current_len = 1
    return (max_char, max_len)
```

---

## Exercise 3: Remove consecutive duplicates

**Question**  
Write a function `squeeze(s)` that removes consecutive duplicate characters from a string, keeping only the first occurrence of each run.

Example:
```
squeeze("aaabbcdddde")  → "abcde"
```

**Hints**  
Build a new string, only adding a character when it differs from the previous one.

**Solution**
```python
def squeeze(s):
    if not s:
        return ""
    result = [s[0]]
    for char in s[1:]:
        if char != result[-1]:
            result.append(char)
    return ''.join(result)
```

---

## Exercise 4: Valid parentheses (simple)

**Question**  
Write a function `is_balanced(s)` that checks whether a string containing only `(`, `)`, `[`, `]`, `{`, `}` is properly balanced. Return `True` if every opening bracket has a matching closing bracket in the correct order, otherwise `False`.

Example:
```
is_balanced("{[()]}")  → True
is_balanced("([)]")    → False
```

**Hints**  
A stack (list) is the classic approach.

**Solution**
```python
def is_balanced(s):
    stack = []
    pairs = {')': '(', ']': '[', '}': '{'}
    for char in s:
        if char in '([{':
            stack.append(char)
        elif char in ')]}':
            if not stack or stack[-1] != pairs[char]:
                return False
            stack.pop()
    return len(stack) == 0
```
