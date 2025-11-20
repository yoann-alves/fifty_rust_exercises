# Exercise 50: Web Scraper

## 🎯 Objectives

Build a web scraping tool:

- Fetch HTML pages from websites
- Parse HTML to find specific elements
- Extract data (titles, links, prices, etc.)
- Save results in a structured format
- Implement rate limiting (be respectful!)
- Handle errors gracefully

## 📚 Concepts

- HTTP requests
- HTML parsing
- CSS selectors
- Rate limiting
- Error handling
- Data serialization
- Ethical scraping practices

## 📖 Background

**Web scraping** is automated data extraction from websites. Instead of manually copying information, a program fetches web pages and extracts structured data.

**How it works:**

1. Send HTTP request to get HTML
2. Parse the HTML document
3. Use selectors to find specific elements (like finding all `<h2>` tags with class "title")
4. Extract the data (text, attributes, links)
5. Save to file or database

**Real-world example:**

```
Website shows:
  <article>
    <h2 class="title">Breaking News</h2>
    <a href="/article/123">Read more</a>
    <span class="author">Alice</span>
  </article>

Your scraper extracts:
  Title: "Breaking News"
  URL: "/article/123"
  Author: "Alice"
```

**Ethics matter:**

- **Rate limiting**: Don't hammer servers with requests
- **robots.txt**: Check if scraping is allowed
- **User-Agent**: Identify your bot
- **APIs first**: Use official APIs when available
- **Legal**: Respect terms of service

## ⚙️ Requirements

**First Pass:**

- ✅ Fetches an HTML page
- ✅ Parses HTML and finds elements
- ✅ Extracts specific data
- ✅ Saves results to a file
- ✅ Waits between requests (rate limiting)
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain what you're scraping and why
- ✅ **Multiple pages**: Handle pagination or lists of URLs
- ✅ **Robust extraction**:
  - Handle missing elements gracefully
  - Clean/normalize extracted data
  - Extract multiple types of data (text, attributes, links)
- ✅ **Output formats**:
  - JSON (structured data)
  - CSV (tabular data)
  - Console output for debugging
- ✅ **Proper rate limiting**:
  - Configurable delay between requests
  - Respect server's rate limits
  - Don't make concurrent requests without control
- ✅ **Error handling**:
  - Network failures
  - Invalid HTML
  - Missing elements
  - HTTP errors (404, 500, etc.)
  - Continue scraping even if one page fails
- ✅ **Retry logic**: Retry failed requests with exponential backoff
- ✅ **Configuration**: CLI args or config file for URLs, selectors, rate limits

## 🚫 Constraints

- Use `reqwest` for HTTP (recommended)
- Use `scraper` or similar for HTML parsing (recommended)
- Use `serde` and `serde_json` for JSON output
- **Mandatory**: Implement rate limiting - minimum 1 second between requests
- Respect websites: don't scrape aggressively

## 💡 Approaches

**HTTP client:**

- Build a client with timeout
- Set custom User-Agent header
- Handle response status codes
- Read response body as text

**HTML parsing:**

- Parse HTML into a document structure
- Use CSS selectors to find elements
- Navigate the DOM tree
- Extract text content or attributes

**Rate limiting strategies:**

- Sleep between requests
- Track request timestamps
- Sliding window approach
- Token bucket algorithm

**Data extraction patterns:**

- Find container elements first
- Extract data from each container
- Handle optional fields
- Validate extracted data

**Pagination:**

- Extract "next page" link
- Loop until no more pages
- URL patterns (page=1, page=2, etc.)
- Stop conditions

**Error recovery:**

- Retry with exponential backoff
- Skip failed pages and continue
- Log errors for manual review
- Partial success is acceptable

## ✅ Validation

Your scraper should handle scenarios like these:

```
# Single page scrape
Target: https://example.com/articles
Extract: Article titles, authors, dates
Output: articles.json with 25 entries
Rate: 1 request, 1 second delay

# Multiple pages
Target: https://example.com/articles?page=1..5
Extract: Same data across pages
Output: articles.json with 125 entries
Rate: 5 requests, 5 seconds total (1s between each)

# With errors
Page 1: Success (20 articles)
Page 2: Success (20 articles)
Page 3: HTTP 500 error - retry - success (20 articles)
Page 4: Success (15 articles)
Total: 75 articles extracted
```

**Expected output structure (JSON):**

```json
[
  {
    "title": "First Article",
    "url": "https://example.com/article/1",
    "author": "Alice",
    "date": "2025-01-15"
  },
  {
    "title": "Second Article",
    "url": "https://example.com/article/2",
    "author": "Bob",
    "date": "2025-01-14"
  }
]
```

**Expected output structure (CSV):**

```csv
title,url,author,date
First Article,https://example.com/article/1,Alice,2025-01-15
Second Article,https://example.com/article/2,Bob,2025-01-14
```

**Console output example:**

```
Scraping: https://example.com/articles
Found 25 articles
Waiting 1s before next request...
Scraping: https://example.com/articles?page=2
Found 20 articles
Scraping complete!
Total articles: 45
Saved to: articles.json
```

**Error handling example:**

```
Scraping: https://example.com/page1
✓ Success (20 articles)

Scraping: https://example.com/page2
✗ Error: Connection timeout
Retrying in 2s...
✓ Success (20 articles)

Scraping: https://example.com/page3
✗ Error: HTTP 404
Skipping page and continuing...

Final: 40/60 articles extracted (66% success)
```

## 🔍 Challenge

Add support for JavaScript-rendered pages using a headless browser, implement distributed scraping across multiple machines, create a visual dashboard showing scraping progress in real-time, or build a configuration format that lets non-programmers define what to scrape without writing code.

---

**Previous:** [49_parallel_sorter](../49_parallel_sorter/README.md)
