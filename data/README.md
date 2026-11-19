# Updating the ABZN Lab website

Everything that changes on the site (team, publications, news, software, equipment, research, the recruiting banner, stats, links) is read from a spreadsheet when the page opens. You never edit `index.html`.

There are two ways to keep that spreadsheet. Pick one.

## The Google Sheet (active, nothing to set up)

The site reads this sheet every time it opens:
https://docs.google.com/spreadsheets/d/16iduezkIRjY_VqzfTmB8dpkZz41bqc38xC7xwi2oosM

It is shared as "anyone with the link can view" (the site needs that to read it; only you can edit). It is already wired into `index.html` and works even when the page is opened from your own disk. There is no publish step and no file to upload.

**To update the site:** open the sheet, add or change a row, then reload the site (Ctrl+F5). Google may serve the previous version for a minute or two.

**Photos and figures, with no upload to GitHub:**

1. Use the Google Drive folder "ABZN website images" (https://drive.google.com/drive/folders/1cHONnzuOEFiBVc7gkyLZgXwM-cYBwbE3). It is already shared as "anyone with the link can view", so files dropped into it inherit that.
2. Drop the image there (a roughly square headshot about 600×600 px for people; a tightly cropped figure about 1600 px wide for research).
3. Right-click the file → Share → Copy link, and paste the link into the `photo` cell (team) or `image` cell (research). Reload the site.

Leave `photo` empty to show initials instead (typed in `initials`, or made from the name). A plain file name such as `student-jane.png` still works for files uploaded to the site's `assets` folder on GitHub.

## Fallback · CSV files in this folder

If the sheet is ever unavailable or you prefer not to use Google, set `SHEET_ID: ''` in `index.html` and the site reads the `.csv` files in this folder instead (same columns). Edit them in Excel, File → Save As → **"CSV UTF-8 (Comma delimited) (*.csv)"**, and upload to the hosted `data` folder. Browsers block this path when the page is opened from disk; it works once hosted.

## Rules that keep things working

- Never rename a tab or file, never delete or rename the header row. Column order does not matter; column names do (lower case).
- A row is ignored when its key cell is empty: `name` for team / software / equipment, `title` for publications / news / research, `key` for settings. Extra blank rows at the bottom are fine.
- Several tags in one cell: separate with `|` (for example `YOLOv11|Sentinel-2|ArcGIS`). In research `chips`, commas work too.
- Dates in `news`: `2026-08-15`, `2026-08` or `2026`. Newest shows first. Leave `date` empty and fill `label` (for example `Earlier`) for undated items; they sort last.
- Yes/no cells (`hiring`, `new`): type `YES`, or leave empty for no.
- Any image size works. Member photos are scaled to fill the circle and the overflow is cropped (keeping the upper part, where the face usually is), so a roughly square headshot is best. Research images are never cropped: the frame takes the shape of the figure (between 4:5 and about 2:1), so charts, axes and legends stay complete. Extremely wide or tall figures get a small cream margin.
- Photos and figures, two ways. (a) A web link: upload the image to a Google Drive folder that is shared as "anyone with the link can view", right-click → Share → Copy link, and paste that link into the `photo` or `image` cell. No GitHub upload needed. Any other direct image link works too, and a GitHub "blob" link is converted automatically. (b) A file name such as `student-jane.png`, for a file that sits in the site's `assets` folder on GitHub. Missing or broken image = initials are shown for people, an empty frame for research.
- If a whole section fails to load, the site silently shows the built-in copy. Check that the file saved as CSV UTF-8 and that the key column is filled.

## Columns

**settings** (`key`, `value`): `hiring` (YES shows the recruiting banner and the open positions), `recruit_text`, `recruit_link`, `email`, `scholar_url`, `github_url`, `linkedin_url`, `coords` (footer), `marquee` (the ticker under the hero, items separated by `|`), and up to six stats: `stat1_value`, `stat1_decimals`, `stat1_suffix`, `stat1_label` … `stat6_label`.

**team**: `order`, `kind` (`pi`, `member` or `open`), `level`, `name`, `role`, `focus`, `photo`, `initials`, `bio` (PI only), `email`, `scholar`, `github`, `linkedin` (PI only). `open` rows become the "Open positions" band; remove them when a position is filled.

The team is shown as a hierarchy, always in this order: PI, then **Postdoctoral researchers**, **Ph.D. students**, **M.S. students**, **Undergraduate researchers**, **Alumni**. The `level` cell decides the group: `postdoc`, `phd`, `ms`, `undergrad` or `alumni` (`pi` for the PI). Within a group, `order` sets the sequence. When a student graduates, change their `level` to `alumni` and, if you like, their `role` to e.g. `Ph.D. 2027 · now at USDA`; alumni are shown in a muted style. If `level` is empty the site guesses from the `role` text (e.g. "Ph.D. student", "UnderGrad Student"), but filling it in is safer. Empty groups are not shown.

**publications**: `year`, `title`, `authors`, `venue`, `url`, `new` (YES shows the badge; a paper from the current year is flagged automatically when this is empty), `order` (within a year). Sorted newest year first.

**news**: `date`, `label`, `title`, `text`.

**software**: `order`, `name`, `description`, `url`, `icon` (`convert`, `layers`, `plant`, `grid`, `rows`, `github`), `style` (`all` for the dark "all repositories" card).

**equipment**: `order`, `name`, `description`, `spec` (short mono text on the right, e.g. `400–1000 nm`), `icon` (`drone`, `camera`, `spectrum`, `thermal`, `lidar`, `gpu`).

**research**: `order`, `title`, `metric` (wrap a number in asterisks to make it gold: `YOLOv11 · *0.98* precision`), `text`, `chips` (`|`-separated), `image` (file in `assets`), `alt` (image description).
