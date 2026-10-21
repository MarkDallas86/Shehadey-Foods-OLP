# Instructions for Claude

You are helping Mark (Concurrent PM) and John (Concurrent integration architect) run the Shehadey Foods onboarding.

## Read first
1. `context/project-overview.md`
2. `context/decisions.md`
3. `action-items.md`
4. The latest file in `meetings/`

## Rules
- Facts not yet confirmed by the client or Orderful are written as questions, not statements. Mark them `(unconfirmed)`.
- Answer every question asked in a message.
- Use US English.
- Keep customer contact details (emails, phone numbers) out of this repo. Refer to people by role.
- Do not mix in data from other Concurrent clients.
- When new info arrives (call notes, emails, files): add a meeting file or source doc, then update `decisions.md`, `open-questions.md`, and `action-items.md`.
- Filing: specs and samples go in `specs/<doc type>/` (`layout/`, `samples/`); other received files go in `source-docs/from-client/`, `source-docs/from-orderful/`, or `source-docs/internal/`; anything Claude or Mark produces goes in `outputs/`. Never edit files in `source-docs/`.
- File names: lowercase-with-hyphens, no spaces; dated files start with `YYYY-MM-DD-`.
- Mapping work: draft in `specs/<doc type>/mapping.md`; log anything unclear in `specs/<doc type>/questions.md` rather than guessing.
- Do not run git commands; Mark commits and pushes in GitHub Desktop.
- Never write credentials (SFTP passwords, keys) into any file.

## Vocabulary
- ERMS: Numeric Computer Systems dairy ERP (four plants), on-prem iSeries, no source access.
- AX 2009 / Gentran: Mid Valley's ERP and in-house EDI translator (Phase 2).
- Aptean: current EDI/VAN provider being replaced.
- BizLink: Shehadey's OpenText file-transfer tool (folder watch).
- Tray: Concurrent's iPaaS used for the translation.
