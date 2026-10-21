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
