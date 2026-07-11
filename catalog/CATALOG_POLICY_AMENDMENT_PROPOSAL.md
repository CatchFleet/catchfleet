# Catalog Policy Amendment Proposal — July 2026

## Status

**APPROVED July 7, 2026 and merged into
`docs/systems/CATALOG_REVIEW_POLICY.md`** (Amendments A, B, C, D). The legacy
fleet threshold is confirmed at **25 airframes**, with one founder
modification: the fleet-threshold arm is a rebuttable presumption, not a
verdict. Documented evidence of regular ADS-B activity rebuts it and keeps
the identity collectible (protects small-but-active fleets such as the 747
Dreamlifter and BelugaXL). This file is kept as the historical proposal
record; the policy document is authoritative. Nothing here changes seed data
by itself; every resulting catalog change still passes the existing review
and seed-gate process.

## Motivation

The June 30, 2026 review pass exposed three structural gaps:

1. The `legacy` decision is currently driven by an unmeasurable intuition
   ("historical, mostly non-primary, non-active"). This has produced
   misclassifications: A340-300 is marked legacy while airframes remain in
   scheduled passenger service, and entire families (A300, A310, A340) were
   swept into legacy as blocks rather than judged per identity.
2. Rarity is coming (M11+ candidate) and risks colliding conceptually with
   legacy unless the boundary is written down before rarity design starts.
3. Non-airplane aircraft (rotorcraft, GA, and beyond) have no defined catalog
   home, and the main Dex's finite-and-completable principle must not absorb
   them by default.

---

## Amendment A — Measurable Legacy Rule

### Rule

A catalog identity receives `catalog_status = legacy` only when **both** hold:

1. **Production has ended** for the identity (no new airframes of the proposed
   collectible identity are being built), **and**
2. **Reasonable catch expectation has ended**, shown by at least one of:
   - the worldwide active/airworthy fleet for the identity is below the
     **legacy fleet threshold** (initial value: **25 airframes**; a tunable
     policy constant, not a per-row judgment call), or
   - the identity has no remaining scheduled commercial service **and** no
     significant cargo, government, or military operator base producing
     regular ADS-B activity.

In plain terms: **legacy means a reasonable station cannot be expected to
catch this identity anymore.** If players' antennas can still realistically
hear it this year, it is collectible, however old the design is.

### Evidence and re-review

- Every `legacy` decision must record, in the review data: the evidence basis
  (fleet estimate or service status), the source label, and a
  `legacy_reviewed_at` date.
- Legacy decisions are re-reviewed at least **annually**, and immediately when
  a review question is raised (e.g. a player catches a supposedly-legacy
  identity repeatedly).
- Families must not be marked legacy as a block. Family-level legacy status is
  only ever the emergent result of every member identity independently meeting
  the rule.

### Promotion and demotion

- Promotion `legacy → collectible` is expected and non-destructive: existing
  catches, Fleet Log records, and unlock history remain valid (per
  `DEX_ENGINE.md`). Promotion increases the primary completion denominator;
  players who already caught the identity gain the unlock via the existing
  re-resolution/unlock path.
- Demotion `collectible → legacy` is allowed on re-review but must never
  delete or invalidate existing unlocks. A demoted identity's existing unlocks
  remain; it simply leaves the primary denominator.

### Expected immediate effect (to be confirmed row by row in re-review)

- Remain legacy without controversy: Concorde, An-225, L-1011 TriStar,
  707-320, 727-200, 737-200, DC-9-30, MD-90, EMB 120, Saab 2000, CRJ100.
- Promotion candidates (evidence check required): A340-300, A340-600,
  A310-300 (tanker/government/cargo activity), A300-600 (freighter fleet is
  large; see the linked freighter-evidence dependency), 717-200 (still in
  scheduled service), MD-11 (active freighter fleet, pending the
  passenger/freighter evidence rule), MD-82/MD-88, Fokker 70/100 (regional
  operators), CRJ200 (active regional/cargo fleet), 737-400 (cargo fleet),
  Dash 8-100/-200, ATR 42-300/72-200 (cargo/regional).

The list above is illustrative for scoping, not a decision. Each row gets its
own evidence and decision in the re-review pass.

---

## Amendment B — Legacy And Rarity Are Different Axes

### Principle

- **Legacy answers: "why can't you catch this?"** It is a completion rule: it
  decides whether an identity belongs to the primary Dex denominator. It lives
  in `catalog_status`.
- **Rarity answers: "how impressive is it that you caught this?"** It is a
  celebration/presentation attribute. It must never change any completion
  numerator or denominator, and it must never live in `catalog_status`.

The two axes are independent: an identity can be collectible and common
(737-800), collectible and rare (C919 heard from Europe), or legacy and a
trophy (a still-flying MD-88). Rarity layers on top of legacy; it never
replaces or modifies it.

### Constraints on future rarity design

1. Rarity is stored as a separate attribute or derived value, never as a
   `catalog_status` value and never as a review `decision`.
2. Rarity must not gate unlocks, eligibility, or completion math.
3. Rarity should ultimately derive from data (share of stations that have
   observed the identity), consistent with the signal-first principle. Until
   the player base is large enough for that to be meaningful, a static curated
   tier derived from global active fleet size is acceptable as Phase 1
   (proposed tiers: `common / uncommon / rare / exotic`).
4. Regional rarity is explicitly deferred; it must not complicate Phase 1.
5. Legacy identities may carry rarity for display, but a legacy catch remains
   outside primary completion regardless of its rarity tier.

---

## Amendment C — Collection Classes (DEFERRED — July 5, 2026)

**Founder decision, July 5, 2026: rotorcraft and general aviation collections
are deferred.** The principle below is recorded so future work starts from an
agreed boundary, but no review pass, no vocabulary change, no schema work, and
no UI work happens now. Until this amendment is activated, out-of-class
catches keep the existing honest path: `resolved_uncatalogued` in Fleet Log —
visible, preserved, counting toward nothing.

### Principle (recorded for future activation)

The Variant Catalog gains a **collection class** dimension. Each class is its
own finite, curated, completable collection with its own denominator. Classes
are presented as separate Dex collections (the folder-tab pattern reserved in
M9), never merged into one unbounded list.

### Initial class vocabulary

- `fleet` — the current main Dex: transport-category and reviewed
  special/military fixed-wing aircraft. Unchanged scope.
- `rotorcraft` — a future curated helicopter collection (candidate first set:
  common civil types with reliable designators, e.g. H125, H135, H145, AW139,
  B429, S-92, R44; exact set requires its own review pass).
- `general_aviation` — a future curated GA collection. Deliberately curated
  and small; the GA universe is effectively infinite and must not be imported
  wholesale.
- Classes with weak or absent 1090 MHz presence (balloons, gliders, UAV) are
  deliberately out of scope until reviewed.

### Rules

1. A collection class is added only through a dedicated review pass under this
   policy; imported typecodes never create a class or its members
   (unchanged principle: evidence, not authority).
2. Every catalog identity belongs to exactly one class. Completion is computed
   per class; there is no cross-class combined denominator.
3. Catches outside every curated class keep the existing honest path:
   `resolved_uncatalogued` in Fleet Log — visible, preserved, counting toward
   no collection, promotable later. This generalizes the "an incomplete catch
   should feel unfinished, not wasted" principle to vehicle classes.
4. The existing `category` field (Passenger Jet, Military, …) remains a data
   attribute inside a class and is still not a collection.

---

## Amendment D — Family Integrity At Seed Time

Two clarifications prompted by the 737 family drift found in production:

1. **Seeded hierarchy must match reviewed hierarchy.** A seed migration must
   not assign a variant to a family other than the one recorded in the
   review data. If the desired family structure changes, the review data
   changes first, then the seed.
2. **Generation-based family exceptions must be written down.** If a
   generation split (e.g. 737 Original/Classic/NG/MAX) is kept, the
   player-facing rationale is documented in the review data; if the default
   single-platform family is kept (e.g. one "737 Family"), all member
   variants use it consistently. Mixed states are a seed-gate failure.

---

## Decisions Recorded (July 5, 2026)

- **737 families: single `737 Family`** (policy default, Option 1). All 737
  variants — Original, Classic, NG, and MAX generations, collectible and
  legacy — live under one `737 Family`. Generation remains available as a
  variant attribute/label, never as a family. Feeds backlog item 1.
- **Collection classes (rotorcraft, general aviation): deferred.** See
  Amendment C above; recorded for future activation, no work now.
- **Rarity tiers: `common / uncommon / rare / unicorn`,** with the Phase 1
  fleet bands (>=1000 / 200–999 / 25–199 / <25-and-active) and the bounded
  one-step curator adjustment. Every cataloged type carries a tier (no null);
  weak evidence is recorded as low confidence in review data, with a
  tie-break toward the more common band. Regional rarity confirmed deferred.
  Full rules in `RARITY_DESIGN_NOTE.md`, which supersedes the tier naming in
  Amendment B's constraint 3.

## Open Questions For Founder Decision (all resolved)

1. Legacy fleet threshold: is 25 airframes the right initial constant?
   **RESOLVED July 7, 2026: confirmed at 25** (see Status above), with the
   rebuttable-presumption modification. Note kept for the record: the
   approved rarity bands use the same 25 boundary by design (below 25 and
   retired → legacy; below 25 and active → unicorn), so changing this
   constant later moves both.
