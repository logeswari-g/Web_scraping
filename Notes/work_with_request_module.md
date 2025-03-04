# **HTTP Requests Using the `requests` Module in Python**

The `requests` module in Python is a popular library for making HTTP requests.

---

## **1. Installing the `requests` Module**
To use the `requests` module, install it first (if not already installed):
```bash
pip install requests
```

Then, import it in your Python script:
```python
import requests
```

---

## **2. Making Basic HTTP Requests**

### **a. Sending a GET Request**
The `GET` method retrieves data from a specified URL.
```python
import requests
response = requests.get("https://jsonplaceholder.typicode.com/posts/1")
print(response.status_code)  # HTTP status code
print(response.json())  # JSON response
```

### **b. Sending a POST Request**
The `POST` method submits data to a server.
```python
import requests
url = "https://jsonplaceholder.typicode.com/posts"
data = {"title": "Test Post", "body": "This is a test.", "userId": 1}
response = requests.post(url, json=data)
print(response.status_code)
print(response.json())
```

---

## **3. Handling Response Data**

### **Checking Status Codes**
- `200 OK` – Success.
- `201 Created` – Resource successfully created.
- `400 Bad Request` – Client-side error.
- `401 Unauthorized` – Authentication required.
- `404 Not Found` – Resource not found.
- `500 Internal Server Error` – Server issue.

Example:
```python
response = requests.get("https://jsonplaceholder.typicode.com/posts/1")
if response.status_code == 200:
    print("Success!")
else:
    print(f"Failed with status code: {response.status_code}")
```

### **Parsing JSON Responses**
```python
response = requests.get("https://jsonplaceholder.typicode.com/posts/1")
data = response.json()
print(data["title"])  # Access specific fields
```

---

## **4. Sending Custom Headers**
Custom headers help in authentication and modifying request properties.
```python
headers = {"User-Agent": "MyApp/1.0"}
response = requests.get("https://jsonplaceholder.typicode.com/posts", headers=headers)
print(response.status_code)
```

---

## **5. Sending Query Parameters**
Query parameters filter and modify requests.
```python
params = {"userId": 1}
response = requests.get("https://jsonplaceholder.typicode.com/posts", params=params)
print(response.json())
```

---

## **6. Using Sessions for Persistent Connections**
```python
session = requests.Session()
response = session.get("https://example.com/protected")
print(response.status_code)
```

---

## **7. Uploading file using request**
```python
url = "https://httpbin.org/post"
files = {"file": open("sample.txt", "rb")}
response = requests.post(url, files=files)
print(response.json())
```

---

## **7. Download image file using request**
```python
url = "https://via.placeholder.com/150"
response = requests.get(url)

if response.status_code == 200:
    with open("image.jpg", "wb") as file:
        file.write(response.content)
    print("Image downloaded successfully.")
else:
    print("Failed to download image.")
```

---
