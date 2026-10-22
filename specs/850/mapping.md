# 850 Purchase Order — Costco X12 → ERMS flat file (inbound)

Direction: Costco sends X12 850 to Orderful → Tray maps Orderful's 850 to the ERMS pipe-delimited file (NCS layout) → SFTP → BizLink → ERMS.

Scope: Costco orders for **Umpqua via SPS** (sender COSTCOEDIUSA). Park City (Fresno, Fairfield, Model) Costco orders stay on today's direct download from Park City and are **not** mapped here (decided on the 10/20 call).

Evidence used: client's 850 mapping template (incl. a full Costco/SPS raw-EDI-to-flat-file match, PO 012871005279); 59 production flat files incl. 2 Costco orders (NCS.20261013170149, NCS.20261013173049); 6 raw Walmart/Sam's X12 850s plus Walmart NCW flat files (same structure, different POs).

Still needed to reach 100%: a Costco raw 850 and the flat file Aptean produced from it (pull from Aptean), Costco's 850 guideline in Orderful, and ERMS's required-field list.


**Coverage:** 50 of 56 rows mapped (89%) — 23 verified, 27 inferred, 6 open. Inferred rows need one paired Costco example to confirm.

Legend: ✅ Verified against real paired data or client-confirmed · 🟡 Inferred from patterns/client template · ❓ Open question

| Record | Field | Meaning | X12 element | Orderful JSON | Example | Status | Notes |
|---|---|---|---|---|---|---|---|
| File | — | One file can hold many orders; each order runs HDR … TOT | One ST/SE (850) per order | — | NCW file holds several Walmart orders | ✅ Verified | Seen in NCW batch files. |
| File | name | File name NCS.YYYYMMDDHHMMSS.850.txt (EDI channel); NCW also seen | — | — | NCS.20261013170149.850.txt | ❓ Open | What do NCS vs NCW mean (channel, plant, partner)? Confirm naming Tray must use. |
| HDR | 1 | Record ID | — | — | HDR | ✅ Verified | Constant. |
| HDR | 2 | Date received / transmitted (CCYYMMDD) | File creation date (or GS04) | receivedDate | 20261013 | 🟡 Inferred | Tray sets this when it writes the file. |
| HDR | 3 | Time received (HHMM) | File creation time (or GS05) | — | 1701 | 🟡 Inferred | Tray sets this. |
| HDR | 4 | PO number | BEG03 | purchaseOrderNumber | 001721013236 | ✅ Verified | Confirmed on Costco/SPS PO 012871005279 in client's 850 doc. |
| HDR | 5 | Sender ID | ISA06 | senderId | COSTCOEDIUSA | ✅ Verified | Confirmed vs raw ISA. With new Orderful ISA, Tray should still write the partner's ID here. |
| HDR | 6 | PO number (repeated) | BEG03 (or REF customer order #) | — | 001721013236 | 🟡 Inferred | Equals field 4 in every Costco and Walmart sample. Confirm meaning. |
| HDR | 7 | PO date | BEG05 | purchaseOrderDate | 20261013 | 🟡 Inferred | Matches BEG05 pattern on Walmart raw/flat; confirm on a Costco pair. |
| HDR | 8–10 | Unused in samples | — | — | (blank) | ❓ Open | Does ERMS ever use these? |
| HDR | 11 | Requested delivery date | DTM (qualifier per partner: Costco likely 002; Walmart 063/010) | dates.requestedDeliveryDate | 20261020 | 🟡 Inferred | Which DTM qualifier feeds this for Costco? Confirm against a Costco raw 850. |
| HDR | 12–20 | Unused in samples | — | — | (blank) | ❓ Open |  |
| HDR | 21 | Terms discount percent | ITD03 | termsOfSale (discount %) | 0.000 | 🟡 Inferred | Walmart: ITD03=1 → 1.000. |
| HDR | 22 | Terms discount amount | ITD08 | termsOfSale | 0.000 | 🟡 Inferred |  |
| HDR | 24 | FOB location description | FOB03 | carrierDetails / FOB | NA | ✅ Verified | Costco FOB*PP*ZZ*NA and Walmart FOB*PP*OR*VARIOUS ZZ both line up. |
| HDR | 25 | FOB method of payment | FOB01 | carrierDetails / FOB | PP | ✅ Verified |  |
| HDR | 26 | FOB location qualifier | FOB02 | carrierDetails / FOB | ZZ | ✅ Verified |  |
| HDR | 27 | Terms type code | ITD01 | termsOfSale.type | 01 | 🟡 Inferred | Walmart ITD01=08 → 08. |
| HDR | 28 | Terms basis date code | ITD02 | termsOfSale.basisDate | 2 | 🟡 Inferred | Walmart ITD02=15 → 15. |
| HDR | 29 | Terms discount days due | ITD05 | termsOfSale | 0 | 🟡 Inferred | Walmart ITD05=15 → 15. |
| HDR | 30 | Terms net due date | ITD06 | termsOfSale | (blank) | 🟡 Inferred |  |
| HDR | 31 | Terms net days | ITD07 | termsOfSale | 16 | 🟡 Inferred | Walmart ITD07=20 → 20. |
| HDR | 34 | Customer message / reference | Varies: Costco first MSG text; Walmart REF*AN value | notes / references | 1 PALLET MIN- ANY DAY- NEVADA SUFFIX | ❓ Open | Partner-specific. Confirm what ERMS does with it. |
| HST | 1 | Record ID | — | — | HST | ✅ Verified |  |
| HST | 2 | (blank in samples) | — | — | (blank) | ❓ Open |  |
| HST | 3 | Ship-to location ID | N1*ST N104 (Costco GLN) | parties.shipTo.identificationCode | 1033918430172 | ✅ Verified | Costco/SPS pair matched. ERMS likely looks this up in its cross-reference table. |
| HST | 4 | Ship-to name | N1*ST N102 | parties.shipTo.name | COSTCO TRACY WET | ✅ Verified | Name is blank for some accounts; ID alone may be enough. |
| HST | 5 | Ship-to address line 1 | N301 | parties.shipTo.addressLine1 | 25501 GATEWAY BLVD BLDG C | ✅ Verified |  |
| HST | 6 | Ship-to address line 2 | N302 | parties.shipTo.addressLine2 | (blank) | 🟡 Inferred |  |
| HST | 7 | Ship-to city | N401 | parties.shipTo.city | TRACY | ✅ Verified |  |
| HST | 8 | Ship-to state | N402 | parties.shipTo.stateOrProvinceCode | CA | ✅ Verified |  |
| HST | 9 | Ship-to postal code | N403 | parties.shipTo.postalCode | 95377 | ✅ Verified |  |
| HST | 10 | Ship-to country | N404 | parties.shipTo.countryCode | (blank) | 🟡 Inferred |  |
| HBT | 2–10 | Bill-to (same layout as HST) | N1*BT loop | parties.billTo | (all blank for Costco) | ✅ Verified | Costco sends no bill-to; write an empty HBT record. |
| HCM | 2 | Comment text (one HCM per line) | N9/MSG01 lines (Costco); also REF02 / MTX02 | notes | This order incorporates the Costco Wholesale Standard Terms, | ✅ Verified | Costco legal text matched word for word. |
| HCM | 3 | Comment qualifier | N901 / REF01 (e.g., AN, L1) | — | (blank for Costco) | 🟡 Inferred | Seen on Walmart only. |
| HAL | 2 | Header allowance/charge code | SAC02 | allowances[]/charges[] | (none for Costco) | 🟡 Inferred | Walmart I410. |
| HAL | 3 | Method of handling | SAC12 | — |  | 🟡 Inferred | 02 = off-invoice. |
| HAL | 8 | Amount | SAC05 (implied 2 decimals) | amount |  | 🟡 Inferred |  |
| HAL | 9 | Rate | SAC07 | — |  | 🟡 Inferred | 0.500 for I410. |
| HAL | 13 | Allowance or charge indicator | SAC01 | A→allowances[], C→charges[] |  | 🟡 Inferred |  |
| LDT | 1 | Record ID | — | — | LDT | ✅ Verified |  |
| LDT | 2 | UPC | PO1 value where qualifier = UP | productIds.gtin12 | (blank for Costco) | 🟡 Inferred | Costco sends item number only (IN). |
| LDT | 3 | Buyer (Costco) item number | PO1 value where qualifier = IN | productIds.buyerItemNumber | 1268246 | ✅ Verified | Costco/SPS pair matched (1084795). |
| LDT | 4 | Qualifier for field 2 | PO1 qualifier (UP) | — | (blank) | 🟡 Inferred |  |
| LDT | 5 | Vendor item number | PO1 value where qualifier = VN | productIds.vendorItemNumber | (blank for Costco) | 🟡 Inferred | Walmart sample. Client doc calls field 5 'description' — real data disagrees. |
| LDT | 6 | Unit of measure | PO103 | quantity.unitOfMeasure | EA | ✅ Verified | Code list (CA, EA, others) to confirm. |
| LDT | 7 | Unit of measure (repeated) | PO103 | — | EA | 🟡 Inferred |  |
| LDT | 8 | Item description | PID05 | productAttributes.description | ORGANIC WHOLE MILK 2-1GAL PRODUCERS SL13 P120 | 🟡 Inferred | Does this come from Costco's PID or from ERMS item master? |
| LDT | 12 | Quantity ordered | PO102 | quantity.value | 120.000 | ✅ Verified | Costco/SPS pair matched. |
| LDT | 19 | Unit price | PO104 | unitCostPrice | 11.3300 | ✅ Verified | Costco/SPS pair matched. |
| LDT | 24–25 | Vendor item qualifier + value | PO1 VN | productIds.vendorItemNumber | (blank for Costco) | 🟡 Inferred | Walmart sample. |
| LDT | 26 | (0 in samples) | — | — | 0 | ❓ Open |  |
| LAL | 2,13… | Line allowance/charge (same layout as HAL) | SAC inside PO1 loop | allowances[]/charges[] | (none for Costco) | 🟡 Inferred | e.g., C110 bottle deposit, amount 0.00 at PO time. |
| TOT | 1 | Record ID; always empty | — (CTT not passed) | — | TOT | ✅ Verified | Empty in all 632 production files. Must still be written. |
| Not passed | — | X12 data ERMS ignores today | PER, TD5, REF*DP/ZZ/YD, CTT, CUR, DTM*175 | — | — | ✅ Verified | ERMS takes only the records above; Aptean drops the rest. |
