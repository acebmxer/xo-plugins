# Security Policy

## Supported Versions

Each plugin is versioned independently in its own `package.json`. Only the
latest version of each plugin, on the `main` branch, receives fixes.

| Version              | Supported          |
| --------------------- | ------------------ |
| Latest (`main`)       | :white_check_mark: |
| Older tags/releases    | :x:                |

## Reporting a Vulnerability

Please report security issues **privately** — do not open a public issue for
a suspected vulnerability.

Use GitHub's private vulnerability reporting:

1. Open this repository's **Security** tab.
2. Click **Report a vulnerability**.
3. Include the affected plugin and version, a description, reproduction
   steps, and the impact.

Expect an initial acknowledgement within a few days. Once a fix is available
it will land on `main` and be noted in [CHANGELOG.md](CHANGELOG.md).

## Scope

This policy covers the plugin code in this repository. In particular:

- **`xo-server-nanokvm`** stores a NanoKVM device's username and password in
  XO's plugin configuration, and sends the password through the fixed,
  publicly-documented obfuscation NanoKVM's own firmware expects (see the
  comment at the top of `xo-server-nanokvm/lib/aes-legacy.js`) — this is
  **not** a secret encryption scheme; the actual protection is the HTTPS
  connection to the device. A report about the strength of that obfuscation
  itself is out of scope (it matches NanoKVM's firmware by design); a report
  about credentials leaking anywhere else (logs, error messages, a
  non-HTTPS fallback) is in scope.
- **`xo-server-host-power-manager`** can power hosts off via XO's own
  `Host.shutdown` and power them on via XO's built-in power-on or
  `xo-server-nanokvm`. A report that its thresholds or cooldown logic can be
  driven to power off a host XO's own HA/evacuation checks should have
  protected is in scope.

Vulnerabilities in **Xen Orchestra itself** (`xo-server`/`xo-web`, not these
plugins) should be reported upstream at
<https://github.com/vatesfr/xen-orchestra/security/policy>. Vulnerabilities
in NanoKVM's own firmware should be reported to
[Sipeed](https://github.com/sipeed/NanoKVM).
