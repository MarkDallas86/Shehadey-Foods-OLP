# Open questions

## SFTP / BizLink (host TBD — John deciding)
- Who hosts: Shehadey or Concurrent? Added cost?
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
