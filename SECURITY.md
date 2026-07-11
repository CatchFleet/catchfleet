# Security Policy

Catch Fleet is a small Alfa, but it handles real user accounts and real
radio-derived observations, so security reports are taken seriously.

## Reporting a vulnerability

Please **do not open a public issue** for security problems. Use GitHub's
private vulnerability reporting on this repository instead: **Security tab →
"Report a vulnerability"**. You'll get an acknowledgment within a few days;
this is a solo project, so please allow a little patience on the fix
timeline. Coordinated disclosure is appreciated; you'll be credited if you
want to be.

## Scope

- The game at [playcatchfleet.com](https://playcatchfleet.com): accounts,
  helper keys, the device-link flow, the observation apply pipeline.
- The Listener release builds in
  [catchfleet/listener](https://github.com/catchfleet/listener).

## A note on spoofed catches

Yes, we know: a client that speaks the Listener's protocol can fabricate
observations without an antenna, and ADS-B itself is unauthenticated.
Server-side anti-spoofing for competitive surfaces is on the roadmap and is
a precondition for opening the Listener source. Reports of *novel* integrity
bypasses (auth, key handling, cross-user effects) are still very welcome;
"I can fake my own sightings" on its own is a known limitation of the Alfa,
not a new finding.
