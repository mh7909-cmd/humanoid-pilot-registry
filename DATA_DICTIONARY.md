# Data Dictionary: Humanoid Pilot Registry v1.0

Scope: publicly reported industrial humanoid work in manufacturing and logistics, 2023 through the cutoff date of September 20, 2026. The unit of analysis is a maker-model-partner-site episode, dated from the earliest credible public evidence of an industrial evaluation, pilot, or deployment involving a specific maker and operating partner or site. A materially different model or project at the same partner becomes a new record (Figure 02 at BMW Spartanburg and the later Figure 03 evaluation are separate episodes).

A record was included when public evidence identified a humanoid or humanoid-like general-purpose robot, industrial work in scope, and an operating organization or a clearly labeled company-level milestone. The robot need not be bipedal (the AgiBot A2-W is wheeled, kept with that caveat). Excluded: investor relationships with no operating deployment, pure laboratory research, entertainment demonstrations, and consumer/home use.

Unknown quantities were left blank. Payment was not inferred from the word "partnership," scale was not inferred from a production target, and continuation was not inferred from the absence of a cancellation notice. Every row carries at least one source URL; load-bearing status decisions favor partner-side or independent evidence.

## Columns

- `company` - the robot maker.
- `robot_model` - the specific model deployed or evaluated.
- `deployment_partner_site` - the operating partner and site, or a company-level milestone where no single site is named.
- `sector` - the partner's industry (e.g., automotive manufacturing, logistics).
- `country` - deployment country, with state or region where relevant.
- `first_public_evidence_date` - earliest credible public evidence of the episode. Dates are as precise as the sources allow; a month-only date stays month-level.
- `first_evidence_url` - URL of the source establishing the record.
- `source_quality_tier` - tier of the record's key evidence (see Source quality tiers below).
- `current_stage` - furthest verified stage at the cutoff (see Stage ontology below).
- `stage_evidence` - the evidence supporting the stage coding.
- `fleet_size` - observed or claimed number of units, with the claim's source noted. Vendor-only fleet claims are labeled as such.
- `tasks` - the industrial task(s) the robot performed.
- `hours_throughput_claims` - published operating metrics (hours, throughput, success rates), attributed to their source.
- `human_oversight` - evidence on supervision or human support, where reported.
- `outcome_6mo`, `outcome_12mo`, `outcome_18mo` - status at each horizon after episode start. Blank where the horizon is not yet reachable or follow-up evidence does not exist (see Censoring below). Where a source reported a range, elapsed time is shown as an interval rather than a falsely exact count.
- `notes_conflicts` - source conflicts, caveats, and the related-party flag (see below). Conflicts are recorded rather than collapsed into an unqualified number.

## Stage ontology

The stage field records the furthest verified stage at the cutoff. These labels describe evidence, not an inevitable ladder; a project may skip a reported stage.

1. `announced` - a future partnership, test, order, or intended deployment is public, but on-site operation is not verified.
2. `testing` - the system is being evaluated in a lab, innovation center, maker facility, or controlled customer setting short of a live operating pilot.
3. `pilot_on_site` - the robot has performed the stated task at a real partner facility, with no qualifying paid continuation established.
4. `paid_deployment` - a named operating customer has a formal paid commitment beyond a short evaluation. RaaS contracts and partner-confirmed purchase orders can qualify, with delivery caveats recorded.
5. `scaled_fleet` - multiple units or sites operate beyond an initial deployment, supported by strong evidence of continuing commercial use. Vendor-only fleet claims are labeled as such.
6. `discontinued_stalled` - affirmative evidence shows that the project ended, robots were removed, the task reverted, or a planned program did not proceed.

Commercial deployment is defined narrowly in the paper: a named operating customer, an industrial task at a real site, and partner-confirmed consideration or a formal paid commitment beyond a time-limited evaluation.

## Source quality tiers

Four tiers, in order of weight for load-bearing status decisions:

- `partner_statement` - a release, filing, newsroom item, or direct statement from the organization operating the robot. Carries the most weight on site, task, quantity, payment, and continuation.
- `independent_reporting` - an established outlet or specialist publication that identifies evidence rather than simply reproducing a release.
- `press_release` - an announcement release, used for dates and stated intent; does not by itself confirm customer use.
- `vendor_claim` - from the robot maker. Useful for specifications, intent, and maker-side milestones, but does not independently confirm customer use.

The paper additionally describes a lead tier: a source that points toward a case but is not sufficient for a load-bearing decision. Lead-tier material did not qualify rows for the frozen registry on its own.

## Related-party flag

A pilot is flagged in `notes_conflicts` when the customer or deployment partner also has a material relationship with the maker: investment, ownership, common corporate control, contract manufacturing, or a comparable strategic tie. Seven such structures are identified in the registry: Mercedes-Benz-Apptronik, Schaeffler-Agility, Magna-Sanctuary AI, EQT-1X, Hyundai-Boston Dynamics, POSCO-Persona AI, and CATL-Galbot.

The flag is not an accusation and does not make the engineering work unreal. It answers a narrower question: how independent is the evidence of outside demand? The paper's main conversion outcome uses arm's-length, partner-confirmed events, with the full maker-partner set shown alongside.

## Censoring and outcome windows

The cutoff is September 20, 2026. An episode that has not converted by that date is not automatically a failure. If a pilot started too recently to reach a six-, twelve-, or eighteen-month horizon, the corresponding outcome is right-censored. If public evidence stops while no source confirms an ending, the stage is coded from the last verified evidence with follow-up uncertainty noted. Only affirmative contrary evidence supports `discontinued_stalled`.

Only about eight older pilots had the full outcome windows at risk with useful public follow-up, so the paper reports counts and observed event times rather than a pseudo-precise conversion percentage.
