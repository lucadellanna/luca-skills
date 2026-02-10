---
name: download-earnings
description: Download the last 4 quarterly earnings reports for a company from SEC EDGAR. Use when "download earnings", "get earnings reports", "fetch quarterly filings".
last-updated: 2026-02-09T14:56:55Z
---

Download the most recent quarterly earnings filings (10-Q) from SEC EDGAR and save them locally. See `criteria.md` for filing selection logic and `template.md` for output format.

### 1. Get company

Ask the user for a company name or ticker symbol.

### 2. Resolve ticker to CIK

The SEC requires a contact name and email on all requests to their data service.

Check `.skillstate.json` for a saved `sec_contact` field. If found, use it. If `.skillstate.json` is missing or unparseable, treat it as empty and create/repair it (preserving any existing standard fields if present).

If no `sec_contact` is saved, ask the user:

> The SEC requires a name and email address on all requests to their filing database. This is sent directly to sec.gov with each request. If you want, I can save it locally on your machine so you won’t be asked again. Example: `Jane Smith (jane@example.com)`. What should I use?

If the user wants it saved, store their response in `.skillstate.json` under the `sec_contact` field so they won't be asked again. If they prefer not to save it, use it only for this run.

Use the `sec_contact` value as the `User-Agent` header on every SEC request in this run.

Fetch `https://www.sec.gov/files/company_tickers.json` to find the company's CIK number.

- Search by ticker (exact match, case-insensitive) first.
- If no ticker match, search by company name (partial match).
- If multiple matches, present the options and ask the user to confirm.
- If no match, tell the user the company wasn't found on EDGAR and stop.

Keep both forms of the CIK:
- `cik` = the numeric CIK with no leading zeros (e.g. `320193`) — use this for EDGAR Archives URLs.
- `padded_cik` = the 10-digit, zero-padded CIK (e.g. `0000320193`) — use this for the submissions API URL below.

### 3. Fetch filing history

Fetch `https://data.sec.gov/submissions/CIK{padded_cik}.json` (with the same User-Agent).

The response contains a `filings.recent` object with arrays: `form`, `filingDate`, `accessionNumber`, `primaryDocument`, `primaryDocDescription`.

It may also include `reportDate` (the period of report). Capture it when present for the output summary.

Filter and select filings per `criteria.md`.

### 4. Download filings

Create the output directory: `./earning-reports/{TICKER}/`

For each selected filing:
- Compute `accession_number_no_dashes` by removing dashes from `accessionNumber`.
- Build the document URL: `https://www.sec.gov/Archives/edgar/data/{cik}/{accession_number_no_dashes}/{primaryDocument}`
- If `primaryDocument` is missing or empty, fetch the filing directory `index.json` and select the first HTML report per `criteria.md`.
- Before downloading, check whether the destination file already exists and is non-empty. If so, skip it and note it in the summary.
- Download the document using curl or equivalent with the User-Agent header.
- Create `safe_form` for filenames by replacing `/` with `-` (e.g. `10-Q/A` → `10-Q-A`) and trimming spaces.
- Save as `./earning-reports/{TICKER}/{filingDate}_{safe_form}_{accession_number_no_dashes}.html` (or appropriate extension).
- Verify the file is non-empty and not an error page.

Respect EDGAR's rate limits — wait briefly between requests if downloading multiple files.

If any SEC request returns a rate limit or transient error (e.g. 429/503), wait and retry a few times with increasing delays. If it still fails, stop and explain what happened.

### 5. Present summary

Use the format from `template.md` to show the user what was downloaded.
