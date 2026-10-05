# Farewell Wall Video

Farewell Wall is a small single-file web app that turns a colleague's name and team messages into an animated whiteboard-style video you can preview and download.

## Key features

- Canvas-based whiteboard animation (client-side only).
- Add a colleague name, a centered final message, and multiple team messages.
- Drag-and-drop reorder for team messages with immediate preview updates.
- Theme selector (Auto / Light / Dark) persisted in localStorage (`themePref`).
- Iconify icons and Picnic CSS for lightweight UI styling.
- Preview (play/stop) and generate a downloadable video (MediaRecorder with audio mixing).

## Important files

- `index.html` — single-file app containing HTML, CSS, and JavaScript (primary file to edit).
- `img/sticky_note_collage.svg` — hero image used on the home screen.
- `README.md` — this document.

## Quick preview (local)

- Open index.html in a browser (double-click) or serve the folder:

  - Python: `python3 -m http.server 8000` then open http://localhost:8000
  - Node: `npx http-server -c-1`

There is no build step or package manager required.

## Data model & DOM hooks

The app uses a simple DATA structure in the inline script:

```
DATA = { name, final, notes: [{ a, t }, ...] }
```

Critical DOM IDs (do not rename unless updating the script): `nm`, `fin`, `nl`, `cv`, `play`, `stop`, `rec`, `dl`, `snd`, `mus`, `music-vol`, `add`, `clr`, `shuf`.

## Customization

- Visual variables are at the top of the stylesheet (`:root`): `--bg`, `--fg`, `--card`, `--accent`.
- Canvas constants (resolution and font) live at the top of the inline script (`W`, `H`, `FONT`).
- Theme preference stored in `localStorage.themePref` and applied via `data-theme` on `<html>`.

## Recording & browser notes

- The recorder attempts MP4 first and falls back to WebM; many browsers only support WebM for MediaRecorder.
- Generating a recording is done in real time and may take ~40s for a full run.
- HTML5 drag-and-drop can be inconsistent on some touch devices; a pointer/touch fallback is recommended if mobile support is critical.

## Development notes

- Make small, surgical edits to `index.html` (markup, styles, inline JS) to preserve app behavior.
- There are no tests or linters configured. Add tooling if you plan automated checks.
- For large refactors consider splitting CSS/JS into separate files.

## Known limitations & next steps

- Mobile drag fallback needed for reliable touch reordering.
- Cross-browser testing for MediaRecorder/Audio (Safari, Firefox) — expect WebM-only in many cases.
- Accessibility: keyboard reorder for messages and ARIA labels can be improved.

## Contributing

Open a pull request with clear scope. Small UI fixes and documentation updates welcome.
