[G2 Scraper](https://apify.com/memo23/g2-scraper?fpr=data)

## Overview

Extract software and service listings from G2.com search results. Get detailed information including product names, ratings, review counts, vendor details, and descriptions for market analysis and competitor tracking.

The **G2 Search Results Scraper** is a specialized tool designed to extract structured data from [G2.com](https://www.g2.com/) search pages. This scraper delivers key data points for software products and services found via search queries, enabling efficient market research.

With this scraper, users gain access to **product listings** matching specific search terms. The tool captures **essential performance metrics** such as star ratings and review counts, alongside descriptive snippets and vendor info.

**Key metrics** are extracted, including Rating out of 5, Total Review Count, and Product Description Snippets.

The scraper excels at capturing **search result metadata**, such as the rank of the result, sponsorship status, and pricing indicators (free trial, etc).

**Ease of use** is a priority - simply provide a G2 search URL, and the scraper handles pagination to retrieve all matching results up to your specified limit.

Whether you're a market researcher tracking competitor positioning, a software buyer comparing tools, or a data analyst investigating software trends, this scraper provides the structured dataset needed for informed decisions.

---

## Features

- **Search Scraping**:

- Automatically iterates through search result pages (pagination)
- Supports keyword queries via direct URLs
- Handles G2's search layout to extract product cards
- **Comprehensive Product Data**:

- Extracts core product details: Product Name, Description Snippet, and Thumbnail Image
- Captures unique identifiers like Product ID and UUID
- Identifies listing type and pricing indicators (Free Trial, Entry Level Price)
- **Vendor & Seller Info**:

- **Vendor Name**: The company behind the software
- **Seller Links**: Direct URLs to vendor profiles on G2
- **Performance Metrics**:

- **Ratings**: Star rating details (out of 5 and out of 10)
- **Reviews**: Total number of reviews on G2
- **Metadata & Categories**:

- Captures rank position in search results
- Identifies "Sponsored" listings
- Retrieves associated software categories
- **Efficient Data Extraction**:

- optimized for search result parsing
- Robust error handling and bypass mechanisms for protected pages
- Designed for high-concurrency scraping

---

## How to Use

1. **Set Up**: Ensure you have an Apify account and access to the Apify platform.
2. **Provide Input Data**: Input specific scraping parameters, specifically the `startUrls` pointing to G2 search results.
3. **Adjust Scraper Settings**: Configure settings like `maxItems`, `maxConcurrency`, and `maxRequestRetries` to optimize performance.
4. **Run the Scraper**: Execute the scraper on the Apify platform.
5. **Download Results**: Export the scraped data in your preferred format (JSON, CSV, Excel).

### Usage Limitations

**Free Users**: Non-paying users are limited to scraping a fixed number of listings per run. To access unlimited scraping and all features, please upgrade to a paid Apify account.

**Paid Users**: Enjoy unlimited scraping, multiple start URLs, and full access to all scraper features.

---

## Input Configuration

To use the scraper, configure the input parameters as follows. You typically only need to provide a G2 Search URL.

```
{
    "startUrls": [
        {
            "url": "https://www.g2.com/search?query=databricks"
        },
        {
            "url": "https://www.g2.com/search?query=crm+software"
        }
    ],
    "maxItems": 100,
    "maxConcurrency": 20,
    "minConcurrency": 1,
    "maxRequestRetries": 5,
    "proxy": {
        "useApifyProxy": true,
        "apifyProxyGroups": [
            "RESIDENTIAL"
        ]
    }
}
```

### Input Fields Explanation

- **Start URLs** (`startUrls`): The URLs from which the scraper will begin extracting data. The scraper accepts:

- **G2 Search URLs**: Links to search results on G2.com
- Example: `https://www.g2.com/search?query=project+management`
- **Max Items** (`maxItems`): Maximum number of listings to scrape per run. Default is `100`.
- **Max Concurrency** (`maxConcurrency`): Maximum number of pages processed simultaneously.
- **Min Concurrency** (`minConcurrency`): Minimum number of pages processed simultaneously.
- **Max Request Retries** (`maxRequestRetries`): Number of retries for failed requests.
- **Proxy Configuration** (`proxy`): Settings for reliable and anonymous scraping. **Residential proxies are highly recommended** for G2.

---

## Output Structure

The scraper produces structured JSON output with comprehensive product data.

### Sample Data

```
{
  "scrapedAt": "2026-01-24T12:20:50.165Z",
  "searchUrl": "https://www.g2.com/search?query=databricks",
  "query": "databricks",
  "itemType": "Software",
  "resultRank": 1,
  "foundVia": "g2",
  "isSponsored": false,
  "pricingType": null,
  "productName": "Azure Databricks",
  "productId": 67962,
  "productUuid": "f326c17a-5165-4436-ae44-948c44a6ad31",
  "productUrl": "https://www.g2.com/products/azure-databricks/reviews",
  "reviewsUrl": "https://www.g2.com/products/azure-databricks/reviews",
  "thumbImageUrl": "https://images.g2crowd.com/uploads/vendor/image/359/13bbb369c8268754a786f3dce328f6ce.jpeg",
  "descriptionSnippet": "Azure Databricks is a unified, open analytics platform developed collaboratively by Microsoft and Databricks. Built on the lakehouse architecture, it seamlessly integrates data engineering, data science, and machine learning within the Azure ecosystem. This platform simplifies the development and deployment of data-driven applications by providing a collaborative workspace that supports multiple programming languages, including SQL, Python, R, and Scala. By leveraging Azure Databricks, organizat",
  "vendorName": "Microsoft",
  "vendorId": 359,
  "sellerName": "Microsoft",
  "sellerUrl": "https://www.g2.com/sellers/microsoft",
  "ratingOutOfFive": 4.5,
  "ratingOutOfTen": 9,
  "reviewCount": 228,
  "relatedCategories": [
      "Big Data Analytics"
  ],
  "categoriesDetailed": [
      {
          "id": 1041,
          "name": "Big Data Analytics",
          "url": "https://www.g2.com/categories/big-data-analytics"
      }
  ]
}
```

---

## Output Fields Explanation

Below is an exhaustive explanation of every field in the output JSON dataset.

### 1. Metadata & Search Context

- **scrapedAt**: ISO 8601 timestamp indicating exactly when this data point was extracted (e.g., "2026-01-24T12:20:50.165Z").
- **searchUrl**: The complete G2 search URL used to discover this listing. Useful for debugging or traceability.
- **query**: The specific keyword or phrase used in the search (e.g., "databricks").
- **resultRank**: The rank of this product in the search results (1 = top result).
- **foundVia**: The source platform identifier (static value "g2").
- **itemType**: The type of item returned, usually "Software" or "Service".

### 2. Listing Status & Pricing

- **isSponsored**: Boolean (`true`/`false`) indicating if this is a paid/promoted listing in the search results.
- **pricingType**: Text indicating the pricing model or offer, such as "Free Trial", "Free", or `null` if not specified.

### 3. Core Product Information

- **productName**: The official name of the software or service (e.g., "Azure Databricks").
- **productId**: G2's internal numeric ID for the product (e.g., 67962).
- **productUuid**: G2's internal unique alphanumeric identifier (UUID).
- **productUrl**: Canonical URL to the product's main page or reviews on G2.
- **reviewsUrl**: Direct URL to the reviews section for this product.
- **thumbImageUrl**: URL for the product's logo or thumbnail image from G2's CDN.
- **descriptionSnippet**: A brief summary or description of the product as displayed on the search result card.

### 4. Vendor Details

- **vendorName**: Name of the company that produces the software.
- **vendorId**: G2's internal numeric ID for the vendor company.
- **sellerName**: Often identical to vendorName, represents the "seller" entity on G2.
- **sellerUrl**: Direct link to the vendor's profile page on G2.

### 5. Performance Metrics

- **ratingOutOfFive**: The aggregate star rating of the product on a scale of 0 to 5 (e.g., 4.5).
- **ratingOutOfTen**: The rating normalized to a scale of 0 to 10 (e.g., 9).
- **reviewCount**: The total number of valid user reviews for the product on G2.

### 6. Categorization

- **relatedCategories**: An array of string names for the primary categories this product belongs to (e.g., ["Big Data Analytics"]).
- **categoriesDetailed**: A detailed array of category objects, each containing:

- `id`: Numeric category ID.
- `name`: Human-readable category name.
- `url`: Link to the specific category page on G2.

---

## Benefits of the G2 Search Scraper

- **Market Intelligence**: Quickly gather lists of players in specific software software categories.
- **Competitor Analysis**: Compare ratings and review counts across multiple products in a niche.
- **Lead Generation**: Identify vendors and software providers in target industries.
- **Trend Monitoring**: Track new entrants and rising stars in G2 search results.
- **Structured Data**: Get clean, JSON formatted data ready for analysis tools.

---

## Why Choose the G2 Search Scraper?

This scraper allows you to bypass the need for manual copy-pasting from search results. It automates the collection of high-level product metrics, allowing you to focus on analysis rather than data entry.

**Use Cases:**

- Populating internal competitor databases.
- Aggregating software options for procurement research.
- Monitoring brand visibility in search results.

---

## Technical Implementation

The scraper uses a robust approach:

1. **Cheerio Parsing**: Utilizes efficient HTML parsing to extract data from G2's server-rendered search pages.
2. **Pagination Handling**: Automatically detects and navigates to "Next" pages to ensure complete data coverage up to your limit.
3. **Resiliency**: Built to handle standard G2 layouts and fallback to safe defaults if specific metadata is missing.

---

## Explore More Scrapers

If you found the G2 Search Results Scraper useful, check out other powerful scrapers and actors at [memo23's Apify profile](https://apify.com/memo23). We offer a wide range of tools to enhance your web scraping and automation needs.

---

## Support

- For issues or feature requests, please use the [Issues](https://console.apify.com/actors/ftbw0YFo17iTQ2qjv/issues) section of this actor.
- For further assistance, contact the author:

- Author's website: [https://muhamed-didovic.github.io/](https://muhamed-didovic.github.io/)
- Email: [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)

---

## Additional Services

- Request customization or a full dataset: [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)
- Need other platforms scraped? Contact [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)
- For API services of this scraper, reach out to [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)
- Custom integrations and automation solutions available

---

## Legal & Compliance

This scraper is designed for legitimate business and research purposes. Users are responsible for:

- Complying with G2.com's terms of service.
- Respecting robots.txt and rate limiting.
- Using scraped data in accordance with applicable laws.
- Obtaining necessary permissions for commercial use of data.

---

## FAQ

**Q: How many listings can I scrape?**
A: Free users can scrape a limited number per run. Paid users have unlimited access governed by their plan.

**Q: Does it scrape full reviews?**
A: No, this version focuses on Search Results and high-level metadata to ensure stability and speed.

**Q: Are financials extracted?**
A: No, G2 does not typically provide public financial data like revenue.

**Q: How often is data updated?**
A: Data is scraped in real-time from the search results.