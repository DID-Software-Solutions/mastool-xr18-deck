# MasTool XR18: rehearsal rig presentation

Slides for the band about how the XR18 rehearsal rig works: the signal flow, what matters to each player, high-pass and low-pass filters, how swaps and saved in-ear mixes work, and a checklist for rehearsal day.

| Language | Slides | PDF |
|---|---|---|
| English | https://did-software-solutions.github.io/mastool-xr18-deck/ | [xr18-rehearsal.pdf](xr18-rehearsal.pdf) |
| עברית | https://did-software-solutions.github.io/mastool-xr18-deck/he/ | [xr18-rehearsal-he.pdf](xr18-rehearsal-he.pdf) |

- Next/previous slide: arrow keys, or click/tap a side of the screen (English: right = next, Hebrew: left = next). **F** = fullscreen. On a phone, turn it sideways.
- The **English / עברית** button in the top corner switches language and stays on the same slide.
- The Hebrew version keeps the audio terms in English (mix, send, low-cut...) and explains them in a glossary at the end (slides 30-31).

The app itself lives in the private repo `DID-Software-Solutions/xr18-config`.

## Files

| File | What |
|---|---|
| `index.html` | English slides. One file, no build step, nothing to install |
| `he/index.html` | Hebrew slides (right-to-left) |
| `rehearsal-control-mac.png` | App screenshot used on the "The app" slide (both languages) |
| `xr18-rehearsal.pdf`, `xr18-rehearsal-he.pdf` | PDF versions (16:9) |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

Change a slide in both languages. In the Hebrew file, wrap numbers with units and negative levels in `<span class="l">...</span>` so they stay left-to-right (`-20 dB`, `80 Hz`).

## Update the PDFs

After editing, rebuild the PDFs with Chrome:

```sh
C="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
"$C" --headless=new --no-pdf-header-footer --print-to-pdf="$PWD/xr18-rehearsal.pdf" "file://$PWD/index.html"
"$C" --headless=new --no-pdf-header-footer --print-to-pdf="$PWD/xr18-rehearsal-he.pdf" "file://$PWD/he/index.html"
```

Every change is pushed straight to `main` (no PRs) and is live within a minute or two.

## Documentation

| Doc | What it covers |
|---|---|
| [docs/slide-outline.md](docs/slide-outline.md) | Every slide with its purpose and the app feature it describes, English and Hebrew numbers |
| [docs/editing.md](docs/editing.md) | How the deck is built, editing and translating slides, PDFs, local preview, deploy |
| [docs/link-map.md](docs/link-map.md) | How the deck, the app, the site and the PDFs relate, and what to update when the app changes |

See also [CONTRIBUTING.md](CONTRIBUTING.md).
