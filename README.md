# WooCommerce Product Data Extraction

## Project Overview

This project demonstrates an end-to-end **web data extraction and product catalogue cleaning workflow** using a live WooCommerce-powered e-commerce website.

I extracted the website's complete public product catalogue through its **WooCommerce Store API**, processed the returned nested JSON data, cleaned and validated the records, and delivered the final dataset in structured **CSV and Excel formats**.

The final extraction contained **324 products across 33 API pages**.

---

## Business Objective

The objective was to turn raw product catalogue data from a live e-commerce website into a clean, structured and reusable dataset suitable for:

* Product catalogue management
* Data analysis and reporting
* E-commerce data processing
* Inventory and product research
* Downstream data workflows

---

## Data Source

**Source website:** Male Vega Dish
**Platform:** WooCommerce
**Data access method:** Public WooCommerce Store API
**API endpoint:**

`https://malevegadish.com/wp-json/wc/store/v1/products`

The website provides a publicly accessible, read-only catalogue API without requiring authentication for product catalogue retrieval.

---

## Extraction Workflow

The project followed this workflow:

**Source Website → Public API → Pagination → JSON Extraction → Transformation → Cleaning → Validation → Excel/CSV Delivery**

### 1. API Reconnaissance

I first verified that the website's WordPress/WooCommerce API was accessible and returning valid JSON responses.

The product endpoint was tested using Python's `requests` library before beginning the full extraction.

### 2. Product Data Extraction

The API returned product information in a nested JSON structure.

The extraction captured business-relevant fields including:

* Product ID
* Product Name
* SKU
* Current Price
* Regular Price
* Currency
* Sale Status
* Average Rating
* Review Count
* Categories
* Stock Status
* Product URL

### 3. Pagination Handling

The catalogue contained multiple API pages rather than a single response.

I identified:

* **324 total products**
* **33 API pages**
* **10 records per page** for the extraction process
* **4 records on the final page**

The extraction loop processed the complete catalogue instead of collecting only the first page.

### 4. Request Reliability

The extraction included basic safeguards for real-world API behaviour:

* Request timeouts
* Retry handling for temporary failures
* HTTP error handling
* Controlled request delays
* Extraction logging

Temporary HTTP responses such as `429`, `500`, `502`, `503`, and `504` were handled through retry logic.

### 5. JSON Transformation

The raw API response contained nested objects and lists.

I transformed the nested structures into a flat tabular dataset by:

* Extracting fields from the `prices` object
* Converting API price values from minor currency units
* Flattening category names
* Flattening brand information
* Preserving missing values where appropriate

### 6. Data Cleaning

The extracted dataset initially contained a `Brands` field with no populated values across the catalogue.

After assessing the missingness, the field was removed rather than introducing artificial values.

I also:

* Standardized text fields
* Converted ratings to numeric values
* Removed unnecessary whitespace
* Preserved the one legitimate missing category value
* Maintained the original raw JSON separately for traceability

---

## Data Quality Validation

Before delivery, the cleaned dataset was validated against several business and structural rules.

### Final Validation Results

| Check                    | Result |
| ------------------------ | -----: |
| Products collected       |    324 |
| Unique Product IDs       |    324 |
| Duplicate Product IDs    |      0 |
| Failed extraction pages  |      0 |
| Missing Product Names    |      0 |
| Missing SKUs             |      0 |
| Missing Currency         |      0 |
| Missing Product URLs     |      0 |
| Negative Current Prices  |      0 |
| Negative Regular Prices  |      0 |
| Negative Review Counts   |      0 |
| Ratings below 0          |      0 |
| Ratings above 5          |      0 |
| Price consistency errors |      0 |

The final dataset passed the extraction and data-quality checks.

---

## Final Dataset

The cleaned dataset contains **324 records and 12 business-relevant fields**:

1. `Product_ID`
2. `Product_Name`
3. `SKU`
4. `Current_Price`
5. `Regular_Price`
6. `Currency`
7. `On_Sale`
8. `Average_Rating`
9. `Review_Count`
10. `Categories`
11. `In_Stock`
12. `Product_URL`

---

## Deliverables

The project includes:

* `Web_Data_Extraction_Portfolio.ipynb` — complete Python workflow
* `products_clean.csv` — cleaned CSV dataset
* `products_clean.xlsx` — cleaned Excel dataset
* `raw_products.json` — preserved raw API response
* `extraction_log.txt` — page-level extraction and validation log
* `Project_Overview.pdf` — concise project documentation

---

## Tools & Technologies

**Python**
**Requests**
**Pandas**
**JSON**
**Google Colab**
**WooCommerce Store API**

---

## Key Skills Demonstrated

* Web Data Extraction
* API Data Extraction
* REST API
* WooCommerce Data Extraction
* E-commerce Product Data
* JSON Data Processing
* Pagination
* Request Error Handling
* Data Cleaning
* Data Transformation
* Data Validation
* Data Quality Assurance
* Structured Dataset Creation
* Excel Data Processing
* CSV Data Delivery

---

## Project Outcome

The result is a complete, validated and structured product catalogue extracted from a live e-commerce API.

Instead of leaving the information in its original nested JSON format, I converted it into a clean dataset that can be directly used for **analysis, reporting, catalogue management and further data-processing workflows**.
