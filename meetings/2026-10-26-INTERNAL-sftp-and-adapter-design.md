# 2026-10-26 — INTERNAL: SFTP decision and adapter design

Attendees (Concurrent): Mark (PM), John (sales), Isaac, Michel (engineer), Mauricio (dev).
Transcript: `source-docs/transcripts/2026-10-26-INTERNAL-sftp-and-adapter-design.vtt`

## Decisions
- **SFTP:** Concurrent must provide it (John: it was a deal requirement), but we won't run our own server. Use **CouchDrop** (managed SFTP, ~$50/month for one mailbox/folder). Isaac sets up the account and puts credentials in 1Password for Michel. GCP's serverless SFTP is an option for future clients.
- **Build approach:** a generic, reusable **adapter / SFTP connector in MagicPass V3** that translates Orderful **Mosaic JSON** ↔ flat files (pipe-delimited first; CSV/XML later), driven by a mapping config. The target is Orderful's JSON, not X12 — Orderful produces the X12.
- **Mosaic:** Mark confirmed recent live onboardings use Mosaic for 850 in and 856/810 out. Should reduce partner-specific mapping.
- **First flow:** 850 — read from Orderful, write the ERMS flat file to SFTP.

## Open points
- Field lengths (min/max) aren't in the client's templates. Plan: infer from sample history with Claude; Mark can ask Adam if it turns out to be critical.
- R.C. Moore Tray flows (V2, single partner) are a reference for how the pieces work.

## Next steps
- Isaac: create the CouchDrop account today; credentials in 1Password.
- Michel + Mauricio: design the adapter; draft Jira stories (SFTP connector, Mosaic API, Orderful auth, technical design); rough estimate for review **Tue 10/27, 9:00–9:30 ET**.
- Mark: schedule the 10/27 9:00 ET review (before the noon client call); add the R.C. Moore Tray flow links to the repo; share the Tray flows with Michel.
- Mark: rename the "10-21" agenda and mapping workbook files so the date isn't misleading.
