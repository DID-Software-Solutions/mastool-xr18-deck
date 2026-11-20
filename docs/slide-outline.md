# Slide outline

Slide-by-slide map of the deck. The English deck has 30 slides and the Hebrew deck has 31. Counts come from the `<section class="slide">` elements in `index.html` and `he/index.html`.

The "App feature or doc" column names the section of the app README (repo `DID-Software-Solutions/xr18-config`) or the source module that the slide describes. See [link-map.md](link-map.md) for how to use this when the app changes.

## English deck

| # | Title | Purpose | App feature or doc |
|---|---|---|---|
| 1 | The XR18, the in-ears and the app that runs them | Title slide | App README intro |
| 2 | From no in-ears to everyone hearing their own mix | Why the rig exists and what it gives the band | App README intro, Run it |
| 3 | How sound flows through the rig | One-page signal flow: sources, channel strip, sends, in-ear mixes | The setup, Safety behaviour (`plan.py`) |
| 4 | What's plugged in where | Per-channel table: name, source, low-cut, 48V, pan, mute group | The setup (channel table, `plan.CHANNELS`) |
| 5 | Which jack feeds whose in-ears | Output jacks, roles, duet jacks, USB send and return | The setup (in-ear mix table, `plan.ROLES`, `plan.BUSES`) |
| 6 | What matters to you | Section divider, Part 1 | None |
| 7 | Or: three bass channels, one fixed seat | Bass player view: channels, low-cut, starting mix, mute group 4, Hi-Z | The setup, `plan.default_mix` |
| 8 | Dan / Jonny: each of you keeps your own mix | Guitar view: pan, 70 Hz low-cut, swap behaviour, mute group 3 | The setup, Run it (autosave) |
| 9 | Ben / Barak: solo or duet | Vocals view: solo vs Both, Aux 5 and 6, low-cut, no mute group | The setup (duet rows), `plan.DUET` |
| 10 | Daniel / Nadav: your mix is the channel faders | Drums view: Main L/R, drum low-cuts, mute group 2 | The setup, Safety behaviour |
| 11 | The operator's job: pick people, flip switches, check | What the laptop operator does before and during rehearsal | Run it, Modules (`app.py`) |
| 12 | Filters: low-cut, high-cut, high-pass, low-pass | Section divider, Part 2 | None |
| 13 | The name says what's allowed through | Filters 101 with two curve charts (drawn by the page script) | `hz_to_hpf`, OSC addresses (`preamp/hpf`) |
| 14 | Where each instrument lives, and where we cut | Range bars against each low-cut (the `rows` array in the page script) | The setup (low-cut values) |
| 15 | Every low-cut has a reason | Table of low-cut values and the reason for each | The setup, `plan.CHANNELS` |
| 16 | How everything is managed | Section divider, Part 3 | None |
| 17 | Why your mix is only yours | Pre-fader sends diagram and what the app remembers per player | The setup (all sends pre-fader), State file (`prefs`) |
| 18 | What happens when you click "Jonny" | Five-step swap: read, save, dip, load, restore | `Rehearsal.set_player`, Safety behaviour |
| 19 | No Save button. Ever. | Autosave, undo depth, the state file, the log | State file, Log file |
| 20 | Channel on/off, room-mic power and mute groups | Switches, 48V sequence for room mics, mute group table | Run it (Channels, Mute groups), `plan.MUTE_GROUPS` |
| 21 | Two singers, two separate mixes | Duet mode diagram | The setup (duet rows), `plan.DUET_BUS` |
| 22 | Every input, straight to the laptop over USB | USB recording routing and the backing-track catch | Recording over USB |
| 23 | One window, top to bottom | Annotated screenshot (`rehearsal-control-mac.png`) | Run it, `app.py` |
| 24 | Set up vs Sync vs Check | What each of the three buttons writes | `Rehearsal.apply_base`, `.sync`, `.check` |
| 25 | Built so nobody gets a blast in their ears | Safety behaviour table | Safety behaviour |
| 26 | How the app talks to the mixer | OSC, stack, CLI, simulator, CI | Stack, Command line, OSC addresses used, Develop |
| 27 | What the app doesn't touch | Boundaries: gain, EQ, Hi-Z, cables, what is not saved per player | Device-day checklist |
| 28 | Checklist | Ten steps for rehearsal day | Device-day checklist |
| 29 | Where it stands | Done list and still-to-do list | Device-day checklist, CHANGELOG |
| 30 | Words you'll hear | Glossary (14 terms, two columns) | None |

## Hebrew deck

Hebrew slides 1 to 29 match the English slides with the same numbers. The Hebrew deck then has two glossary slides instead of one.

| # | Title | Note |
|---|---|---|
| 1 to 29 | Same content as English 1 to 29 | Slide 1 adds one line saying the audio terms stay in English and the glossary is at the end |
| 30 | Glossary, part 1 of 2 | Core mixing terms: in-ears, mix, aux, send, fader, pre-fader, tap, master, Main L/R, channel strip, gain, pan, stereo and mono, link, mute, talkback, dB, Hz, patch |
| 31 | Glossary, part 2 of 2 | Filters, mics and recording terms: low-cut, high-cut, cutoff, rumble, bleed, headroom, EQ, 48V, condenser and dynamic, DI, Hi-Z, cab, kick and snare, overheads, ambience, backing track, E-Pad, USB send and return, DAW, OSC |

Differences to keep in mind:

- The Hebrew glossary is larger than the English one (40 terms against 14), because the Hebrew deck keeps audio terms in English and explains them there.
- The language button on the Hebrew deck caps the slide number at 30, so Hebrew slide 31 opens English slide 30.
- The English language button opens `he/#N` with the same N. Slides 1 to 29 line up one to one.
- The Hebrew deck is right to left. Slide 3 arrows point left, and "next" is a click on the left half of the screen.

## Counting slides

```sh
grep -c '<section class="slide' index.html he/index.html
```

This prints 30 for `index.html` and 31 for `he/index.html`.
