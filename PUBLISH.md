# Publishing the ABZN Lab website to GitHub

The live site is https://alibgisrs.github.io/Mymsulab/ and is served by GitHub Pages from the `main` branch of https://github.com/AliBgisrs/Mymsulab.

## What needs publishing, and what does not

- **Never**: text content, members, publications, news, research rows. They come from the Google Sheet and appear on the live site as soon as the sheet is edited.
- **Never**: photos and figures that are given as Google Drive links in the sheet.
- **Only when changed**: `index.html` (design changes), files in `assets/` (images referenced by file name), files in `data/` (the CSV fallback and its README).

## The weekly job

A scheduled task in the Claude desktop app, "ABZN website · Monday publish to GitHub", runs every Monday at 8:00 on this computer. It compares this folder with the repository and, when something differs, uploads the changed files through Claude in Chrome (the GitHub web upload page) and commits them to `main`. It reports back in the Claude session that created it.

Conditions for it to work:

1. The Claude desktop app is open on this PC at 8:00 on Monday. If it is closed, the task runs the next time the app is opened.
2. Chrome is signed in to GitHub as `AliBgisrs`, and the Claude in Chrome extension is installed and connected.
3. Nothing else is needed: no git, no terminal.

## Doing it by hand (same steps)

1. Open https://github.com/AliBgisrs/Mymsulab/upload/main (for images: `/upload/main/assets`, for CSVs: `/upload/main/data`).
2. Drag the changed files onto the page.
3. Type a short commit summary, keep "Commit directly to the main branch", click "Commit changes".
4. Wait one or two minutes, then reload the live site with Ctrl+F5.

## Detection rules the job uses

- `index.html`: uploaded when the local file differs from https://raw.githubusercontent.com/AliBgisrs/Mymsulab/main/index.html.
- `assets/` and `data/`: uploaded when a local file name is missing from the repository folder. A changed image that keeps its old name is not detected; give edited images a new name (for example `pc-2.jpg`) and update the sheet cell.
