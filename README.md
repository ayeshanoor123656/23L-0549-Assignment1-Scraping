# Web Scraping Datasets

Two product datasets collected via web scraping from public sandbox e-commerce sites, demonstrating scraping of **dynamically loaded (infinite scroll)** and **statically paginated** pages.

## Files

| File | Rows | Source site type | Description |
|---|---|---|---|
| `23L_XXXX_versionA_dynamic_products.csv` | 147 | Infinite-scroll (JS-rendered) | Clothing products scraped from an infinite-scroll demo store |
| `23L_XXXX_versionA_static_products__1_.csv` | 3,000 | Static, paginated (94 pages) | Video game products scraped from a paginated demo store |

## `23L_0549_versionA_dynamic_products.csv`

Scraped from an infinite-scroll e-commerce demo. Products were captured in batches as the page was scrolled, since content loads dynamically via JavaScript.

| Column | Type | Description |
|---|---|---|
| `product_name` | string | Name of the product |
| `price` | string | Listed price (e.g. `$52`) |
| `image_url` | string | URL of the product image |
| `scroll_batch` | int | Which scroll/load batch (0–16) the product appeared in |
| `appeared_before_scroll` | bool | Whether the product was visible before any scrolling occurred |
| `sku` | string | Product SKU/code (missing for 4 rows) |
| `short_description` | string | Short product description (missing for 4 rows) |
| `detail_url` | string | Link to the product's detail page |

**Notes:** 4 rows have missing `sku` and `short_description` values.

## `23L_0549_versionA_static_products_.csv`

Scraped from a statically paginated e-commerce demo (video game listings) across 94 listing pages.

| Column | Type | Description |
|---|---|---|
| `name` | string | Name of the product |
| `price` | string | Listed price (e.g. `91,99 €`) |
| `in_stock` | bool | Whether the product was in stock at scrape time |
| `description` | string | Full product description (missing for 30 rows) |
| `detail_url` | string | Link to the product's detail page |
| `listing_page` | int | Listing page number the product was found on (1–94) |

**Notes:** 30 rows have missing `description` values.

## Collection Method

Data was collected using automated web scraping scripts:
- The **dynamic** dataset required simulating scroll events to trigger lazy-loaded content (e.g. via a headless browser / Selenium-style approach), with each load batch tracked in `scroll_batch`.
- The **static** dataset was collected by iterating through paginated listing pages and parsing the resulting HTML.

## Usage

```python
import pandas as pd

dynamic_df = pd.read_csv("23L_0549_versionA_dynamic_products.csv")
static_df = pd.read_csv("23L_0549_versionA_static_products_.csv")
```

## License

Data was scraped from public demo/sandbox e-commerce sites intended for scraping practice. Intended for educational and research use.
