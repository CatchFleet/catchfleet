# Fleet Dex Catalog Review Draft

## Status

This is a human-review-only catalog draft. It is not seed data and it is not
an executable catalog seed.

- The CSV contains 171 candidate aircraft variants after the July 7, 2026
  Wave A rename pass.
- The first catalog decision pass is complete.
- Every row now has an explicit review decision.
- An `approved` or `legacy` decision does not authorize seeding by itself.
- Source labels provide a traceable review starting point. They do not establish
  legal certainty, licensing rights, or guaranteed factual completeness.
- The prototype catalog is used only as a sanity check for omissions and naming
  differences. It is not a source of truth.

The row-level review data is maintained in
`aircraft_variant_catalog_review.csv`.

## First Decision Pass

The first decision pass produced:

| Decision | Rows |
| --- | ---: |
| `approved` | 70 |
| `legacy` | 32 |
| `defer` | 26 |
| `rename` | 19 |
| `merge` | 3 |
| `split` | 2 |
| `reject` | 0 |
| `needs_review` | 0 |
| **Total** | **152** |

The July 7, 2026 legacy re-review (see below) later moved 14 of the 32
legacy rows to `approved`. The July 7, 2026 Wave A rename pass added 19
approved series-level rows, so the current CSV totals are 103 approved and 18
legacy.

The pass approves clean, currently useful identities while preserving honest
uncertainty elsewhere:

- Common current passenger, regional, turboprop, and cleanly identified special
  aircraft form the approved M0 core.
- Selected military transports, tankers, special-mission aircraft, and other
  resolver-safe military identities are intentionally allowed. Broad
  family-level military rows still require rename or defer.
- Business jets are approved only where the designator is reasonably
  model-specific. Broad codes such as `GLEX`, `CL60`, `GLF4`, `GLF5`, and
  `F2TH` remain rename candidates rather than specific approved models.
- Historical, mostly non-primary, and non-active identities are accepted as
  `legacy`. These rows are seed-eligible valid identities but remain excluded
  from primary Dex completion.
- Shared passenger/freighter codes and candidates requiring unimplemented
  aircraft-level evidence are deferred.
- Broad or unstable manufacturer, series, and model names require rename.
- `737-900 / 737-900ER` is approved as one combined resolver-safe identity
  because `B739` cannot distinguish the two in all cases. `777-200` /
  `777-200ER` and ERJ-140 still require merge work before they can become
  resolver-safe identities.
- Beechcraft 1900 and L-410 Turbolet require split review because the current
  rows span multiple subvariants.

The resulting catalog-status proposal is:

| Catalog status | Rows |
| --- | ---: |
| `collectible` | 153 |
| `legacy` | 18 |
| **Total** | **171** |

The current review-file normalization check finds no alias collisions, including
among approved and legacy rows. This is a draft check only. Production
normalization, shared-code resolver rules, and the full seed gate must still
pass before any approved or legacy row becomes seed data.

## Legacy Re-Review (July 7, 2026)

All 32 legacy rows were re-reviewed under the measurable legacy rule
(`CATALOG_REVIEW_POLICY.md`: production ended AND catch expectation ended;
fleet threshold 25 as a rebuttable presumption). Founder approved the full
pass on July 7, 2026. The CSV gained two columns: `legacy_evidence` (evidence
basis and source label) and `legacy_reviewed_at`.

- **14 rows promoted `legacy -> collectible`:** 717-200, 737-400, CRJ200,
  Fokker 100, Fokker 50, A340-300, A340-600, A310-300, A300-600, 747-400,
  Dash 8-100, Dash 8-200, ATR 42-300, ATR 72-200. Each has documented
  regular ADS-B activity (scheduled, cargo, or government service).
  Promotions are non-destructive: existing catches and unlock history remain
  valid, and the primary completion denominator grows.
- **18 rows confirmed legacy**, six of them recorded as borderline (A318,
  737-600, 737-200, MD-82, EMB 120 Brasilia, Fokker 70) to be revisited with
  real player catch data at the next re-review in a few months.
- Passenger/freighter splits are unchanged: MD-11, DC-10-30, and 747-400
  passenger identities were judged on passenger fleets only; freighter
  identities remain their own deferred rows.

## Wave A Rename Pass (July 7, 2026)

Founder approved the Wave A rename pass documented in
`docs/archive/WAVE_A_CATALOG_IMPLEMENTATION.md`. The pass keeps the 19 original
`rename` rows as review history and adds 19 new approved, collectible
series-level identities whose granularity matches their available type
designator evidence.

The Wave A rows intentionally use series-level names for broad designators
such as GLF4, GLF5, CL60, GLEX, and F2TH. Manufacturer decisions are recorded
in the CSV: Avro, Dornier, Lockheed Martin for F-16, and Canadair for CL-415.
C-130J remains out of scope for this wave.

## Catalog Boundary

The Variant Catalog is separate from the Aircraft Database.

- The Variant Catalog defines finite canonical collectible identities such as
  `737-800`, `A321LR`, or `ATR 72-600`.
- The Aircraft Database identifies physical aircraft by ICAO24/Mode-S hex and
  may contain registration, operator, owner, and source-specific model text.
- OpenSky aircraft metadata must not create Variant Catalog records.
- Imported physical-aircraft metadata may provide resolver evidence, but
  catalog membership requires an explicit human-reviewed decision.
- Customer codes, engine options, conversions, and source-specific model names
  may become aliases or aircraft metadata. They must not automatically become
  separate collectible variants.

## First 151 Scope

The First 151 is a deliberately game-oriented review set rather than an
encyclopedic aircraft list. It combines:

- A strong base of common current passenger aircraft
- Passenger turboprops needed for regional coverage
- Common and iconic freighters
- Recognizable business jets
- A limited military and special-mission sample
- Iconic legacy aircraft with high gameplay value
- Resolver edge cases where ICAO type codes are broader than proposed Dex
  variants

The draft avoids obscure one-off aircraft unless the row provides a useful
identity, alias, or catalog-boundary test.

## Category Vocabulary

The CSV uses only this initial controlled vocabulary:

| Category | Rows | Intended review meaning |
| --- | ---: | --- |
| Passenger Jet | 90 | Passenger aircraft primarily powered by jet engines, including candidates with legacy catalog status |
| Passenger Turboprop | 19 | Regional or commuter passenger turboprops |
| Cargo Jet | 10 | Dedicated or converted jet freighter candidates |
| Business Jet | 30 | Purpose-built business-aviation jet candidates |
| Military | 15 | Military transports, tankers, surveillance aircraft, and fighters |
| Special | 7 | Distinctive special-purpose aircraft that do not fit ordinary cargo or military grouping |
| **Total** | **171** | |

`category` describes the aircraft candidate. `catalog_status` separately
describes whether the candidate is proposed as `collectible` or `legacy`.
Legacy is not a category. Historical passenger aircraft remain categorized as
`Passenger Jet`, while `catalog_status = legacy` expresses their catalog
treatment. Both fields remain subject to review.

## Manufacturer Coverage

| Manufacturer | Rows |
| --- | ---: |
| Boeing | 38 |
| Airbus | 27 |
| Bombardier | 11 |
| Cessna | 11 |
| Embraer | 11 |
| Gulfstream | 8 |
| McDonnell Douglas | 8 |
| ATR | 6 |
| Lockheed Martin | 6 |
| Dassault | 5 |
| De Havilland Canada | 4 |
| Dornier | 4 |
| Antonov | 3 |
| COMAC | 3 |
| Fokker | 3 |
| Avro | 2 |
| BAe / Avro | 2 |
| Canadair | 2 |
| Saab | 2 |
| Sukhoi | 2 |
| Tupolev | 2 |
| Aerospatiale / BAC | 1 |
| Air Tractor | 1 |
| Beechcraft | 1 |
| Eurofighter | 1 |
| General Dynamics | 1 |
| Ilyushin | 1 |
| LET | 1 |
| Lockheed | 1 |
| Northrop Grumman | 1 |
| Xian | 1 |
| Yakovlev | 1 |
| **Total** | **171** |

Bombardier is the canonical manufacturer candidate for CRJ rows. Mitsubishi's
program-support history is recorded in `review_notes` rather than being joined
into the manufacturer name.

## CSV Columns

Each row contains:

1. `manufacturer`
2. `family`
3. `variant_name`
4. `icao_type_codes`
5. `aliases`
6. `category`
7. `catalog_status`
8. `sources`
9. `confidence`
10. `decision_reason`
11. `decision`
12. `review_notes`

Multiple candidate ICAO designators or aliases are separated with `|`.
`icao_type_codes` is intentionally plural because one proposed collectible may
map to multiple designators, and one designator may also be too coarse to
distinguish multiple proposed collectibles.

## Source Labels

The CSV uses conservative labels such as:

- `ICAO Doc 8643 lookup`: ICAO's
  [Aircraft Type Designators search](https://www.icao.int/operational-safety/doc-8643-aircraft-type-designators/search)
- Manufacturer `product pages`
- Manufacturer `history pages`
- `independent aviation reference review`
- `manufacturer and museum history pages`
- `prototype catalog sanity check`

The `prototype catalog sanity check` label means only that the existing
prototype list was checked for omissions, naming differences, or regressions.
It is never the sole authority for a candidate.

Before seed creation, reviewers should verify each accepted row against the
current source record and separately assess any attribution or licensing
requirements.

## Pre-Decision-Pass Fixes

The draft removes coarse shared type codes from direct aliases where they
would collide across proposed passenger and freighter variants:

- `DC10` remains informational in `icao_type_codes` for DC-10F and DC-10-30,
  but is not a direct alias for either candidate.
- `MD11` remains informational in `icao_type_codes` for MD-11 and MD-11F, but
  is not a direct alias for either candidate.
- ERJ-140 does not use `E135` as a direct alias. Its ICAO mapping must be
  externally verified, then merged or deferred if it cannot be distinguished
  safely from ERJ-135.
- A legacy passenger MD-11 candidate replaces the cancelled SpaceJet M90
  candidate, keeping the original First 151 review set at 151 rows. (The CSV
  now holds 152 rows after the June 30, 2026 Identity Review alpha expansion.)
- An-225 Mriya remains `Special` but now has `catalog_status = legacy` because
  no active airframe exists.

Coarse shared type codes such as `DC10` and `MD11` must not directly unlock a
specific passenger or freighter variant. Aircraft-level model, role,
conversion, or historical evidence is required.

## Notable Ambiguous Mappings

### A321neo, A321LR, and A321XLR

All three candidates use `A21N`. The draft keeps them as separate review
candidates because they have meaningful gameplay identities, but ICAO type code
alone cannot distinguish them. The baseline A321neo row is approved and owns
the direct `A21N` alias. A321LR and A321XLR remain deferred, do not carry
`A21N` as a direct alias, and require verified aircraft-level model evidence
before resolution or unlock.

### 737-900 and 737-900ER

Both candidates use `B739`. The June 30, 2026 Identity Review alpha expansion
approves one combined `737-900 / 737-900ER` row because typecode evidence
cannot safely distinguish 737-900 from 737-900ER in all cases. Exactly one row
may own the normalized direct alias `b739`; separate 737-900 and 737-900ER
variants must not be seeded without future aircraft-level model evidence and a
new catalog review.

### 777-300 and 777-300ER

`777-300` and `777-300ER` remain separate approved catalog identities because
their direct ICAO type designators are distinct: `B773` and `B77W`. This is
different from `B739`, where one designator spans the combined 737-900 /
737-900ER identity.

### 777-200 and 777-200ER

Both candidates use `B772`. Aircraft-level model evidence is required if they
remain separate collectibles. Both rows are marked `merge` for the M0 catalog
pass.

### E175

The E175 row carries `E75L|E75S`, representing long-wing and short-wing
configurations. The first pass approves one canonical E175 collectible spanning
both designators; normalization must preserve that one-to-one catalog mapping.

### Citation CJ2 and CJ2+

`C25A` is approved as one combined `Citation CJ2 / CJ2+` identity. The catalog
does not approve CJ3 / `C25B` as part of this decision. Direct aliases that
would normalize to the same value, such as separate `Citation CJ2` and
`Citation CJ2+` strings, should not both be seeded; the direct typecode plus
combined display aliases provide the resolver-safe mapping.

### Embraer Legacy 600/650

`E35L` is approved as a new Embraer `Legacy Family` business jet identity:
`Legacy 600/650`. It is not an ERJ-145 or `E145` alias, even though the
aircraft lineage is related.

### Boeing 737-400

`B734` is accepted as `legacy` under the single Boeing `737 Family` (the
July 5, 2026 catalog decision merged all 737 generations into one family).
It is a valid resolver identity but remains excluded from primary Dex
completion.

### Dash 8-400 / Q400

`DH8D` appears with Dash 8-400, DHC-8-400, DHC-8-Q400, and Q400 naming. The
first pass approves one Dash 8-400 candidate and preserves the other names as
aliases.

### Passenger and Freighter Roles

Several ICAO designators do not encode role or conversion status:

- `A306`: passenger A300-600 and A300-600F
- `A332`: passenger A330-200 and A330-200F
- `B738`: passenger 737-800 and 737-800BCF
- `B744`: passenger 747-400 and 747-400F
- `B748`: 747-8 Intercontinental and 747-8F
- `B752`: passenger and freighter 757-200 aircraft
- `B763`: passenger and freighter 767-300 aircraft
- `MD11` and `DC10`: historical passenger, freighter, and converted roles

These shared designators must never automatically unlock a cargo or freighter
variant from type code alone. The resolver must require aircraft-level model,
role, or conversion evidence when the proposed Dex identity includes freighter
status.

### Broad Business-Jet Codes

Codes such as `C56X`, `CL60`, `GLEX`, `GLF4`, `GLF5`, and `F2TH` may span
multiple marketed models or derivatives. A reviewer must either rename an
overly specific candidate to a series-level identity or require aircraft-level
model evidence. The broad designator alone must not resolve a specific marketed
model.

## Review Questions

Review each CSV row for:

1. Is the manufacturer and family hierarchy canonical enough for M0?
2. Is the proposed variant the correct lowest collectible boundary?
3. Can the proposed identity be resolved safely from the listed evidence?
4. Does an ICAO designator cover multiple proposed variants or roles?
5. Are aliases overly broad, ambiguous, customer-specific, or
   source-specific?
6. Is the category correct under the initial controlled vocabulary?
7. Should `catalog_status` be `collectible`, `legacy`, or deferred?
8. Are the source labels sufficient and independently verified?
9. Should the candidate remain in the First 151?

## Seed Gate

The draft contains 84 approved and 18 legacy seed-eligible decisions (after
the July 7, 2026 legacy re-review pass), but none are seed data yet. Before any database seed is created:

1. The production alias-normalization implementation must be run against all
   approved and legacy aliases and must report no collisions.
2. Ambiguous type-code mappings must have explicit resolver behavior,
   especially approved passenger defaults that share codes with deferred
   freighter candidates.
3. Current ICAO and manufacturer source records must be rechecked for approved
   rows.
4. All `rename`, `merge`, and `split` work must produce new reviewable rows
   before those candidates can be reconsidered.
5. Deferred rows must remain out of M0 seed data until their stated evidence or
   resolver dependency exists.
6. Legacy rows must be seeded with `catalog_status = legacy` so they remain
   available to Fleet Log, aircraft detail pages, Legacy or Special views, and
   future achievements.
7. Primary Dex completion must count only rows with
   `catalog_status = collectible`.
8. Rows marked `defer`, `rename`, `merge`, `split`, `reject`, or
   `needs_review` must not be seeded.
9. The reviewed catalog must remain separate from imported physical-aircraft
   metadata.
