# Devlog: The First Month

*June 10 to July 11, 2026. 351 commits, twelve closed milestones, one
antenna. Entries reconstructed from the commit log; the embarrassing parts
kept in on purpose.*

**June 10.** Created the repo at breakfast: `Initial commit from Create Next
App`. By the end of the day the prototype hears planes. SBS1 in, catches
out. The idea survived contact with reality in under twelve hours, which is
more than most ideas manage.

**June 12.** Threw the prototype away. Not a pivot, a promise: this time
schema first, decisions written down before code. Two days of architecture
and data-model documents before a single feature.

**June 13.** The "First 151" review began: every candidate aircraft needs a
sourced, written-down decision before it may enter the Dex. Reviewing 151
aircraft by hand felt like a detour. It turned out to be the most
load-bearing decision of the month; that paper trail is now
[`catalog/`](../catalog/) in this repo.

**June 14.** M0 and M1 closed on the same day. The pipeline runs on the
clean schema, accounts and usernames exist. The game has players in theory.

**June 17.** The resolver got its contract, and it never changed after this
day: every identification carries a confidence label, a source and a reason.
When it does not know, it says so. Unknown aircraft become mystery signals,
not errors. Distance also became a mechanic: your farthest catch is a
tracked record.

**June 18 to 19.** The helper sprint, three milestones in three days. A
local SBS1 helper, guarded idempotent ingestion (the same session posted
twice lands exactly once), then the continuous live loop with reconnect
resilience. A station can now listen all day unattended.

**June 21 to 25.** The game leaves localhost. Helper keys, an invite gate, a
bundled helper, a read-only admin panel. The deploy ritual is born this
week: push, rebuild, smoke test against production. Nothing counts as done
until it is verified live. This rule gets no exceptions and it has paid for
itself several times already.

**June 30.** Setup-friction week: clearer Windows instructions, SBS1
reconnect support, a flush fix for busy feeds. The most boring commits of
the month and probably the most valuable ones.

**July 1.** M7 closes on the only milestone that actually matters: the
first external tester's first catch. Heartbeat telemetry (M8) lands the same
day, so the site can honestly say whether your station is alive.

**July 3.** Two milestones close in one day. M9 gives the game its face, the
Dex-centric dashboard and the vintage-ticket look. M10 does the groundwork:
local-time rendering (older sightings had been displaying three hours off,
that one stung), FIRST CATCH and LONGEST CATCH stamps, adaptive Listener
cadence, and a storage diet that takes the production database from 422 MB
to 93 MB.

**July 5 to 7.** Catalog week. Wave A adds 19 series-level identities after
a full review pass; the collectible denominator becomes 103. Every type gets
trivia and specs. 53 types get Julien Scavini technical plates (CC BY-SA,
credited on every one); the rest wear honest archive placeholders until a
genuinely licensed drawing is found. House rule: attribution is never
invented. Also this week, an overeager coding agent ran a database reset and
deleted 519,963 imported reference rows from the local machine. Reimported.
New house rule: agents do not run database resets.

**July 8.** Rarity goes live. Four tiers: common, uncommon, rare, unicorn.
"Unicorn" is real spotter slang, and that is exactly why it won over
anything that sounds like a loot table.

**July 10.** Patches ship (M11): a 17-patch wall, tiered series, a
three-slot showcase like a pilot jacket's chest, detail pages with stories,
and a retroactive backfill so day-one catches counted. The Listener grows up
the same day: native binaries, a device-link flow (approve your Listener in
the browser, no key copy-paste), a one-line installer, Raspberry Pi support.
Also fixed: the Listener now survives an SBS1 queue overflow instead of
quietly exiting.

**July 11.** The resolver gains a second reference source (ADS-B Exchange);
mystery signals drop from about 51% to about 36.5% of unknowns. And the
month ends with the catch of the month: during the July NATO summit, this
station recorded VC-25A. Air Force One, from a home antenna. That single
catch is already shaping the roadmap (see Notable Airframes in the
[roadmap](../docs/roadmap.md)).

M12 begins deliberately small: respond to real testers, calibrate patch
thresholds against real reception data, no new big systems. The Alfa is
live, seats invited in small waves.

---

*Catch Fleet is built by one radio amateur and a lot of AI coding agents.
The design docs in this repo are the actual instructions the code is written
from. 73.*
