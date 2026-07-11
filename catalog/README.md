# The Catalog

The Dex is only as honest as its catalog. This directory is the paper trail:
every aircraft candidate that has been considered for the collectible catalog,
with a sourced, written-down decision for each one.

## Files

| File | What it is |
| --- | --- |
| [`aircraft_variant_catalog_review.csv`](aircraft_variant_catalog_review.csv) | The review ledger: 171 candidate rows, each with ICAO type codes, sources, a confidence call, a decision and the reason for it |
| [`aircraft_variant_catalog_review.md`](aircraft_variant_catalog_review.md) | The narrative companion to the CSV: how the review passes ran and what the columns mean |
| [`CATALOG_REVIEW_POLICY.md`](CATALOG_REVIEW_POLICY.md) | The law. What may enter the catalog, at what granularity, and what evidence counts |
| [`CATALOG_POLICY_AMENDMENT_PROPOSAL.md`](CATALOG_POLICY_AMENDMENT_PROPOSAL.md) | Ratified amendments, including Amendment B, the legacy/rarity boundary ("legacy answers *why can't you catch this?*; rarity answers *how impressive is it that you caught this?*") |

## The rules that matter

- **Collection is keyed on ICAO hex.** You collect physical airframes, not
  registrations that change hands next year.
- **Imported metadata is evidence, never catalog authority.** An upstream
  database calling something a "737-800" doesn't put it in the Dex; a
  reviewed decision does.
- **Granularity is a decision, not an accident.** Some families collect at
  series level, some at variant level; each row records why.
- As of July 2026 the live catalog stands at **103 collectible types and 18
  legacy types**, across 65 families and 23 manufacturers.

## Suggesting a change

Catalog suggestions are welcome: open an
[issue](https://github.com/catchfleet/catchfleet/issues) with your sources. Every
change follows the review policy: sourced, decided, documented. "It would be
cool to catch X" is a fine starting point, but the row that lands in the CSV
will have evidence behind it.
