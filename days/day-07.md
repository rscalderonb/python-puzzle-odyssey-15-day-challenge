# Day 07 – File handling and text processing

## Exercise 1: Count lines, words, characters

**Question**  
Write a function `file_stats(path)` that reads a text file and returns a tuple `(lines, words, characters)`.

**Hints**  
Use `with open(...)` and process the content carefully. Count characters including whitespace.

**Solution**
```python
def file_stats(path):
    with open(path, 'r', encoding='utf-8') as f:
        content = f.read()
    lines = content.count('\n') + (1 if content and not content.endswith('\n') else 0)
    words = len(content.split())
    characters = len(content)
    return (lines, words, characters)
```

---

## Exercise 2: Find longest line

**Question**  
Write a function `longest_line(path)` that returns the longest line (by character count) from a text file. If there are ties, return the first one encountered.

**Hints**  
Read line by line and keep track of the maximum.

**Solution**
```python
def longest_line(path):
    longest = ""
    with open(path, 'r', encoding='utf-8') as f:
        for line in f:
            if len(line) > len(longest):
                longest = line.rstrip('\n')
    return longest
```

---

## Exercise 3: Filter lines containing keyword

**Question**  
Write a function `filter_lines(path, keyword)` that returns a list of all lines from the file that contain the given keyword (case-insensitive).

**Hints**  
Strip the newline and check membership after lowercasing.

**Solution**
```python
def filter_lines(path, keyword):
    keyword = keyword.lower()
    result = []
    with open(path, 'r', encoding='utf-8') as f:
        for line in f:
            if keyword in line.lower():
                result.append(line.rstrip('\n'))
    return result
```

---

## Exercise 4: Write unique sorted lines

**Question**  
Write a function `unique_sorted(input_path, output_path)` that reads all lines from the input file, removes duplicates, sorts them alphabetically, and writes the result to the output file.

**Hints**  
Use a set for uniqueness, then sort, then write.

**Solution**
```python
def unique_sorted(input_path, output_path):
    with open(input_path, 'r', encoding='utf-8') as f:
        lines = {line.rstrip('\n') for line in f}
    sorted_lines = sorted(lines)
    with open(output_path, 'w', encoding='utf-8') as f:
        for line in sorted_lines:
            f.write(line + '\n')
```
