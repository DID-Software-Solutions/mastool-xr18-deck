# MasTool XR18: rehearsal rig presentation

Slides for the band about how the XR18 rehearsal rig works: the signal flow, what matters to each player, high-pass and low-pass filters, how swaps and saved in-ear mixes work, and a checklist for rehearsal day.

**Open it:** https://did-software-solutions.github.io/mastool-xr18-deck/

- Next/previous slide: arrow keys, or click/tap the right/left half of the screen. **F** = fullscreen. On a phone, turn it sideways.
- PDF to send around: [xr18-rehearsal.pdf](xr18-rehearsal.pdf)

The app itself lives in the private repo `DID-Software-Solutions/xr18-config`.

## Files

| File | What |
|---|---|
| `index.html` | The slides. One file, no build step, nothing to install |
| `rehearsal-control-mac.png` | App screenshot used on the "The app" slide |
| `xr18-rehearsal.pdf` | PDF version (30 pages, 16:9) |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

## Update the PDF

After editing `index.html`, rebuild the PDF with Chrome:

```sh
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --no-pdf-header-footer \
  --print-to-pdf="$PWD/xr18-rehearsal.pdf" "file://$PWD/index.html"
```

Every change is pushed straight to `main` (no PRs) and is live within a minute or two.
