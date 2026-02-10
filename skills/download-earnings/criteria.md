# Filing selection criteria

## Which filings to download

- Prefer **10-Q** filings (quarterly reports for US-listed companies).
- If the company has no 10-Q filings, check for **20-F** (annual report for foreign filers) or **6-K** (interim report for foreign filers). Offer these as alternatives and explain the difference.
- **"Last 4"** means the 4 most recent filings by filing date.
- If fewer than 4 are available, download what exists and tell the user.

## Which document within a filing

- Each filing contains multiple documents. Use the `primaryDocument` field from the EDGAR submissions API — this is the main report.
- If `primaryDocument` is missing or ambiguous, fetch the filing directory index (`https://www.sec.gov/Archives/edgar/data/{cik}/{accession_number_no_dashes}/index.json`) and select:
  - The first file ending in `.htm` or `.html`, excluding obvious index pages like `*-index.html`.
  - If no HTML files exist, fall back to the first non-empty file in the index and warn the user.

## Avoiding re-downloads

- Before downloading a filing, check if a file with the same name already exists in the output directory.
- If it exists and is non-empty, skip re-downloading it.
- Tell the user which filings were skipped: "2 filings already downloaded, 2 new filings downloaded."

## Verification

- Each downloaded file should be non-empty.
- If a downloaded file is very small (< 1 KB) or contains an error message instead of a filing, flag it and tell the user.
- If the most recent filing is older than 6 months, note that the company may not be filing regularly.

## SEC API health check

This skill depends on SEC EDGAR's public API. If any of the following happen, stop and tell the user clearly — do not silently proceed with bad data:
- The company tickers endpoint returns unexpected JSON structure (missing expected fields like `cik_str`, `ticker`, `title`).
- The submissions endpoint returns unexpected JSON structure (missing `filings.recent` or its expected arrays).
- Multiple consecutive downloads return empty files or error pages.

Suggest the user check whether SEC EDGAR is experiencing issues or whether the API format has changed. Link them to https://www.sec.gov/edgar/searchedgar/companysearch for manual access as a fallback.
