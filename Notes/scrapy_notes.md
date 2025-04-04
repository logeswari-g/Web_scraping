# 🕷️ Scrapy Complete Notes with Real-time Example

---

## 📌 1. Introduction to Scrapy

- Scrapy is a Python framework for extracting data from websites.
- It's built on **Twisted**, an asynchronous networking library.
- Used for web crawling, scraping, and data mining.

---

## 📁 2. Project Structure

When you run `scrapy startproject myproject`, you get:

```
myproject/
│
├── scrapy.cfg
└── myproject/
    ├── __init__.py
    ├── items.py          # Data container
    ├── middlewares.py    # Modify requests/responses
    ├── pipelines.py      # Post-processing
    ├── settings.py       # Configuration
    └── spiders/          # Spider definitions
```

---

## 🧱 3. Basic Commands

| Command | Description |
|--------|-------------|
| `scrapy startproject project_name` | Create new project |
| `scrapy genspider spider_name domain.com` | Create spider |
| `scrapy crawl spider_name` | Run the spider |
| `scrapy shell 'url'` | Open interactive shell |
| `scrapy list` | List all spiders |
| `scrapy runspider file.py` | Run standalone script |

---

## 🕷️ 4. Real-Time Spider Example

We’ll scrape quotes from `http://quotes.toscrape.com`.

### Step 1: Start a project

```bash
scrapy startproject quotes_scraper
cd quotes_scraper
```

### Step 2: Create a spider

```bash
scrapy genspider quotes quotes.toscrape.com
```

### Step 3: Edit the spider `quotes_scraper/spiders/quotes.py`

```python
import scrapy

class QuotesSpider(scrapy.Spider):
    name = 'quotes'
    start_urls = ['http://quotes.toscrape.com']

    def parse(self, response):
        for quote in response.css('div.quote'):
            yield {
                'text': quote.css('span.text::text').get(),
                'author': quote.css('small.author::text').get(),
                'tags': quote.css('div.tags a.tag::text').getall()
            }

        next_page = response.css('li.next a::attr(href)').get()
        if next_page:
            yield response.follow(next_page, self.parse)
```

### Step 4: Run the spider

```bash
scrapy crawl quotes -o quotes.json
```

---

## 🔍 5. Selectors (CSS and XPath)

**CSS Selector Examples:**

```python
response.css('title::text').get()
response.css('div.quote > span.text::text').getall()
```

**XPath Examples:**

```python
response.xpath('//span[@class="text"]/text()').get()
response.xpath('//div[@class="quote"]').getall()
```

---

## 📦 6. Using Items

Define structured data in `items.py`:

```python
import scrapy

class QuoteItem(scrapy.Item):
    text = scrapy.Field()
    author = scrapy.Field()
    tags = scrapy.Field()
```

Use in spider:

```python
from quotes_scraper.items import QuoteItem

item = QuoteItem()
item['text'] = quote.css('span.text::text').get()
yield item
```

---

## 🔄 7. Pipelines

Used for cleaning or saving scraped data.

```python
class QuotesPipeline:
    def process_item(self, item, spider):
        item['text'] = item['text'].strip('“”')
        return item
```

Enable in `settings.py`:

```python
ITEM_PIPELINES = {
    'quotes_scraper.pipelines.QuotesPipeline': 300,
}
```

---

## ⚙️ 8. Key Settings

```python
ROBOTSTXT_OBEY = False
DOWNLOAD_DELAY = 1
USER_AGENT = 'Mozilla/5.0'
FEED_EXPORT_ENCODING = 'utf-8'
```

---

## 🔗 9. Pagination

```python
next_page = response.css('li.next a::attr(href)').get()
if next_page:
    yield response.follow(next_page, self.parse)
```

---

## 🌐 10. Handling Login (Authenticated Sites)

```python
def start_requests(self):
    return [scrapy.FormRequest(
        url='http://example.com/login',
        formdata={'user': 'john', 'pass': '123'},
        callback=self.after_login
    )]

def after_login(self, response):
    yield response.follow('/protected/page', self.parse_protected)
```

---

## 🧪 11. Testing Selectors with Shell

```bash
scrapy shell 'http://quotes.toscrape.com'
```

Then try:

```python
response.css('small.author::text').getall()
```

---

## 🛡️ 12. Avoid Getting Blocked

- Set `DOWNLOAD_DELAY`
- Rotate User-Agents and IPs
- Use Proxies
- Use Headless browsers (Selenium/Playwright) if needed
- Use services like ScraperAPI, BrightData, Crawlera

---

## ⚡ 13. Performance Tuning

```python
CONCURRENT_REQUESTS = 32
AUTOTHROTTLE_ENABLED = True
DOWNLOAD_TIMEOUT = 15
```

---

## 🧹 14. Clean Code Tips

- Use Items for structured data
- Keep parsing logic clean
- Validate and clean data in Pipelines
- Use logging for debug info

---

## 📤 15. Exporting Data

```bash
scrapy crawl quotes -o quotes.csv
scrapy crawl quotes -o quotes.jl
scrapy crawl quotes -o quotes.json
```

---

## 📚 More

- [Docs](https://docs.scrapy.org)
- [Selectors Cheat Sheet](https://devhints.io/xpath)
- [Quotes to Scrape](http://quotes.toscrape.com)

---
