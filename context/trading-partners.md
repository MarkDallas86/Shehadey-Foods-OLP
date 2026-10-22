# Trading partners (Phase 1, from client inventory)

Full detail: `source-docs/EDI_VAN_Migration_Trading_Partners.xlsx`.

## Pilot: Costco (4 relationships)
- Invoice via SPS Commerce (UMPQUA): 850, 860, 997 in / 810 out
- ASN (PRODNCS): 856 out — Costco requires accurate ASNs; most ERMS 856s lack pallet/SSCC data
- VMI (PRODDAIR): 852 both directions
- Via Park City Group (3 plants): 810 (inferred)
- Question: which relationships are in the pilot?

## Watch list
- Walmart: legacy qualifier-12 IDs; 850/864/852/812/820 in, 810/856/852 out
- UCS grocery (Safeway, C&S, WinCo, Smart & Final, Kroger DSD): 875/880/876/894/895, GS07=T
- Family Dollar: version 4030
- Adventist/Dignity: shared clearinghouse IDSINC437
- Smart & Final: possible FTP requirement
- Sodexo: qualifier mismatch by direction
- Walgreens, Saladinos: verify still active
- Cross-plant routing: Dollar General, Harbor Foods, Safeway, Walmart
- Mid Valley list: not yet received

## Costco channels (confirmed 2026-10-20)
- **Umpqua (Oregon):** direct EDI via SPS (sender COSTCOEDIUSA). 850 in, 810 out, 856 in testing with SPS. 2 products, ~twice a week. No WMS. Needs 850 mapping before go-live.
- **Park City VMI (Fresno, Fairfield, Model):** 852 carbon copy to Park City; Park City creates the 850, which Shehadey downloads directly (not EDI). 856 now required: Fresno via WMS; Fairfield (~10 Costcos, ~10/day) and Model manual via WebEDI. Park City's EDI provider is ReposiTrak.
- Walmart and Sam's also come through Park City VMI for the California/Nevada plants; Umpqua trades with Walmart directly.
