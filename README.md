# Farewell Wall Video

Farewell Wall is a single-file client-side web app that turns a colleague's name and team messages into an animated whiteboard video you can preview and download.

## Key features

- Canvas-based whiteboard animation (client-side only).
- Add a colleague name, an optional profile image (file input -> base64), a centered final message, and multiple team messages.
- Drag-to-reorder messages with immediate preview updates.
- Theme selector (Auto / Light / Dark) persisted in localStorage (`themePref`).
- Lightweight UI: Iconify icons + Picnic CSS.
- Preview (play/stop) and generate a downloadable video (MediaRecorder with audio mixing).

## Important files

- `index.html` — single-file app containing HTML, CSS, and JavaScript (primary file to edit).
- `assets/music/` — place music files here (the app looks for `music-1.mp3`, `music-2.mp3`, `music-3.mp3`).
- `img/sticky_note_collage.svg` — hero image used on the home screen.
- `README.md` — this document.

## Quick preview (local)

- Open index.html in a browser (double-click) or serve the folder:

  - Python: `python3 -m http.server 8000` then open http://localhost:8000
  - Node: `npx http-server -c-1`

No build step or package manager required.

## Data model & DOM hooks

The app uses a simple DATA structure in the inline script:

```
DATA = { name, final, notes: [{ a, t }, ...], userPic }
```

Critical DOM IDs (do not rename unless updating the script):
- Inputs / UI: `nm`, `fin`, `nl`, `userPic` (file input), `preview` (image preview)
- Canvas & controls: `cv`, `play`, `stop`, `rec`, `dl`, `add`, `clr`, `shuf`
- Music controls: `music-select`, `mus` (checkbox), `music-vol`
- Playback speed: `speed` (note: speed does NOT affect music playback)

## Music behaviour

- Per-note sound effects were removed; the app now plays background music from external files in `assets/music/`.
- The dropdown `music-select` lists: `No music`, `music-1`, `music-2`, `music-3` (hardcoded). Place those files in `assets/music/`.
- Music is decoded with Web Audio and played as an AudioBufferSourceNode; playbackRate is fixed at 1 so changing the preview speed does NOT change music tempo.
- Music is mixed into recordings (MediaRecorder) when recording is enabled.
- Music stops automatically when the preview ends or when playback is stopped.

## Image handling

- Add a profile image using the `userPic` file input. The image is converted to a base64 data URL and shown in the `preview` image element.
- The final note draws the uploaded image as a square at the bottom-center of the note; the image is optional.

## Button/icon alignment

- Buttons use inline-flex with centered icon + label to ensure icons align vertically with text across browsers.

## Recording & browser notes

- Recorder prefers MP4 but falls back to WebM; many browsers only support WebM for MediaRecorder.
- Recording captures video + mixed audio (music if enabled).
- Generating a recording is done in real time and may take as long as the preview (~30–60s depending on content).

## Development notes

- Make targeted edits to `index.html` to preserve behavior. The code intentionally keeps logic inline for simplicity.
- If adding music files, put `music-1.mp3`, `music-2.mp3`, and `music-3.mp3` in `assets/music/`.

## Known limitations & next steps

- Mobile drag fallback needed for reliable touch reordering.
- Cross-browser testing for MediaRecorder/Audio (Safari, Firefox) — expect WebM-only in many cases.
- Accessibility: keyboard reorder for messages and ARIA labels can be improved.

## Music contributions

- [farewell to W. : Partyton](https://pixabay.com/music/beautiful-plays-farewell-to-w-111721/)
- [Best of Luck : amadozapana](https://pixabay.com/music/future-bass-best-of-luck-126966/)
- [Closing Scene - Hopeful Farewell : Sonican](https://pixabay.com/music/ambient-closing-scene-hopeful-farewell-562094/)

## Contributing

Open a pull request with clear scope. Small UI fixes and documentation updates welcome.
