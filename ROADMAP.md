# POV Preservation — Vendor Supply Order Form

Live form for field crews to request supplies (MFS Supply + Home Guard) that POV
orders and ships to them. Built as a single self-contained `index.html`, hosted on
GitHub Pages, with orders logged to a Google Sheet via Apps Script.

---

## Current state (live)

- **Catalog** of common property-preservation supplies from MFS + Home Guard, grouped
  by category, with per-item icons (and an `img:` hook for real product photos).
- **Live totals** that update as quantities change, with a per-supplier free-shipping
  meter ($300 threshold).
- **Key codes on locks** — each lock item supports *multiple* codes, each with its own
  quantity (e.g. 12 @ 35241 + 12 @ 44535). A code is required before an order can send.
- **Ship-to capture** (vendor name, phone, email, address, optional job reference).
- **Bill-back / deduction** — notice on the form + required authorization checkbox at
  checkout; the authorization is recorded on every logged order.
- **Submit → Google Sheet** logging, with email / copy / print as backups. Each order
  gets a reference like `POV-YYYYMMDD-HHMMSS`.

### Where to edit things (all in `index.html`)
- `CONFIG` block (top of the script): `logUrl`, `orderEmail`, company name,
  free-ship threshold, and the bill-back wording (`deductNotice`, `deductConfirm`).
- `CATALOG` array: prices, items, `keyed:true` flag, and `img:"file.jpg"` photo hooks.
- `KEY_CODES` array: the standard REO key codes offered in the lock dropdowns.

---

## Planned enhancements (backlog)

### 1. Tarp size selector
Add a size choice to the tarp line (dropdown or short text), mirroring the key-code
pattern. Selected size flows into the order text and the Sheet log.
- Effort: small.

### 2. Vendor notes / catch-all field
A free-text box near the bottom: "Anything else? (items not listed, special
instructions, misc info)." Logged as its own field/column so it's easy to scan.
- Effort: small.
- Captures everything a fixed catalog can't.

### 3. Direct links to suppliers ("order it yourself")
Links to mfssupply.com and homeguardsupply.com so crews can self-serve later.
- Effort: small.
- Open question: bill-back routes orders through POV on purpose — decide whether
  self-ordering is offered to everyone or only certain vendors, and where the links
  live (footer vs. a dedicated "supplier sites" line).

### 4. Supplier-ready email format (highest value)
When an order lands in POV's inbox, format it so each supplier's portion is a clean
block that can be forwarded straight to the MFS / Home Guard contact in *their*
preferred ordering format — no retyping.
- Effort: medium.
- Needs first: a sample of how POV currently orders from each supplier (do they want
  SKU + qty + key code? a PO/account number? ship-to repeated? subject line format?).
  Match each contact's format exactly.

---

## How to resume
Point Claude at the live form or this repo and name the item (e.g. "let's do the tarp
size selector"). For #4, bring a sample order in each supplier's format.

## Deploy / update reminder
Edit `index.html` in the repo (or replace the whole file) → **Commit changes** →
GitHub Pages redeploys in ~1 minute → hard-refresh the live link (Cmd+Shift+R).
Confirm `logUrl` and `orderEmail` are still set in `CONFIG` after any full-file replace.
