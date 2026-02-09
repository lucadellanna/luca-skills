---
name: download-earnings
description: Download the last 4 quarterly earnings reports for a company from SEC EDGAR. Use when "download earnings", "get earnings reports", "fetch quarterly filings".
version: 2026-02-10
---

Download the most recent quarterly earnings filings (10-Q) from SEC EDGAR and save them locally. See `criteria.md` for filing selection logic and `template.md` for output format.

### 1. Get company

Ask the user for a company name or ticker symbol.

### 2. Resolve ticker to CIK

Fetch `https://www.sec.gov/files/company_tickers.json` to find the company's CIK number.

- Search by ticker (exact match, case-insensitive) first.
- If no ticker match, search by company name (partial match).
- If multiple matches, present the options and ask the user to confirm.
- If no match, tell the user the company wasn't found on EDGAR and stop.

Zero-pad the CIK to 10 digits for the next step (e.g. `320193` → `0000320193`).

Include a User-Agent header on all SEC requests: `luca-skills/1.0 (skills@example.com)`.

### 3. Fetch filing history

Fetch `https://data.sec.gov/submissions/CIK{padded_cik}.json`.

The response contains a `filings.recent` object with arrays: `form`, `filingDate`, `accessionNumber`, `primaryDocument`, `primaryDocDescription`.

Filter and select filings per `criteria.md`.

### 4. Download filings

Create the output directory: `./earnings/{TICKER}/`

For each selected filing:
- Build the document URL: `https://www.sec.gov/Archives/edgar/data/{cik}/{accession-number-no-dashes}/{primaryDocument}`
- Download the document using curl or equivalent with the User-Agent header.
- Save as `./earnings/{TICKER}/{filingDate}_{form}.htm` (or appropriate extension).
- Verify the file is non-empty and not an error page.

Respect EDGAR's rate limit — wait briefly between requests if downloading multiple files.

### 5. Present summary

Use the format from `template.md` to show the user what was downloaded.
