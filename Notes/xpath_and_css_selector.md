# **XPath and CSS Selector Documentation**

XPath and CSS selectors are powerful tools used for navigating and selecting elements in an HTML/XML document, commonly used in web scraping and automation.

---

## **1. What is XPath?**
XPath (XML Path Language) is used to navigate and query XML and HTML documents. It allows selecting elements based on their structure.

### **Basic Syntax:**
```xpath
//tagname[@attribute='value']
```

### **Examples:**
- Select all `<a>` tags:
  ```xpath
  //a
  ```
- Select a specific `<div>` with class `example`:
  ```xpath
  //div[@class='example']
  ```
- Select the first `<p>` inside a `<div>`:
  ```xpath
  //div/p[1]
  ```
- Select an element with a specific text:
  ```xpath
  //h1[text()='Welcome']
  ```

### **XPath Axes (Navigation Methods)**
- **`parent::`** → Select parent node
- **`child::`** → Select child nodes
- **`following-sibling::`** → Select next sibling nodes
- **`preceding-sibling::`** → Select previous sibling nodes

Example:
```xpath
//div[@id='container']/child::p
```

---

## **2. What is a CSS Selector?**
CSS Selectors are used to target elements based on their attributes, classes, and hierarchy in HTML.

### **Basic Syntax:**
```css
tagname[attribute='value']
```

### **Examples:**
- Select all `<p>` tags:
  ```css
  p
  ```
- Select an element by ID:
  ```css
  #element-id
  ```
- Select elements by class:
  ```css
  .example-class
  ```
- Select direct child elements:
  ```css
  div > p
  ```
- Select sibling elements:
  ```css
  div + p
  ```
- Select elements with an attribute:
  ```css
  input[type='text']
  ```

---

## **3. Differences Between XPath and CSS Selectors**
| Feature | XPath | CSS Selector |
|---------|------|-------------|
| Syntax Complexity | More complex | Simpler |
| Works with XML | Yes | No |
| Parent Selection | Yes | No |
| Performance | Slower | Faster |
| Readability | Harder | Easier |

---

## **4. When to Use XPath vs. CSS Selectors?**
- Use **XPath** when dealing with complex XML/HTML structures or when selecting based on text.
- Use **CSS Selectors** for faster and simpler selections when working with HTML.

**Assume we want to scrape product titles from an web page.**

```
<html>
  <body>
    <div class="news">
      <h2>Breaking News</h2>
      <p class="description">This is today's top story.</p>
      <a href="https://example.com/story">Read More</a>
    </div>
  </body>
</html>

```

**Common XPath Queries**

1) Selecting the <h2> tag (by element name)

```
//h2
```

2) Selecting the <p> tag inside div with class news (by class attribute)

```
//div[@class='news']/p
```

3) Extracting the link inside <a> (href attribute)

```
//a/@href
```

4) Finding any <p> element that contains the word "top story"

```
//p[contains(text(), 'top story')]
```

**3. CSS Selectors Explained with Example**

CSS Selectors are used to select elements based on their ID, class, attributes, and hierarchy.

1) Selecting the <h2> tag

```
h2
```

2) Selecting <p> inside .news div

```
.news p
```

3) Extracting the link inside <a>

```
a[href]
```

4) Finding elements that contain "top story" (CSS can't check text directly)

```
p.description
```


