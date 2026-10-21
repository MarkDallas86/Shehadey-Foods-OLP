# Systems and flow

## Outbound (810, 855, 856, 852, 880/894)
ERMS writes flat file → BizLink picks it up → pushes to the **SFTP server (host TBD)** → Tray maps flat file → Orderful JSON → Orderful converts to partner X12 and delivers.

## Inbound (850, 860, 875, etc.)
Partner X12 → Orderful → Tray maps Orderful JSON → ERMS flat file → SFTP → BizLink pulls to ERMS import folder → ERMS imports.
(Unconfirmed: confirm 850 → ERMS file is in Concurrent's scope per SOW.)

## Flat file formats known
- Pipe-delimited NCS/NCW files (ERMS layout, records HDR/HST/HBT/HCM/HAL/LDT/LAL/TOT for 850).
- Fixed-width PRODUCERS_ORDERS (Park City Group format, Costco/Walmart).
- 810 template also carries 880 and 894.

## Plant IDs (current)
PRODNCS, UMPQUA, PRODDAIR, PRODUCENCS, plus two legacy qualifier-12 IDs used for Walmart (5416722638, 2092646583).
