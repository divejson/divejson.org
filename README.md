# divejson.org

Source for <https://divejson.org>, the DiveJSON format's site, served by GitHub Pages.

The site is deliberately thin: the normative content — specification, JSON Schema,
fixtures, validator — lives in [divejson/divejson](https://github.com/divejson/divejson),
and the deploy workflow copies the schema directory from that repository into the site at
publish time, so `https://divejson.org/schema/…` always serves the schema of record
(every DiveJSON schema's `$id` points there). Nothing normative is duplicated here.

Deploys run on push, weekly (to pick up spec-repository changes), and on manual
dispatch.
