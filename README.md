# Antora Dark Theme

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Antora 3.x](https://img.shields.io/badge/antora-3.x-purple.svg)](https://antora.org)

Dark mode supplemental UI for [Antora](https://antora.org) documentation sites.

## Install

Install the published package as a development dependency:

```bash
npm install --save-dev antora-dark-theme
```

Then configure your playbook file(s) (typically `antora-playbook.yml`) to load the supplemental UI from `node_modules`:

```yaml
ui:
  bundle:
    url: https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable
    snapshot: true
  supplemental_files: ./node_modules/antora-dark-theme/supplemental-ui
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
