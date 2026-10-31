# dsh-plugin-market

A DeepSeek Harness plugin market index (format 1) generated from the
[cordis.run](https://cordis.run/plugins) plugin catalog (331 entries).

Add it as a market source in DeepSeek Harness:

1. **Plugins → Discover → Add index source**
2. `https://raw.githubusercontent.com/ccjiao/dsh-plugin-market/main/index.json`

## Contents

- **322 plugins** — 147 published to npm (every non-deprecated version declaring `dsh.bundle`) and
  175 resolved from GitHub repositories (default-branch commit, package directory that declares
  `dsh.bundle`).
- **193 are installable on DSH 0.2.1-rc.5**; 129 declare `engines.dsh` / `@deepseek-ai/dsh*` peer
  ranges for the 0.1.x line and are shown without a compatible version.

## Compatibility metadata

The index carries one `engines.dsh` range per version so the Discover badge matches what
installation accepts: a package-declared `engines.dsh` wins, otherwise the range is derived by
intersecting the package's `@deepseek-ai/dsh*` peer dependency ranges (a single DSH installation
satisfies all of them at one version). Without this, plugins that only declare peers appeared
compatible and were rejected at install time.

## Regenerating

```sh
# 1. snapshot the catalog
curl -s https://cdn.jsdelivr.net/gh/web-casa/Awesome-DeepSeek-Harness-Plugins@main/data/plugins.json \
  -o data/cordis-plugins.json
# 2. npm pass + GitHub pass (GitHub pass needs an authenticated `gh`)
node scripts/build-market-index.mjs data/cordis-plugins.json site
node scripts/add-git-entries.mjs data/cordis-plugins.json site/index.json site/index-v2.json
# 3. check what installs on the current runtime, then publish site/index-v2.json as index.json
node scripts/compat-report.mjs site/index-v2.json 0.2.1-rc.5 site/compat.json
```

DeepSeek Harness caches a successfully read index for 10 minutes.

Titles, descriptions, authors and versions are third-party content; DSH validates the file format
only and installs never happen without confirmation.
