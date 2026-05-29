# Antora Dark Theme

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Antora 3.x](https://img.shields.io/badge/antora-3.x-purple.svg)](https://antora.org)

Dark mode supplemental UI for [Antora](https://antora.org) documentation sites.

## Quick start (recommended)

Point your playbook at the **release UI bundle** (Antora Default UI + this theme, already merged). You only need Antora in your toolchain—not this package on npm.

```yaml
ui:
  bundle:
    # Pin a version for reproducible CI (see GitHub Releases for tags)
    url: https://github.com/antora-supplemental/antora-dark-theme/releases/download/v1.0.9/ui-bundle.zip
    snapshot: true
```

Custom logo, favicon, or a few partials? Add **one** supplemental directory on top of the bundle (not a second theme install):

```yaml
  supplemental_files: ./supplemental-ui-overrides   # e.g. img/logo.svg only
```

See [examples/antora-playbook.yml](examples/antora-playbook.yml).

## Which installation path should I use?

| Goal | Use |
|------|-----|
| Ship dark docs with minimal moving parts | **Method 1** — release `ui-bundle.zip` |
| Logo / favicon / a few UI files | **Method 1** + small `supplemental_files` directory |
| Theme version in `package.json` + many custom partials on Default UI | **Method 2** — npm `supplemental-ui` overlay |
| Fork or heavily edit theme sources | **Method 3** — vendor `supplemental-ui` in your repo |

**Avoid:** listing multiple supplemental **directories** in YAML (Antora does not support that). **Avoid:** copying from `node_modules` on every build unless you intentionally vendor the theme.

The [npm package](https://www.npmjs.com/package/antora-dark-theme) ships the same `supplemental-ui` folder for Method 2 and for theme development; most documentation sites should prefer the release bundle.

## Method 1: Pre-built UI bundle (recommended)

```yaml
ui:
  bundle:
    url: https://github.com/antora-supplemental/antora-dark-theme/releases/download/v1.0.9/ui-bundle.zip
    snapshot: true
  # Optional: only your overrides (single directory)
  supplemental_files: ./supplemental-ui-overrides
```

Use `releases/latest/download/ui-bundle.zip` only if you accept floating updates; pin `releases/download/vX.Y.Z/ui-bundle.zip` in CI.

## Method 2: npm supplemental overlay (advanced)

Use when the theme must live in your Node lockfile **and** you layer many custom partials/CSS on the **Antora Default UI** bundle (not the pre-built theme zip).

```bash
pnpm add -D antora-dark-theme
```

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files: ./node_modules/antora-dark-theme/supplemental-ui
```

For custom files on top of npm, use **one** merged directory: copy `node_modules/antora-dark-theme/supplemental-ui` into your repo (e.g. `supplemental-ui/`), edit there, and point `supplemental_files` at that single path—or use virtual file entries (below).

## Custom overrides (valid Antora patterns)

Antora’s `ui.supplemental_files` accepts **either** a single directory path **or** an array of [virtual files](https://docs.antora.org/antora/latest/playbook/ui-supplemental-files) (`path` + `contents`). A YAML list of multiple **directories** is not supported.

**Small override directory on the release bundle** (typical: logo, favicon):

```yaml
ui:
  bundle:
    url: https://github.com/antora-supplemental/antora-dark-theme/releases/download/v1.0.9/ui-bundle.zip
    snapshot: true
  supplemental_files: ./supplemental-ui-overrides
```

**Virtual files** (single files without a full supplemental tree):

```yaml
  supplemental_files:
    - path: img/logo.svg
      contents: ./branding/logo.svg
```

**Virtual override of one partial:** each entry needs `path` and `contents`. If you replace `partials/head-meta.hbs`, start from this theme’s partial so CSS and dark-mode scripts still load.

## Method 3: Vendor `supplemental-ui` in your repo

Copy the `supplemental-ui` folder from this repository when you maintain a fork or long-lived fork of the theme assets:

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files: ./supplemental-ui
```

## FTN layout stylesheet (optional)

The package also ships `supplemental-ui/css/site-ftn-docs.css`: Source Sans, in-flow header + **doc mast** (breadcrumb / component + version), **ftn-body** + left nav that fills the column, and other layout rules used on [docs.foodtrucknerdz.com](https://docs.foodtrucknerdz.com). It expects the **FTN** Handlebars partials (for example `header` with `ftn-doc-mast`, `body` with `ftn-body`, `main` with `ftn-article`). Load it **after** `site-extra.css` in your `head-meta` (or a merged supplemental directory):

```html
<link rel="stylesheet" href="{{{uiRootPath}}}/css/site-extra.css">
<link rel="stylesheet" href="{{{uiRootPath}}}/css/site-ftn-docs.css">
```

Sites that use only the default Antora layout do not need this file.

## Features

- Dark mode toggle button (sun/moon icons)
- System preference detection
- Persistent preference via localStorage
- No flash of unstyled content (FOUC)
- Works with Antora Default UI — no fork required

## Releasing (maintainers)

Do **not** run `pnpm publish` or `npm publish` on your machine. Set `package.json` `version` to the release, commit, then create and push a `vX.Y.Z` tag (e.g. `git tag v1.0.4 && git push origin v1.0.4`). [.github/workflows/release.yml](.github/workflows/release.yml) runs on that tag, creates the [GitHub Release](https://github.com/antora-supplemental/antora-dark-theme/releases) with the `.tgz` and merged `ui-bundle.zip`, and may publish to the npm registry when trusted publishing is configured.

## Documentation

Full documentation and live demo: [antora-supplemental.github.io/antora-dark-theme](https://antora-supplemental.github.io/antora-dark-theme)

For the full AsciiDoc guide (same content, more detail), see [README.adoc](https://github.com/antora-supplemental/antora-dark-theme/blob/main/README.adoc).

## License

[MIT](LICENSE)
