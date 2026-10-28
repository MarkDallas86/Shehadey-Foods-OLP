# Decisions

| Date | Decision | Source |
|---|---|---|
| 2026-10-09 | Concurrent leads the account (Tray iPaaS integration; Orderful doesn't do iPaaS) | Slack thread (Scott Shields, Isaiah) |
| 2026-10-13 | Start net new with Orderful ISA IDs | Kickoff |
| 2026-10-13 | Costco is the pilot trading partner | Kickoff |
| 2026-10-13 | SFTP host TBD at kickoff — superseded 10/20 (see below) | Kickoff |
| 2026-10-19 | Mapping is done offline: Concurrent reviews specs + 850 files, drafts maps with Claude, tests, and brings Shehadey only the questions | Mark |
| 2026-10-13 | 852s configured for VMI partners via Park City Group | Kickoff notes |
| 2026-10-20 | Park City Group files do not come through EDI (client statement) | Follow-up call (Mark's notes) |
| 2026-10-20 | **Concurrent hosts the SFTP**; client connects via BizLink (file mover) — implementation decided 10/26 (below) | EXTERNAL working session |
| 2026-10-20 | **New Orderful ISA IDs for all partners** (confirmed by client). Plant/location identified by DUNS/store in the 850 | Working session |
| 2026-10-20 | Tray reproduces the exact ERMS flat files; client's mapping templates are the spec | Working session |
| 2026-10-20 | Park City VMI orders (Fresno/Fairfield/Model) stay on direct download — Tray does not build the Park City fixed-width 850 | Working session |
| 2026-10-20 | 852: carbon copy only, not processed in ERMS; Orderful accepts + 997 | Working session |
| 2026-10-20 | Costco 856: Fresno automated (WMS); Fairfield/Model manual via Orderful WebEDI | Working session |
| 2026-10-26 | Costco trade request 220507 created (Shehadey ORDFLSHEHAFOODS → Costco COSTCOEDIUSA, type New, outreach skipped). 852 and COSTCOMASN (856) to follow | Mark |
| 2026-10-26 | SFTP via **CouchDrop** managed service (~$50/month), paid by Concurrent; no self-run server. GCP serverless SFTP considered for future clients | INTERNAL 10/26 |
| 2026-10-26 | Build a reusable **adapter / SFTP connector in MagicPass V3**: Orderful Mosaic JSON ↔ flat files (pipe-delimited first), mapping-config driven. No canonical order data stored (pull → transform → push) | INTERNAL 10/22 + 10/26 |
| 2026-10-26 | Map to **Orderful Mosaic JSON**, not X12; Orderful produces the X12. First flow: 850 Orderful → SFTP | INTERNAL 10/26 |
| 2026-10-27 | 860 (PO change): notification only — email to the order desk; not imported into ERMS | EXTERNAL 10/27 (meetings/2026-10-27-EXTERNAL-client-weekly-sync.md) |
| 2026-10-27 | 820: pass through to the SFTP for HighRadius (X12 or JSON); 824: email to AR. Not imported into ERMS; same for all partners | EXTERNAL 10/27 (meetings/2026-10-27-EXTERNAL-client-weekly-sync.md) |
| 2026-10-27 | Park City VMI 850s into ERMS stay on the existing direct ERMS ↔ Park City job (reconfirmed) | EXTERNAL 10/27 (meetings/2026-10-27-EXTERNAL-client-weekly-sync.md) |
| 2026-10-27 | Costco VMI 850 copy into Orderful: Concurrent creates a trade request with ReposiTrak (existing AS2 to Orderful per their 10/22 email) instead of a call with Kelly | EXTERNAL 10/27 (meetings/2026-10-27-EXTERNAL-client-weekly-sync.md) |
| 2026-10-27 | Mapping inferred from paired samples (flat file + X12 + JSON) and the client template, then validated in testing (reconfirmed) | EXTERNAL 10/27 (meetings/2026-10-27-EXTERNAL-client-weekly-sync.md) |
| 2026-10-27 | Aptean won't be notified until the transition is ready (client) | EXTERNAL 10/27 (meetings/2026-10-27-EXTERNAL-client-weekly-sync.md) |
| 2026-10-27 | One Mosaic-based mapping per doc type for all partners, per-partner required/optional flags in the transformation; no MagicPass TP enrollment, no canonical storage | INTERNAL 10/27 (meetings/2026-10-27-INTERNAL-dev-kickoff-and-client-prep.md) |
| 2026-10-27 | V3 adapter stores the map for both directions (flat file ↔ JSON) | INTERNAL 10/27 (meetings/2026-10-27-INTERNAL-dev-kickoff-and-client-prep.md) |
| 2026-10-27 | Timeline by doc type goes to the client on next week's call, not 10/27 | INTERNAL 10/27 (meetings/2026-10-27-INTERNAL-dev-kickoff-and-client-prep.md) |
| 2026-10-27 | Jira: one Costco story with per-doc-type subtasks (OLP-509 = V3 auth + system-to-system integration story) | INTERNAL 10/27 (meetings/2026-10-27-INTERNAL-dev-kickoff-and-client-prep.md) |
