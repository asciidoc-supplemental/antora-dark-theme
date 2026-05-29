# npm: deprecate CLI vs final patch publish

## `npm deprecate` (registry metadata only)

```bash
npm deprecate antora-dark-theme@* "Your message here"
```

| Where | What users see |
|-------|----------------|
| **npmjs package page** | Yes — a **deprecation banner** on the package (and per-version pages if you deprecated specific versions). Your message text is shown there. |
| **`npm install`** | Yes — `npm WARN deprecated` with your message in the terminal. |
| **README on npmjs** | **No change** — still the README from the last *published tarball*. |

Deprecating the **entire** package can also reduce search visibility on npmjs (per npm docs).

Does not upload new files. No git tag required.

## Final patch `npm publish` (what we use for README)

Publishes a new version whose **README.md** becomes the main tab on npmjs.

| Where | What users see |
|-------|----------------|
| **npmjs package page** | Updated **README** (our formal DEPRECATED notice). |
| **`npm install`** | Warning if `deprecated` is set in the published `package.json` (included in tarball). |
| **Banner** | Use **both**: publish the patch, then `npm deprecate` older versions if you want every version line to show the banner. |

## Recommended one-time sequence

1. Bump patch in `package.json`, remove `"private": true` temporarily.
2. `npm publish --access public` (from package root; `files` controls tarball contents).
3. Restore `"private": true` in git; commit version bump; push; tag `vX.Y.Z` for GitHub `ui-bundle.zip` if needed.
4. Optional: `npm deprecate antora-dark-theme@"<1.0.10" "message"` so older versions also show the banner.

Scoped package:

```bash
npm publish --access public   # in @amdphreak/architexture-theme-antora
```
