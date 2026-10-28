# 2026-10-27 — Email from Adam (Shehadey): "Costco uploaded"

Source: email to Mark, 10/27. Files: `2026-10-27-costco-erms/Costco ERMS/` (unzipped from `2026-10-27-costco-erms.zip`, uploaded by Adam to the Orderful UI).

## What's in the zip
- `850/850_Costco_Umpqua_FlatFile_vs_X12.txt` — PO 012871005279: ERMS flat file vs raw X12 vs JSON, with field correspondence. Confirms HDR 11 = DTM*002 (requested delivery).
- `850_to_810_Umpqua_Costco_Match.txt` — 850 flat → 810 flat → X12 → JSON (Umpqua).
- `810_ParkCity_Costco_FlatFile_vs_X12.txt` and `810_ParkCity_Costco_Store423_FlatFile_vs_X12.txt` — Park City 810 flat file vs X12.
- `810/` — mapping template plus raw ERMS 810 flat files (Umpqua `EDI_OUT.UCOSTCO…`, Park City `EDI_OUT.PCGCOSTCO…`).
- `856/` — Fresno WMS 856 mapping doc, sample `EDI_OUT.PCGCOSTCO….856` files, internal BOL reference.
- `Park City Documentation Files/` — Park City inbound layouts (Costco, Walmart, Pitco), sample data, Costco PO number calculation.
- `costco_orderful_Flow and Tasks.xlsx` — flow diagram and task list (Umpqua and Park City plants).

## Points from the email
- Costco vendor numbers: Umpqua Dairy Products Co 0009125500; Producers Dairy Foods (Fresno) 0003025500.
- Aptean shows Umpqua going out to COSTCOEDIUSA (COSTCO SPS) and Park City going out to 103391843PCG (PCG – COSTCO); may be two different VANs (to clarify with Narvel).
- ERMS 810 flat files are named uniquely by plant: Umpqua `EDI_OUT.UCOSTCO<yymmddhhmm>`, Park City `EDI_OUT.PCGCOSTCO<yymmddhhmm>`.
