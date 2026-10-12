# Changelog

All notable changes to the plugins in this repo are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and each plugin adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html)
against its own `package.json` version — this repo holds more than one
plugin, so each entry names which plugin it's about.

## [Unreleased]

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
