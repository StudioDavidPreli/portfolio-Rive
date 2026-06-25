# portfolio-Rive

Source `.riv` files for davidpreli.com. This repo is asset storage only. The
portfolio build (the `studioDavidPreliSite` repo) pulls these files and vendors
them into `src/assets` at build time, so the deployed site serves fingerprinted
copies from `/_astro/` and never hotlinks back here or to rive.app.

## What lives here

Rive animations for the home feed and the nav reel preview. The authoritative map
from each file to its section, original id, size, and theme behavior is
`reference/rive-inventory.md` in the site repo. Treat that file as the index; this
repo holds the bytes.

Active set: POPP'EM, VARIABLE DANCERS, RAINING MAN, JUMP ROPE, FLYING, and the nav
reel preview (`quick_cat`). ICONS and DROPLET were cut as sections, so their `.riv`
files are not part of the active build (see DECISIONS #7 in the site repo).

Two files carry both a light and a dark state and are theme-aware: RAINING MAN and
`quick_cat`. The rest render the same in either theme.

## How the site consumes these

- Runtime is `@rive-app/canvas`, self-hosted. The site does not use rive.app embed
  iframes. Self-hosting is what lets the resting frame be held programmatically
  under reduced motion.
- Each Rive island hydrates `client:visible`, so the WASM runtime defers until the
  piece scrolls into view.
- Reduced motion holds a resting frame. The state machine does not play and is not
  slowed. Rive bakes its interpolation at author time, so a static pose is the
  correct treatment, not a shortened duration.
- `.riv` is served with the correct MIME type from the site's `_headers` file so
  the runtime fetches cleanly.

## Naming

Files use working names (for example `shapedhands_v03.riv` is VARIABLE DANCERS).
The id-to-file-to-section mapping lives in `rive-inventory.md`; keep that file
current when a name changes here.
