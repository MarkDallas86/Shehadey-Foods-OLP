# 2026-10-27 — EXTERNAL: Weekly client sync

Attendees: Mark (Concurrent PM); Shehadey: Adam (ERMS/EDI lead), Becky (Mid Valley EDI, left early), Narvel (IT/EDI). John (Concurrent) couldn't attend.
Transcript: `source-docs/transcripts/2026-10-27-EXTERNAL-client-weekly-sync.vtt`

## What was covered
- **Concurrent update:** the dev team has started. The SFTP server (CouchDrop) is being stood up, and connection details for BizLink will follow. The Costco trade request has been created. Mark has reviewed the Aptean files (plenty of X12 examples to use as first tests). The dev team is working on the 850 parsing/translation flow.
- **Costco vendor number:** there's no single Shehadey number. It's an SAP-style number (30255) plus a plant suffix. Mark expects to send Costco all four plant vendor numbers when testing starts. Adam and Narvel will find the email that lists them.
- **860 (PO change):** rare (only 3 Costco 860s in Aptean since May). ERMS won't process them, so they'll be notification only: an email to the order desk.
- **820 / 824:** no 820s and only two 824s in Aptean. Adam recently went live with HighRadius (payment processor) for ERMS. Today he moves Target and Walmart 820s from the Aptean SFTP to HighRadius with BizLink as raw X12. Going forward, 820s should land on the server for HighRadius (X12 or JSON; Adam will ask which they prefer), and 824s go by email to AR. Neither is processed into ERMS. This is the standard for all partners.
- **852 / VMI:** the Costco 852 is a carbon copy to Park City; Shehadey doesn't process it. Park City builds the VMI 850s, and an ERMS job pulls them straight from Park City's SFTP in the Park City flat-file format. This path stays as is.
- **Costco certification:** the deadline Costco gave was 10/15, which has passed. No new hard deadline. The holdup has been getting the Park City/ReposiTrak 850 into Orderful (needed to build 856s).
- **ReposiTrak 850 copy:** ReposiTrak replied (10/22 email, Mark and John copied) that it already has an AS2 connection with Orderful. Instead of a separate call with Orderful (Kelly), Concurrent will start the trade request with ReposiTrak.
- **Flow diagram:** Adam walked through two streams.
  - Umpqua: Costco 850 via SPS → Aptean SFTP → ERMS. The 856 is manual (no WMS). The 810 goes out via SPS.
  - Park City VMI: the 850 goes to Fresno (automated 856 via WMS) and to Fairfield/Model (manual, likely Orderful WebEDI).
  - Adam will add Aptean to the diagram and send it.
- **Mapping approach:** confirmed. Use paired flat files + X12 + the client's template to infer about 90% of the mapping, then close gaps in testing. Adam showed a paired Umpqua 850 (flat file / raw X12 / JSON / field correspondence) and one 810. He'll fix the template, upload the zip to the website and let Mark know.
- **Aptean:** month-to-month. Shehadey hasn't told Aptean yet and will hold off until the transition is ready.

## Decisions
- 860s: notification only (email to the order desk). Not imported into ERMS.
- 820s: pass through to the SFTP for HighRadius (X12 or JSON). 824s: email to AR. Not imported into ERMS. Same handling for all partners.
- Park City VMI 850s into ERMS stay on the existing direct ERMS ↔ Park City job (reconfirmed).
- Get the Costco VMI 850 copy into Orderful by having Concurrent create a trade request with ReposiTrak (it has an existing AS2 connection to Orderful, per its email). This replaces the call with Kelly.
- Mapping is inferred from paired samples and the client template, then validated in testing (reconfirmed).
- Aptean won't be notified until the transition is ready (client decision).

## Open points
- Costco vendor numbers for each plant (30255-<plant>)? (Adam/Narvel)
- Which email address should get 860 notifications (order desk), and which AR address should get 824s?
- Does HighRadius prefer X12 or JSON for the 820?
- ReposiTrak's existing AS2 connection with Orderful: confirm the details and the right ISA/IDs (unconfirmed).
- Which partners besides Target and Walmart send 820s/824s today?

## Next steps
- Shehadey (Adam/Narvel): send the Costco vendor numbers for each plant.
- Shehadey (Adam): send the order-desk email for 860s and the AR email for 824s.
- Shehadey (Adam): ask HighRadius whether it prefers X12 or JSON for the 820.
- Shehadey (Adam): add Aptean to the Costco flow diagram and send it.
- Shehadey (Adam): upload the paired 850 and 810 samples (flat file / X12 / JSON), plus two more of each, to the website and tell Mark.
- Mark: create a trade request with ReposiTrak for the Costco VMI 850 copies and request their EDI details.
- Mark: send the client an end-of-day recap of open action items.
