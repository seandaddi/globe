[README.md](https://github.com/user-attachments/files/29070769/README.md)
# Interactive Globe 🌍

An embeddable 3D globe for a personal website that highlights places I've **lived** and **visited**. It auto-syncs from a published Google Sheet, so adding a new place is as simple as editing a spreadsheet — no code changes required.

**Live site:** `https://YOUR-USERNAME.github.io/globe/`

---

## Features

- **Interactive globe** — drag to spin, slow auto-rotate when idle, hover for a label, click a point for details.
- **Two layers** — *Lived* (yellow) and *Visited* (off-white), each toggleable from the legend.
- **Google Sheet sync** — the globe reads its data from a published Google Sheet on every load.
- **Personal notes** — click a place and jot a note; it saves in your browser.
- **Self-contained** — the deployed `index.html` has everything inlined (map data, libraries, fonts) and works offline aside from the live Sheet fetch.

---

## How it's hosted

The file `index.html` is served by **GitHub Pages** from the `main` branch (root folder). It's a single self-contained HTML file — no build step on GitHub's side.

---

## Updating the places (the easy way)

All place data lives in a **published Google Sheet**. To add, edit, or remove a place:

1. Open the Google Sheet.
2. Add or edit a row. Columns:

   | column   | required | notes                                  |
   |----------|----------|----------------------------------------|
   | `name`   | yes      | Place name shown on the globe          |
   | `type`   | yes      | `lived` or `visited`                   |
   | `lat`    | yes      | Latitude (decimal degrees)             |
   | `lng`    | yes      | Longitude (decimal degrees)            |
   | `region` | no       | e.g. "California, USA"                 |
   | `years`  | no       | e.g. "2018 – present"                  |
   | `note`   | no       | Shown in the detail card to visitors   |

3. Save. The globe shows the change the next time the page loads.

> Tip: to get coordinates, right-click a spot in Google Maps and the lat/lng is at the top of the menu.

The Sheet must be published: **File → Share → Publish to web → (the sheet) → Comma-separated values (.csv) → Publish.**

---

## Embedding on Google Sites (or any site)

Use an iframe pointing at the GitHub Pages URL:

```html
<iframe src="https://YOUR-USERNAME.github.io/globe/"
        style="width:100%;height:600px;border:0;"></iframe>
```

In Google Sites specifically: **Insert → Embed → By URL** → paste the GitHub Pages URL → resize the block → **Publish**.

---

## Changing the design (colors, layout, behavior)

The source of truth is **`Globe.dc.html`**. The deployed `index.html` is a compiled, inlined bundle of it. To change the look:

1. Edit `Globe.dc.html`.
2. Re-bundle it into a single self-contained file.
3. Save that bundle as `index.html`.
4. Upload the new `index.html` to this repo (**Add file → Upload files → Commit** — same filename overwrites the old one).
5. GitHub Pages redeploys in ~1 minute; hard-refresh to see it.

Tweakable defaults near the top of the logic in `Globe.dc.html`:

- `SHEET_CSV_URL` — the published Google Sheet CSV link (data source).
- `KML_SOURCES` — optional Google My Maps KML files, used only if no Sheet URL is set.
- The baked-in `places` array — an offline fallback used if the Sheet can't be reached.

---

## Files in this repo

| file                    | purpose                                                        |
|-------------------------|----------------------------------------------------------------|
| `index.html`            | The deployed, self-contained globe (this is what GitHub serves)|
| `Globe.dc.html`         | Editable source for the globe                                  |
| `Globe (embeddable).html` | The bundled output (copied to `index.html` for deployment)   |
| `places.csv`            | Starter spreadsheet — import into Google Sheets                |
| `lived.kml` / `visited.kml` | Original Google My Maps exports (reference / backup)       |

---

## Troubleshooting

- **Globe won't drag or click** → make sure you uploaded the latest `index.html`, then hard-refresh (Cmd/Ctrl + Shift + R). GitHub Pages can cache the old file for a minute or two.
- **A new place isn't showing** → confirm the Sheet is still *published* and the row has valid `lat`/`lng` numbers, then reload.
- **404 on the GitHub Pages URL** → check that `index.html` is at the repo **root** (not in a subfolder) and that Pages is set to deploy from `main` / `(root)`.
