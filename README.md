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
- Not listed: 43 catalog entries (33 whose package name is already covered by an npm entry,
  10 whose repository could not be resolved), plus entries with no `dsh.bundle`.

## Regenerating

```sh
# 1. snapshot the catalog
curl -s https://cdn.jsdelivr.net/gh/web-casa/Awesome-DeepSeek-Harness-Plugins@main/data/plugins.json \
  -o data/cordis-plugins.json
# 2. npm pass + GitHub pass (needs an authenticated `gh`)
node scripts/build-market-index.mjs data/cordis-plugins.json site
node scripts/add-git-entries.mjs data/cordis-plugins.json site/index.json site/index-v2.json
# 3. publish site/index-v2.json as index.json
```

DeepSeek Harness caches a successfully read index for 10 minutes.

Titles, descriptions, authors and versions are third-party content; DSH validates the file format
only and installs never happen without confirmation.
