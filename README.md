# divejson.org

Source for <https://divejson.org>, the DiveJSON format's site, served by GitHub Pages.

The site is deliberately thin: the normative content — specification, JSON Schema,
fixtures, validator — lives in [divejson/divejson](https://github.com/divejson/divejson),
and the deploy workflow copies the schema directory from that repository into the site at
publish time, so `https://divejson.org/schema/…` always serves the schema of record
(every DiveJSON schema's `$id` points there). Nothing normative is duplicated here.

Deploys run on push here, on manual dispatch, and daily. They also run when
[divejson/divejson](https://github.com/divejson/divejson) asks them to: a schema change
that passes conformance there triggers this workflow, so the schema of record reaches the
site in about a minute rather than waiting for a scheduled rebuild. That trigger
authenticates as a GitHub App, and if it is ever revoked it fails silently from this
repository's side — the daily rebuild is the safety net that keeps the site tracking the
spec regardless.

## The mark

`favicon.svg` is the DiveJSON mark, and the same artwork serves as the divejson
organisation's avatar on GitHub. The other two icons are generated from it:

- `favicon.ico` at 16, 32 and 48px. The 16px size carries the dive profile alone, because
  at that size the full mark's stroke falls below one pixel and the braces blur into it.
- `apple-touch-icon.png` at 180x180, for iOS home-screen bookmarks. It is deliberately
  opaque: iOS composites transparency onto black rather than preserving it, and the system
  applies its own rounded mask, so the artwork is full-bleed here.

All three are named individually in the deploy workflow's assemble step. Anything added
beside them has to be added to that `cp` line as well — the workflow copies named files rather
than the repository, so a new asset is otherwise committed but never served.
