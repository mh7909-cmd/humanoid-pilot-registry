# Humanoid Pilot Registry — Data Dictionary (v1.1)

Cutoff: September 20, 2026. Companion to "From Demo to Deployment: Measuring Humanoid Pilot Conversion"
(Mayank Hinduja, NYU Stern). Repository: https://github.com/mh7909-cmd/humanoid-pilot-registry

## Columns

### Original registry fields (v1.0)
- `company` — robot maker.
- `robot_model` — model deployed.
- `deployment_partner_site` — partner and site.
- `sector`, `country` — industry sector and country of the site.
- `first_public_evidence_date`, `first_evidence_url` — earliest dated public evidence.
- `source_quality_tier` — independent_reporting | press_release | partner_statement | vendor_claim.
- `current_stage` — furthest verified stage at cutoff (see ontology below).
- `stage_evidence` — dated evidence notes supporting the stage code.
- `fleet_size`, `tasks`, `hours_throughput_claims`, `human_oversight` — deployment descriptors.
- `outcome_6mo`, `outcome_12mo`, `outcome_18mo` — horizon outcome codes (right-censored where the window had not elapsed by the cutoff).
- `notes_conflicts` — conflicting reports and coding notes.

### Recode fields (added v1.1)
- `record_id` — stable ID, HPR-001 through HPR-038 in source-file order.
- `paid_commitment_verified` — TRUE when dated evidence shows a formal paid commitment (signed commercial agreement, RaaS contract, or purchase order) beyond a time-limited evaluation.
- `on_site_verified` — TRUE when dated evidence shows the robot operating at the named site.
- `partner_confirmed` — TRUE when the site-operating partner (not only the maker) confirms the **paid commitment decision** (agreement signing, purchase order) in a release, filing, newsroom item, or direct statement to the press. Maker-issued claims are never coded TRUE here. This field records confirmation of the commitment, **not** confirmation of post-agreement operation; post-commitment on-site operation evidence is labeled separately in `operational_evidence_source`. v1.1 bases: HPR-004 (GXO releases), HPR-007 (TMMC president quoted confirming the Digit deployment decision, Feb 19 2026), HPR-008 (Mercado Libre announced the agreement), HPR-031 (Fulin placed the order; Fulin GM later confirmed operation to the press, Nov 2025).
- `delivery_verified` — TRUE only when evidence verifies delivery of the committed scope (units delivered, not merely units observed operating). Observing robots at work on site does not by itself verify the full order quantity. Refined in v1.1: the v1.0-era reading was ambiguous on this point.
- `continued_beyond_evaluation` — TRUE when affirmative evidence shows the deployment continued beyond the initial evaluation, pilot, or demo phase, **as of the last verified report on or before the cutoff**. Silence after the last verified report is not treated as evidence of continuation or of ending; the gate is evaluated on what the record affirmatively shows, not on the absence of later reports. The date of that last report is recorded in `last_affirmative_report_date`.
- `conversion_tier` — qualifying_conversion | commercial_commitment_pending_operation | not_applicable (see tiers below).
- `related_party` — TRUE when the partner has a material relationship with the maker (see Related-Party Flag).
- `related_party_type` — the relationship, when flagged.
- `pilot_demo_date` — Date (YYYY-MM-DD or YYYY-MM) of the first pilot, proof-of-concept, or public live demo evidencing the maker-partner relationship. Distinct from `first_public_evidence_date`, which is the first public record of any kind. Timing intervals in the paper are computed from this field.
- `pilot_demo_evidence_url` — Direct URL of the pilot/demo report, when available.
- `commitment_date` — Date of the paid commitment (purchase order or commercial agreement signing). Timing intervals end at this field.
- `commitment_evidence_url` — Direct URL evidencing the paid commitment.
- `operational_evidence_source` — Source type of the best available post-commitment on-site operation evidence: `partner` (partner-issued), `independent` (independent journalism or reporting), `maker-issued` (maker statements only), `partner+independent` (both), `unverified` (none found). This is a v1.1 labeling field, not a frozen gate; it is what distinguishes agreement confirmation from operation confirmation.
- `last_affirmative_report_date` — Date of the last affirmative on-site operation report on or before the cutoff; anchors the continuation gate.
- `internal_maker_use` — TRUE when the maker operates its own robots in its own facilities (see Internal Maker Use). These rows are not maker-partner demand episodes.

## Six-stage ontology

1. **announced** — a future partnership, test, order, or intended deployment is public, but on-site operation is not verified.
2. **testing** — evaluation in a lab, innovation center, maker facility, or controlled customer setting short of a live operating pilot.
3. **pilot_on_site** — the robot performed the stated task at a real partner facility, with no qualifying paid continuation established.
4. **paid_deployment** — a named operating customer has a formal paid commitment beyond a short evaluation. RaaS contracts and partner-confirmed purchase orders can qualify, with delivery caveats recorded.
5. **scaled_fleet** — multiple units or sites operate beyond an initial deployment, supported by strong evidence of continuing commercial use. Vendor-only fleet claims are labeled as such.
6. **discontinued_stalled** — affirmative evidence of ending, removal, reversion, or non-proceeding.

## The frozen conversion rule (Section 3.2) and its v1.1 operationalization

The frozen rule is the four-gate sequence in Figure 2 of the paper: public record → paid commitment (purchase order, RaaS contract) → site-level deployment (named facility, not company-level) → continuation (operating or renewed at cutoff). A record counts as a strict paid conversion only when it passes every gate in sequence. That rule was frozen before coding and is unchanged in v1.1. Gate 4 (continuation) is evaluated as of the last verified report on or before the cutoff: the gate asks whether the record affirmatively shows operation beyond the initial evaluation phase, not whether silence after the last report implies anything.

The v1.1 gate fields operationalize the rule for machine checking: `paid_commitment_verified`, `on_site_verified`, `partner_confirmed`, `continued_beyond_evaluation`. Two further fields are v1.1 additions, not frozen gates. `partner_confirmed` records the paper's evidence standard (Section 3.3): partner-issued or independent evidence is what confirms customer use; maker-issued claims alone do not. `delivery_verified` is a v1.1 sensitivity field: for quantity-based commitments (a purchase order for N units), it records whether the committed scope was verified; for RaaS service deployments that disclose no unit quantity, the committed scope is the commercial deployment itself. `delivery_verified` does not determine the tier; it supports the paper's delivered-service sensitivity analysis, presented separately from the frozen-rule result.

## Conversion tiers

- **qualifying_conversion** — passes every frozen gate. v1.1: HPR-004 (Agility Robotics / GXO), HPR-007 (Agility Robotics / Toyota Motor Manufacturing Canada), HPR-031 (AgiBot / Fulin Precision).
- **commercial_commitment_pending_operation** — paid commercial agreement, but on-site operation not verified by the cutoff. v1.1: HPR-008 (Agility Robotics / Mercado Libre).
- **not_applicable** — all other records (34).

## Related-Party Flag

A record is flagged when the customer or deployment partner also has a material relationship with the maker: investment, ownership, common corporate control, contract manufacturing, or a comparable strategic tie. The flag answers one question: how independent is the evidence of outside demand? Seven records are flagged in v1.1:

| record_id | Maker — Partner | Tie |
|---|---|---|
| HPR-010 | Apptronik — Mercedes-Benz | strategic partnership / tech investment |
| HPR-006 | Agility Robotics — Schaeffler | strategic partnership |
| HPR-018 | Sanctuary AI — Magna | investment (Magna investor in Sanctuary AI) |
| HPR-016 | 1X Technologies — EQT portfolio companies | investment (EQT Ventures investor in 1X) |
| HPR-036 | Boston Dynamics — Hyundai Metaplant | ownership (Hyundai Motor Group owns Boston Dynamics) |
| HPR-029 | Persona AI — POSCO | strategic partnership (POSCO DX) |
| HPR-038 | Galbot — CATL | strategic partnership |

Excluding these seven reduces the external maker-partner comparison set from 33 to 26; no qualifying conversion depends on a flagged tie.

## Internal Maker Use — why it is separate from the related-party ties

Three records describe a maker operating its own robots in its own facilities: HPR-013 (Tesla Optimus at Tesla's Fremont factory), HPR-015 (Unitree robots at Unitree's own factory), HPR-035 (XPeng IRON at XPeng's Guangzhou factory). These are **not** flagged as related-party, for a definitional reason: the related-party flag requires an *external partner* whose demand independence is in question. A tied partner's adoption decision might reflect capital, ownership, or strategy rather than stand-alone customer return, so the flag discounts the demand signal. Internal maker use has no partner and no demand signal to discount — it is internal operations and R&D, not evidence about outside willingness to pay. Flagging it as "related-party" would imply a partner transaction existed to be skeptical of; instead it sits outside the maker-partner demand comparison entirely. The flag is not an accusation and does not make the engineering work unreal.

## Denominator accounting (v1.1)

38 source records, minus HPR-009 (Ricoh: a service/support relationship, not a deployment site), minus HPR-023 (UBTECH: a company-level batch-delivery milestone with no named operating site), minus the three internal-maker-use rows (HPR-013, HPR-015, HPR-035: no external partner, so no maker-partner demand episode), leaves **33 external maker-partner episodes**. Excluding the seven related-party ties leaves **26 external arm's-length episodes**, the denominator for the strict-conversion result. The internal-use rows remain in the file with `internal_maker_use=TRUE`; they are non-converting by construction (no customer transaction to convert) and are excluded from the demand denominator rather than counted inside it.

## Censoring

An episode that has not converted by the cutoff is not automatically a failure. If a pilot started too recently to reach a six-, twelve-, or eighteen-month horizon, the corresponding outcome is right-censored. If public evidence stops with no confirmation of an ending, the stage is coded from the last verified evidence with follow-up uncertainty marked. Only affirmative contrary evidence supports "discontinued or stalled."

## Coding-decision log (v1.1)

- **Mercado Libre (HPR-008)**: recoded `paid_deployment` → `announced`. The December 2025 release is future-tense ("will integrate"); the partner frames it as testing; no partner-issued or independent evidence of on-site operation at San Antonio by the cutoff. Tier: `commercial_commitment_pending_operation`.
- **Fulin Precision (HPR-031)**: evaluated against the frozen four gates. New evidence: Xinhua Finance, 2025-11-15 (republished by Eastmoney; bylined reporters, Beijing dateline) — journalists visited Fulin's Mianyang smart factory, observed AgiBot A2-W robots working at multiple line positions, and Fulin GM Wang Jun confirmed the deployment to the press. Direct URL of the Xinhua Finance report (republished): https://finance.eastmoney.com/a/202511153565377982.html. Paid August 2025 order for ~100 units (SCMP, independent) → verified operation November 2025 → continuation with co-located teams; no affirmative ending. All four frozen gates pass → tier `qualifying_conversion`. The `delivery_verified=FALSE` coding is a separate v1.1 sensitivity field: the report confirms operation but does not verify delivery of the full ~100-unit scope. That sensitivity is presented in the paper apart from the frozen-rule result; it was not used to move the case.
- **Toyota/TMMC (HPR-007)**: retained as qualifying, with evidence separated by phase. (a) Pre-contract pilot: year-long pilot with 3 Digits (development, proof-of-technology, onsite phases), per TMMC sources; pilot evidence does not verify the contracted rollout. (b) Signed agreement: commercial RaaS agreement signed Feb 19, 2026 (The Robot Report, independent reporting); TMMC president Tim Hollander quoted confirming the Digit deployment decision in TMMC's manufacturing facilities (partner-issued); agreement independently reported (TechCrunch, Forbes). (c) Contracted rollout: April 2026 rollout planned (per Agility, Feb 2026); execution and current on-site operating status evidenced only by Agility Robotics present-tense statements (June 24 and July 14, 2026); no partner-issued or independent source confirmed the April 2026 rollout execution or unit counts by the cutoff. Gate coding: `paid_commitment_verified=TRUE` on (b); `partner_confirmed=TRUE` on (b) (deployment decision, not rollout execution); `on_site_verified=TRUE` and `continued_beyond_evaluation=TRUE` on (c) (maker-issued only, disclosed here); `delivery_verified=TRUE` because the RaaS commitment discloses no unit quantity. `operational_evidence_source=maker-issued`: the contracted rollout's execution rests on Agility statements only. Agility Robotics is the maker and is never treated as partner-side.
- **NEURA 4NE-1 (HPR-027)**: first-evidence URL and date corrected to the NEURA–Bosch partnership report (The Robot Report, 2026-01-16). The prior URL pointed at an unrelated article.
- **Tesla Optimus (HPR-013)**: first-evidence URL verified correct (Electrek, 2026-09-07, "XPeng starts IRON humanoid robot production as Tesla Optimus stalls" — Tesla section covers Optimus at Fremont; date matches). No change.

## Version history

- **v1.0** (September 2026): initial public release. 18 columns. Preserved unchanged.
- **v1.1** (September 26, 2026): recode release. Added `record_id`, gate fields (`paid_commitment_verified`, `on_site_verified`, `partner_confirmed`, `continued_beyond_evaluation`), sensitivity field `delivery_verified`, `conversion_tier`, `related_party`, `related_party_type`, `internal_maker_use` (28 columns). Stage changes: Mercado Libre `paid_deployment` → `announced` (tier `commercial_commitment_pending_operation`). Fulin evaluated against the frozen four gates with new November 2025 evidence → tier `qualifying_conversion`; `delivery_verified=FALSE` recorded as a separate sensitivity (full ~100-unit scope unverified), presented in the paper apart from the frozen-rule result. Toyota evidence separated by phase (pilot / signed agreement / contracted rollout) with maker-only rollout evidence disclosed. NEURA URL/date fix. Denominator recalculated: 33 external maker-partner episodes (internal maker use excluded), 26 external arm's-length after removing seven related-party ties. The frozen four-gate rule is unchanged.
- **v1.1a** (September 26, 2026): evidence-record hardening. Added `pilot_demo_date`, `pilot_demo_evidence_url`, `commitment_date`, `commitment_evidence_url`, `operational_evidence_source`, `last_affirmative_report_date` (34 columns). Gate 4 wording fixed for every case: continuation evaluated as of the last verified report, silence not treated as evidence. `partner_confirmed` narrowed to confirmation of the paid commitment decision; post-commitment operation evidence labeled per case in `operational_evidence_source` (GXO partner+independent; TMMC maker-issued; Fulin independent). GXO outcome windows recomputed from the Dec 6, 2023 pilot start (no paid conversion within 6 months; agreement at ~6.7 months). Xinhua direct URL added to the Fulin evidence record. SOURCES.md added listing primary sources per record.
