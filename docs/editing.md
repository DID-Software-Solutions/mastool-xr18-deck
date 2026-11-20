# Editing the deck

How the deck is built, how to change it, and how to publish it.

## How it is built

- Each language is one self-contained HTML file: `index.html` (English) and `he/index.html` (Hebrew). Styles, slides and script live in the same file.
- There is no build step and nothing to install. Open the file in a browser.
- The only other asset is `rehearsal-control-mac.png`, used on slide 23 in both languages (`he/index.html` loads it as `../rehearsal-control-mac.png`).
- Each slide is a `<section class="slide">` inside `#deck`. Title and divider slides add `title` or `section` to the class.
- A comment such as `<!-- 17 -->` sits above each slide. The comments are for humans only and are not read by the script.
- The page script finds all `.slide` elements, shows one at a time, and scales the 1280 by 720 stage to the window.
- The footer with the slide number ("17 / 30") is added by the script to every slide except title and divider slides. The total updates by itself.
- Charts on slides 13, 14, 17 and 21 are SVG. On slides 13 and 14 the script draws them. The values are in `filterChart(...)` calls and in the `rows` array.
- The PDFs are produced by printing the pages. A `@media print` rule shows every slide, one per page, at 1280 by 720.

## Navigation

| Action | English | Hebrew |
|---|---|---|
| Next slide | Right arrow, Page Down, Space, Enter, click right half | Same keys plus Down arrow, click left half |
| Previous slide | Left arrow, Page Up, Backspace, click left half | Same keys plus Up arrow, click right half |
| First or last slide | Home, End | Home, End |
| Fullscreen | F | F |
| Jump to a slide | Add `#N` to the URL | Add `#N` to the URL |

The language button (top right in English, top left in Hebrew) keeps you on the same slide. The English page links to `he/#N`. The Hebrew page links to `../#N` and caps N at 30, because English has no slide 31. If you change the English slide count, update that cap in the `show()` function of `he/index.html`.

## Right-to-left handling

- `he/index.html` sets `<html lang="he" dir="rtl">`, so layout, lists and tables flow right to left.
- The CSS mirrors the English file: list padding moves to the right, table text aligns right, colour swatches get a left margin, the progress bar grows from the right, and the title gradient is flipped.
- Charts are drawn left to right, because frequency always runs low to high from the left. The rule `svg{direction:ltr}` keeps them that way. Add `class="rtl"` to an SVG when its text labels are Hebrew (slides 17 and 21 do this).
- Technical terms stay in English inside Hebrew sentences. The glossary on slides 30 and 31 explains them.

### The `<span class="l">` rule

Hebrew text can reorder numbers, units and minus signs. Wrap every number with a unit, and every negative level, in `<span class="l">` in the Hebrew file:

```html
<span class="l">-20 dB</span>
<span class="l">80 Hz</span>
<span class="l">Aux 3-4</span>
```

The class sets `direction:ltr`, isolates the text from the surrounding bidi flow, and stops it from wrapping. Without it, `-20 dB` can render as `20- dB`. The same CSS applies to `<code>` and `<kbd>`, so those need no wrapper.

Check each Hebrew slide in the browser after editing. Bidi problems show up on screen, not in the source.

## Add, remove or reorder a slide

Do the same change in both files.

1. Add, delete or move the `<section class="slide">...</section>` block in `index.html`.
2. Repeat in `he/index.html`. Copy the English block and translate it (see below).
3. Renumber the `<!-- N -->` comments in both files so they stay in order.
4. Update every place that holds a slide number:
   - The "slides 30-31" sentence in `README.md`.
   - The language button cap in `he/index.html` (`Math.min(cur+1,30)`).
   - `docs/slide-outline.md` and the slide numbers in `docs/link-map.md`.
   - Any text on a slide that points at another slide by number.
5. Count the slides in each file (command below) and open both decks to check the footer totals.
6. Rebuild both PDFs.

```sh
grep -c '<section class="slide' index.html he/index.html
```

Adding slides at the end of the Hebrew deck, after the glossary, is the one case where the English deck does not need a matching slide. Glossary slides are the only planned difference between the two decks.

## Translate a slide

1. Copy the English `<section>` into `he/index.html` at the same position.
2. Translate the visible text. Keep class names, inline styles, the structure and the `<b>`, `<i>` and `<code>` tags.
3. Keep technical terms in English: mix, send, aux, low-cut, 48V, Check mixer, and the button names from the app.
4. Wrap numbers with units and negative levels in `<span class="l">`.
5. Reverse arrows in flow diagrams. The Hebrew deck uses `←` where English uses `→`.
6. Copy the `src` of any image with `../` in front of the path.
7. Reuse the Hebrew wording already used for the same idea on other slides. Search the file before inventing a new phrase.
8. If you add a new technical term, add it to the glossary on slide 30 or 31.
9. Open the slide in the browser and check that numbers, units and arrows read correctly.

## Keep the two languages in sync

Run through this list before every commit that touches a slide.

- [ ] The change is made in `index.html` and in `he/index.html`.
- [ ] Every number, unit and channel reference is identical in both files (low-cut values, channel numbers, jack names, levels in dB).
- [ ] `grep -c '<section class="slide'` shows 30 for English and 31 for Hebrew, or the new agreed counts.
- [ ] Slide comments are renumbered in both files.
- [ ] Hebrew numbers with units and negative levels are wrapped in `<span class="l">`.
- [ ] Charts match: the `filterChart(...)` calls and the `rows` array hold the same values in both files.
- [ ] New terms appear in the Hebrew glossary.
- [ ] The slide numbers in `README.md` and in the files under `docs/` are current.
- [ ] Both decks open without console errors and the language button keeps the slide.
- [ ] Both PDFs are rebuilt and show the same page counts as the HTML.

A quick comparison of the numbers that appear in each file:

```sh
for f in index.html he/index.html; do grep -o '[0-9][0-9]* Hz' "$f" | sort | uniq -c; done
```

The two lists match today. The only extra line is `000 Hz`, which comes from "1,000 Hz" in the Hebrew glossary. Any other difference is worth a look.

## Preview locally

```sh
python3 -m http.server 8000
```

Run it in the repo root, then open `http://localhost:8000/` for English and `http://localhost:8000/he/` for Hebrew. Double-clicking the HTML files also works. A local server matches the GitHub Pages behaviour for relative paths.

## Rebuild the PDFs

Use Chrome in headless mode from the repo root. This is the command from the README. It has been run against both decks and produces 30 pages for English and 31 for Hebrew.

```sh
C="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
"$C" --headless=new --no-pdf-header-footer --print-to-pdf="$PWD/xr18-rehearsal.pdf" "file://$PWD/index.html"
"$C" --headless=new --no-pdf-header-footer --print-to-pdf="$PWD/xr18-rehearsal-he.pdf" "file://$PWD/he/index.html"
```

Chrome may print unrelated warnings about displays or web apps. Ignore them if the "bytes written" line appears. On Linux or Windows, use the path of your Chrome or Chromium binary.

After a rebuild, check the page count and flip through the PDF. A page that spills over means a slide has too much content for 720 pixels.

## Deploy

- The site is served by GitHub Pages from the `main` branch. `.nojekyll` tells Pages to serve the files as they are.
- Merged changes go live within a minute or two.
- English: https://did-software-solutions.github.io/mastool-xr18-deck/
- Hebrew: https://did-software-solutions.github.io/mastool-xr18-deck/he/

The README states that every change is pushed straight to `main`, with no PRs. That rule is unchanged. The documentation in this folder was proposed through a pull request instead, so the maintainer can review it before it lands. See [CONTRIBUTING.md](../CONTRIBUTING.md) for the short version.

Commit messages follow Conventional Commits (`docs: ...`, `fix: ...`, `feat: ...`).

## Open items

- **Speaker notes.** The HTML has no notes mechanism. There is no presenter view, no `<aside>` handling and no notes in the page script. Adding notes needs a script change and a design decision, so it is listed here and not done.
- **Automated checks.** Slide counts and numbers are compared by hand with the commands above. A small script could do it.
- **App version stamp.** The deck does not say which app version it describes. Slide 29 could carry one.
