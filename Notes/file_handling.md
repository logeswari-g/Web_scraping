
# **Basics of File Handling in Python**  

File handling in Python allows users to **read, write, update, and manage files** stored on a system. Python provides built-in functions for handling files efficiently.

---

## **2. File Handling Modes in Python**  

Python provides different modes for working with files:  

| Mode | Description |
|------|-------------|
| `"r"`  | Read mode (default); raises an error if the file doesn’t exist. |
| `"w"`  | Write mode; creates a new file or overwrites an existing one. |
| `"a"`  | Append mode; adds new content at the end of a file. |
| `"r+"` | Read and write; file must exist. |
| `"w+"` | Write and read; overwrites an existing file. |
| `"a+"` | Append and read; preserves existing content. |
| `"rb"` | Read a binary file. |
| `"wb"` | Write a binary file. |

---

## **3. Opening and Closing Files**  

### **Opening a File (`open()`)**  
The `open()` function is used to open a file in Python.  
```python
file = open("example.txt", "r")  # Open file in read mode
```

### **Closing a File (`close()`)**  
After using a file, it should be closed to free system resources.  
```python
file.close()  # Closes the file
```

🔹 **Best Practice:** Use `with open()` to handle files automatically.  
```python
with open("example.txt", "r") as file:
    content = file.read()
    print(content)
# File closes automatically after exiting the block
```

---

## **4. Reading Files**  

| Method | Description |
|--------|-------------|
| `read()` | Reads the entire file as a string. |
| `readline()` | Reads a single line at a time. |
| `readlines()` | Reads all lines and returns a list. |

### **Examples**  

#### **Reading the whole file:**
```python
with open("example.txt", "r") as file:
    content = file.read()
    print(content)
```

#### **Reading line by line:**
```python
with open("example.txt", "r") as file:
    for line in file:
        print(line.strip())  # Removes extra newlines
```

---

## **5. Writing to Files**  

| Method | Description |
|--------|-------------|
| `write()` | Writes a string to the file (overwrites existing content). |
| `writelines()` | Writes a list of strings to the file. |

### **Writing Example**
```python
with open("output.txt", "w") as file:
    file.write("Hello, this is a test file!\n")
    file.write("Writing in Python is easy.")
```

### **Appending to a File**
```python
with open("output.txt", "a") as file:
    file.write("\nAppending new content.")
```

---

## **6. Working with Binary Files**  
Binary files (like images, PDFs, and videos) require `"rb"` or `"wb"` modes.  

### **Copying an Image File**
```python
with open("image.jpg", "rb") as source, open("copy.jpg", "wb") as destination:
    destination.write(source.read())
```

---

## **7. Checking if a File Exists**  
Before opening a file, check if it exists to avoid errors.  

```python
import os

if os.path.exists("example.txt"):
    print("File exists!")
else:
    print("File not found!")
```

---

## **8. Deleting a File**  
To delete a file, use the `os.remove()` function.  

```python
import os

if os.path.exists("example.txt"):
    os.remove("example.txt")
    print("File deleted.")
else:
    print("File does not exist.")
```

---

## **9. Handling File Exceptions**  
Always handle exceptions when working with files to prevent crashes.  

```python
try:
    with open("nonexistent.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("Error: File not found!")
except Exception as e:
    print(f"An error occurred: {e}")
```

---