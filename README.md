# Mushaf — content downloads

Download host for the [Mushaf app](https://github.com/ahmedReda1)'s optional content packs: tafsir
databases fetched on demand, so the app install stays small. This repository holds no code; each
**release** is one content version, and its assets are the packs.

| Release tag | Matches app content version |
|---|---|
| `content-2026.11.25` | 2026.11.25 |

## Files

Each asset is a gzipped SQLite database: `<tafsir-id>.db.gz`. The app downloads it, decompresses it
and checks its SHA-256 against the manifest built into the app; a file that doesn't match is
discarded. Don't rename or re-compress assets.

| File | Tafsir | Language | Source |
|---|---|---|---|
| `saadi.db.gz` | Tafsir al-Sa'di — Abd al-Rahman al-Sa'di | Arabic | Quran.com API |
| `ibn-kathir-ar.db.gz` | Tafsir Ibn Kathir | Arabic | Quran.com API |
| `tabari.db.gz` | Tafsir al-Tabari | Arabic | Quran.com API |

These are classical works; the texts were obtained through the Quran.com API. Specific digital
editions may carry their own terms — see the app's licensing notes.

Modern translated tafsirs (e.g. English abridgements) are **not** published here until
redistribution permission is granted by their publishers.

## Publishing a new content version

From the app repository, after `py pipeline/build.py`:

```sh
gh release create content-<version> --repo ahmedReda1/mushaf-content \
  build/downloads/saadi.db.gz build/downloads/ibn-kathir-ar.db.gz build/downloads/tabari.db.gz
```

Only upload packs cleared for redistribution (`license_status` in `pipeline/config/sources.json`).
