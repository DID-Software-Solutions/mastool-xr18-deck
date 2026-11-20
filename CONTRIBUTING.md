# Contributing

Thanks for helping with the MasTool XR18 deck. The full guide is in [docs/editing.md](docs/editing.md). This page is the short version.

## The basics

- The deck is two hand-written HTML files: `index.html` (English) and `he/index.html` (Hebrew). There is no build step.
- Every slide change goes in both languages. Use the checklist in [docs/editing.md](docs/editing.md#keep-the-two-languages-in-sync).
- In the Hebrew file, wrap numbers with units and negative levels in `<span class="l">...</span>`.
- Preview with `python3 -m http.server`, then open both languages.
- Rebuild both PDFs after a slide change. The command is in [docs/editing.md](docs/editing.md#rebuild-the-pdfs).
- When the app changes, use the checklist in [docs/link-map.md](docs/link-map.md) to find the slides to update.

## Proposing a change

Open a pull request with a focused change and a short description of what moved and why. Commit messages follow Conventional Commits, for example `docs: ...` or `fix: ...`.

The README notes that routine slide fixes are pushed straight to `main`. Larger changes and documentation are welcome as pull requests so they can be reviewed first.

## Before you commit

- Both languages updated, slide counts checked.
- PDFs rebuilt.
- No personal details such as emails, usernames or local paths in files or commit messages.
