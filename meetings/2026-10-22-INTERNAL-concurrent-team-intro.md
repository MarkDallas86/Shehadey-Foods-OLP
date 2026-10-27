# 2026-10-22 — INTERNAL: Concurrent team intro to Shehadey

Attendees (Concurrent): Mark (PM), Michel (engineer), Mauricio (dev), Vinod. John accepted but didn't join.
Transcript: `source-docs/transcripts/2026-10-22-INTERNAL-concurrent-team-intro.vtt`

## What was covered
- Mark walked the team through the project, the integration flow page and the Costco mapping workbook.
- Scope confirmed: message translation only. Orderful ↔ SFTP ↔ BizLink; no access to ERMS; BizLink just repoints to our SFTP.
- Plant complexity: Umpqua (no WMS, no pallet data for 856 → WebEDI); Fresno (WMS; Park City VMI orders non-EDI, but 856 out through our integration); Fairfield/Model (WebEDI; ReposiTrak AS2 is between Shehadey and Orderful, not us). Phase 2 = Mid Valley, same architecture, new mappings.
- Some partners need 875/880 instead of 850/810 — different structures, more mapping work.
- Costco is a store (not dropship) partner.

## Points raised
- **SFTP hosting (Vinod):** avoid running our own server — lessons from OpenTrans (certificate upkeep, outages). Prefer the client or a managed third-party SFTP, and pass any cost to the client. Ask Isaac for his view.
- **Platform (Michel/Vinod):** Shehadey is a pull → transform → push pipeline with no canonical order data stored (like V2). Customers still get the Integration Health tab (logs, success rate), which may reduce the need for SOS Jira tickets.
- **Timeline:** sales said Costco live by Oct 19 — already missed. Client lead has not set a hard date; wants steady progress.

## Next steps
- Michel + Mauricio: build the new SFTP connector in MagicPass V3, then the transformation pipelines once mappings are set.
- Mark: share the repo (done); check with Isaac on SFTP; sync with John on Monday 10/26.
