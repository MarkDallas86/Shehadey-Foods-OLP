# 856 Ship Notice — ERMS flat file → X12 856 (outbound)

Direction: ERMS writes the .856 flat file → BizLink → SFTP → Tray maps to Orderful's 856 → Orderful sends X12 to Costco.

Scope: Costco requires accurate ASNs with SSCC labels. Only the UW-style program (true pallets) carries SSCCs. Fresno has a WMS (automated); Fairfield and Model will use Orderful WebEDI manually; Umpqua has no WMS yet. So automated Costco 856s are only realistic where UW-style data exists.

Evidence used: client's 856 mapping template + open questions; EDI_UW.856 (real, Walmart, with SSCC) and EDI_RA_redacted.856 (order-only).

Still needed: a Costco 856 example (from Aptean/SPS testing), Costco's 856 guideline, and sources for ship-from, carrier, BOL and packaging/weight.


**Coverage:** 27 of 36 rows mapped (75%) — 17 verified, 10 inferred, 9 open. Inferred rows need one paired Costco example to confirm.

Legend: ✅ Verified against real paired data or client-confirmed · 🟡 Inferred from patterns/client template · ❓ Open question

| Record | Field | Meaning | X12 element | Orderful JSON | Example | Status | Notes |
|---|---|---|---|---|---|---|---|
| File | — | Two source programs: UW (true pallets, SSCC) and RA (order only, no pallets) | BSN05 0001 (S-O-T-I) for UW; 0002 (S-O-I) for RA | — | EDI_UW.856 / EDI_RA_redacted.856 | ✅ Verified | Client doc. Costco needs SSCC, so only UW-style meets Costco. |
| HDR | 2–3 | File date / time | BSN03 / BSN04 | — | 20260808 / 013009 | 🟡 Inferred |  |
| HDR | 4 | Order number | BSN02 (shipment ID); PRF01 fallback | shipmentId | 59704817 | ✅ Verified | Client doc ✅. |
| HDR | 5 | Ship-to GLN | N1*ST N104 (UL) | parties.shipTo | 0078742017389 | ✅ Verified | Equals HS field 3. |
| HDR | 6 | PO number | PRF01 (preferred) | purchaseOrderNumber | (blank in samples) | ✅ Verified | Rule: use PO if present, else order number (client doc). |
| HDR | 7 | Order date | PRF04 | purchaseOrderDate | 20260806 | ✅ Verified | Client doc ✅. |
| HDR | 8 | Delivery date | DTM*017 (estimated delivery) | dates.deliveryDate | 20260810 | 🟡 Inferred |  |
| HDR | 11 | Vendor number | REF*IA | references | 1002805 (RA) | 🟡 Inferred | Captured, not mapped by client. |
| HDR | 13–14 | Order number repeat / date | DTM*011 (ship date)? | — | 59704817 / 20260810 | ❓ Open |  |
| HDR | 18 | Date | ? | — | 20260909 | ❓ Open |  |
| HS | 2 | Store / location number | N1*ST N104 (92) | parties.shipTo.identificationCode | 02051314 | 🟡 Inferred | Which ID Costco wants comes from its guideline. |
| HS | 3 | Ship-to GLN | N1*ST N104 (UL) | parties.shipTo | 0078742017389 | ✅ Verified |  |
| HS | 4 | Ship-to name | N1*ST N102 | parties.shipTo.name | Walmart UMP 1772 KF | ✅ Verified | Client doc ✅. |
| HS | 5–9 | Address, city, state, zip | N301/N302, N401–N403 | parties.shipTo | 1108 SE 10th Street … AR 92716 | ✅ Verified | Client doc ✅. |
| HO | 2 | Order reference | PRF? / REF | — | 59704817 | ❓ Open | Client doc: meaning unconfirmed. |
| HO | 3 | Order / ship date | DTM*011 | dates.shipDate | 20260806 | ✅ Verified | Client doc ✅. |
| HO | 4 | Shipment SSCC (UW only) | MAN*GM at shipment level? | — | 00712030097048176 | ❓ Open | Client doc: differs from pallet SSCCs. |
| HI | 2 | ERMS item number | LIN VN | productIds.vendorItemNumber | 000201112 | ✅ Verified | Client doc ✅. |
| HI | 3 | Customer item number | LIN IN | productIds.buyerItemNumber | 9091809 | 🟡 Inferred |  |
| HI | 5 | UPC | LIN UP | productIds.gtin12 | 071580000100 | ✅ Verified | Client doc ✅. |
| HI | 6 | Unit of measure | SN103 | quantityShipped.unitOfMeasure | EA | ✅ Verified | Client doc ✅. |
| HI | 8 | Item description | PID*F | productAttributes.description | WHOLE UMPQUA PLASTIC GAL | ✅ Verified | Client doc ✅. |
| HI | 13 | Quantity (ordered = shipped) | SN102 | quantityShipped.value | 48.00 | ✅ Verified | Client doc ✅. RA can't show short ships. |
| HI | 14 | Quantity shipped? | SN102 (if populated) | — | 0 | ❓ Open | 0 in UW sample. Which field is the real shipped quantity? |
| HI | 17 | Units per case | PO4*01 | — | 4 | 🟡 Inferred |  |
| HI | 20 | Line number | LIN01 | purchaseOrderLineId | 0 (UW) / 1…n (RA) | ✅ Verified | Client doc ✅. |
| HI | 21 | Unit price | — (not usually on 856) | — | 4.63000 | 🟡 Inferred | Include only if Costco requires. |
| HI | 25 | Short vendor item | LIN VN? | — | 01112 | ❓ Open |  |
| HI | 26 | Pallet SSCC (UW only) | HL*T/P + MAN*GM (SSCC-18) | pallets[] | 00000712030229800011 | ✅ Verified | Rows sharing this value = one pallet (client doc). |
| HI | 32 | Stack-high count (UW only) | TD1 / PAL (per guideline) | pallets[].stackHighCount | 6 | 🟡 Inferred |  |
| Not in file | — | Ship-from party | N1*SF | parties.shipFrom | — | ❓ Open | Default per plant from config? |
| Not in file | — | Carrier | TD5 (SCAC) | carrierDetails | — | 🟡 Inferred | Hardcode; Shehadey uses its own trucks ('self'). |
| Not in file | — | Bill of lading / PRO | REF*BM / REF*CN | references | — | ❓ Open | No source in ERMS. |
| Not in file | — | Packaging / weight | TD1 | — | — | ❓ Open | Costco may require. |
| Not in file | — | Purpose | BSN01 = 00 (original) | purpose | — | 🟡 Inferred | Hardcode. |
| — | — | Hierarchy and counts | HL loops; CTT01 | — | — | ✅ Verified | Tray builds from file order. |
