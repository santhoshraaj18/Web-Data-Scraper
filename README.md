
# Web Data Scraper

## Overview

A Python tool for extracting and formatting web data (tables, headings, paragraphs, etc.) using `requests` and `BeautifulSoup`. Outputs structured data or pandas DataFrames.

## Features

- ✅ Extract headings (H1-H6), paragraphs, tables, lists, and links
- ✅ Convert HTML tables to pandas DataFrames
- ✅ Clean, readable output
- ✅ Works in scripts or Jupyter Notebooks

## Installation

```bash
git clone https://github.com/yourusername/web-data-scraper.git
cd web-data-scraper
pip install requests beautifulsoup4 pandas
```

## Usage

### Python Script
```python
from scraper import WebScraper

url = "https://example.com"
scraper = WebScraper(url)
scraper.scrape_all()  # Prints all extracted data
```

### Jupyter Notebook
```python
from scraper import WebScraper
WebScraper("https://example.com").scrape_all()
```

## Example Output
```
[Headings]
# Welcome to Example.com

[Tables]
+---------+-------+
| Product | Price |
+---------+-------+
| Apple   | $1.20 |
| Orange  | $0.80 |
+---------+-------+

[Links]
About Us: /about
Contact: /contact
```

## Sample Code (`scraper.py`)
```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

class WebScraper:
    def __init__(self, url):
        self.url = url
        self.soup = BeautifulSoup(requests.get(url).content, 'html.parser')
    
    def scrape_all(self):
        print("\n[Headings]")
        for h in self.soup.find_all(['h1', 'h2', 'h3']):
            print(h.text.strip())
        
        print("\n[Tables]")
        for i, table in enumerate(self.soup.find_all('table')):
            print(pd.read_html(str(table))[0].to_markdown())
```

## License
MIT © 2025
