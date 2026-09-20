# xo-plugins

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
