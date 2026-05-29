# Antora Dark Theme

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Antora 3.x](https://img.shields.io/badge/antora-3.x-purple.svg)](https://antora.org)

Dark mode UI for [Antora](https://antora.org) documentation sites.

## The habit: use the release UI bundle

**The better solution—and the one you should standardize on—is the GitHub release `ui-bundle.zip`.** Antora Default UI plus this theme, already merged. One pinned URL in your playbook—no theme in `package.json`, no `node_modules` copy step.

Discover releases on [GitHub Releases](https://github.com/antora-supplemental/antora-dark-theme/releases) and the [Antora Supplemental docs portal](https://antora-supplemental.github.io/docs/) (extensions registry).

> **Former npm package:** deprecated and unpublished. Migration and lessons learned: [npm deprecation guide](https://antora-supplemental.github.io/antora-dark-theme/antora-dark-theme/guide/npm-deprecation.html).

```yaml
ui:
  bundle:
    url: https://github.com/antora-supplemental/antora-dark-theme/releases/download/v1.0.9/ui-bundle.zip
    snapshot: true
  supplemental_files: ./supplemental-ui-overrides   # optional: your logo, favicon, …
```

See [examples/antora-playbook.yml](examples/antora-playbook.yml). Overrides: one supplemental directory or [virtual files](https://docs.antora.org/antora/latest/playbook/ui-supplemental-files)—never multiple directories.

## Vendor `supplemental-ui` (forks only)

Copy `supplemental-ui/` from this repo for a maintained fork; point `supplemental_files` at it with the Default UI bundle.

## FTN layout stylesheet (optional)

Legacy FTN partials may load `supplemental-ui/css/site-ftn-docs.css` after `site-extra.css`. Default layout sites do not need it.

## Features

Dark mode toggle, system preference, `localStorage` persistence, no FOUC.

## Releasing (maintainers)

Push a `vX.Y.Z` tag; [.github/workflows/release.yml](.github/workflows/release.yml) creates a GitHub Release with **`ui-bundle.zip` only** (no npm).

## Documentation

- [Live demo](https://antora-supplemental.github.io/antora-dark-theme)
- [Full guide (AsciiDoc)](README.adoc)
- [npm deprecation & lessons learned](https://antora-supplemental.github.io/antora-dark-theme/antora-dark-theme/guide/npm-deprecation.html)

## License

[MIT](LICENSE)
