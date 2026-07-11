# Patches Design Note — M11 Planning Input

## Status

Approved direction, July 5, 2026 (naming, categories, tier mechanics, and
showcase decided by founder in chat). **The core system SHIPPED in M11
(deployed July 10, 2026):** launch scope, the P4.1 renames (e.g.
`first-catch` → `first-contact`, `dex-progress` → `type-rating`), and the
17-item wall are frozen in
`docs/archive/M11_PATCHES_IMPLEMENTATION_PLAN.md`; the ongoing system
contract is `docs/engines/PATCH_ENGINE.md`; copy/visual rules live in
`docs/DESIGN_LANGUAGE.md` ("Patches vocabulary"). This note remains the
design rationale plus the spec for the **deferred** items below (fleet-log,
watchkeeper, night-owl, the Operators category, hidden patches), whose TBD
thresholds still await week-1 tester data (M12 calibration). Where a name
or category below differs from the launch inventory, the M11 plan's table
supersedes it.

Governing principle (ROADMAP): **patches and collections are the primary
source of prestige.** XP, if it ever exists, supports progression and is
never the main goal.

## Naming And Routes (decided)

- Player-facing word is **"Patches"**, everywhere. The word "achievement"
  never appears in player-facing copy (same register decision as rejecting
  Epic/Legendary for rarity: gamer-platform vocabulary clashes with the
  vintage-document aesthetic).
- Code, schema, and docs use `patch`. Unlike type/variant there is no legacy
  split to preserve, so the player word and the code word match.
- The word "badge" is reserved for UI notification affordances (e.g. the
  unseen-unlocks dot on the Dex nav item) and is never a synonym for patch.
- Routes follow the existing username-scoped family:
  - `/[username]/patches` — canonical public patch wall
  - `/patches` — current-user shortcut/redirect (M7 pattern)
  - `/[username]/patches/[patch-slug]` — patch detail page
- Patch slugs: kebab-case, English, stable (renaming a patch never changes
  its slug — same rule as catalog slugs). **Tiered series share one slug**
  (`family-album`, `globetrotter`); tiers render inside the series page, so
  earning a higher tier never changes the URL. Single patches get their own
  slug (`first-catch`, `positive-id`, `night-shift`, `cold-case`,
  `alpha-crew`).
- The page title is a DESIGN_LANGUAGE/copy decision, not a route decision;
  candidates recorded: "Patch Wall", "Decorations & Awards" (NATOPS
  register). The slug stays `/patches` regardless.

## Design Principles

1. **Every patch tells a story.** If "how did you earn that?" has a
   one-sentence story ("caught an A380 from 400 km"), the patch is right. If
   the answer is only a number, it is weak; number-patches are few and
   carry large thresholds.
2. **Inflation kills prestige.** At launch most patches must be visible but
   distant. Empty spots on the wall are the prestige. Roughly: ~10 earnable
   in the first month, ~15 over months, ~5 on a multi-year horizon.
3. **Tiered series beat singles.** One design, several rewards, a next
   target always in range.
4. **Earned is earned.** A patch is never revoked — not by catalog changes,
   legacy re-review promotions, family growth, or rule changes. Identical to
   the rarity and legacy principles: history is history.
5. **Patch = door.** Where a patch has an underlying universe, its detail
   page shows it (the Operators stats page is the first instance). This is a
   reusable pattern, not a one-off page.

## Categories And Initial Set (~33)

### 1. First Flight (2)

- `first-catch` — the station's first catch of any kind, including an
  unresolved mystery signal. Celebrates "my antenna works".
- `positive-id` — the first fully resolved identity, i.e. the first Dex
  unlock. Celebrates "I know what that was", and teaches the catch-vs-identity
  distinction on night one. For most players the two land minutes apart;
  that is fine — onboarding celebration should be generous.

### 2. Fleet Milestones (1 series + 1 late series)

- `fleet-log` series — distinct airframes heard (unique ICAO hex). **Not**
  types, **not** sightings. Draft tiers 500 / 2,500 / 10,000 / 50,000 —
  explicitly TBD: a busy station can log 150–400 unique airframes on day
  one, so tiers are calibrated from real alpha week-1 station data. Target
  shape: tier I within the first weeks, top tier a multi-year horizon.
- `million-watch` series — total sightings 100K / 500K / 1M (ROADMAP
  candidates). Deliberately a single late series: sighting volume is the
  metric M9 intentionally demoted, so it gets a patch but never the
  spotlight.

### 3. Dex Progress (Family Album + certificates + completion)

- `family-album` series — **level = size of the completed family.** Complete
  any family with 3 collectible types → Level I; 4 types → Level II; 5 →
  Level III. Rules:
  - Families with fewer than 3 collectible types never trigger a level (they
    still count toward Dex percentage as normal).
  - The ladder is data-indexed and grows with the catalog automatically:
    Wave B additions (e.g. MAX 7/10 → a 7-type 737 Family) create Levels
    IV–V without a design change.
  - Level is assessed at the moment of completion and never revoked. If a
    family later gains a type, the patch stands; the family simply shows as
    incomplete again.
  - Current catalog support (collectible counts, post single-737-family
    decision): 5 types — A320 Family, 737 Family, Citation Family; 4 types —
    A330, 777, E-Jet; 3 types — 787, CRJ. Three real rungs on day one.
  - Supersedes the earlier "First Family Completed" idea (Level I is that
    moment).
- `constructors-certificate` series — complete every collectible type of a
  manufacturer: Airbus (17) and Boeing (18) at launch. Both deliberately
  include unicorns (the Belugas; the Dreamlifter), making these multi-year
  prestige objects — by design, stated honestly. No "except unicorns"
  softening: rarity never gates completion, and difficulty is the point.
  Embraer (9) is a borderline future addition. Manufacturers below 3
  collectible types are excluded by the same ≥3 rule.
- `first-manufacturer` — first completed manufacturer with ≥3 collectible
  types.
- `dex-progress` series — primary Dex 25% / 50% / 75% / 100%
  (collectible denominator only, per the legacy rules). The 100% patch is
  the most prestigious object in the game.

### 4. Range / DX (1 series)

- `dx` series — farthest catch 100 / 200 / 300 / 400+ km. The word DX is
  correct here (it genuinely means distance, unlike in rarity naming where
  it was banned for that exact reason). This is the hardware-pride category:
  antenna upgrades become visible on the wall.

### 5. Operators (5–6)

Callsign-prefix based (ICAO Doc 8585 mapping); no operator Dex exists — the
patch detail page is the operator experience (decided July 5, 2026):

- `globetrotter` series — 10 / 25 / 50 distinct operators heard.
- `night-shift` — 5 distinct cargo operators.
- `flag-carrier-hunter` — flag carriers of 10 distinct countries.
- `government-frequency` — 3 distinct government/military operators.

Detail page (`/[username]/patches/globetrotter` and siblings): tier progress
on top; **Heard** section ranked by aircraft count ("THY · 87 aircraft ·
412 sightings · first heard May 12"); **Not yet heard** section listing the
curated operator catalog's remaining entries in locked-tile styling, grouped
Airlines / Cargo / Government-Military so thematic patch targets are
visible.

Honesty rules: operator identity comes only from observed callsigns
(~46% of fleet rows carry one); catches without callsigns simply never
count — signal honesty, not a bug. An airframe heard under two operators'
callsigns counts for both. Alliance-themed sets (Star Alliance etc.) are
parked: alliance names are the same trademark caution as manufacturer logos.

Dependencies: a curated operator catalog (100–200 entries) with its own
mini review pass under CATALOG_REVIEW_POLICY discipline (sourced,
decided), and a callsign-prefix mapping table.

### 6. Rare Air (5) — depends on Rarity Phase 1

- `first-rare`, `first-unicorn`, `rare-collector` (10 rare types),
  `first-legacy` (first legacy-status catch), and `cold-case` — first
  mystery signal that later resolves: the patch that rewards re-resolution
  and embodies "an incomplete catch is unfinished, not wasted".

### 7. Watchkeeper (3 + flavor)

- `watchkeeper` series — 7 / 30 / 90 days of continuous station operation.
  **This is the station's streak, never the player's**: the receiver
  listens by itself and no daily-login mechanic is acceptable (that would be
  a dark pattern foreign to this game). Hardware fails; a tolerance window
  (draft: outages under 24h don't break the streak) is part of the rule, TBD
  with the health-signal data available from M8 heartbeats.
- Flavor singles: `night-owl` / `dawn-patrol` (N catches in the 02:00–05:00
  local window; N TBD).

### 8. Alpha Crew (1, closes forever)

- `alpha-crew` — founding patch for alpha testers. Never earnable again.
  Cross-links with launch comms: worth promising in the invite email.

## Mechanics (decided)

- **Retroactive grant.** When the system ships, existing history
  (fleet_logs, sightings, distances, unlock facts) is scanned once and all
  earned patches are granted. "Counting starts today" would erase the first
  50 stations' work.
- **Never revoked** (principle 4). Applies across catalog growth, legacy
  promotions, threshold retuning (retuned thresholds apply prospectively;
  granted patches stand).
- **Hidden patches: few.** 2–3 undocumented oddities (e.g. hearing the same
  airframe 100 times) for community discovery; everything else visible and
  targetable.
- **Showcase.** Every player selects up to 3 patches to highlight; shown on
  the public profile header (Dex page header is a candidate second surface).
  Default before any selection: the 3 most recently earned (an empty
  showcase on a new player reads sad); once the player picks, the selection
  is stable. Visual concept: three patch slots, a pilot jacket's chest.
- **Compute once, read many** (M10 directive): patch evaluation and the
  operator aggregates behind detail pages use precomputed per-user
  aggregates, not per-view fleet scans.

## Visual Direction (for the design pass)

Embroidered aviation patch aesthetic (squadron/route patches), same design
family and same trademark caution as the manufacturer roundel work: no real
airline/manufacturer logos, wordmarks, or emblems — own-design only, names
as plain text are nominative use.

## Open Items

Still open (M12 inputs):

1. Threshold calibration from alpha week-1 data: fleet-log tiers,
   watchkeeper tolerance, night-owl N.
2. Operator catalog review pass (scope: which 100–200 operators; flag
   carrier list per country).

Resolved by the M11 build (July 8–10, 2026):

3. Page title copy: **"Patch Wall"**, eyebrow "Decorations & Awards"
   (recorded in DESIGN_LANGUAGE).
4. Launch inventory: **17 wall items, 16 active** (`cold-case` deferred) —
   the ~33 draft set was cut; deferred items return with calibration.
5. Retroactive grant: shipped as `scripts/patches-backfill.ts` (dry-run
   first) plus the post-apply evaluation hook.
