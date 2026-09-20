# xo-plugins

[![CI](https://github.com/acebmxer/xo-plugins/actions/workflows/ci.yml/badge.svg)](https://github.com/acebmxer/xo-plugins/actions/workflows/ci.yml)
[![License: AGPL-3.0-or-later](https://img.shields.io/badge/license-AGPL--3.0--or--later-blue.svg)](LICENSE)
[![Last commit](https://img.shields.io/github/last-commit/acebmxer/xo-plugins)](https://github.com/acebmxer/xo-plugins/commits)
[![Issues](https://img.shields.io/github/issues/acebmxer/xo-plugins)](https://github.com/acebmxer/xo-plugins/issues)
[![Stars](https://img.shields.io/github/stars/acebmxer/xo-plugins)](https://github.com/acebmxer/xo-plugins/stargazers)
[![Forks](https://img.shields.io/github/forks/acebmxer/xo-plugins)](https://github.com/acebmxer/xo-plugins/forks)
[![Node.js](https://img.shields.io/badge/node-%3E%3D18-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![xo-server-nanokvm](https://img.shields.io/badge/xo--server--nanokvm-v0.1.1-informational)](xo-server-nanokvm/package.json)
[![xo-server-host-power-manager](https://img.shields.io/badge/xo--server--host--power--manager-v0.2.0-informational)](xo-server-host-power-manager/package.json)

Custom [Xen Orchestra](https://xen-orchestra.com/) `xo-server` plugins,
usable on their own — no dependency on any other project.

## What's here

- [`xo-server-nanokvm`](xo-server-nanokvm) — lets other plugins power a host
  on through a [Sipeed NanoKVM](https://wiki.sipeed.com/nanokvm) device
  wired to that host's power/reset header.
- [`xo-server-host-power-manager`](xo-server-host-power-manager) — powers an
  "extra" pool host on/off based on CPU or memory thresholds, via XO's
  built-in host power-on or `xo-server-nanokvm`.

Each plugin's own README has install and configuration instructions.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Security

See [SECURITY.md](SECURITY.md) for how to report a vulnerability.

## License

AGPL-3.0-or-later, matching [Xen Orchestra](https://github.com/vatesfr/xen-orchestra)
itself — see [LICENSE](LICENSE).

## Also maintained in install_xen_orchestra

These plugins are also shipped inside
[install_xen_orchestra](https://github.com/acebmxer/install_xen_orchestra)'s
`plugins/` folder, for its `--custom-plugins` installer, which is the
source of truth for them. The two copies are kept in sync automatically by
CI on both sides (see [`notify-install-repo.yml`](.github/workflows/notify-install-repo.yml)
here and `docs/custom-plugins.md` there); this repo exists for anyone who
wants the plugins without the rest of that project.
