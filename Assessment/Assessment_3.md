# **Practical Questions on the `requests` Module in Python**
---

## **1. Basic GET Request**
**Write a Python script to send a `GET` request to `https://jsonplaceholder.typicode.com/posts/1` and print the response JSON.**

---

## **2. Handling Errors in HTTP Requests**
**How do you handle errors in an HTTP request using `requests`? Write a script that catches exceptions when requesting `https://example.com`.**

---

## **3. Sending Query Parameters**
**Make a `GET` request to `https://jsonplaceholder.typicode.com/posts` with a query parameter that filters results by `userId=1`. Print the JSON response.**

---

## **4. Modifying Request Headers**
**Modify request headers to include a custom `User-Agent`. Send a `GET` request to `https://httpbin.org/headers` and print the response.**

---

## **5. Sending a POST Request**
**Write a script to send a `POST` request to `https://jsonplaceholder.typicode.com/posts` with the following JSON data:**
```json
{
  "title": "New Post",
  "body": "This is a test post.",
  "userId": 1
}
```
**Print the response JSON.**

---

## **6. Sending a PUT Request (Updating Data)**
**Update an existing post by sending a `PUT` request to `https://jsonplaceholder.typicode.com/posts/1` with updated `title` and `body`. Print the updated response.**

---

## **7. Sending a DELETE Request**
**Write a script to send a `DELETE` request to `https://jsonplaceholder.typicode.com/posts/1` and print the response status code.**

---

## **8. Using a Session for Persistent Requests**
**Use the `requests.Session()` object to maintain a session while making multiple requests to `https://httpbin.org/cookies/set?name=value`. Retrieve the stored cookies.**

---

## **9. Downloading an Image**
**Download an image from `https://via.placeholder.com/150` and save it as `image.jpg`.**

---

## **10. Uploading a File**
**Upload a text file named `sample.txt` to `https://httpbin.org/post` using a `POST` request. Print the response JSON.**
