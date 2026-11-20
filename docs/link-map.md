# Link map: deck, app, site and PDFs

## How the pieces relate

- **The app** lives in the private repo `DID-Software-Solutions/xr18-config`. It sets up the XR18 and saves each player's in-ear mix. The agreed setup is data in `xr18rehearsal/plan.py`.
- **The deck** (this repo) explains the app and the rig to the band. It is written by hand. Nothing is generated from the app, so no tool warns you when the two drift apart.
- **The Pages site** serves `index.html` and `he/index.html` from `main` at https://did-software-solutions.github.io/mastool-xr18-deck/.
- **The PDFs** (`xr18-rehearsal.pdf`, `xr18-rehearsal-he.pdf`) are printed from the same HTML files. They are committed, so they go stale until someone rebuilds them.
- **The screenshot** `rehearsal-control-mac.png` is a copy of the app's `docs/rehearsal-control-mac.png`. The two files are identical today.
- The app README points to the deck and says to update it there when the plan changes. The changelog of the app records the deck's move to this repo (v0.5.2) and the 70 Hz guitar low-cut (v0.5.3).

```
xr18-config (app)                 mastool-xr18-deck (this repo)
  plan.py  --- written by hand --->  index.html, he/index.html
  README, CHANGELOG                    |            |
  docs/rehearsal-control-mac.png       |            +--> Pages site (main branch)
        copied by hand --------------> rehearsal-control-mac.png
                                       +--> PDFs (Chrome print)
```

The source of truth for every number is the app: `plan.py` first, then the app README. If the deck and the app disagree, check `plan.py` and fix the deck.

## What to update for each kind of app change

Slide numbers refer to the English deck. Hebrew slides 1 to 29 use the same numbers. See [slide-outline.md](slide-outline.md).

| App change | Deck places to update |
|---|---|
| Low-cut value on a channel | Slide 4 (table), the role slide for that channel (7 to 10), slide 14 (`rows` array in the script), slide 15 (table and reason text). Slide 13 says "12 of our channels" and changes only if a channel gains or loses a low-cut |
| Low-cut added or removed on a channel | Same as above, plus the count on slide 13 and the "off" rows on slides 4 and 15 |
| New or changed mute group | Slide 3 (channel strip box), slide 4 (Mute grp column), slides 7 to 10 (role slides), slide 20 (table and text), slide 23 (Mute groups row) |
| New channel, or a channel number shift | Slides 3, 4, 7 to 10 (own channels), 13 (count), 14 (`rows`), 15, 17 (17 inputs), 18 (17 sends), 20 (mute table), 22 (USB 1-16), 23, 27 (17 inputs), 28 (patch step), and the glossary if there is a new term |
| Starting mix levels | Slides 7, 8 and 17 |
| In-ear mix, jack or bus change | Slides 3, 5, 7 to 10, 21, 23 |
| Player added or renamed | Slides 3, 5, 7 to 10, 18, 21, 23, and the swap example on slide 18 |
| Pan, link or 48V change | Slides 3, 4, 8, 20, 25 |
| Ambience (room) mic behaviour | Slides 4, 20, 25, 28 (step 5) |
| USB recording routing | Slides 3, 5, 22, 28 (step 8) |
| Button or label renamed, new button | Slides 11, 23, 24, 25, 28 |
| Autosave interval, undo depth, state file path or keys | Slides 8, 11, 18, 19 |
| Safety behaviour | Slides 18, 20, 25 |
| Protocol, CLI, stack or CI | Slide 26 |
| Boundaries (what the app does or does not touch) | Slide 27 |
| Release status, device-day progress | Slide 29 |
| New window layout | Screenshot file, slide 23 |

The Hebrew file needs the same edit for each row. Remember `<span class="l">` around numbers with units.

## When the app changes, update the deck

Use this list after any app release that touches the plan, the window or the behaviour.

- [ ] Read the app `CHANGELOG.md` entries since the last deck update.
- [ ] Open `plan.py` and compare the values the deck shows: low-cuts, 48V, pans, mute groups, starting levels, buses, roles, players.
- [ ] Find the rows that match the change in the table above, and edit those slides in `index.html`.
- [ ] Make the same edits in `he/index.html`.
- [ ] Search both files for the old value (for example `grep -n '80 Hz' index.html he/index.html`) so no stray copy is left. Slides 4, 14 and 15 each hold their own copy of low-cut values.
- [ ] If the window changed, take a new screenshot, replace `rehearsal-control-mac.png`, and check that slide 23 still matches the labels.
- [ ] Update slide 29 if something moved from "still to do" to "done".
- [ ] Walk through both decks in the browser, then run the sync checklist in [editing.md](editing.md#keep-the-two-languages-in-sync).
- [ ] Rebuild both PDFs and check the page counts.
- [ ] Update [slide-outline.md](slide-outline.md) if slide titles, order or counts changed.
- [ ] Commit the deck change with a message that names the app version, for example `docs: guitar low-cut 70 Hz (app v0.5.3)`.

## Example: the guitar low-cut moved to 70 Hz (app v0.5.3)

The change touched slide 4 (table row for channels 5-6), slide 8 (guitar role text), slide 14 (`["Gtr 1-2 (5-6)", ..., 73, 6000, 70]`) and slide 15 (table row and the 73 Hz reason). It was made in both languages and in both PDFs. That is the pattern to follow for any value change.
