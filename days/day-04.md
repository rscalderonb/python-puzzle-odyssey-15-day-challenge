# Day 04 – Dictionaries and counting

## Exercise 1: Word frequency

**Question**  
Write a function `word_count(text)` that returns a dictionary mapping each word (case-insensitive) to the number of times it appears. Ignore punctuation by treating only alphabetic characters and spaces as significant.

Example:
```
word_count("Hello hello world!")  → {'hello': 2, 'world': 1}
```

**Hints**  
Clean the text first, then use a dictionary or Counter.

**Solution**
```python
from collections import Counter
import re

def word_count(text):
    words = re.findall(r'[a-zA-Z]+', text.lower())
    return dict(Counter(words))
```

---

## Exercise 2: Invert dictionary

**Question**  
Write a function `invert(d)` that inverts a dictionary so that values become keys and keys become values. Assume all values are unique and hashable.

Example:
```
invert({'a': 1, 'b': 2})  → {1: 'a', 2: 'b'}
```

**Hints**  
Simple dictionary comprehension works well.

**Solution**
```python
def invert(d):
    return {v: k for k, v in d.items()}
```

---

## Exercise 3: Group by length

**Question**  
Write a function `group_by_length(words)` that takes a list of strings and returns a dictionary where keys are string lengths and values are lists of words of that length.

Example:
```
group_by_length(["hi", "hello", "hey", "world"])  → {2: ['hi'], 5: ['hello', 'world'], 3: ['hey']}
```

**Hints**  
Use `setdefault` or `defaultdict`.

**Solution**
```python
from collections import defaultdict

def group_by_length(words):
    groups = defaultdict(list)
    for word in words:
        groups[len(word)].append(word)
    return dict(groups)
```

---

## Exercise 4: Most common character

**Question**  
Write a function `most_common_char(s)` that returns the character that appears most frequently in the string (case-sensitive). If there is a tie, return the one that appears first in the string.

Example:
```
most_common_char("abracadabra")  → 'a'
```

**Hints**  
Count frequencies, then find the maximum while preserving order of first appearance.

**Solution**
```python
from collections import Counter

def most_common_char(s):
    if not s:
        return None
    counts = Counter(s)
    max_count = max(counts.values())
    for char in s:
        if counts[char] == max_count:
            return char
```
