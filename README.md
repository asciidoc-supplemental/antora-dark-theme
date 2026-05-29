# Antora Dark Theme

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Antora 3.x](https://img.shields.io/badge/antora-3.x-purple.svg)](https://antora.org)

Dark mode UI for [Antora](https://antora.org) documentation sites.

## The habit: use the release UI bundle

**The better solution—and the one you should standardize on—is the GitHub release `ui-bundle.zip`.** It is Antora Default UI plus this theme, already merged. One pinned URL in your playbook, no theme package in `package.json`, no copying from `node_modules`, no invalid stacks of supplemental directories.

Discover releases and catalog metadata on the [Antora Supplemental docs portal](https://antora-supplemental.github.io/docs/) (extensions registry and related projects)—**not** on npm. The [npm package](https://www.npmjs.com/package/antora-dark-theme) is legacy surface area; **npm publishing is planned to end.** Do not start new projects on npm. Migrate existing installs to the bundle.

```yaml
ui:
  bundle:
    url: https://github.com/antora-supplemental/antora-dark-theme/releases/download/v1.0.9/ui-bundle.zip
    snapshot: true
  # Optional: one small directory of *your* files only (logo, favicon, …)
  supplemental_files: ./supplemental-ui-overrides
```

Pin `releases/download/vX.Y.Z/...` in CI. See [examples/antora-playbook.yml](examples/antora-playbook.yml).

## npm package (deprecated — do not adopt)

| | Release bundle | npm `antora-dark-theme` |
|--|----------------|-------------------------|
| **Verdict** | Correct default | Legacy; avoid |
| **Install** | Playbook URL only | `npm install` pollutes the Node graph for a static UI |
| **Discovery** | [GitHub Releases](https://github.com/antora-supplemental/antora-dark-theme/releases), [Supplemental docs portal](https://antora-supplemental.github.io/docs/) | npm registry (being retired) |
| **Typical mistake** | — | Two supplemental dirs, sync scripts from `node_modules` |

npm remains published only until downstreams migrate. It exists today so old lockfiles keep resolving; **new work must use the bundle.**

If you still consume npm today, move to the bundle URL above and delete the dependency. Vendoring `supplemental-ui` in git is acceptable for forks; npm is not.

## Custom overrides (one supplemental directory)

Antora allows **one** supplemental directory **or** virtual files—not a YAML list of multiple directories.

```yaml
  supplemental_files: ./supplemental-ui-overrides   # e.g. img/logo.svg
```

Virtual single-file entries: see [Antora supplemental UI](https://docs.antora.org/antora/latest/playbook/ui-supplemental-files).

## Vendor `supplemental-ui` (forks only)

Maintainers of a theme fork may copy `supplemental-ui/` from this repo and point `supplemental_files` at it with the Default UI bundle. That is source control, not npm.

## FTN layout stylesheet (optional)

The repo ships `supplemental-ui/css/site-ftn-docs.css` for the legacy FTN partial set ([docs.foodtrucknerdz.com](https://docs.foodtrucknerdz.com)). Load after `site-extra.css` when you use those partials. Default layout sites do not need it.

## Features

- Dark mode toggle (sun/moon)
- System preference detection
- Persistent preference via `localStorage`
- No FOUC
- Works without forking Antora Default UI

## Releasing (maintainers)

Tag-driven release: [.github/workflows/release.yml](.github/workflows/release.yml) produces GitHub Release assets (`ui-bundle.zip`, `.tgz`). **Primary artifact is `ui-bundle.zip`.** npm publish on the tag is legacy and will be removed from the workflow once adoption of the bundle (and the Supplemental catalog) is complete—do not treat npm as the distribution channel.

## Documentation

- Live demo: [antora-supplemental.github.io/antora-dark-theme](https://antora-supplemental.github.io/antora-dark-theme)
- Full guide: [README.adoc](README.adoc)
- Catalog hub: [antora-supplemental.github.io/docs](https://antora-supplemental.github.io/docs/)

## License

[MIT](LICENSE)
