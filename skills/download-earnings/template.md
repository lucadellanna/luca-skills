# Output format

After downloading, present this summary to the user:

---

## Earnings filings downloaded for {COMPANY} ({TICKER})

| Period | Filed | Form | File |
|--------|-------|------|------|
| {period_of_report} | {filing_date} | {form_type} | `earnings/{TICKER}/{filename}` |
| ... | ... | ... | ... |

Saved to: `./earnings/{TICKER}/`
{N} filing(s) downloaded.

---

If any filings couldn't be downloaded, add a note explaining what went wrong and what the user can do (e.g. check their internet connection, try again later, or visit EDGAR directly).

If the company is a foreign filer and 20-F/6-K filings were downloaded instead of 10-Q, note this clearly:

> Note: {COMPANY} is a foreign filer and does not file 10-Q reports. The filings above are {form_type} reports, which serve a similar purpose.
