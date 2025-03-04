# **BeautifulSoup: Web Scraping with Python**  

**BeautifulSoup** is a Python library used for **parsing HTML and XML documents**. It helps extract and navigate web page content efficiently, making it a popular tool for **web scraping**.  

---

## **1. Installing BeautifulSoup**  
To use BeautifulSoup, install it along with `requests` for handling web requests:  
```bash
pip install beautifulsoup4 requests
```

---

## **2. Importing and Creating a BeautifulSoup Object**  
BeautifulSoup requires an HTML/XML document as input. Typically, we fetch web pages using the `requests` module.

### **Example: Fetching and Parsing an HTML Page**
```python
import requests
from bs4 import BeautifulSoup

# Fetch HTML content from a webpage
url = "https://example.com"
response = requests.get(url)

# Create a BeautifulSoup object
soup = BeautifulSoup(response.text, "html.parser")

# Print formatted HTML
print(soup.prettify())
```
- `"html.parser"` → Default parser for handling HTML.
- `"lxml"` or `"html5lib"` → Alternative parsers that may work better for certain cases.

---

## **3. Navigating the HTML Structure**  
BeautifulSoup provides different ways to locate elements.

### **Find Elements by Tag Name**
```python
# Find the first <h1> tag
print(soup.h1.text)

# Find all <p> tags
paragraphs = soup.find_all("p")
for p in paragraphs:
    print(p.text)
```

### **Find Elements by Class or ID**
```python
# Find element with class "example-class"
element = soup.find(class_="example-class")
print(element.text)

# Find element with ID "main"
element = soup.find(id="main")
print(element.text)
```

### **Using CSS Selectors**
```python
# Select all elements with class "example"
elements = soup.select(".example")
for el in elements:
    print(el.text)

# Select an element with ID
element = soup.select_one("#main")
print(element.text)
```

---

## **4. Extracting Attributes**  
You can extract attributes like `href` from `<a>` tags.
```python
# Extract all links from <a> tags
for link in soup.find_all("a"):
    print(link.get("href"))
```

---

## **5. Modifying the HTML Content**  
BeautifulSoup allows modifying the HTML tree.
```python
# Change the text of an element
soup.h1.string = "New Title"

# Add a new attribute
soup.h1["style"] = "color: red;"

print(soup.prettify())
```

---

## **6. Removing Elements**  
You can remove unwanted elements.
```python
# Remove all <script> tags
for script in soup.find_all("script"):
    script.decompose()
```

---

## **7. Handling Real-World Web Scraping Issues**  
### **Dealing with Dynamic Content**  
Some websites use JavaScript to load content dynamically, which `requests` and BeautifulSoup alone **cannot** handle. You may need **Selenium** for such cases.

### **Handling Headers and User-Agents**  
Some websites block automated scrapers. To bypass restrictions, use headers:
```python
headers = {"User-Agent": "Mozilla/5.0"}
response = requests.get(url, headers=headers)
```

---

## **8. Complete Example: Scraping News Headlines**  
```python
import requests
from bs4 import BeautifulSoup

url = "https://news.ycombinator.com/"
headers = {"User-Agent": "Mozilla/5.0"}
response = requests.get(url, headers=headers)

soup = BeautifulSoup(response.text, "html.parser")

# Extract and print all news titles
for item in soup.select(".titleline a"):
    print(item.text)
```