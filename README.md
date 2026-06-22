[G2 Scraper](https://apify.com/fatihtahta/g2-scraper?fpr=data)

# G2 Scraper | Fast & Reliable | $7 / 1k

**Slug:** `fatihtahta/g2-scraper`
**Price:** **$7.00 per 1,000 saved products**

Turn any **G2 search results page** into clean, structured company/product data you can actually use. Just point at a search URL and get a deduped dataset for research, enrichment, and analysis.

---

## What is G2?

**G2** is one of the largest software marketplaces and review platforms. Companies list their products, collect verified user reviews, and are organized into categories (e.g., CRM, Marketing Automation, BI). Search pages typically show a product’s **name, vendor, rating, review count, description snippet, categories, logos**, and links to the product and seller pages. That’s exactly the information this actor captures—at scale.

---

## What You Get (Features & Fields)

This actor extracts the **public data shown on G2 search result pages** and saves each product row as a structured record:

- **Identity & Links**

- `productName`, `vendorName`, `itemType` (e.g., “Software”)
- `productUrl`, `reviewsUrl`
- `sellerName`, `sellerUrl`
- `thumbImageUrl` (logo, not a placeholder)
- **IDs & Rank**

- `productId`, `productUuid`, `vendorId` *(when present in the page metadata)*
- `resultRank` *(position in the list when available)*
- **Ratings & Social Proof**

- `ratingOutOfFive` (0–5), `ratingOutOfTen` (0–10)
- `reviewCount`
- **Content & Taxonomy**

- `descriptionSnippet` (the visible summary on the card)
- `relatedCategories` (names)
- `categoriesDetailed` (array of `{ id, name, url }`)
- **Provenance**

- `searchUrl`, `query`, `scrapedAt`, `foundVia`

**Use it for:**

- Company & product **enrichment** (ratings, review counts, categories, logos).
- **Market landscaping** and category mapping.
- **Competitor lists** and shortlist generation.
- Feeding downstream **research, scoring, and prioritization** workflows.

---

## 📥 Input Configuration

- `startUrl` *(string, required)*: A **G2 search results** URL
Examples:

- `https://www.g2.com/search?query=mention`
- `https://www.g2.com/search?query=crm`
- `maxItems` *(integer, optional)*: Hard cap on saved results.

> Tip: Keep the URL simple. The actor will handle page numbers for you.

---

## 📦 Input & Output Examples

### Example Input

```
{
  "startUrl": "[https://www.g2.com/search?query=mention](https://www.g2.com/search?query=mention)",
  "maxItems": 120,
  "proxyConfiguration": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

### Example Output Item

Each dataset item represents a **product row** from the search page:

```
{
  "scrapedAt": "2025-09-06T12:42:32.358Z",
  "searchUrl": "https://www.g2.com/search?query=mention",
  "query": "mention",
  "itemType": "Software",
  "productId": 20638,
  "productUuid": "901093dc-bf92-47b1-a2d0-588fe09ba66f",
  "vendorId": 16830,
  "resultRank": 4,
  "productName": "Mentionlytics",
  "vendorName": "Mentionlytics Ltd",
  "ratingOutOfFive": 4.9,
  "ratingOutOfTen": 9.8,
  "reviewCount": 90,
  "descriptionSnippet": "Web & Social Media Monitoring tool that tracks mentions across the web and social platforms.",
  "thumbImageUrl": "https://images.g2crowd.com/uploads/product/hd_favicon/374068704d3e8ad9268aa24d76a7029f/mentionlytics.svg",
  "relatedCategories": [
    "Media Monitoring",
    "Social Media Analytics",
    "Social Media Management",
    "Social Media Listening Tools"
  ],
  "categoriesDetailed": [
    {"id": 350, "name": "Media Monitoring", "url": "https://www.g2.com/categories/media-monitoring"},
    {"id": 240, "name": "Social Media Analytics", "url": "https://www.g2.com/categories/social-media-analytics"}
  ],
  "sellerName": "Mentionlytics Ltd",
  "sellerUrl": "https://www.g2.com/sellers/mentionlytics-ltd",
  "productUrl": "https://www.g2.com/products/mentionlytics/reviews",
  "reviewsUrl": "https://www.g2.com/products/mentionlytics/reviews",
  "foundVia": "g2"
}
```

---

## 💰 Pricing (Simple & Transparent)

- **$7.00 per 1,000 saved products.**
Only pay for **successfully saved** items.
Example: 10,000 products cost **(10,000 / 1,000) × $7.00 = $70.00**.

## ⚖️ Legal

This scraper extracts **publicly visible information** from G2 search pages. You’re responsible for how you use the data. If your use case involves personal data (e.g., user-generated content), ensure you have a lawful basis (GDPR/CCPA/etc.). When in doubt, talk to your counsel.

---

## ❓ Support

Questions, bugs, or feature requests? Open an issue on the **Issues** tab of the actor page in Apify Console and it'll be solved around the clock.

Happy Scraping!
**Fatih**