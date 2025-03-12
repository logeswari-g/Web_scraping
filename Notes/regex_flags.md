## **1. Introduction to Regex Flags**
Python uses the `re` module for regular expressions, and flags modify how regex patterns behave.

Commonly used flags:
- **`re.IGNORECASE` (`i`)** → Case-insensitive matching.
- **`re.DOTALL` (`s`)** → Allows `.` to match newline characters (`\n`).
- **Global Search (`g`)** is implicit in `re.findall()` (no need for a separate flag).

---

## **2. Explanation of Flags**

### **1. `re.IGNORECASE` (`i` flag) – Case Insensitive Matching**
- By default, regex is case-sensitive.
- `re.IGNORECASE` makes the pattern match letters in any case.
- Example:
  ```python
  import re
  
  pattern = re.compile(r"hello", re.IGNORECASE)
  print(pattern.search("HELLO"))  # Matches
  ```

### **2. `re.DOTALL` (`s` flag) – Dot Matches Newlines**
- Normally, `.` does **not** match newlines (`\n`).
- The `re.DOTALL` flag allows `.` to match any character, including newlines.
- Example:
  ```python
  import re
  
  text = "Hello\nWorld"
  pattern = re.compile(r"Hello.World", re.DOTALL)
  print(pattern.search(text))  # Matches "Hello\nWorld"
  ```

### **3. Handling Global Search (`g` flag)**
- In Python, **global search is default** when using `re.findall()`, so there is no explicit `g` flag.
- Example:
  ```python
  import re
  
  text = "banana"
  matches = re.findall(r"a", text)  # Finds all occurrences
  print(matches)  # ['a', 'a', 'a']
  ```

- If you need to replace all occurrences (like `g` in JavaScript), use `re.sub()`:
  ```python
  import re
  
  text = "banana"
  result = re.sub(r"a", "*", text)  # Replaces all 'a' with '*'
  print(result)  # "b*n*n*"
  ```

---

## **4. Combining Multiple Flags**
- Flags can be combined using `|` (bitwise OR) operator.
- Example:
  ```python
  import re
  
  pattern = re.compile(r"hello.world", re.IGNORECASE | re.DOTALL)
  print(pattern.search("HELLO\nWORLD"))  # Matches
  ```

---

## **5. Summary**
| Flag | Python Equivalent | Example |
|------|------------------|---------|
| `i`  | `re.IGNORECASE` | `re.compile(r"hello", re.IGNORECASE)` |
| `g`  | Use `re.findall()` | `re.findall(r"a", text)` |
| `s`  | `re.DOTALL` | `re.compile(r"hello.world", re.DOTALL)` |

These flags can be used together for more powerful regex pattern matching in Python.
