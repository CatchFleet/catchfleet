# Catch Fleet: Public Roadmap

*Curated from the internal roadmap. Last updated July 11, 2026. Dates are
close dates verified against production, not plans.*

## How to read this

Work runs in numbered milestones (M0, M1, and so on): small, closable, each
one deployed and smoke-tested before it is called done. The **long-horizon
themes** further down are product direction, not scheduled work; things
graduate from a theme into a numbered milestone when their time comes.

## Milestone history

| Milestone | What shipped | Closed |
| --- | --- | --- |
| **M0, Foundation** | The core pipeline on a clean schema: SBS1 observation to identity to fleet log to Dex unlock | June 14, 2026 |
| **M1, Users** | Accounts, usernames, public profiles | June 14, 2026 |
| **M2, Identity** | The reference database with full provenance, and the resolver: every identification carries a confidence label, a source and a reason | June 17, 2026 |
| **M3, Live Signals** | Live ingestion decisions plus the station distance foundation (range as a mechanic) | June 17, 2026 |
| **M4, Local Helper** | The SBS1 helper prototype: your decoder's output becomes observations | June 18, 2026 |
| **M5, Guarded Apply** | Idempotent, guarded ingestion: the same session posted twice lands exactly once | June 19, 2026 |
| **M6, Live Receiver UX** | The continuous live loop with reconnect resilience | June 19, 2026 |
| **M7, Hosted Alfa First Catch Loop** | The game on the public internet: helper keys, bundled helper, the first external tester's first catch | July 1, 2026 |
| **M8, Alfa Operations & Receiver Health** | Helper heartbeat telemetry and station health surfaces | July 1, 2026 |
| **M9, Dex-Centric UI + Visual Identity** | The dashboard/fleet/Dex restructure and the vintage-ticket visual language | July 3, 2026 |
| **M10, Ground Maintenance** | Local-time rendering, catch stamps, adaptive Listener cadence, a 4.5x storage diet | July 3, 2026 |
| **M11, Rarity + Patches** | Rarity tiers (common, uncommon, rare, unicorn) on every type, and the Patch Engine: 17-patch wall, showcase, retroactive backfill | July 10, 2026 |

## Now: M12, Launch Response + Calibration

Deliberately narrow and reactive: the first wave of real testers is on the
air, and this phase exists to respond to what they hit. Setup friction gets
fixed, and thresholds for the deferred patch series (fleet-log, watchkeeper,
night-owl, the Operators category) get calibrated against real week-one
reception data instead of guesses. **No new big systems in M12.** Features
like an Operator Dex are parked for beta on purpose, so the game keeps
visibly growing while more players arrive.

Also in flight: a second reference source (ADS-B Exchange) landed for the
resolver, dropping mystery signals from about 51% to about 36.5% of
unknowns, and a "Wave B" catalog expansion is under review against fresh
reception data.

## Long-horizon themes

### Collection Game

The Dex grows: operator collections, streaks, richer activity reports.
Three founder-decided directions worth naming:

- **Generations.** Everything current is **Generation Alfa**. Future
  content waves (new patch sets, new aircraft, eventually other craft
  classes) arrive as new generations rather than silent catalog edits.
- **Notable Airframes.** The Dex is type-based, but fame is airframe-based:
  a VC-25A is a Dex type, while *the* airframe serving as Air Force One is a
  story. A small registry of famous individual aircraft will decorate
  catches on the ticket and in Recent Events, with dedicated patches. The
  ground truth exists: during the July 2026 NATO summit, the founder's own
  station genuinely recorded VC-25A and its escort wave.
- **Event Patches.** The sky has a calendar: summits, airshows, sports
  charters, type farewells. Pre-announced event windows ("this weekend,
  keep your station listening") become patches; an upcoming-events calendar
  is the future surface. Disaster and relief airlifts are off-limits as
  patch material, permanently.

### Stations

Your receiving station becomes part of your identity: SDR, antenna, LNA and
filter tracking, station notes, optional callsign display, and setup
snapshots attached to important records. Always optional: new players are
never blocked by hardware questions.

### Catch Feeder

The end-state for setup: **one desktop application**. It detects your SDR
over USB, manages the decoder for you, and shows a small live station
window, with no dump1090 to install and no terminal. The current one-line
installer and device-link flow are the first rungs of this ladder.

### Community

Community corrections to aircraft identity, a review queue, and trusted
contributors. The long arc: **the CatchFleet Database**, the merged
multi-source aircraft reference (already about 680k aircraft from OpenSky
and ADS-B Exchange with per-hex conflict tracking), grows community
corrections and is eventually published back to the ecosystem as a public
artifact in its own right.

### Platform Readiness

The unglamorous theme: single-instance assumptions retired, anti-spoofing
for competitive surfaces (a precondition for opening the Listener source),
and the operational floor for growing past the Alfa.

## Principles

- **Real signal first.** No manual catches, no trading, no pay-to-win.
- **Honest uncertainty** beats wrong certainty, everywhere in the pipeline.
- **Patches and collections are the prestige.** XP, if it ever exists,
  supports progression and is never the goal.
