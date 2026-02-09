# Filing selection criteria

## Which filings to download

- Prefer **10-Q** filings (quarterly reports for US-listed companies).
- If the company has no 10-Q filings, check for **20-F** (annual report for foreign filers) or **6-K** (interim report for foreign filers). Offer these as alternatives and explain the difference.
- **"Last 4"** means the 4 most recent filings by filing date.
- If fewer than 4 are available, download what exists and tell the user.

## Which document within a filing

- Each filing contains multiple documents. Use the `primaryDocument` field from the EDGAR submissions API — this is the main report.
- If `primaryDocument` is missing or ambiguous, prefer the first `.htm` file in the filing index.

## Avoiding re-downloads

- Before downloading a filing, check if a file with the same name already exists in the output directory.
- If it exists and is non-empty, skip re-downloading it.
- Tell the user which filings were skipped: "2 filings already downloaded, 2 new filings downloaded."

## Verification

- Each downloaded file should be non-empty.
- If a downloaded file is very small (< 1 KB) or contains an error message instead of a filing, flag it and tell the user.
- If the most recent filing is older than 6 months, note that the company may not be filing regularly.
