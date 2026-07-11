# Catalog Review Policy

## Purpose

This document defines the review policy for deciding which aircraft catalog
candidates are eligible to become seed data.

Catalog review is a deliberate human decision process. Imported metadata,
prototype data, and resolver evidence may inform review, but they must not
silently define the collectible catalog.

## Variant Catalog And Aircraft Database

The Variant Catalog and Aircraft Database serve different purposes.

### Variant Catalog

The Variant Catalog defines curated collectible identities.

Examples:

```txt
Airbus A320neo
Boeing 737-800
ATR 72-600
```

Catalog identities are finite gameplay entries organized by manufacturer,
family, and variant.

## Aircraft Family Taxonomy

An aircraft family represents a player-recognizable aircraft platform or
established product line used to organize the Dex.

Family review must follow these rules:

- Generation labels such as Original, Classic, NG, MAX, and neo do not create
  separate families by default.
- Roles and categories such as Freighter, Cargo, Special, Military, and
  Passenger do not create separate families by default.
- A family must not merely repeat the manufacturer and group otherwise
  unrelated products.
- One-variant families are valid for standalone or expandable platforms.
- Generation-based exceptions require a documented player-facing rationale.
  If the default single-platform family is kept instead, all member variants
  use it consistently; mixed generation states are a seed-gate failure.
- Review must check for duplicate platform concepts elsewhere under the same
  manufacturer before creating a family.
- Changing a variant's family must not change its resolver aliases or canonical
  variant identity.
- A seed migration must not assign a variant to a family other than the one
  recorded in the review data. If the desired family structure changes, the
  review data changes first, then the seed.

Generation, role, category, engine, and marketing information may remain useful
variant attributes or labels without becoming separate hierarchy levels.

### Aircraft Database

The Aircraft Database stores physical aircraft identified by ICAO hex.

It may include:

- Registration
- Operator
- Manufacturer or model text
- Source-specific type information
- Aircraft-level role or conversion information

Aircraft metadata may provide evidence for resolving a physical aircraft to a
catalog variant. It must not automatically create new catalog variants.

OpenSky or other imported physical-aircraft metadata is evidence, not catalog
authority.

## Category And Catalog Status

`category` describes what kind of aircraft the candidate is.

The initial controlled values are:

- `Passenger Jet`
- `Passenger Turboprop`
- `Cargo Jet`
- `Business Jet`
- `Military`
- `Special`

`legacy` is not a category.

`catalog_status` describes how a valid catalog identity participates in the
Dex:

- `collectible`: included in primary Dex completion
- `legacy`: valid aircraft identity excluded from primary Dex completion

For example, a Boeing 727-200 may have:

```txt
category: Passenger Jet
catalog_status: legacy
```

### Reference-Only And Excluded (M2)

`catalog_status` values `collectible` and `legacy` apply only to curated
catalog identities. They are not the only resolver/catalog outcomes.

Imported reference entities can remain `reference_only` / uncatalogued /
unreviewed.

`reference_only` and `resolved_uncatalogued` may appear in the M2
resolver/catalog outcome vocabulary, but they are not seeded Dex catalog
statuses:

- `reference_only`: the resolver may know an entity that is not a curated
  catalog identity.
- `resolved_uncatalogued`: a referenced entity was identified but has not been
  promoted into the curated catalog.

Neither counts toward the Dex.

Promotion of a reference entity to `collectible` or `legacy` is a curated,
future-facing decision under this policy. It does not happen automatically on
import.

`excluded` is distinct from `reference_only`: excluded means intentionally
blocked, invalid, or out of scope, and must never count. See the identity
states in `engines/RESOLVER_ENGINE.md`.

## Shared ICAO Type Codes

An ICAO type designator may be broader than the proposed collectible
identities.

If the same ICAO type code can map to multiple candidate variants, it must not
directly unlock all of them.

The review may allow the coarse or default variant to use the type code as an
alias only when that mapping is explicit and does not create an alias
collision. More specific variants require aircraft-level evidence.

Examples:

- `A21N` may indicate A321neo, A321LR, or A321XLR.
- `B739` may indicate 737-900 or 737-900ER.
- `B772` may indicate 777-200 or 777-200ER.

For these cases:

- One normalized alias must not point to multiple variants.
- A coarse type-code match must not unlock every candidate.
- Specific variants require model evidence tied to the physical aircraft.
- If reliable disambiguation is unavailable, the candidate should be renamed,
  merged, or deferred.

## Passenger And Freighter Ambiguity

Some passenger and freighter aircraft share the same ICAO type designator.

Examples include:

- `A332`: A330-200 and A330-200F
- `B738`: 737-800 and 737-800BCF
- `B744`: 747-400 and 747-400F
- `B748`: 747-8 Intercontinental and 747-8F
- `B752`: passenger and freighter 757-200 aircraft
- `B763`: passenger and freighter 767-300 aircraft
- `DC10`: passenger, freighter, converted, and tanker DC-10 histories
- `MD11`: passenger, freighter, and converted MD-11 histories

These shared codes must not automatically unlock a freighter or converted
freighter variant.

A freighter variant requires aircraft-level evidence such as:

- A verified physical-aircraft model
- A known role
- A known conversion status
- A sufficiently specific trusted source record

Type code alone is not sufficient when the proposed catalog identity includes
freighter role or conversion status. Coarse shared codes such as `DC10` and
`MD11` must not be seeded as direct aliases for specific passenger or freighter
variants without aircraft-level evidence.

## Broad Business Jet Designators

Some business jet designators span multiple marketed models or derivatives.

Examples include:

- `GLF4`
- `GLF5`
- `CL60`
- `GLEX`
- `F2TH`

These designators may be too coarse for specific model-level resolution. A
candidate using one of these codes should take one of three paths:

1. Become a series-level collectible that matches the available evidence.
2. Require aircraft-level model evidence before resolution and unlock.
3. Be deferred until reliable disambiguation is available.

A broad designator must not be presented as proof of a more specific marketed
model.

## Military Aircraft

Military aircraft are allowed in the Variant Catalog.

Military candidates may be approved when they have:

- Strong gameplay value
- Realistic signal-backed catch potential
- A useful and sufficiently specific resolver identity
- A type designator that does not imply unsupported model certainty

Transport, tanker, and special-mission aircraft are generally better early
catalog candidates than broad fighter-family identities because their
designators are often more specific and their signal-backed resolver coverage
is easier to explain.

A military category is not itself a reason to defer a candidate. Broad or
family-level military designators should still be renamed, deferred, merged, or
split when they cannot safely support the proposed identity.

## Main Dex Completion

Primary Dex completion includes only variants with:

```txt
catalog_status = collectible
```

Legacy aircraft remain valid identities. They may still appear in:

- Fleet Log
- Aircraft detail pages
- Legacy or special catalog views
- Future achievements
- Future activity or rarity features

Legacy variants do not count toward primary Dex completion.

## Legacy Rule

Approved July 7, 2026 (Amendment A). A catalog identity receives
`catalog_status = legacy` only when **both** hold:

1. **Production has ended** for the identity: no new airframes of the
   proposed collectible identity are being built, and
2. **Reasonable catch expectation has ended**, shown by at least one of:
   - the worldwide active/airworthy fleet for the identity is below the
     **legacy fleet threshold** (policy constant: **25 airframes**), or
   - the identity has no remaining scheduled commercial service **and** no
     significant cargo, government, or military operator base producing
     regular ADS-B activity.

The fleet threshold is a rebuttable presumption, not a verdict: documented
evidence of regular ADS-B activity (daily production-support flights, active
government or military operations, scheduled niche service) rebuts it and
keeps the identity collectible. Small-but-active fleets such as the 747
Dreamlifter or BelugaXL stay collectible under this reading. The constant
deliberately matches the Phase 1 rarity band boundary: below 25 and still
active is unicorn territory, not legacy.

In plain terms: legacy means a reasonable station cannot be expected to catch
this identity anymore. If players' antennas can still realistically hear it
this year, it is collectible, however old the design is.

### Evidence and re-review

- Every `legacy` decision must record, in the review data: the evidence basis
  (fleet estimate or service status), the source label, and a
  `legacy_reviewed_at` date.
- Legacy decisions are re-reviewed at least annually, and immediately when a
  review question is raised (for example a player repeatedly catching a
  supposedly-legacy identity).
- Families must not be marked legacy as a block. Family-level legacy status
  is only ever the emergent result of every member identity independently
  meeting the rule.

### Promotion and demotion

- Promotion `legacy -> collectible` is expected and non-destructive: existing
  catches, Fleet Log records, and unlock history remain valid (per
  `DEX_ENGINE.md`). Promotion increases the primary completion denominator;
  players who already caught the identity gain the unlock via the existing
  re-resolution/unlock path.
- Demotion `collectible -> legacy` is allowed on re-review but must never
  delete or invalidate existing unlocks. A demoted identity's existing
  unlocks remain; it simply leaves the primary denominator.

## Legacy And Rarity Are Different Axes

Approved July 7, 2026 (Amendment B).

- **Legacy answers: "why can't you catch this?"** It is a completion rule: it
  decides whether an identity belongs to the primary Dex denominator. It
  lives in `catalog_status`.
- **Rarity answers: "how impressive is it that you caught this?"** It is a
  celebration/presentation attribute. It must never change any completion
  numerator or denominator, and it must never live in `catalog_status`.

The two axes are independent: an identity can be collectible and common
(737-800), collectible and rare (C919 heard from Europe), or legacy and a
trophy (a still-flying MD-88). Rarity layers on top of legacy; it never
replaces or modifies it.

Constraints on rarity design (full rules in
`docs/design-notes/RARITY_DESIGN_NOTE.md`; Phase 1 shipped in M11 as
`aircraft_variants.rarity_tier`, migration
`20260707150000_rarity_phase1_tiers.sql`):

1. Rarity is stored as a separate attribute or derived value, never as a
   `catalog_status` value and never as a review `decision`.
2. Rarity must not gate unlocks, eligibility, or completion math.
3. Rarity should ultimately derive from data (share of stations that have
   observed the identity). Until the player base is large enough for that to
   be meaningful, the static curated Phase 1 tiers apply:
   `common / uncommon / rare / unicorn` with fleet bands
   >=1000 / 200-999 / 25-199 / below-25-and-active. Every cataloged type
   carries a tier (no null); weak evidence is recorded as low confidence
   with a tie-break toward the more common band.
4. Regional rarity is explicitly deferred; it must not complicate Phase 1.
5. Legacy identities may carry rarity for display, but a legacy catch remains
   outside primary completion regardless of its rarity tier.

## Collection Classes (Deferred)

Founder decision, July 5, 2026: rotorcraft and general aviation collections
are deferred (Amendment C). The boundary is recorded so future work starts
from an agreed principle, but no review pass, no vocabulary change, no schema
work, and no UI work happens now. Until activation, out-of-class catches keep
the existing honest path: `resolved_uncatalogued` in Fleet Log, visible,
preserved, counting toward nothing.

Recorded principle: the Variant Catalog gains a collection class dimension
(`fleet` / `rotorcraft` / `general_aviation`); each class is its own finite,
curated, completable collection with its own denominator, added only through
a dedicated review pass under this policy. Every catalog identity belongs to
exactly one class; there is no cross-class combined denominator. The existing
`category` field remains a data attribute inside a class and is still not a
collection.

## Review Decisions

Each catalog review row must have one documented decision.

### `needs_review`

The candidate has not completed review. It is not eligible for seed data.

### `approved`

The candidate identity, hierarchy, category, catalog status, evidence rules,
and aliases have been accepted. An approved row is eligible for seed migration
only after normalization and alias collision checks pass.

### `legacy`

The candidate is accepted as a valid catalog identity with
`catalog_status = legacy`. It is excluded from primary Dex completion.

This is a review decision, not an aircraft category. A `legacy` decision is
eligible for catalog seed migration after the same normalization, collision,
and seed-gate checks required for an approved row.

Legacy rows must be seeded so resolved aircraft can use the identity in Fleet
Log, aircraft detail pages, Legacy or Special views, and future achievements.

### `defer`

The candidate may be valid, but available evidence or product policy is not
sufficient for a current decision. It is not eligible for seed data.

### `rename`

The proposed identity is useful, but its manufacturer, family, variant name,
or collectible granularity must change before approval.

### `split`

The candidate combines multiple identities that should be reviewed as separate
catalog variants.

### `merge`

Multiple candidates are too granular or cannot be reliably distinguished and
should become one catalog identity.

### `reject`

The candidate should not become a catalog variant. Examples may include
duplicate identities, source artifacts, customer codes, or identities that do
not fit the collectible boundary.

Rows with `decision = approved` or `decision = legacy` are eligible for catalog
seed migration. Eligibility alone is not enough: alias collision,
normalization, and all other seed-gate checks must also pass.

Rows with `decision = defer`, `rename`, `merge`, `split`, `reject`, or
`needs_review` are not seed-eligible.

## Seed Gate

Before any catalog seed migration:

1. Every seeded row must have a documented review decision.
2. Every seeded row must have `decision = approved` or `decision = legacy`.
3. Rows with `decision = defer`, `rename`, `merge`, `split`, `reject`, or
   `needs_review` must not be seeded.
4. Alias normalization collisions must be checked.
5. Normalized aliases must map to no more than one canonical variant.
6. Shared-code mappings must have explicit resolver behavior.
7. Passenger, freighter, and conversion ambiguity must be handled explicitly.
8. Broad business jet mappings must use an approved series-level boundary or
   require aircraft-level evidence.
9. Approved and legacy catalog rows must remain separate from physical-aircraft
   imports.
10. Aircraft Database imports must not create manufacturers, families,
    variants, or aliases without catalog review.
11. Primary Dex completion queries must count only rows with
    `catalog_status = collectible`; seeded legacy rows remain valid identities
    but do not increase the primary completion denominator.
12. The seeded manufacturer/family/variant hierarchy must match the reviewed
    hierarchy exactly. Family drift (a variant seeded into a family other
    than the reviewed one, or a mixed generation-family state) is a seed-gate
    failure.

If any gate fails, the affected row must not be included in the seed migration.
