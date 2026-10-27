# Open questions

## SFTP / BizLink (Concurrent hosts — decided 10/20)
- Added cost to Concurrent? (internal)
- Can Tray connect directly to Shehadey's SFTP without BizLink?
- BizLink outbound IP addresses to whitelist?
- SSH key or password?
- One folder per plant, or shared? Separate sandbox and production folders?
- File naming, polling frequency, archive/error handling?
- Can BizLink send one file to two destinations (shadow test vs Aptean)?
- Can ERMS produce test files and keep test 850s out of production?

## Scope
- Is the 850 → ERMS flat file in Concurrent's scope (SOW)?
- Doc types: 17 in inventory vs ~7 priced. Do 820/812/864/824 go into ERMS or stay in Orderful?
- Does Tray produce both inbound formats (pipe-delimited and Park City fixed-width)?

## Costco pilot
- Which of the 4 relationships are in the pilot? How is the ASN data gap closed?
- SPS testing portal access (credentials to be shared by client).

## Net new ISA
- Who notifies each partner of the new ID, and in what order?

## From Mark's kickoff notes
- Is there one ERMS layout per doc type for all partners, or partner-specific variants?
- Does ERMS hold partner-specific values (store numbers, partner item numbers), or did Aptean add them via cross-reference tables? Can those be exported?
- How will ASNs and labels be handled (per partner)? Most ERMS 856s won't be done for most partners.
- Historical data: Orderful asked them to import history in the Orderful UI — status?
- Carbon-copy 852s from Shehadey to Park City Group — confirm setup.

## Aptean pain points (ask on next call)
- Biggest frustration with Aptean today? What does success look like?
- Known from docs: ~$8K/mo, confusing kilo-character billing, two separate EDI setups, weak error visibility (no 997s, silent failures).

## From the 2026-10-20 follow-up
- Aptean access offered by the client (unconfirmed): what access, and can we view existing maps and cross-references there?
- Park City Group files don't come through EDI (per client). Does Park City stay fully outside Orderful? Does Tray still need to produce the fixed-width format?

## From the 2026-10-20 working session
- Costco certification status and go-live date? (10/15 certification target missed)
- Can Park City / ReposiTrak send Costco 850s to Orderful via AS2, so WebEDI can build 856s for Fairfield/Model?
- Umpqua Costco 856: RA program (no SSCC) or WebEDI? Costco requires SSCC.
- Field-level required fields for ERMS import; how to handle orders missing required data.
- Does Aptean apply partner-specific logic on top of the ERMS layout?
- What do NCS vs NCW file prefixes mean?
- Line-level mapping questions: see `specs/<doc>/questions.md`.

## Doc type scope and commercials (added 2026-10-26)
- For the ERMS/EDI lead: Does ERMS import any of the 860, 876, 895, 820, 812, 864 or 824 today, or does Aptean just receive them?
- Internal (John): Which doc types are in the signed scope? Sales list (Tray opportunity, per intake brief): 850, 875, 880, 810, 856, 855, 945. The 945 isn't in the client inventory; the 894 (3 partners) isn't on the sales list.
- Internal (John): Are one-time per-partner setup fees, ongoing per-partner subscription, per-doc-type fees and Concurrent onboarding services spelled out in the signed order form/SOW? Intake brief only lists $5,500/doc type (Tray), VAN 3¢/transaction, AS2/SFTP no cost, $5,400/mo year-4 renewal at 45 partners, 3-year ramp (all "AE promises to verify").

## From INTERNAL calls 10/22 and 10/26
- Field min/max lengths for ERMS flat files: infer from sample history; ask Adam only if critical.
- Pass the CouchDrop SFTP cost through to the client? (raised 10/22)
- Does the V3 adapter need different structures for 875/880 partners vs 850/810? (yes per 10/22 — plan for it)
