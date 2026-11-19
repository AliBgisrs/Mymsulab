# ABZN Lab website · project handbook

Website of the ABZN Lab (Dr. Ali Bazrafkan, Precision Agriculture, Montana State University).
This file lists every piece of the project, where it lives, and how to keep it running. Keep it with the project.

## Where everything is

| Piece | Location | Purpose |
|---|---|---|
| Live website | https://alibgisrs.github.io/Mymsulab/ | Public address to share |
| Source repository | https://github.com/AliBgisrs/Mymsulab (branch `main`) | Permanent copy of the site: `index.html`, `assets/`, `data/`, this handbook, `PUBLISH.md`. GitHub Pages serves the site from here. |
| Working folder (PC) | `C:\Ali\Claude\Mymsulab` | Where design changes are made before being pushed to GitHub |
| Content sheet | https://docs.google.com/spreadsheets/d/16iduezkIRjY_VqzfTmB8dpkZz41bqc38xC7xwi2oosM | All text content: team, publications, news, software, equipment, research, settings. Read by the live site on every page load. Shared "anyone with the link can view". |
| Image folder (Drive) | https://drive.google.com/drive/folders/1cHONnzuOEFiBVc7gkyLZgXwM-cYBwbE3 | Photos and figures referenced by link from the sheet. Shared "anyone with the link can view". |
| Backup folder (Drive) | https://drive.google.com/drive/folders/1xBwCSNe-qtOtq0S3ZaUJsaKEmGCwMRuu | Copies of this handbook, `PUBLISH.md` and `data/README.md`. The site files themselves are archived in the GitHub repository (Code → Download ZIP). |
| Design canvas | https://claude.ai/artifact/5mYA24jnV7NjZ7tpkvAQNg | Design mock-ups (desktop, phone, style tile) made before the site was built |
| Weekly publish job | Claude desktop app → Scheduled → "ABZN website · Monday publish to GitHub" | Mondays 08:00, pushes changed files from the PC folder to GitHub through Chrome |

## How the site works

- `index.html` is the whole site: one file with the HTML, CSS and JavaScript, plus Three.js loaded from a CDN for the hero animation. No build step, no server code.
- On load, the page reads the seven tabs of the Google Sheet through Google's visualization endpoint and fills the sections. If the sheet cannot be reached it falls back to the CSV files in `data/`, and if those fail it shows the copy built into the HTML.
- Images in the sheet can be a file name (served from `assets/`) or a web link (Google Drive share links are converted automatically).
- Team members are grouped by the `level` column: PI, postdoc, phd, ms, undergrad, alumni.

## Routine updates (no technical steps)

1. Text, people, papers, news: edit the Google Sheet, reload the site.
2. Pictures: drop the file in the Drive image folder, copy its share link, paste the link into the `photo` or `image` cell.
3. Details and column lists: `data/README.md`.

## Design changes

Edit `index.html` in the working folder (or ask Claude to), then publish: `PUBLISH.md` explains the Monday job and the manual upload. Keep the palette (#1d241a green, #d9a441 gold, #b3452c rust, #f5f3ec cream) and the fonts Source Serif 4, Archivo, JetBrains Mono.

## Recovering the project

- Lost the PC folder: download the repository (GitHub → Code → Download ZIP). It is complete.
- Lost GitHub access: the same files can be hosted anywhere that serves static files; the sheet and Drive links keep working.
- Lost the sheet: `data/*.csv` in the repository holds a copy of the content as of the last publish; set `SHEET_ID: ''` in `index.html` to use it, or import the CSVs into a new sheet, share it by link and put its id in `SHEET_ID`.
- Moving to a university server: copy `index.html`, `assets/` and `data/` into the web root. Nothing else is needed.

## Accounts involved

GitHub `AliBgisrs` (repository and Pages), the Google account that owns the sheet and the Drive folder, and the Claude account that holds the design canvas and the scheduled job. Nothing is stored anywhere else.
