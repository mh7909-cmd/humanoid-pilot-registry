# Humanoid Pilot Registry (v1.0)

Data supplement to the working paper:

**From Demo to Deployment: What Predicts Humanoid Pilot Conversion?**
Mayank Hinduja, NYU Stern

This repository contains the frozen registry used in the paper: 38 records of publicly reported industrial humanoid pilots and deployments in manufacturing and logistics, coded from public evidence through September 20, 2026 (the registry cutoff date).

## Contents

- `humanoid_pilot_registry.csv` - the registry exactly as analyzed in the paper. 38 records: 36 maker-partner episodes, one Ricoh correction row (a service partner, not a deployment site, retained so the exclusion is auditable), and one company-level UBTECH Walker S2 delivery milestone.
- `DATA_DICTIONARY.md` - column definitions, the six-stage ontology, source-quality tiers, the related-party flag, and censoring rules, taken from the paper's methodology.

## Stage mix at cutoff

pilot_on_site 18, testing 7, announced 6, paid_deployment 4, discontinued_stalled 2, scaled_fleet 1.

## Source tiers at cutoff

independent_reporting 15, press_release 12, partner_statement 9, vendor_claim 2.

## Citing this registry

Hinduja, M. (2026). *Humanoid Pilot Registry* (v1.0) [Data set]. Supplement to "From Demo to Deployment: What Predicts Humanoid Pilot Conversion?" GitHub. https://github.com/mh7909-cmd/humanoid-pilot-registry

Replace `<username>` with the account hosting this repository.

## License

The data is released under CC BY 4.0. You may share and adapt it with attribution.

## Versioning

- v1.0 (September 2026): initial public release, matching the working paper's frozen registry. Future versions will note recoding decisions in this file.
