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

🎟️ **Alfa:** seats are limited, invited in small waves →
[playcatchfleet.com](https://playcatchfleet.com)
👀 **Live example Dex** from the founder's own station →
[playcatchfleet.com/sedergine/dex](https://playcatchfleet.com/sedergine/dex)
📖 **Flight Manual** (Pre-Flight checklist, troubleshooting, glossary) →
[playcatchfleet.com/manual](https://playcatchfleet.com/manual)

<!-- [SCREENSHOT: Dex sayfası] ve [SCREENSHOT: ticket temalı fleet kartı]
buraya eklenecek: media/ altına koyup linkleyin -->

## What this repository is

This is the **open side** of Catch Fleet. The application code lives in a
private repository; what we publish here is everything that shapes it:

| Path | What lives there |
| --- | --- |
| `docs/roadmap.md` | Product themes and milestone history (M0–M11 closed, M12 active) |
| `docs/design-notes/` | Rarity, patches, and other feature design notes — the actual working documents |
| `catalog/` | The catalog review data: `aircraft_variant_catalog_review.csv` with a documented decision for all 171 aircraft candidates reviewed to date, plus the review policy and its amendments |
| `type-content/` | Per-type trivia, fun facts and specs, exactly as rendered in the game |
| `devlog/` | Weekly Alfa reports and change notes |

Why this split? Catch Fleet is a solo project built with AI coding agents
(more below), and the most honest thing to open isn't a pile of generated
code — it's the decisions. Every aircraft in the catalog has a reviewed,
sourced, written-down reason for existing at the granularity it does. That
paper trail is this repo. The one piece of code you actually run on your own
machine, the [Listener](https://github.com/catchfleet/listener), is fully
open source — anything that touches your machine and your key should be
inspectable, no exceptions.

## How the game works

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
  year. Imported metadata is evidence, never catalog authority — the review
  policy in `catalog/` is the law here.
- Your **station keeps exploring** while you're away. Coming back feels
  like reading an expedition report.

## What you need to play

Any SDR that can hear 1090 MHz (a ~$30 RTL-SDR dongle with its stock antenna
is a perfectly good day-one station), a decoder you probably already run
with SBS1 output, Node.js LTS for the Listener, and an Alfa invite. The
full, honest walk-through lives in the
[Flight Manual](https://playcatchfleet.com/manual).

## Privacy, stated plainly

- Raw ADS-B/SBS1 packets are never stored or transmitted.
- Exact station coordinates are private and never appear in any public
  page or payload.
- Helper keys are shown once, stored hashed, and revocable.

## This project is vibe coded

Catch Fleet is designed and run by Meriç ([TA3DIY](https://github.com/ta3diy)),
a radio amateur, not a professional developer. AI coding agents write the
code from the written design docs you can read right here; the founder does
the game design, the catalog research, the reviews and the testing against
his own antenna. These are the actual working documents, not marketing. If
you're curious what one person plus AI tooling can ship, this repo is an
honest answer.

## Issues and contributing

**Bug reports and setup-friction notes are the most valuable contribution
during the Alfa** — open them in
[Issues](https://github.com/catchfleet/catchfleet/issues). Corrections to
`type-content/` (a wrong range figure, a better fun fact) are very welcome
as issues or PRs against this repo. Catalog suggestions are welcome too,
with the caveat that catalog changes follow the review policy: sourced,
decided, documented.

## Status

Alfa, live at [playcatchfleet.com](https://playcatchfleet.com). Milestones
M0 through M11 are closed; M12 (launch response + calibration) is active. The waitlist is the way in.

---

*Catch Fleet is the first product of Catch. Motto: collect the invisible
world. 73.*
