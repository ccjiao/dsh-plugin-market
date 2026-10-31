# dsh-plugin-market

A DeepSeek Harness plugin market index (format 1), generated from the
[cordis.run](https://cordis.run/plugins) catalog and filtered to the plugins that install on
**DSH 0.2.1-rc.5**.

Add it as a market source in DeepSeek Harness:

1. **Plugins → Discover → Add index source**
2. `https://raw.githubusercontent.com/ccjiao/dsh-plugin-market/main/index.json`

## Contents

- **193 plugins** — every one has at least one version whose `engines.dsh` accepts DSH 0.2.1-rc.5.
  Incompatible plugins (129) and incompatible versions (726) are removed, so Discover never offers an
  install the compatibility gate would reject.
- The catalog had 331 entries; 147 publish to npm, 175 exist only as GitHub repositories
  (default-branch commit + package directory declaring `dsh.bundle`), and the rest share a package
  name or could not be resolved.

## Compatibility metadata

The index carries one `engines.dsh` range per version: a package-declared range wins, otherwise it is
derived by intersecting the package's `@deepseek-ai/dsh*` peer ranges (a single DSH installation
satisfies all of them at one version). This is what makes filtering meaningful: plugins that only
declare peers are pinned to the runtime line they were built against.

## Regenerating

```sh
# 1. snapshot the catalog
curl -s https://cdn.jsdelivr.net/gh/web-casa/Awesome-DeepSeek-Harness-Plugins@main/data/plugins.json \
  -o data/cordis-plugins.json
# 2. npm pass + GitHub pass (GitHub pass needs an authenticated `gh`)
node scripts/build-market-index.mjs data/cordis-plugins.json site
node scripts/add-git-entries.mjs data/cordis-plugins.json site/index.json site/index-full.json
# 3. keep only versions compatible with the target runtime
node scripts/filter-market-index.mjs site/index-full.json 0.2.1-rc.5 site/index.json
node scripts/compat-report.mjs site/index.json 0.2.1-rc.5 site/compat.json
```

Publish `site/index.json`. DeepSeek Harness caches a successfully read index for 10 minutes, and
raw.githubusercontent caches the previous file for several minutes after a push.

Titles, descriptions, authors and versions are third-party content; DSH validates the file format
only and installs never happen without confirmation.
