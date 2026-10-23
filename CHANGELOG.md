# Changelog

All notable changes to the plugins in this repo are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and each plugin adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html)
against its own `package.json` version — this repo holds more than one
plugin, so each entry names which plugin it's about.

## [Unreleased]

## [xo-server-host-power-manager 0.2.2] - 2026-10-21

### Fixed

- `xo-server-host-power-manager`: the "Average CPU utilization %" metric
  works. Every poll failed reading host stats ("no such object undefined"),
  so a rule using it never acted, memory trigger included. A poll can no
  longer start while the previous one is still running, so one condition
  can't press a NanoKVM power button twice.
- `xo-server-host-power-manager`: settings that make the plugin misbehave
  are refused on save, with an error naming the rule: two rules for the
  same host, overlapping or equal power-on/power-off thresholds, a poll
  interval under 10 seconds, a cooldown under 1 minute. A refused save keeps
  the previous settings running. A failed power-off now waits for the
  cooldown instead of retrying every poll. Settings saved earlier that break
  one of these rules stop the plugin at the next xo-server start until they
  are corrected.
- `xo-server-host-power-manager`: before a NanoKVM press, the plugin reads
  the NanoKVM's power LED and presses only when it reads off (not on, not
  unreadable). New per-rule "Boot wait (minutes)" setting (default 10):
  after a power-on, no further power-on until the host shows Running or the
  wait has passed. A host XO shows as Unknown is left alone, and a disabled
  (maintenance) running host is not shut down. The Test result logs
  `heldBackBecause`.

## [xo-server-host-power-manager 0.2.1] - 2026-10-12

### Fixed

- `xo-server-host-power-manager`: adding a second (or later) rule through
  XO's plugin configuration form failed with `invalid parameters` /
  `must have required property 'cpu'`. The configuration schema required
  every rule to include both a `cpu` and a `memory` trigger object, but XO's
  generic schema-driven config form only submits a trigger's object if the
  user actually expanded that section — leaving one collapsed (e.g. a
  memory-only rule where CPU is never touched) omits the key from the
  payload entirely instead of sending `{ metric: 'none' }`. `cpu` and
  `memory` are no longer required at the schema level, and a missing one is
  now normalized to `{ metric: 'none' }` when configuration loads, matching
  the schema's own documented behavior that a trigger can be skipped.

## [xo-server-host-power-manager 0.2.0] - 2026-09-20

### Added

- `xo-server-host-power-manager`: added two memory metrics, "Lowest free
  memory % on any one running host" and "Lowest free memory GB on any one
  running host" (`percentFreeMin` / `absoluteFreeMinGb`), alongside the
  existing pool-wide free % and free GB metrics. The existing metrics sum
  every running host's free memory together before comparing it to the
  threshold, which can hide one host running tight while another has slack
  — e.g. a 15GB-free host and a 40GB-free host average out to a
  comfortable-looking 55GB pool total. The new metrics instead track the
  single tightest host's own free memory, so a rule can react to that host
  specifically instead of the pool average. `getMemory()` in
  `lib/metrics.js` now also returns `minFreeBytes`/`minFreePercent`
  alongside the existing pool-wide `totalBytes`/`freeBytes`.
