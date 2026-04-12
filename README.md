# Antora Dark Theme

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Antora 3.x](https://img.shields.io/badge/antora-3.x-purple.svg)](https://antora.org)

Dark mode supplemental UI for [Antora](https://antora.org) documentation sites.

## Install

Install the published package as a development dependency:

```bash
# npm
npm install --save-dev antora-dark-theme

# pnpm
pnpm add -D antora-dark-theme

# yarn
yarn add -D antora-dark-theme

# bun
bun add -d antora-dark-theme
```

Then configure your playbook file(s) (typically `antora-playbook.yml`) to use the theme.

### Method 1: Use pre-built bundle (Recommended)

The easiest way to use this theme is to point your Antora playbook directly to the latest pre-built UI bundle. This includes the Antora Default UI plus all dark mode enhancements without requiring any local package installation.

```yaml
ui:
  bundle:
    url: https://github.com/antora-supplemental/antora-dark-theme/releases/latest/download/ui-bundle.zip
    snapshot: true
```

### Method 2: Use as npm dependency

Install the package:

```bash
pnpm add -D antora-dark-theme
```

Then reference the supplemental UI from `node_modules`:

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files: ./node_modules/antora-dark-theme/supplemental-ui
```

### Method 3: Stacked Overrides (Deep Customization)

To override the dark theme's own overrides with your project-specific customizations, use an array for `supplemental_files`. Paths listed later take precedence.

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files:
    - ./node_modules/antora-dark-theme/supplemental-ui
    - ./site/src
```

## Features

- Dark mode toggle button (sun/moon icons)
- System preference detection
- Persistent preference via localStorage
- No flash of unstyled content (FOUC)
- Works with Antora Default UI — no fork required

## Documentation

Full documentation and live demo: [antora-supplemental.github.io/antora-dark-theme](https://antora-supplemental.github.io/antora-dark-theme)

For other installation options, including the pre-built UI bundle and copying `supplemental-ui` directly, see the [official README.adoc](https://github.com/antora-supplemental/antora-dark-theme/README.adoc).

## License

[MIT](LICENSE)
