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

## From the 2026-10-27 calls
- Costco vendor numbers for each plant (30255-<plant suffix>)? No single Shehadey number. (Adam/Narvel)
- Order-desk email for 860 notifications? AR email for 824s?
- Does HighRadius prefer X12 or JSON for the 820?
- Which partners besides Target and Walmart send 820s/824s today?
- ReposiTrak's existing AS2 connection with Orderful: confirm the details and IDs (unconfirmed).
- Costco certification: the 10/15 target passed; Costco has set no new hard deadline (per Adam). Watch for one.
- Internal: who administers the "Orderful Led Projects" 1Password vault (Aptean credentials) so Michel gets lasting access?

## For Adam — ERMS 850 import (from Michel's questions, 2026-10-28)
- Costco vendor numbers confirmed by Adam 10/27: Umpqua 0009125500, Producers/Fresno 0003025500 (arrives in 850 REF*VR). Plant routing in MagicPass will key off REF*VR — confirm.
- Folders: should all Costco 850 flat files go to one ERMS pickup folder, or one per plant (Umpqua vs Fresno)? The flat file has no plant/vendor field — how does ERMS assign the plant today (Aptean mailbox UMPQUA vs PRODNCS)?
- Adam's flow says only Umpqua gets Costco EDI 850s, but Aptean shows Costco 850s to PRODNCS (Tracy depot, vendor 0003025500). Which plant ships those, and is that flow in scope?
- File names: what do NCS and NCW mean? Does ERMS pick up by prefix + ".850.txt" or the exact NCS.YYYYMMDDHHMMSS.850.txt pattern? OK to bump the timestamp (or add a sequence) when two POs land in the same second? Today Aptean batches several POs per file — is one PO per file OK?
- ERMS import: which fields must every order have, and which does ERMS check against its own setup (Costco item number, ship-to/store)? Can you export the Costco items and ship-tos set up in ERMS so MagicPass can pre-check and alert?
- Always-empty positions (HDR 8-10 and 12-20, HST 2, LDT 26 = 0): confirm ERMS ignores them so we can leave them as Aptean sends them.
- Header message: what does ERMS do with the HDR customer message (screen, pick ticket)? When a PO has two special-instruction lines (e.g., PO 010731019278), which goes in HDR? Please send that PO's flat file.
