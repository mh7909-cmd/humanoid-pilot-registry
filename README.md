# Humanoid Pilot Registry (v1.1)

Data supplement to the working paper:

**From Demo to Deployment: Measuring Humanoid Pilot Conversion**
Mayank Hinduja, NYU Stern

This repository contains the registry used in the paper: 38 records of publicly reported industrial humanoid pilots and deployments in manufacturing and logistics, coded from public evidence through September 20, 2026 (the registry cutoff date). v1.1 is a recode release: the frozen four-gate conversion rule is unchanged, and a disclosed delivery-scope refinement was added (see DATA_DICTIONARY.md).

## Contents

- `humanoid_pilot_registry.csv` - the registry as analyzed in the paper. 38 records: 36 maker-partner episodes, one Ricoh correction row (a service partner, not a deployment site, retained so the exclusion is auditable), and one company-level UBTECH Walker S2 delivery milestone. 34 columns: the 18 original fields plus `record_id`, four conversion-gate fields, sensitivity field `delivery_verified`, `conversion_tier`, `related_party`, `related_party_type`, `internal_maker_use`, and six timing/source-label fields (`pilot_demo_date`, `pilot_demo_evidence_url`, `commitment_date`, `commitment_evidence_url`, `operational_evidence_source`, `last_affirmative_report_date`).
- `DATA_DICTIONARY.md` - column definitions, the six-stage ontology, the frozen four-gate conversion rule and its v1.1 operationalization, source-quality tiers, the related-party flag, internal-maker-use coding, censoring rules, and the v1.1/v1.1a coding-decision log.
- `SOURCES.md` - per-record primary sources with direct URLs for the pilot/demo, first public evidence, and paid commitment phases (also lists the Fulin Xinhua report URL).

## Stage mix at cutoff

pilot_on_site 18, testing 7, announced 7, paid_deployment 3, discontinued_stalled 2, scaled_fleet 1.

## Conversion tiers at cutoff

qualifying_conversion 3 (GXO, Toyota/TMMC, Fulin Precision), commercial_commitment_pending_operation 1 (Mercado Libre), not_applicable 34.

The registry's headline result under the frozen four-gate conversion rule is three strict conversions. A separate delivered-service sensitivity is disclosed in DATA_DICTIONARY.md and the paper: GXO's deployment is verified by partner and independent sources; Toyota's contracted-rollout execution rests on maker-issued statements only; Fulin's full ~100-unit delivery scope is unverified.

## Related-party and internal use

Seven records are flagged for a material maker-partner tie (investment, ownership, strategic partnership): Mercedes-Benz-Apptronik, Schaeffler-Agility, Magna-Sanctuary AI, EQT-1X, Hyundai-Boston Dynamics, POSCO-Persona AI, CATL-Galbot. Three records are coded as internal maker use (Tesla at Fremont, Unitree at its own factory, XPeng at Guangzhou) and sit outside the maker-partner demand comparison entirely: internal use has no external partner and no demand signal, so it is not a related-party tie and is excluded from the demand denominator.

Denominator: 38 source records minus Ricoh (service), minus the UBTECH company-level batch milestone, minus three internal-use rows = 33 external maker-partner episodes; minus seven related-party ties = 26 external arm's-length episodes.

## Citing this registry

Hinduja, M. (2026). *Humanoid Pilot Registry* (v1.1) [Data set]. Supplement to "From Demo to Deployment: Measuring Humanoid Pilot Conversion." GitHub. https://github.com/mh7909-cmd/humanoid-pilot-registry

## License

The data is released under CC BY 4.0. You may share and adapt it with attribution.

## Versioning

- v1.0 (September 2026): initial public release, matching the working paper's frozen registry. 18 columns. Stage mix: pilot_on_site 18, testing 7, announced 6, paid_deployment 4, discontinued_stalled 2, scaled_fleet 1. Preserved unchanged.
- v1.1 (September 26, 2026): recode release. Added `record_id`, gate fields, sensitivity field `delivery_verified`, `conversion_tier`, `related_party`, `related_party_type`, `internal_maker_use` (28 columns). Mercado Libre recoded `paid_deployment` → `announced`. Fulin evaluated against the frozen four gates with new November 2025 evidence → `qualifying_conversion` (three strict under the frozen rule); `delivery_verified=FALSE` recorded as a separate disclosed sensitivity. Toyota evidence separated by phase with maker-only rollout evidence disclosed. NEURA first-evidence URL/date corrected. Denominator recalculated: 33 external maker-partner episodes, 26 external arm's-length. The frozen conversion rule was not changed.
- v1.1a (September 26, 2026): evidence-record hardening, no tier changes. Added `pilot_demo_date`, `pilot_demo_evidence_url`, `commitment_date`, `commitment_evidence_url`, `operational_evidence_source`, `last_affirmative_report_date` (34 columns). Gate 4 (continuation) wording fixed for every case: evaluated as of the last verified report, silence not treated as evidence. `partner_confirmed` narrowed to partner confirmation of the paid commitment decision; post-commitment operation evidence labeled per case (`operational_evidence_source`: GXO partner+independent; TMMC maker-issued; Fulin independent; Mercado Libre unverified). GXO outcome windows recomputed from the December 6, 2023 pilot start (no paid conversion within 6 months; agreement at ~6.7 months). Xinhua direct URL added to the Fulin evidence record; SOURCES.md added. Timing figures regenerated from the registry date fields.
