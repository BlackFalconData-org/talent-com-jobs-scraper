# Talent.com Jobs Scraper - Structured Listings

Extract structured data from [talent.com](https://talent.com) — structured job listings from talent.com across 11 markets (US, CA, UK, DE, FR, NL, BE, CH, AT, NO) with O*NET classification, geo, salary, publisher provenance, and incremental change detection.

**[Talent.com Jobs Scraper - Structured Listings on Apify →](https://apify.com/blackfalcondata/talent-com-jobs-scraper?fpr=1h3gvi)**


## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.


---

## Key features




**Search with filters** — Search by keyword and location. Filter by 🌍 country, 💼 job type, remote filter, and more.

**Multiple input modes** — search query or job urls (direct detail fetch). Switch modes without re-scraping.

**Direct URL mode** — Paste a list of listing URLs and fetch each one directly. Skips search — ideal for monitoring known IDs.

**Detail enrichment** — Fetch full job descriptions, salary data, contact information for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 1.000). Set to 0 for the full catalog.

**Proxy support** — Route traffic through Apify Proxy or your own proxy group to avoid regional blocks and rate limits.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases




**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from talent.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from talent.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on talent.com to inform pricing decisions, hiring plans, or candidate negotiations.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "software engineer",
  "country": "US",
  "location": "New York",
  "maxResults": 25,
  "maxPages": 3,
  "includeDetails": false
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `mode` | enum | `"search"` | Input mode. "search" runs a keyword search; "jobUrls" fetches each supplied detail URL directly. |
| `jobUrls` | array | — | List of talent.com detail URLs (e.g. https://www.talent.com/view?id=abc123def456). Used when mode = "jobUrls". Supports all 11 country subdomains. |
| `query` | string | — | Job search keywords. Use JSON array for multi-query (e.g. ["software engineer", "data scientist"]). |
| `country` | enum | `"US"` | Which talent.com market to search. Each country maps to a country-specific subdomain. |
| `location` | string | — | City, state, or region. Use JSON array for multi-location (e.g. ["New York", "Remote"]). |
| `startUrls` | array | — | Direct search or job detail URLs. Overrides query+country when provided. |
| `maxResults` | integer | `25` | Maximum total job listings to return (0 = unlimited). |
| `maxPages` | integer | `5` | Maximum SERP pages to scrape per search source. |
| `maxConcurrency` | integer | `3` | Parallel SERP page fetch concurrency. Page 1 is fetched sequentially; pages 2..N run in parallel at this concurrency. Benchmark-recommended: 3. |
| `daysOld` | integer | — | Only emit jobs posted within the last N days. Leave empty to include all. |
| `jobType` | enum | — | Filter by employment type. |
| `remoteFilter` | enum | — | Limit results to remote or hybrid jobs. |
| `includeDetails` | boolean | `false` | Fetch each job's detail page for full description when SERP description is a ref placeholder. |
| `descriptionMaxLength` | integer | `0` | Truncate description to this many characters. 0 = no truncation. |
| `compact` | boolean | `false` | Output only core fields (for AI-agent/MCP workflows). |
| `incrementalMode` | boolean | `false` | Compare against previous run state. Requires stateKey. |
| `stateKey` | string | — | Stable identifier for the tracked search universe (e.g. "us-software-nyc"). |
| `emitUnchanged` | boolean | `false` | When incremental, also emit records that haven't changed. |
| `emitExpired` | boolean | `false` | When incremental, also emit records no longer found. |
| `skipReposts` | boolean | `false` | When incremental, skip jobs whose content matches an expired job from a prior run (cross-run repost detection). |
| `proxyConfiguration` | object | `{"useApifyProxy":true}` | Network routing configuration for outbound requests. |

---

## FAQ

<!-- WRITE: 4-6 Q&A pairs relevant to this product -->

**Is it legal to scrape talent.com?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

<!-- WRITE: 4-6 honest limitations -->

- <!-- WRITE: limitation 1 -->
- <!-- WRITE: limitation 2 -->


## Output fields

Every listing returns the same 60-field schema. Missing values are `null` — never omitted.

- `jobId`
- `jobKey`
- `internalId`
- `title`
- `titleRaw`
- `company`
- `companyRaw`
- `locationText`
- `locationRaw`
- `city`
- `region`
- `country`
- `lat`
- `lng`
- `isRemote`
- `jobType`
- `onetCode`
- `onetTitle`
- `language`
- `salaryMin`
- `salaryMax`
- `salaryAvg`
- `salaryPeriod`
- `salaryText`
- `postedAt`
- `expiresAt`
- `rediscoveredAt`
- `applyType`
- `applyUrl`
- `canonicalUrl`
- `feedSource`
- `feedProvider`
- `campaignId`
- `isPpc`
- `ppcValue`
- `googleIndexed`
- `description`
- `descriptionHtml`
- `descriptionMarkdown`
- `descriptionLength`
- `snippet`
- `extractedEmails`
- `sourceDomain`
- `sourceCountry`
- `searchQuery`
- `searchUrl`
- `isSponsored`
- `fetchedAt`
- `detailFetched`
- `contentHash`
- `changeType`
- `trackedHash`
- `firstSeenAt`
- `lastSeenAt`
- `previousSeenAt`
- `expiredAt`
- `stateKey`
- `isRepost`
- `repostOfId`
- `repostDetectedAt`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "b6a6882122e2b25df4dff1fc01f9f75267395c832376d42c4f70257d623c9735",
  "jobKey": "196d185eb971",
  "internalId": "578673845954158641",
  "title": "Software Engineer",
  "titleRaw": "Software Engineer",
  "company": "TradeJobsWorkforce",
  "companyRaw": "TradeJobsWorkforce",
  "locationText": "10163 New York, NY, US",
  "locationRaw": "10163 New York, NY, US",
  "city": "New York",
  "region": "New York",
  "country": "us"
}
```

*Truncated — full records contain 60 fields. See Output fields for the complete schema.*


**[Try Talent.com Jobs Scraper - Structured Listings now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/talent-com-jobs-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.00005 |
| Result | $0.0015 |

See the [actor on Apify](https://apify.com/blackfalcondata/talent-com-jobs-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data




- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [LinkedIn Jobs Scraper](https://apify.com/blackfalcondata/linkedin-jobs-scraper?fpr=1h3gvi) — World's largest professional network — global job listings, no login required
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---

---

*Last updated: 2026 04*
