# ⚙️ `middlewares.py` in Scrapy Framework

## 📌 What is `middlewares.py`?

- `middlewares.py` contains **middleware classes** that sit between the **Scrapy engine** and the **Downloader/Spider**.
- Middleware is used to **process requests and responses** globally — before they reach the spider or before they are sent to the web.

---

## 🔄 Types of Middleware in Scrapy

Scrapy uses two main types of middleware:

1. **Spider Middleware**: Interacts with spider input/output.
2. **Downloader Middleware**: Interacts with requests/responses passing to/from the downloader.

---

## 🕸️ Spider Middleware

- Located between the **engine** and **spider**.
- Processes:
  - Responses before they reach the spider.
  - Items or requests returned from the spider.

### Basic Structure

```python
class MySpiderMiddleware:
    def process_spider_input(self, response, spider):
        return None

    def process_spider_output(self, response, result, spider):
        for item in result:
            yield item

    def process_spider_exception(self, response, exception, spider):
        pass

    def process_start_requests(self, start_requests, spider):
        for request in start_requests:
            yield request
```

---

## 🌐 Downloader Middleware

- Located between the **engine** and the **downloader**.
- Processes:
  - Requests before they reach the downloader.
  - Responses before they reach the engine.

### Basic Structure

```python
class MyDownloaderMiddleware:
    def process_request(self, request, spider):
        return None  # or a Response or a Request

    def process_response(self, request, response, spider):
        return response  # or a new Response or Request

    def process_exception(self, request, exception, spider):
        pass
```

---

## ⚙️ Activating Middleware in `settings.py`

```python
DOWNLOADER_MIDDLEWARES = {
    'myproject.middlewares.MyDownloaderMiddleware': 543,
}

SPIDER_MIDDLEWARES = {
    'myproject.middlewares.MySpiderMiddleware': 543,
}
```

- The number (`543`) sets the **order of execution**.
- Lower numbers run **first**.

---

## ✅ Common Use Cases

### 🔁 Retry Middleware

- Automatically retry failed requests.

### 🕵️‍♂️ User-Agent Rotation

```python
import random

class RandomUserAgentMiddleware:
    def __init__(self, user_agents):
        self.user_agents = user_agents

    @classmethod
    def from_crawler(cls, crawler):
        return cls(crawler.settings.getlist('USER_AGENTS'))

    def process_request(self, request, spider):
        request.headers['User-Agent'] = random.choice(self.user_agents)
```

### 🌐 Proxy Middleware

```python
class ProxyMiddleware:
    def process_request(self, request, spider):
        request.meta['proxy'] = 'http://your.proxy.server:port'
```

---

## 📚 Summary

- `middlewares.py` allows you to manipulate requests/responses globally.
- **Spider Middleware**: between engine and spider.
- **Downloader Middleware**: between engine and downloader.
- Useful for retries, logging, headers, proxies, and response validation.
