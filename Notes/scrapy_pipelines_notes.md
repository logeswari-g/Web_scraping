# 📄 `pipelines.py` in Scrapy Framework

## 📌 What is `pipelines.py`?

- `pipelines.py` is a core component of a Scrapy project.
- It defines **Item Pipeline** classes used to **process items** after they are scraped by spiders.
- You can use it to **clean**, **validate**, **filter**, or **store** scraped data.

---

## 🔄 Item Flow in Scrapy

1. Spider yields an `Item`.
2. Scrapy engine sends the item through the defined pipelines in the order of their priority.
3. Each pipeline can:
   - Modify the item.
   - Drop the item using `DropItem`.
   - Pass the item to the next pipeline.

---

## 🏗️ Basic Structure of `pipelines.py`

```python
class MyPipeline:
    def process_item(self, item, spider):
        # Example: clean a field
        item['name'] = item['name'].strip()
        return item
```

- `process_item(self, item, spider)` is the required method.
- Must return the item or raise `DropItem`.

---

## ⚙️ Activating Pipelines in `settings.py`

```python
ITEM_PIPELINES = {
    'myproject.pipelines.MyPipeline': 300,
}
```

- The number (`300`) defines the **priority**.
- Lower numbers run **first**.
- Multiple pipelines can be used and ordered by priority.

---

## 🔧 Additional Lifecycle Methods

```python
def open_spider(self, spider):
    # Called when the spider is opened
    pass

def close_spider(self, spider):
    # Called when the spider is closed
    pass

@classmethod
def from_crawler(cls, crawler):
    # Access Scrapy settings or crawler instance
    pass
```

---

## ✅ Common Use Cases

### 🧹 Cleaning or Formatting Data

```python
item['price'] = float(item['price'].replace('$', ''))
```

### 🚫 Filtering Duplicates

```python
from scrapy.exceptions import DropItem

class DuplicatesPipeline:
    def __init__(self):
        self.seen = set()

    def process_item(self, item, spider):
        if item['id'] in self.seen:
            raise DropItem("Duplicate item found")
        self.seen.add(item['id'])
        return item
```

### 🗃️ Saving to Database

```python
import sqlite3

class SQLitePipeline:
    def open_spider(self, spider):
        self.conn = sqlite3.connect("items.db")
        self.cursor = self.conn.cursor()

    def process_item(self, item, spider):
        self.cursor.execute("INSERT INTO items (title) VALUES (?)", (item['title'],))
        self.conn.commit()
        return item

    def close_spider(self, spider):
        self.conn.close()
```

---

## 📚 Summary

- `pipelines.py` lets you process, filter, and save scraped items.
- Pipelines are processed in the order defined in `ITEM_PIPELINES`.
- Ideal for data cleaning, validation, transformation, and storage.
