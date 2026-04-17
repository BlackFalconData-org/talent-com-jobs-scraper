# Talent.com Jobs Scraper - Structured Listings

Extract structured data from [talent.com](https://talent.com) — structured job listings from talent.com across 11 markets (US, CA, UK, DE, FR, NL, BE, CH, AT, NO) with O*NET classification, geo, salary, publisher provenance, and incremental change detection.

**[Talent.com Jobs Scraper - Structured Listings on Apify →](https://apify.com/blackfalcondata/talent-com-jobs-scraper)**

---

## Key features

**Search with filters** — Search by keyword and location. Filter by country, job type, remote filter, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, direct apply URLs for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from talent.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from talent.com.

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

---

## Related products by Black Falcon Data

- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Indeed Job Scraper](https://github.com/BlackFalconData-org/indeed-job-scraper) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://github.com/BlackFalconData-org/glassdoor-job-scraper) — Glassdoor listings with company ratings

---

*Last updated: 2026 04*
