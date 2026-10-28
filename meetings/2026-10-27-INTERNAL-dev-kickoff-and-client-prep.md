# 2026-10-27 — INTERNAL: Dev kickoff and client-call prep

Attendees (Concurrent): Mark (PM), John (sales), Isaac, Michel (engineer), Mauricio (dev).
Transcript: `source-docs/transcripts/2026-10-27-INTERNAL-dev-kickoff-and-client-prep.vtt`

## What was covered
- Mark added Michel and Mauricio to the Shehadey org in Orderful. Mosaic is set at the relationship level. The Costco trade request was missing guidelines until this morning, so Mark still has to configure the relationships for Mosaic.
- Michel is building the part of the V3 engine that imports a file-description config and turns a delimited flat file into flat JSON. CSV and other formats come later. John asked that the map be stored for both directions (flat file → JSON and JSON → flat file). Michel confirmed it will be.
- Mapping inputs: Michel has reviewed the 850 analysis. Mark said the repo also covers the other doc types (built from the client's Word doc plus live flat-file and EDI payloads).
- Per-partner mapping: John asked whether each trading partner needs its own map. Michel said no. Mosaic normalizes the data, so there's no MagicPass trading-partner enrollment and no canonical storage. Each partner gets an object in the transformation that marks which fields are required or optional, but the fields are the same.
- Aptean access: the credentials are in a 1Password vault ("Orderful Led Projects"). Michel doesn't have access, and Mark can't add him because he isn't the vault admin. A shared item would expire after 7 days.
- Michel asked for more sample flat files created directly by the client. Mark will ask on today's client call for paired Costco 850s (EDI + matching ERMS flat file).
- Jira: Michel created story OLP-509 under Mark's epic. It covers the V3 changes for the new authentication and the new system-to-system integration type (no canonical data stored).

## Decisions
- One Mosaic-based mapping per doc type for all trading partners, with per-partner required/optional flags inside the transformation. No trading-partner enrollment in MagicPass and no canonical data stored.
- The V3 adapter stores the map for both directions.
- Don't give the client a timeline today. Share a timeline by doc type on next week's client call.
- Jira structure: one Costco story with the per-doc-type items as subtasks (Costco is the only partner for now).
- Priority: get the 850 Orderful → flat file → SFTP flow done (target this week). After that, the client has to build its outbound flat files for the 856/810.

## Open points
- Who is the admin of the "Orderful Led Projects" 1Password vault? Michel needs lasting access to the Aptean credentials.
- Does Mauricio need his own Orderful login? Michel said probably not for this client.
- Does Michel need Orderful MCP access through his getconcurrent login? (He said probably not.)

## Next steps
- Michel: bottom-up development plan / rough estimate by doc type, for the next client call (week of 11/2).
- Michel + Mauricio: continue the 850 flow build. They met right after this call.
- Mark: configure the Costco relationships for Mosaic.
- Mark: ask the client for more 850 flat-file + EDI pairs and share them with Michel.
- Mark: ask in the general Slack channel who administers the 1Password vault, so Michel can get Aptean access.
- Mark: restructure Jira (one Costco story with subtasks).
- Mark: make this internal prep call a weekly recurring meeting before the client call.
