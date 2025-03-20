## 1. What is Selenium?
Selenium is an automation tool primarily used for testing web applications but can also be used for web scraping. It allows interaction with web elements just like a real user.

### Features of Selenium:
- Supports multiple browsers (Chrome, Firefox, Edge, etc.)
- Interacts with JavaScript-rendered content
- Handles dynamic elements and AJAX calls
- Supports headless browsing

## 2. Installing Selenium
Install Selenium using pip:
```bash
pip install selenium
```
Download the appropriate WebDriver (ChromeDriver, GeckoDriver, etc.) from their official sources and place it in a known directory.

## 3. Setting Up Selenium
### Import Required Libraries
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time
```
### Launching a Web Browser
```python
driver = webdriver.Chrome()  # Change to webdriver.Firefox() for Firefox
driver.get("https://example.com")
time.sleep(3)  # Wait for page to load
```

## 4. Locating Elements
Selenium provides multiple ways to locate elements on a webpage:

| Method | Syntax |
|--------|--------|
| ID | `driver.find_element(By.ID, "element_id")` |
| Name | `driver.find_element(By.NAME, "element_name")` |
| Class Name | `driver.find_element(By.CLASS_NAME, "class_name")` |
| Tag Name | `driver.find_element(By.TAG_NAME, "tag_name")` |
| CSS Selector | `driver.find_element(By.CSS_SELECTOR, "css_selector")` |
| XPath | `driver.find_element(By.XPATH, "xpath")` |

Example:
```python
element = driver.find_element(By.NAME, "q")
element.send_keys("Selenium Web Scraping")
element.send_keys(Keys.RETURN)
```

## 5. Extracting Data
After locating elements, you can extract text or attributes.
```python
title = driver.title
print("Page Title:", title)

paragraph = driver.find_element(By.TAG_NAME, "p").text
print("Paragraph Text:", paragraph)
```

## 6. Handling Dynamic Content
To wait for elements to load, use Selenium’s `WebDriverWait`:
```python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)
element = wait.until(EC.presence_of_element_located((By.ID, "dynamic_element")))
```

## 7. Handling Pagination
Loop through pages and scrape data:
```python
while True:
    scrape_data()  # Custom function to extract required information
    try:
        next_button = driver.find_element(By.LINK_TEXT, "Next")
        next_button.click()
        time.sleep(2)
    except:
        break  # Exit loop if no "Next" button found
```

## 8. Handling Headless Browsing
Run Selenium without opening a browser window:
```python
from selenium.webdriver.chrome.options import Options

options = Options()
options.add_argument("--headless")
driver = webdriver.Chrome(options=options)
```

## 9. Handling Cookies and Sessions
```python
cookies = driver.get_cookies()
print(cookies)

driver.add_cookie({"name": "test_cookie", "value": "12345"})
```

## 10. Taking Screenshots
```python
driver.save_screenshot("screenshot.png")
```

## 11. Closing the Browser
```python
driver.quit()  # Closes all browser windows and ends session
```

### Example: Selenium with BeautifulSoup
```python
from bs4 import BeautifulSoup
html = driver.page_source
soup = BeautifulSoup(html, "html.parser")
data = soup.find("div", class_="content").text
print(data)
```
