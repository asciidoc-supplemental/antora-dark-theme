# Refreshing the npm registry README (one-time)

The public text on [npmjs.com/package/antora-dark-theme](https://www.npmjs.com/package/antora-dark-theme) comes from `README.md` in the **last published tarball**.

To update it after editing `README.md` / `deprecated` in `package.json`:

1. Temporarily remove `"private": true` from `package.json` (restore after publish).
2. Bump patch version (e.g. `1.0.10`).
3. Tag is **not** required for npm-only notice; either:
   - `npm publish --access public` from a maintainer machine (workflow no longer publishes npm), or
   - `npm deprecate antora-dark-theme "<deprecated message>"` for install warnings without a new README.

Prefer publishing one final patch so the registry README matches `README.md`.

Then deprecate or unpublish on npm when traffic is zero.
