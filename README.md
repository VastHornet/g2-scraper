[G2 Scraper](https://apify.com/automation-lab/g2-scraper?fpr=data)

Extract reviews, ratings, and product metadata from [G2.com](https://www.g2.com) — the world's largest B2B software review platform with 5M+ reviews and 220K+ products. Get full review text, sentiment themes, all rating dimensions, switching data, and product listings in structured JSON/CSV — no browser required, no proxy needed.

## 🎯 What does it do?

This actor connects directly to G2's public Elasticsearch API and extracts structured data at high speed using plain HTTP requests. No headless browser, no residential proxy — just fast, cheap, reliable scraping.

Three modes are available:

- **Product Reviews** — scrape all reviews for one or more G2 products by URL or slug. Get full review text, star ratings, NPS scores, per-dimension ratings (ease of use, quality of support, etc.), sentiment themes, and switching data.
- **Product Search** — search G2's product catalog by keyword. Get product metadata, review counts, average ratings, categories, and direct links.
- **Category Browse** — list the top products in any G2 category (e.g. "CRM", "Project Management", "Video Conferencing") sorted by review volume.

## 👥 Who is it for?

### 🧠 Competitive intelligence analysts

Monitor what users love and hate about competing products. The `loveTheme` and `hateTheme` fields give you G2's NLP-extracted sentiment categories for every review — without reading thousands of pages manually.

### 📊 Product managers and researchers

Track how a product's ratings evolve over time. Sort by newest reviews, filter by minimum NPS, and pull structured data that feeds directly into your analysis pipeline.

### 💼 Sales and marketing teams

Identify switching patterns: `switchedFromOtherProduct` and `switchedReason` tell you exactly who moved to a product and why. Build battlecards from real user data at scale.

### 🏢 Investor due diligence teams

Cross-reference review volume, average rating, and rating trend for a batch of software companies. Scrape hundreds of products in one run using category browse mode.

### 🤖 AI / LLM training pipelines

G2 reviews are high-quality, domain-specific B2B text with structured metadata. Use them as training or evaluation data for sentiment classifiers, summarization models, or product comparison tools.

### 📈 Market researchers

Build category-level datasets. Browse any G2 category and get all top products with ratings and review counts — sorted by popularity — ready for benchmarking.

## ✅ Why use this scraper?

- **HTTP-only, no browser** — runs in 256 MB RAM, starts in seconds, costs far less than Playwright-based scrapers
- **No proxy needed** — G2's Elasticsearch API is publicly accessible
- **Cheaper than alternatives** — $0.005/review vs competitors charging $0.0065–$0.01/review (up to 50% savings)
- **29 fields per review** — including all rating dimensions, sentiment themes, and switching data that most scrapers miss
- **5M+ reviews available** — full `search_after` pagination handles products with tens of thousands of reviews
- **Multiple modes in one actor** — reviews, product search, and category browse without needing separate tools
- **Batch products** — pass multiple product URLs or slugs in one run and get all reviews combined

## 💰 How much does it cost to scrape G2 reviews?

This actor uses **pay-per-event** pricing — you only pay for what you actually scrape.

| Event | Price |
| --- | --- |
| Run started | $0.01 (one-time per run) |
| Review scraped | $0.005 per review |
| Product scraped | $0.003 per product |

**Example costs:**

| Task | Items | Cost |
| --- | --- | --- |
| 100 reviews for one product | 100 reviews | $0.01 + $0.50 = **$0.51** |
| 1,000 reviews for a product | 1,000 reviews | $0.01 + $5.00 = **$5.01** |
| Top 50 CRM products | 50 products | $0.01 + $0.15 = **$0.16** |
| Search results (25 products) | 25 products | $0.01 + $0.075 = **$0.085** |

**Compared to alternatives:**

- zen-studio G2 scraper: approx 30% more expensive per review
- powerai G2 scraper: approx 2× more expensive per review
- This actor: **$0.005/review** (FREE tier) — among the cheapest G2 scrapers on the Store

Tiered volume discounts are applied automatically as your Apify usage grows.

## 🚀 How to use it

### Step 1 — Choose your mode

Open the actor on [Apify Store](https://apify.com/automation-lab/g2-scraper) and select a scraping mode:

- **Product Reviews** — you want reviews for specific products
- **Product Search** — you want to find products by keyword
- **Category Browse** — you want to list top products in a G2 category

### Step 2 — Configure inputs

**For Product Reviews:**

1. Paste one or more G2 product URLs (e.g. `https://www.g2.com/products/slack/reviews`) or just slugs (`slack`, `hubspot`, `salesforce`)
2. Set `maxReviews` (default: 100, max: 50,000 per product)
3. Choose a sort order: Newest First, Most Helpful, Highest Rating, or Lowest Rating
4. Optionally set a minimum NPS rating (0–10) to filter out low-quality reviews

**For Product Search or Category Browse:**

1. Enter a keyword or category name in the `searchQuery` field
2. Set `maxProducts` (default: 25, max: 1,000)

### Step 3 — Run and export

Click **Start**. Results appear in the dataset in real time. Export as JSON, CSV, Excel, or XML from the Apify Console or via API.

## 📥 Input parameters

| Parameter | Type | Default | Used in mode |
| --- | --- | --- | --- |
| `mode` | select | `product_reviews` | All |
| `productUrls` | string list | `[slack reviews URL]` | `product_reviews` |
| `maxReviews` | integer | `100` | `product_reviews` |
| `sortReviews` | select | `newest` | `product_reviews` |
| `minRating` | integer (0–10) | — | `product_reviews` |
| `searchQuery` | string | — | `product_search`, `category_browse` |
| `maxProducts` | integer | `25` | `product_search`, `category_browse` |

**Sort options for reviews:**

- `newest` — Most recently submitted
- `helpful` — Most helpful votes first
- `rating_high` — Highest NPS score first
- `rating_low` — Lowest NPS score first (useful for finding pain points)

## 📤 Output fields

### Review fields (29 fields)

| Field | Description | Type |
| --- | --- | --- |
| `reviewId` | Unique G2 review ID | string |
| `title` | Review title | string |
| `nps` | NPS score (0–10) | number |
| `starRating` | Star rating (1–5, derived from NPS) | number |
| `reviewText` | Full review body text | string |
| `publishedAt` | Publication date (ISO 8601) | string |
| `submittedAt` | Submission date (ISO 8601) | string |
| `updatedAt` | Last updated date (ISO 8601) | string |
| `reviewerName` | Reviewer display name | string |
| `country` | Reviewer's country | string |
| `region` | Reviewer's region/state | string |
| `helpfulVotes` | Number of helpful votes received | number |
| `sourceType` | How the review was collected | string |
| `responseType` | Review format: `text` or `video` | string |
| `easeOfUse` | Ease of use rating (0–10) | number |
| `easeOfSetup` | Ease of setup rating (0–10) | number |
| `easeOfAdmin` | Ease of administration rating (0–10) | number |
| `qualityOfSupport` | Quality of support rating (0–10) | number |
| `meetsRequirements` | Meets requirements rating (0–10) | number |
| `loveTheme` | G2 NLP theme: what users love | string |
| `hateTheme` | G2 NLP theme: what users dislike | string |
| `switchedFromOtherProduct` | Product the reviewer switched from | string |
| `switchedReason` | Reason they switched | string |
| `companySegment` | Company size segment code | number |
| `industry` | Industry code | number |
| `productId` | Internal G2 product ID | number |
| `productName` | Product name | string |
| `productSlug` | Product URL slug | string |
| `url` | Direct link to the review on G2 | string |

**Example review output:**

```
{
  "reviewId": "9a2f3b1c-...",
  "title": "Best team messaging tool we've used",
  "nps": 9,
  "starRating": 5,
  "reviewText": "We've been using Slack for 3 years and it has transformed...",
  "publishedAt": "2025-11-14T00:00:00.000Z",
  "submittedAt": "2025-11-13T18:42:00.000Z",
  "reviewerName": "Sarah M.",
  "country": "United States",
  "helpfulVotes": 12,
  "easeOfUse": 9,
  "easeOfSetup": 8,
  "qualityOfSupport": 7,
  "meetsRequirements": 9,
  "loveTheme": "Ease of Use",
  "hateTheme": "Pricing",
  "switchedFromOtherProduct": "Microsoft Teams",
  "switchedReason": "Better integrations and UX",
  "productName": "Slack",
  "productSlug": "slack",
  "url": "https://www.g2.com/products/slack/reviews/9a2f3b1c-..."
}
```

### Product fields (15 fields)

| Field | Description | Type |
| --- | --- | --- |
| `productId` | Internal G2 product ID | string |
| `name` | Product name | string |
| `slug` | URL slug | string |
| `description` | Product description | string |
| `vendorName` | Vendor/company name | string |
| `productUrl` | Official product website | string |
| `type` | Product type classification | string |
| `categoryNames` | G2 categories the product belongs to | string[] |
| `reviewCount` | Total number of reviews | number |
| `averageRating` | Average rating (float) | number |
| `starRating` | Star rating (1–5) | number |
| `g2Rating` | G2's composite rating score | number |
| `thumbnailUrl` | Product thumbnail image URL | string |
| `faviconUrl` | Product favicon URL | string |
| `url` | G2 product page URL | string |

**Example product output:**

```
{
  "productId": "12345",
  "name": "HubSpot CRM",
  "slug": "hubspot",
  "description": "HubSpot CRM makes it easy to organize, track, and grow your pipeline.",
  "vendorName": "HubSpot",
  "productUrl": "https://www.hubspot.com",
  "categoryNames": ["CRM", "Marketing Automation"],
  "reviewCount": 12483,
  "averageRating": 4.4,
  "starRating": 4,
  "g2Rating": 4.4,
  "url": "https://www.g2.com/products/hubspot"
}
```

## 💡 Tips for best results

- **Batch multiple products in one run** — add all your product URLs to `productUrls` and they will be processed sequentially. One $0.01 start fee covers all products in the run.
- **Use `sortReviews: rating_low`** to collect negative reviews for pain point analysis without reading all reviews first.
- **Set `minRating`** to 7+ to filter for promoter reviews only (NPS ≥ 7 = passives and promoters on a 10-point scale).
- **Category browse returns products sorted by review count** — the most-reviewed products appear first, giving you the category leaders automatically.
- **Use slugs instead of full URLs** when scripting — `slack`, `hubspot`, `salesforce` are shorter and equally valid.
- **For products with 10K+ reviews**, the actor automatically switches to `search_after` cursor pagination for reliable retrieval beyond Elasticsearch's default 10K limit.
- **Combine modes** — run category browse first to find slugs, then run product reviews on the top 5 products.

## 🔌 Integrations

### Google Sheets auto-export

Connect the actor to a Google Sheets integration via Apify's built-in webhooks. Every run automatically appends new reviews to your spreadsheet — useful for tracking new reviews weekly on a schedule.

### Slack / Teams alerts for new negative reviews

Set up a scheduled run that pulls the last 7 days of reviews sorted by `rating_low`, filters for NPS < 5, and posts a summary to your Slack channel via a webhook integration.

### Make / Zapier pipeline for CRM enrichment

Trigger the actor via Apify's API from a Make scenario. When a new competitor deal enters your CRM, automatically fetch 100 reviews of that competitor's G2 product and add them as deal notes.

### Competitive intelligence dashboard

Schedule weekly runs for 10–20 competitor products. Store results in a dataset, connect to Google Looker Studio or Retool, and track rating trends, sentiment themes, and review volumes over time.

### Vector database for RAG

Export reviews as JSON, chunk by `reviewText`, and load into a vector database (Pinecone, Weaviate, Qdrant). Build a product intelligence chatbot that answers questions by retrieving relevant user feedback.

## 🖥️ API usage

Run this actor programmatically from any language using the Apify API.

### Node.js (Apify client)

```
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_APIFY_TOKEN' });

const run = await client.actor('automation-lab/g2-scraper').call({
    mode: 'product_reviews',
    productUrls: ['https://www.g2.com/products/slack/reviews'],
    maxReviews: 500,
    sortReviews: 'newest',
});

// Reviews and products are stored in separate named datasets
const reviewsDatasetId = run.storageIds.datasets.reviews;
const { items: reviews } = await client.dataset(reviewsDatasetId).listItems();
console.log(reviews);
```

### Python (Apify client)

```
from apify_client import ApifyClient

client = ApifyClient(token="YOUR_APIFY_TOKEN")

run = client.actor("automation-lab/g2-scraper").call(run_input={
    "mode": "product_reviews",
    "productUrls": ["https://www.g2.com/products/hubspot/reviews"],
    "maxReviews": 1000,
    "sortReviews": "helpful",
})

# Reviews are in the named "reviews" dataset
reviews_dataset_id = run["storageIds"]["datasets"]["reviews"]
for item in client.dataset(reviews_dataset_id).iterate_items():
    print(item["title"], item["nps"])
```

### cURL

```
curl -X POST \
  "https://api.apify.com/v2/acts/automation-lab~g2-scraper/runs?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "mode": "category_browse",
    "searchQuery": "CRM",
    "maxProducts": 50
  }'
```

Fetch results once the run completes:

```
$curl "https://api.apify.com/v2/datasets/{DATASET_ID}/items?token=YOUR_APIFY_TOKEN&format=json"
```

## 🤖 Using with Claude via MCP (Model Context Protocol)

This actor is compatible with the Apify MCP server, which lets you run it directly from Claude without writing any code.

### Setup — Claude Desktop

1. Install the [Apify MCP server](https://apify.com/apify/actors-mcp-server)
2. Add your Apify token to Claude Desktop's MCP config
3. Ask Claude to run the G2 scraper naturally

### Setup — Claude Code (CLI)

Add the Apify MCP server to your Claude Code config:

```
{
  "mcpServers": {
    "apify": {
      "command": "npx",
      "args": ["-y", "@apify/actors-mcp-server"],
      "env": { "APIFY_TOKEN": "YOUR_APIFY_TOKEN" }
    }
  }
}
```

### Example prompts for Claude

> "Run the automation-lab/g2-scraper actor to get the 200 most helpful reviews for Salesforce on G2, then summarize the top 5 complaints."

> "Use the G2 scraper to find the top 20 products in the 'Project Management' category and show me a table with their names, review counts, and average ratings."

> "Scrape 500 Slack reviews sorted by lowest rating and identify the most common pain points mentioned in the hateTheme field."

> "Fetch reviews for both HubSpot and Pipedrive, then compare their average easeOfUse and qualityOfSupport scores."

Claude will call the actor, wait for results, and process the dataset automatically — no code required.

## ⚖️ Legality — Is it legal to scrape G2?

G2's reviews are publicly accessible without authentication. This actor only requests data that any anonymous visitor can see in their browser — the same data G2 exposes through its own search API.

Key points:

- **No login required** — the actor does not bypass any authentication or access controls
- **Public data only** — all scraped content is visible to anyone visiting G2.com
- **Polite scraping** — the actor adds a 200ms delay between requests and processes 100 items per page
- **No PII beyond public reviewer names** — reviewer job titles, profile URLs, and company names are not available through the API and are not scraped

You are responsible for ensuring your use of scraped data complies with applicable laws in your jurisdiction (GDPR, CCPA, etc.) and G2's Terms of Service. This actor is intended for legitimate business intelligence, research, and competitive analysis use cases. Do not use scraped data to contact, profile, or target individual reviewers.

## 🔧 Troubleshooting

**Run succeeded but dataset is empty** — Verify your product slug or URL is correct. Open the G2 product page and copy the slug from the URL path (e.g. `/products/salesforce-crm/reviews` → slug is `salesforce-crm`). Do not include the `/reviews` suffix when using a bare slug.

**Fewer reviews than the product page shows** — G2's public search API only exposes reviews that have passed moderation. Draft or removed reviews are not included. Also check your `minRating` filter — it will silently exclude reviews below the threshold.

**`chargedEventCounts` shows `review:0`** — This means no reviews matched your filters. Try removing `minRating` (defaults to 1, which includes all) and re-running. Also confirm the product has publicly visible reviews by browsing its G2 page.

**Charged `review:N` events but reviews dataset is empty after run** — This is a transient platform state: the dataset upload completed but the storage URL query returned stale results. Wait 30–60 seconds and fetch the dataset again via the API URL shown in the actor output.

**Run failed with `ETIMEDOUT` or `EAI_AGAIN`** — G2's search API is temporarily unreachable. Retry the run — the actor uses exponential backoff on retries, but persistent network failures will abort the run cleanly.

## ❓ FAQ

**Q: Can I scrape reviews for multiple products at once?**
Yes. Add multiple URLs or slugs to the `productUrls` list. The actor processes them sequentially in a single run, so you pay one $0.01 start fee for all products combined.

**Q: What's the maximum number of reviews I can get?**
Up to 50,000 per product per run. For products with more than 10,000 reviews, the actor uses `search_after` cursor pagination to reliably retrieve all results beyond Elasticsearch's standard 10K limit.

**Q: Can I get pros and cons separately?**
No. G2's API returns review text as a single combined blob (`reviewText`). There are no separate `pros` and `cons` fields in the underlying data. Use the `loveTheme` and `hateTheme` fields instead — these are G2's NLP-extracted sentiment themes for each review.

**Q: Does this scraper need a proxy?**
No. G2's Elasticsearch API (`search.g2.com`) is publicly accessible without authentication or IP restrictions. No residential or datacenter proxy is needed.

**Q: Can I get reviewer job title, company, or profile URL?**
No. These fields are not available through G2's public search API. The actor only returns fields that the API exposes: reviewer name, country, region, and company segment code (an integer, not a company name string).

**Q: The run returned 0 results for my product. What should I check?**
First verify the product slug: go to the product's G2 page and copy the slug from the URL (`/products/YOUR-SLUG/reviews`). Make sure you're not including the `/reviews` suffix when entering a bare slug. If the product has no approved public reviews, the run will return an empty dataset — this is expected behavior, not an error.

**Q: I'm getting fewer reviews than expected. Why?**
The `minRating` filter reduces results to only reviews at or above your NPS threshold. Also, `maxReviews` is a per-product limit. If you're scraping multiple products, the total will be up to `maxReviews × number of products`.

**Q: What does `companySegment` mean?**
It's an integer code from G2's internal classification (e.g. 1 = small business, 2 = mid-market, 3 = enterprise). G2 does not expose the string label through the search API.

## 🔗 Related scrapers

These actors from the same author cover adjacent data sources:

- [**Capterra Scraper**](https://apify.com/automation-lab/capterra-scraper) — reviews and product data from Capterra, G2's main competitor
- [**Trustpilot Scraper**](https://apify.com/automation-lab/trustpilot-scraper) — consumer reviews from Trustpilot across all industries
- [**Google Maps Reviews Scraper**](https://apify.com/automation-lab/google-maps-reviews-scraper) — reviews and ratings from Google Maps business listings

---

Built and maintained by [automation-lab](https://apify.com/automation-lab) on the Apify platform.