# Specs

One folder per doc type. Each holds `layout/` (client spec docs), `samples/` (raw EDI + matching flat files), `mapping.md` (field → X12 → Orderful JSON, with status) and `questions.md`.

Approach: Concurrent reviews specs and samples offline, drafts maps with Claude, tests, and brings Shehadey only the questions that don't make sense. The client's mapping templates are the spec (no formal ERMS spec exists).

## Status (2026-10-21)
| Doc | Direction | Mapped | Notes |
|---|---|---|---|
| 850 | Costco X12 → ERMS pipe file | 89% | Needs a Costco raw 850 + matching flat file |
| 810 | ERMS file → X12 810 | 86% | Sample is Dollar General; need a Costco pair |
| 856 | ERMS file → X12 856 | 75% | Costco needs SSCC; ship-from/carrier/BOL sources missing |

Full detail: `outputs/2026-10-21-costco-mapping-workbook.xlsx`.

## What's here
- `850/layout/` — client 850 research doc; `park-city/` layouts (Costco 50A, Walmart 60A, Pitco), sample PDFs, Costco PO number calculation
- `850/samples/pipe-delimited/` — 59 production NCS/NCW flat files (2 Costco)
- `850/samples/park-city-fixed-width/` — PRODUCERS_ORDERS files (Park City; not being mapped)
- `850/samples/raw-x12/` — 6 raw Walmart/Sam's 850s
- `810/` — template, open questions, live 810 sample
- `856/` — template, open questions, UW (real, unredacted) and RA samples
