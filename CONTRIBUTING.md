# Contributing

Thanks for helping improve these Xen Orchestra plugins!

## Two-way sync with install_xen_orchestra

These plugins are also shipped inside
[install_xen_orchestra](https://github.com/acebmxer/install_xen_orchestra)'s
`plugins/` folder. A change pushed to `main` or `dev` **here** is
automatically dispatched to that repo and pulled into its `plugins/<name>/`
folder (see [`notify-install-repo.yml`](.github/workflows/notify-install-repo.yml)),
and a change made to a plugin folder **there** is pushed back here the same
way. You can open a pull request against either repo — just expect the
matching commit to show up as a `sync:` commit in the other one shortly
after it merges.

## Development setup

Each plugin is a plain `xo-server` plugin (a `xo-server-*` npm package) with
no build step. You need:

- Node.js >= 18
- Each plugin has a `test/` folder using Node's built-in test runner
  (`node --test`, via `npm test` in that plugin's folder) — no test
  framework dependency to install. No lint config exists yet for either
  plugin. If you add the first lint config for a plugin, wire the matching
  CI step in the same pull request rather than leaving it silently unrun.

## Before opening a pull request

Run what CI runs:

```bash
# from the repo root
for pkg in */package.json; do
  node -e "JSON.parse(require('fs').readFileSync('${pkg}', 'utf8'))"
done

find . -name '*.js' -not -path './node_modules/*' -exec node --check {} \;

# then, from each plugin's own folder that has a test/ folder:
npm test
```

## Coding conventions

- `'use strict'` at the top of every file, matching the existing plugins.
- Match the existing style in the plugin you're touching (indentation,
  quoting, `lib/` layout) rather than introducing a new one.
- Keep each plugin's `README.md` in sync with any configuration or behavior
  change — it's the only documentation a user configuring the plugin in XO's
  web UI has.

## Commit messages

Recent history in this repo uses short, prefixed commit subjects (`ci:`,
`sync:`, `fix:`, `feat:`) in the style of
[Conventional Commits](https://www.conventionalcommits.org/) — follow that
style. Add user-facing changes to [CHANGELOG.md](CHANGELOG.md) under
`[Unreleased]`.

## Opening a pull request

GitHub pre-fills new PRs from
[.github/pull_request_template.md](.github/pull_request_template.md) — fill
it in rather than replacing it.
