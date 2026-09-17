# Changelog

All notable changes to WR Editor Fix. Versions below v1.0.0 mean known
issues still exist (see the README's "Known issues" section) — v1.0.0 is
reserved for once everything currently known is actually fixed.

## v0.2.0 — Stuck Downloads exposed

- Exposed the experimental "Stuck Downloads" fix in the shipped config
  (`[Stuck Downloads]` section, `SkipStuckDownloads` / `SkipStuckLocalAssets`
  / `TimeoutMs`). Fixes the editor hanging forever on "Downloading assets
  (0 of N)" when a server references an asset that 404s. Off by default —
  it was built before v0.1.0 but deliberately held back from the public
  config until now; still less battle-tested than the core crash fix, so
  only turn it on if you actually hit that hang.
- Fixed a real install-layout bug: the plugin only ever looked for its
  `.ini` next to a `.asi` placed directly in `plugins\` root, with the
  `WR Editor Fix` folder as a sibling. If the `.asi` ended up placed
  *inside* that folder instead (a natural result of dragging the whole
  downloaded folder into `plugins\` as one unit), the plugin silently
  fell back to hardcoded defaults with no warning - editing the `.ini`
  appeared to do nothing. Now it checks both layouts and uses whichever
  one actually has a real `.ini` file.
- Added a permanent log line (`WR_Editor_Fix.log`) reporting which
  config file path was resolved and whether it was actually found - so
  "my settings aren't applying" is now a 2-second log check instead of
  a guessing game.
- No changes to the core crash fix or camera features from v0.1.0.

## v0.1.0 — first public release

- Core Rockstar Editor crash fix: stops the editor crashing when a clip
  references a custom asset (vehicle / MLO / prop / ytyp) that got
  unloaded, and the same crash pattern in streaming/asset-unload code.
- Editor free camera tweaks, on by default: unlimited camera distance,
  uncapped zoom/FOV, no camera collision, adjustable free-cam move speed
  (live-reloads from the `.ini` while flying).
- Known issue: a crash tied to malformed custom vehicle data on some
  heavily modded servers is not yet fixed — actively being investigated.
