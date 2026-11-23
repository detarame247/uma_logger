# UmaLogger

A single-page chatlog editor for building **Uma Musume-style event logs** — pick an event, add your chatters, write the dialogue, and export the finished log as a PNG, JPG or PDF.

Everything runs in the browser. No account, no server, no build step: `index.html` is the whole app.

<img alt="Static site" src="https://img.shields.io/badge/runtime-browser%20only-7dcb0b"> <img alt="No build step" src="https://img.shields.io/badge/build-none-f9f9f9"> <img alt="Exports" src="https://img.shields.io/badge/export-PNG%20%C2%B7%20JPG%20%C2%B7%20PDF%20%C2%B7%20JSON-ff76a4">

---

## Features

- **Live preview** — a pixel-accurate mock of the in-game log card updates as you type.
- **Event header** — custom event name plus an optional event image, with an empty icon slot when none is set.
- **95 built-in character icons** — searchable picker with name highlighting; click once to add a chatter and use their icon.
- **Custom chatters** — rename anyone, upload your own avatar, reset to the default icon, or remove them (with undo).
- **Rich text messages** — bold, italic, custom/preset colours, text sizes and font families, applied to a selection without losing the caret.
- **Message tools** — reorder up/down, edit, insert above, duplicate, delete.
- **Narration mode** — messages with no name or avatar.
- **Autosave** — your session is kept in `localStorage` and offered back on the next visit.
- **Project files** — save and reload the whole log as JSON.
- **Exports** — PNG, JPG (95% quality) and PDF at 2× resolution, saved wherever you choose via the browser's save picker (falling back to a normal download).
- **Clean exports** — editing controls, message action buttons and the page credit link are excluded from every exported image.

## Quick start

Clone or download the repository and open `index.html` in a modern browser.

```bash
git clone https://github.com/<your-user>/<your-repo>.git
cd <your-repo>
```

Then either double-click `index.html`, or serve the folder locally (recommended, so the icon catalogue loads from `character_icons/icons.json`):

```bash
python -m http.server 8000
# then open http://localhost:8000
```

Opening the file directly also works — the app falls back to its built-in character list when `icons.json` can't be fetched.

## How to use it

The left panel is the editor, split into five tabs; the right panel is the log you are building.

| Tab | What it does |
| --- | --- |
| **Event** | Set the event title and upload an event image (or remove it). |
| **Icons** | Search the character catalogue and click an icon to add that chatter. Clicking someone already in the list selects them instead of duplicating. |
| **Chatters** | Manage names and avatars, add custom chatters, reset or remove entries. |
| **Message** | Pick who is talking (or narration), format the text, then **Send Message**. `Enter` sends, `Shift+Enter` adds a line break. |
| **Export** | Save a PNG, JPG or PDF, or save/load a project file. |

Hovering a message in the preview reveals its action buttons (move, edit, insert, duplicate, delete). Removing a chatter also removes their messages, and the toast offers an undo.

Uploaded images are automatically downscaled (max 512 px on the long side, ~200 KB threshold) so project files stay small.

## Project structure

```
.
├── index.html              # The entire app: markup, styles and logic
├── 47211.ttf               # Custom display font used by the log
├── default.jpg             # Default (avatar-less "Selection") icon
├── character_icons/
│   ├── icons.json          # Catalogue consumed by the icon picker
│   └── *.png               # 95 character icons
└── README.md
```

## Requirements

- A current version of Chrome, Edge, Firefox or Safari.
- An internet connection for the first load: `html2canvas`, `jsPDF` and the Nunito webfont come from CDNs. The custom font, icons and all app logic are local.

## Notes and limitations

- **No autosave history.** Autosave keeps the latest state only; use **Save Project** for anything you want to keep long-term.
- **Exports render the preview at a fixed width.** Very long logs produce one tall image/PDF page rather than paginated pages.
- **The save picker is Chromium-only.** Other browsers fall back to a regular download; the file still goes where your browser puts downloads.
- **Character icons and names are fan-made assets** of the Uma Musume characters and remain the property of their respective owners.

## Credits

- Built by [@Detarame247](https://x.com/Detarame247).
- Rendering for exports by [html2canvas](https://html2canvas.hertzen.com/); PDF generation by [jsPDF](https://github.com/parallax/jsPDF).
- Uma Musume Pretty Derby and its characters are © Cygames, Inc. This is an unofficial fan tool, not affiliated with or endorsed by Cygames.

## License

No license file is included yet. The application code is shared for personal, fan-made use; the bundled character icons, character names and font remain the property of their respective owners and are not covered by any code license.
