# DataFeed Parser (JSON & XML)

This Python utility loads structured data from a URL and converts it into a Pandas `DataFrame`.  
It supports **two formats**: **JSON** and **XML** (including `.xml.gz` files compressed with GZIP).

## Features

### Format Detection
- If the HTTP response header contains `Content-Type: application/json`, or if the URL ends with `.json` or contains `"rest-api"`, the content is treated as **JSON**.
- Otherwise, the content is treated as **XML**.

### JSON Processing
- Handles:
  - A list of objects (`[ {...}, {...} ]`)
  - A dictionary containing a `"jobs"` key (`{"jobs": [ {...}, {...} ]}`)
  - Any other JSON object that can be converted into a DataFrame.

### XML Processing
- Works with both standard `.xml` files and `.xml.gz` (GZIP compressed).
- Searches for elements matching the `job_tag` parameter (default: `"job"`) and extracts their child tags and values.

### Data Cleaning
- Truncates overly long text values.
- Replaces invalid numbers (`NaN` or infinite values) with `NaN`.
- Removes columns that are entirely empty, or fills missing values with `0`.

## Summary
`load_feed_to_dataframe()` automatically detects the data format, reads it, cleans it, and returns it as a ready-to-use Pandas `DataFrame` for analysis.
