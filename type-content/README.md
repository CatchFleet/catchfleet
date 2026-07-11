# Type Content

The trivia, fun facts, specs and technical-plate references for every type in
the Dex: exactly the JSON the game renders. 121 type files, plus 19
manufacturer files under [`manufacturers/`](manufacturers/).

## Shape

```jsonc
{
  "v": 1,
  "trivia": ["…"],          // the flavor text on the type page
  "funFacts": ["…"],        // short, checkable facts (first flight, oddities)
  "specs": [                 // label/value pairs as rendered
    { "label": "Engines", "value": "4x JT3D" }
  ],
  "media": {                 // optional technical plate
    "kind": "drawing",
    "file": "/type-media/boeing-707-300.png",
    "credit": "Julien Scavini",
    "license": "CC BY-SA 3.0",
    "sourceUrl": "https://commons.wikimedia.org/wiki/…"
  }
}
```

## On the drawings

The technical plates are descriptive-geometry drawings by **Julien Scavini**,
used under **CC BY-SA 3.0** via Wikimedia Commons, credited on every plate.
Types without a licensed drawing render an archive-style placeholder instead.
A placeholder is replaced only when a genuinely licensed drawing is found.
**Attribution is never invented.** That rule outranks completeness.

## Corrections welcome

A wrong range figure, a misdated first flight, a better fun fact: these are
exactly the contributions this repo is for. Open an
[issue](https://github.com/catchfleet/catchfleet/issues) or send a PR against the
JSON directly. Facts should be checkable; for anything that changes a spec
value, say where the number comes from.
