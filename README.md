[G2 Scraper](https://apify.com/alizarin_refrigerator-owner/g2-scraper?fpr=data)

Scrape G2.com for B2B software product reviews, ratings, G2 Grid positions, and competitive intelligence. Extract satisfaction scores, market presence data, company size breakdowns, and alternative product recommendations. Essential for SaaS marketing and software market research.

---

## Quick Start

### Test with Demo Mode (free, no API key needed)

```
{
  "demoMode": true,
  "scrapeType": "category_search",
  "productUrl": "https://www.g2.com/products/hubspot-crm/reviews",
  "category": "CRM Software",
  "maxReviewsPerProduct": 10,
  "maxResults": 10,
  "proxyConfiguration": {
    "useApifyProxy": true,
    "apifyProxyGroups": [
      "RESIDENTIAL"
    ]
  }
}
```

### Run with real data

```
{
  "demoMode": false,
  "scrapeType": "category_search",
  "productUrl": "https://www.g2.com/products/hubspot-crm/reviews",
  "category": "CRM Software",
  "companySize": "any",
  "includeReviews": true,
  "maxReviewsPerProduct": 10,
  "includeAlternatives": false,
  "includePricing": true,
  "maxResults": 10,
  "proxyConfiguration": {
    "useApifyProxy": true,
    "apifyProxyGroups": [
      "RESIDENTIAL"
    ]
  },
  "webhookPlatform": "custom"
}
```

---

## Input Parameters

| Parameter | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| `scrapeType` | string | `"category_search"` | No | What to scrape. 'category_search' browses a G2 category page. 'product_profile' scrapes one product (requires Product URL or Product Name). 'alternatives' finds competitors for a product. |
| `productUrl` | string | - | No | Full G2 product page URL. RECOMMENDED — paste the URL from your browser for best results. Example: [https://www.g2.com/products/hubspot-crm/reviews](https://www.g2.com/products/hubspot-crm/reviews) |
| `productName` | string | - | No | Software product name to search on G2 (e.g. 'HubSpot CRM'). Only needed if you don't have a direct Product URL. |
| `category` | string | `"CRM Software"` | No | G2 software category. Common values: CRM Software, Marketing Automation, Project Management, HR Software, Help Desk Software, Email Marketing, SEO Tools, Accounting, E-Commerce, Video Conferencing, Analytics, Website Builder, Live Chat, Chatbot, AI Writing |
| `minRating` | number | - | No | Only include products with this rating or higher (1.0-5.0) |
| `companySize` | string | `"any"` | No | Filter by company size |
| `includeReviews` | boolean | `true` | No | Scrape user reviews for each product |
| `maxReviewsPerProduct` | integer | `10` | No | Maximum reviews to collect per product. Keep low (10-25) for faster runs. |
| `includeAlternatives` | boolean | `false` | No | Include competitor/alternative products |
| `includePricing` | boolean | `true` | No | Include pricing information when available |
| `maxResults` | integer | `10` | No | Maximum number of products to scrape. Start small (5-10) — G2 blocks large requests. |
| `proxyConfiguration` | object | - | No | Proxy settings. Defaults to RESIDENTIAL proxies (recommended for G2). |
| `demoMode` | boolean | `false` | No | When ON, returns realistic sample data WITHOUT hitting G2 (free, instant, no blocking). Turn OFF for real scraping. G2 has aggressive anti-bot protection — real scraping may get blocked. |
| `webhookUrl` | string | - | No | URL to POST results when scraping completes (Zapier, Make, n8n, custom endpoint) |
| `webhookPlatform` | string | `"custom"` | No | Platform-specific payload formatting |
| `webhookHeaders` | object | - | No | Custom HTTP headers to send with webhook (JSON object) |

---

## Pricing

This actor uses **pay-per-event** billing:

| Event | Description | Price |
| --- | --- | --- |
| Product Scraped | Each G2 product profile scraped | $0.06 |

**Demo mode is free** -- no charges for sample data.

---

## Troubleshooting

### "API error 429" or "Rate limit"

Too many requests. Wait a minute and try again, or reduce the number of items per run.

### No results or empty dataset

Check the run log for error messages. Common causes:

- Invalid input format (check the examples above)
- The target data doesn't exist or is too small to track

### How do I test without an API key?

Enable **Demo Mode** in the input. This returns realistic sample data so you can verify the output format works for your workflow.

---

**Built by John Rippy | [Actor Arsenal](https://actorarsenal.com)**