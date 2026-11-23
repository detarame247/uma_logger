# UmaLogger

A browser-only editor for building **Uma Musume-style chat logs**. Set the event header, pick your chatters, write the dialogue, and export the finished log as a PNG, JPG or PDF — or save it as a project file and come back to it later.

There is no account, no server and no build step. `index.html` is the whole application, and everything you type stays in your browser.

![Runtime: browser only](https://img.shields.io/badge/runtime-browser%20only-7dcb0b)
![Build: none](https://img.shields.io/badge/build-none-f9f9f9)
![Export: PNG / JPG / PDF / JSON](https://img.shields.io/badge/export-PNG%20%C2%B7%20JPG%20%C2%B7%20PDF%20%C2%B7%20JSON-ff76a4)

---

## Features

### Event header
- Custom event title that updates the preview as you type.
- Optional event image — upload your own, or clear it to show the empty icon slot.
- **Character Event**: pick one character from the event-art catalogue. The **upper half** of her artwork is cropped into the event icon slot, the square gold frame stays exactly as it is, and she is automatically added to the talkers with her chat icon. Only one Character Event character can be chosen at a time: selecting a different one updates that talker in place (messages included) instead of adding another.

### Chatters
- **95 built-in chat icons** in a searchable picker with match highlighting. Clicking an icon adds that character as a talker; clicking someone already in the list selects them instead of duplicating them.
- Rename anyone, upload a custom avatar, reset back to the default icon, or remove a talker with an undo option.
- **+ Add Chatter** for characters that are not in the catalogue — as many as the scene needs.

### Messages
- Pick the speaker from the talker list, or use **Narration** for a message with no name or avatar.
- Bold, italic, custom colour and four preset colours, seven text sizes, and font families including the bundled `CustomFont`, Nunito, Arial, Courier and Times.
- Formatting applies to a selection without losing the caret.
- Per-message tools: move up/down, edit, insert above, duplicate, delete.
- `Enter` sends, `Shift+Enter` adds a line break. Pasted text is inserted as plain text so outside styling cannot break the layout.

### Saving and exporting
- **Autosave** keeps the current session in `localStorage` and offers to restore it on your next visit.
- **Save Project / Load Project** store the whole log — event, chatters, icons, messages — as JSON.
- **PNG, JPG (95% quality) and PDF** exports render the preview at 2× resolution.
- Files are saved wherever you choose through the browser's save picker, with a normal download as the fallback.
- Exports contain only the log card: editing controls, message action buttons and the page credit link are excluded.

## Quick start

Download or clone this repository, then open `index.html` in a current browser.

Opening the file directly works, but serving the folder locally is recommended:

```bash
python -m http.server 8000
# then open http://localhost:8000
```

Serving over HTTP matters for **Character Event**: browsers block reading pixels from local `file://` images, so on a direct file open the event art is shown whole instead of cropped to its upper half. Everything else works either way.

## How to use it

The left panel is the editor and the right panel is the log you are building.

| Tab | What it does |
| --- | --- |
| **Event** | Set the event title, upload an event image, pick a **Character Event** character, or remove the image. |
| **Icons** | Search the chat icon catalogue; click an icon to add that talker, or to select them if they already exist. |
| **Chatters** | Manage names and avatars, add custom talkers, reset icons, remove entries. |
| **Message** | Choose the talker, format the text, then **Send Message**. `Enter` sends, `Shift+Enter` breaks the line. |
| **Export** | Save a PNG, JPG or PDF, or save and load project files. |

Hovering a message in the preview reveals its action buttons. Removing a chatter also removes their messages, and the toast offers an undo.

Uploaded images are downscaled automatically (max 512 px on the long side) so autosave and project files stay small.

## Project structure

```
.
├── index.html                  # The entire app: markup, styles and logic
├── 47211.ttf                   # Custom display font used by the log
├── default.jpg                 # Default icon for chatters without a character icon
├── character_icons/
│   ├── icons.json              # Catalogue used by the chat icon picker
│   └── *.png                   # 95 chat icons
├── character_event_icons/
│   ├── icons.json              # Catalogue used by the Character Event picker
│   └── *.png                   # 71 full-character event artworks
└── README.md
```

Both `icons.json` files are convenience catalogues: if they cannot be fetched, the app falls back to the built-in lists inside `index.html`.

## Requirements

- A current version of Chrome, Edge, Firefox or Safari.
- An internet connection for the first load: `html2canvas` and `jsPDF` come from cdnjs, and the Nunito webfont comes from Google Fonts. The custom font, icons and all application logic are local.

## Good to know

- **No autosave history.** Autosave keeps the latest state only — use **Save Project** for anything you want to keep.
- **One long page.** Exports render the preview at a fixed width, so a very long log becomes one tall image or PDF page rather than paginated pages.
- **The save picker is Chromium-only.** Other browsers fall back to a regular download; the file still lands where your browser puts downloads.
- **Character Event crops are automatic.** The artwork is cut to a square inside its upper half, so art framed differently may crop awkwardly — upload a manual event image for those cases.
- **No tests or build tooling.** There is nothing to install; the app is a single HTML file plus local assets.

## Credits

- Built by [@Detarame247](https://x.com/Detarame247).
- Image rendering for exports by [html2canvas](https://html2canvas.hertzen.com/); PDF generation by [jsPDF](https://github.com/parallax/jsPDF).
- Uma Musume Pretty Derby and its characters are © Cygames, Inc. This is an unofficial fan tool, not affiliated with or endorsed by Cygames.

## License

No license file is included yet. The application code is shared for personal, fan-made use. The bundled character icons, event art, character names and font remain the property of their respective owners and are not covered by any code license.
