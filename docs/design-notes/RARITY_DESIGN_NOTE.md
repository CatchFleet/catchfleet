# Rarity Design Note — Phase 1

## Status

Approved direction, July 5, 2026 (tier vocabulary and Phase 1 bands decided
by founder). **Phase 1 is IMPLEMENTED and live since M11 (deployed July 8,
2026):** tiers seeded by migration `20260707150000_rarity_phase1_tiers.sql`,
presentation rules in `docs/DESIGN_LANGUAGE.md` ("Rarity presentation"),
policy boundary merged into `docs/systems/CATALOG_REVIEW_POLICY.md`. This
note remains the design rationale and the rule authority for assignment
(bands, curator adjustment, tie-breaks) and for the future Phase 2. Phase 2
stays unscheduled.

Governing principle (Amendment B, `CATALOG_POLICY_AMENDMENT_PROPOSAL.md`):
**legacy answers "why can't you catch this?"; rarity answers "how impressive
is it that you caught this?"** Rarity is a celebration/presentation attribute.
It never touches completion math, unlock eligibility, or `catalog_status`.

## Tier Vocabulary (decided)

```txt
common
uncommon
rare
unicorn
```

- Four tiers. Five cannot produce meaningful separation in a 70–120 type
  catalog; three kills the top tier's specialness.
- "Unicorn" is real spotter/avgeek slang for a once-in-a-lifetime airframe
  sighting; the top tier carries personality while the lower three stay
  boring-and-informative.
- Rejected vocabularies, recorded so they are not re-proposed: video-game
  registers (Epic/Legendary/Mythic — clashes with the vintage-document
  aesthetic) and anything distance-adjacent (DX — distance is a separate
  mechanic; rarity naming must never evoke it).

## Phase 1 Assignment Rule (static, curated)

The base tier derives from the estimated worldwide active fleet of the
catalog identity:

| Tier | Active fleet | Example |
| --- | --- | --- |
| `common` | >= 1000 | A320, 737-800, E190 |
| `uncommon` | 200–999 | A380, 767-400ER, ATR 42-600 |
| `rare` | 25–199 | C919, A330-800, KC-46A |
| `unicorn` | < 25 and still active | 747 Dreamlifter, Beluga ST/XL, B-2 Spirit |

- The 25-airframe boundary is deliberately the same constant as the legacy
  fleet threshold, locking the symmetry: **below 25 and no longer flying →
  legacy; below 25 but still flying → unicorn.** One measurement, two
  different questions. If the legacy threshold constant changes, this band
  boundary changes with it.
- Each assignment records its fleet-estimate source and a review date in the
  review data, like every other catalog fact.

### Curator adjustment (bounded)

A type sitting at a band boundary, or whose raw fleet number is misleading,
may be adjusted by **at most one tier**, with the rationale documented in the
review data. One step is a hard limit; more than one adjustment step turns a
curated list into an arbitrary one. The adjustment produces a single global
tier — rarity is always one value per type, worldwide. Adjustments are
re-checked on the same annual cycle as legacy re-review.

### Every type carries a tier (no null)

Every cataloged identity — collectible and legacy — **must** carry a rarity
tier. Founder decision, July 5, 2026: rarity is a coarse editorial
classification, not a per-aircraft identity claim, and the bands
are an order of magnitude wide; a rough, defensible fleet estimate is always
sufficient to pick a band for a curated catalog of this size. A missing label
is therefore not honesty, it is an inconsistency.

Honesty is preserved inside the review data instead of in the UI:

- Weak or conflicting evidence still produces a decision, recorded with
  `confidence = low` and a rationale; low-confidence rows get priority in the
  annual re-review.
- **Tie-break toward common:** when torn between two adjacent bands, assign
  the more common one. Rarity inflation permanently devalues `unicorn`;
  underselling is cheap to correct, and an upward reclassification later
  makes a good catalog notice, while a downgrade is a disappointment.

## Phase 2 (data-derived, future)

When the player base is large enough for observation statistics to be
meaningful (proposed activation gate: >= 100 active stations), rarity derives
from the share of active stations that observed the identity in a rolling
90-day window:

| Tier | Station share |
| --- | --- |
| `common` | >= 40% |
| `uncommon` | 10–40% |
| `rare` | 2–10% |
| `unicorn` | < 2% |

Two protections:

1. **Hysteresis:** a tier change applies only when the threshold is crossed
   in two consecutive windows, preventing tier yo-yo at band edges.
2. **No silent changes:** when Phase 2 activates, and on every later tier
   change, the change is announced as a catalog notice ("A380 reclassified:
   uncommon → rare") — consistent with the expedition-report aesthetic, and
   it doubles as content.

Phase 2 replaces Phase 1 values; it does not blend with them silently. The
exact blend/transition mechanics are decided when Phase 2 is scheduled, not
now.

## Non-Interference Rules (hard constraints)

1. Rarity is a separate variant attribute (working name: `rarity_tier`),
   **required for every cataloged identity**. It never lives in
   `catalog_status` and is never a review `decision`.
2. Rarity never gates unlocks, eligibility, or completion; it changes no
   numerator and no denominator.
3. Rarity is **per type, not per airframe**. A specific airframe being
   special (government VIP, test aircraft) is a separate, deferred concept.
4. Legacy identities may carry a rarity tier for display; a legacy catch
   remains outside primary completion regardless of tier.
5. **Mystery/unresolved catches have no rarity.** You cannot claim the rarity
   of something you have not identified. When re-resolution assigns an
   identity, the tier appears with it — resolution getting rewarded for free.
6. **Regional rarity is deferred.** Rarity is one global value per type.
   Location-dependent rarity display or scoring is a future concept and must
   not complicate Phase 1 or Phase 2 as specified here.

## UI Guidance (superseded July 8, 2026 — implemented)

Founder review replaced the original quiet-label guidance with the
perforated `RarityTag` system, now shipped and documented in
`docs/DESIGN_LANGUAGE.md` ("Rarity presentation"), including the color
guardrails (never Legacy's amber, never Mystery's pink). The durable
principles that survive from this section: rarity is never a stamp (stamp
inflation would devalue both layers), and it never changes completion math,
unlock eligibility, or denominators.

## Deferred (recorded, not designed)

- Regional rarity (per-location display or scoring).
- Per-airframe specialness (VIP, prototype, special livery).
- Rarity-driven achievements/badges (belongs to the future achievements
  design, which consumes rarity as an input; not the other way around).
