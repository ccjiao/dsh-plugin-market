# dsh-plugin-market

A DeepSeek Harness plugin market index (format 1) generated from the
[cordis.run](https://cordis.run/plugins) plugin catalog.

- `index.json` — the index. Add it as a market source in DeepSeek Harness:
  **Plugins → Discover → Add index source** →
  `https://raw.githubusercontent.com/ccjiao/dsh-plugin-market/main/index.json`
- Regenerate with the generator in the DSH repo (`apps/plugin-market-generator`) or with
  `build-market-index.mjs` from the catalogue snapshot.

Covers the catalog entries published to npm whose versions declare `dsh.bundle`.
Entries that only exist as GitHub repositories, or that declare no bundle, are omitted.

The plugin titles, descriptions, authors and versions are third-party content; DSH validates
the file format only.
