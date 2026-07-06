# Catch Fleet

**A collection game played with a real radio.**

Catch Fleet turns real ADS-B reception into a long-term collection game. A
small open [Listener](https://github.com/catchfleet/listener) sits next to
your existing decoder (readsb, dump1090, anything that speaks SBS1), and
every aircraft your antenna receives on 1090 MHz gets identified and added
to your Dex: types, families, manufacturers.

It is deliberately **not a flight tracker**. There is no global feed, no map
of other people's traffic, no MLAT network. If it's not in your Dex, your
station didn't hear it. Range is a mechanic: your farthest catch is a
tracked record, and antenna upgrades translate directly into collection
progress.

🎟️ **Alpha:** seats are limited, invited in small waves →
[playcatchfleet.com](https://playcatchfleet.com)
👀 **Live example Dex** from the founder's own station →
[playcatchfleet.com/sedergine/dex](https://playcatchfleet.com/sedergine/dex)
📖 **Flight Manual** (Pre-Flight checklist, troubleshooting, glossary) →
[playcatchfleet.com/manual](https://playcatchfleet.com/manual)

<!-- [SCREENSHOT: Dex sayfası] ve [SCREENSHOT: ticket temalı fleet kartı]
buraya eklenecek: docs/media/ altına koyup linkleyin -->

## What you need to play

- Any SDR that can hear 1090 MHz. A ~$30 RTL-SDR dongle with its stock
  antenna is a perfectly good day-one station.
- A decoder you probably already run: readsb, dump1090 or anything with
  SBS1 (BaseStation) output.
- Node.js LTS for the Listener.
- An alpha invite. The full, honest requirements walk-through lives in the
  [Flight Manual](https://playcatchfleet.com/manual).

## How it works

```txt
your antenna → SDR → decoder (SBS1) → Listener → Catch Fleet → your Dex
```

- The **Listener** parses SBS1 locally and posts only bounded, summarized
  observations, authenticated with a revocable per-app key. Raw frames
  never leave your machine.
- The **resolver** turns a hex into an identity with a confidence label, a
  source and a reason. When it doesn't know, it says so: the aircraft
  becomes a **mystery signal** in your Fleet and may resolve later without
  losing your catch history. Wrong certainty is worse than honest
  uncertainty.
- The **catalog** is human-reviewed. Collection is keyed on ICAO hex, so you
  collect physical airframes, not registrations that change hands next
  year. Every collectible identity in the catalog has a documented review
  decision; imported metadata is evidence, never catalog authority.
- Your **station keeps exploring** while you're away. Coming back feels
  like reading an expedition report.

## Privacy, stated plainly

- Raw ADS-B/SBS1 packets are never stored or transmitted.
- Exact station coordinates are private and never appear in any public
  page or payload.
- Helper keys are shown once, stored hashed, and revocable.

## This project is vibe coded

Catch Fleet is designed and run by Meriç ([TA3DIY](https://github.com/ta3diy)),
a radio amateur, not a professional developer. AI coding agents write the
code from written design docs; the founder does the game design, the catalog
research, the reviews and the testing against his own antenna. The design
docs, milestone plans and the catalog review data in this repository are the
actual working documents, not marketing. If you're curious what one person
plus AI tooling can ship, this repo is an honest answer.

## Repository tour

| Path | What lives there |
| --- | --- |
| `docs/ROADMAP.md` | Product themes and milestone history (M0–M10 closed) |
| `docs/systems/` | Engine docs: resolver, Dex engine, catalog review policy |
| `docs/DESIGN_LANGUAGE.md` | The vintage airline-ticket visual identity |
| `docs/ALPHA_BACKLOG.md` | Known issues and alpha feedback intake |
| `data/type-content/` | Per-type trivia, specs and technical plates |

## Contributing during the alpha

The best contribution right now is **playing and reporting**: bug reports
and setup-friction notes go to
[Issues](https://github.com/catchfleet/game/issues). Catalog suggestions are
welcome as issues too, but note that catalog changes follow the review
policy in `docs/systems/CATALOG_REVIEW_POLICY.md`: sourced, decided,
documented. Code PRs are not the focus while the alpha stabilizes.

## Status

Alpha, live at [playcatchfleet.com](https://playcatchfleet.com). Milestones
M0 through M10 are closed; M11 is in planning. The waitlist is the way in.

---

*Catch Fleet is the first product of Catch. Motto: collect the invisible
world. 73.*
