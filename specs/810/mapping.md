# 810 Invoice — ERMS flat file → X12 810 (outbound)

Direction: ERMS writes the .810 flat file → BizLink → SFTP → Tray maps to Orderful's 810 → Orderful sends X12 to Costco.

Scope: Costco invoices for **Umpqua via SPS**. The flat file layout is the same for every customer (per client); Costco-specific requirements come from Costco's 810 guideline in Orderful.

Evidence used: client's 810 mapping template + open questions; live 6-invoice sample (EDITESTredacted.810, a Dollar General example — not Costco). Totals were checked: LDT units shipped sum to TOT field 3 and extended amounts sum to TOT field 5.

Still needed: a Costco 810 flat file with its X12 output (from Aptean), Costco's 810 guideline, the 'IN 810 file layout' doc the client's template refers to, and ERMS note-table export for allowance rate bases.


**Coverage:** 42 of 49 rows mapped (86%) — 24 verified, 18 inferred, 7 open. Inferred rows need one paired Costco example to confirm.

Legend: ✅ Verified against real paired data or client-confirmed · 🟡 Inferred from patterns/client template · ❓ Open question

| Record | Field | Meaning | X12 element | Orderful JSON | Example | Status | Notes |
|---|---|---|---|---|---|---|---|
| File | — | Batch: many invoices per file, each HDR … TOT | One ST/SE (810) per invoice | — | EDITESTredacted.810 has 6 invoices | ✅ Verified | Confirmed in client's 810 doc. |
| HDR | 4 | Ticket / invoice number | BIG02 | invoiceNumber | 59697972 | ✅ Verified | Client doc ✅. |
| HDR | 6 | PO number | BIG04 | purchaseOrderNumber | 2D5J93 | ✅ Verified | Client doc ✅. |
| HDR | 7 | Order / PO date | BIG03 | purchaseOrderDate | 20260730 | ✅ Verified | Client doc ✅. |
| HDR | 8 | Delivery date (used as invoice date) | BIG01 (also DTM*011 ship date) | invoiceDate | 20260809 | ✅ Verified | Client doc ✅. Confirm Costco wants delivery date as invoice date. |
| HDR | 2–3 | File date / time | ISA/GS (generated) | — | 20260810 / 172112 | 🟡 Inferred |  |
| HDR | 14 | Unknown reference | REF? (BOL / ship ticket) | references | 48085467325 | ❓ Open | What is this number? |
| HDR | 15 | Date | DTM*011 (shipped) | dates | 20260809 | 🟡 Inferred |  |
| HDR | 18 | Code '6' | ? | — | 6 | ❓ Open |  |
| HDR | 19 | Date | ITD04 (discount due date)? | termsOfSale | 20260809 | ❓ Open |  |
| HDR | 20 | Terms discount percent | ITD03 | termsOfSale | [TermsDiscountPct] | ✅ Verified | Client doc ✅ (redacted in sample). |
| HDR | 21 | Terms discount amount | ITD08 | termsOfSale | [TermsDiscountAmt] | 🟡 Inferred |  |
| HDR | 27 | Debit/credit indicator | BIG07 (CR = credit memo) | invoiceType | (blank) | ✅ Verified | Blank = invoice, T = credit memo (client doc). |
| HDR | 28 | Code '1' | ? | — | 1 | ❓ Open |  |
| HDR | 30 | Date | ITD06 (net due date)? | termsOfSale | 20260823 | 🟡 Inferred | Same as field 36 in sample. |
| HDR | 32 | Terms discount days | ITD05 | termsOfSale | 0 | ✅ Verified | Client doc ✅. |
| HDR | 34 | Terms net days | ITD07 | termsOfSale | 14 | 🟡 Inferred |  |
| HDR | 35 | Terms description | ITD12 | termsOfSale.description | Due 14 Days | ✅ Verified | Client doc ✅. |
| HDR | 36 | Terms net due date | ITD06 | termsOfSale | 20260823 | 🟡 Inferred |  |
| — | — | Currency | CUR*SE*USD (hardcode) | currency USD | — | ✅ Verified | Domestic only (client doc). |
| HST | 2 | Ship-to location / store number | N1*ST N104 (qualifier 92) | parties.shipTo.identificationCode | 08216001 | 🟡 Inferred | Which ID Costco expects (92 vs UL/GLN) comes from Costco's guideline. |
| HST | 3 | Customer DUNS | N1 N104 (qualifier 1) or REF | parties.buyer? | 069331990 | ❓ Open | Same value in HBT. Buyer vs ship-to? |
| HST | 4–10 | Ship-to name, address, city, state, zip, country | N1*ST N102, N301/N302, N401–N404 | parties.shipTo | [ShipToName]… | ✅ Verified | Client doc ✅. |
| HBT | 2–10 | Bill-to (same layout) | N1*BT loop | parties.billTo | [BillToName]… | ✅ Verified | Client doc ✅. |
| HRT | 3 | Sold-by / ship-from name | N1*SF (or N1*RI) N102 | parties.shipFrom / accountsReceivable | [ShipFromName] | 🟡 Inferred | Which party Costco expects is in its guideline. |
| HRT | 4 | Vendor number assigned by customer? | REF*IA | references | 96510 | ❓ Open | Confirm meaning. |
| HRT | 7 | Supplier DUNS | N1*SF N104 (qualifier 1) | identificationCode | 008860371 | 🟡 Inferred |  |
| HRT | 8–14 | Sold-by address | N3/N4 | address | [ShipFromAddr1]… | 🟡 Inferred |  |
| LDT | 2 | ERMS item number | IT1 VN | productIds.vendorItemNumber | 000000135 | ✅ Verified | Client doc ✅. |
| LDT | 3 | Customer item number | IT1 IN (buyer item) | productIds.buyerItemNumber | 29439302 | 🟡 Inferred | Client doc says field 25; sample shows it in field 3. Confirm. |
| LDT | 5 | UPC | IT1 UP (12) / UK (13–14) | productIds.gtin12/gtin13 | 072935001353 | ✅ Verified | Choose qualifier by length. |
| LDT | 6 | Unit of measure | IT103 | quantityInvoiced.unitOfMeasure | EA | ✅ Verified | EA/CS lookup (client doc). |
| LDT | 8 | Item description | PID*F**…*PID05 | productAttributes.description | [ItemDescription] | ✅ Verified |  |
| LDT | 10 | Price per case | CTP or derive | — | 30.25020 | 🟡 Inferred | 400 cases × 30.2502 = 12,100.08 (field 15). |
| LDT | 13 | Quantity ordered | — (or IT1 if partner wants ordered) | — | 2400.00 | 🟡 Inferred |  |
| LDT | 14 | Units shipped / invoiced | IT102 | quantityInvoiced.value | 2400.00 | ✅ Verified | Sum equals TOT field 3 (9,441). |
| LDT | 15 | Extended amount | Used to check TDS | — | 12100.08000 | ✅ Verified | Sum equals TOT field 5 (42,387.465). |
| LDT | 17 | Units per case | PO4*01 (pack) | — | 6 | 🟡 Inferred |  |
| LDT | 19 | Line number | IT101 | lineNumber | 1 | ✅ Verified | Increments 1…n. |
| LDT | 21 | Net unit price | IT104 | unitPrice | [NetUnitPrice] | ✅ Verified | Client doc ✅. |
| LDT | 26 | Gross unit price | CTP (if required) | — | [GrossUnitPrice] | 🟡 Inferred |  |
| LDT | 32 | Brand code | PID or REF | productAttributes.brand | [Brand] | ✅ Verified | Client doc ✅. |
| LDT | 33 | Brand description | — | — | [BrandDescription] | ❓ Open | No home found yet. |
| HMC | 2,4,5,7 | Header allowance/charge: description, amount, A/C indicator, code | SAC01, SAC02, SAC05, SAC12, SAC15 (header) | allowances[]/charges[] | HMC\|\|BACKHAUL\|\|0\|02\|54\|\| | 🟡 Inferred | Rules per client doc; rate-vs-total basis lives in ERMS note table. |
| LAL | — | Line allowance/charge | SAC inside IT1 loop | flattened to invoice-level (Orderful) | LAL\|\|Off Invoice Promotion\|\|@AC\|5\|02\|\| | 🟡 Inferred | Per-case vs per-unit rate needs ERMS note-table config. |
| TOT | 2 | Invoice total | TDS01 (implied 2 decimals) | invoiceTotal | [InvoiceTotal] | ✅ Verified | Client doc ✅. |
| TOT | 3 | Total units | CTT02 (hash total) | — | 9441.00 | ✅ Verified | Verified = sum of LDT 14. |
| TOT | 5 | Sum of extended amounts | TDS02 (amount subject to terms) | — | 42387.46500 | 🟡 Inferred | Verified = sum of LDT 15. |
| — | — | Line count | CTT01 (computed) | — | — | ✅ Verified | Tray computes. |
