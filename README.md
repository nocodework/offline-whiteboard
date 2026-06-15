<div align="center">

# 🧩 offline-whiteboard

### A private, offline whiteboard in a **single HTML file.**

No account. No server. No tracking. Your data never leaves your browser.

[![License: MIT](https://img.shields.io/badge/license-MIT-7C3AED.svg)](LICENSE)
![Dependencies: 0](https://img.shields.io/badge/dependencies-0-22C55E)
![Single file](https://img.shields.io/badge/single%20file-~60%20KB-3B82F6)
![Network requests: 0](https://img.shields.io/badge/network%20requests-0-22C55E)
![Vanilla JS](https://img.shields.io/badge/vanilla-JS-EAB308)

**[▶ Try it live](https://nocodework.github.io/offline-whiteboard/)** — no signup &nbsp;·&nbsp; or just [download `index.html`](https://raw.githubusercontent.com/nocodework/offline-whiteboard/main/index.html) and open it. That's the whole app.

![offline-whiteboard screenshot](screenshot.png)

</div>

---

## Why this exists

Most whiteboards (Miro, FigJam, …) want an account, run in the cloud, and send your boards to someone else's servers. That's a non-starter if you work somewhere with **no internet access** or **strict security rules** — exactly where a quick visual board is most useful.

**offline-whiteboard** is the opposite:

- 🔒 **Private by design.** Everything is stored locally in your browser (`localStorage`). Nothing is ever uploaded. _Verified: the page makes **0 network requests** — no fonts, no CDN, no analytics._
- 📴 **Works fully offline — even air-gapped.** Copy one file onto a locked-down machine and it just works. No install, no internet, no permissions.
- 📄 **One file.** `index.html` (~60 KB). No build step, no `npm install`, no framework, no dependencies. Open it with a double-click.
- 🆓 **Free & open source** (MIT). Fork it, host it, bundle it, rebrand it.

## Features

- 🟨 **Sticky notes**, rectangles, ellipses and free **text**
- ➡️ **Arrows / connectors** that snap to edges and follow items as you move them
- 🗺️ **Infinite canvas** — pan & zoom (mouse, trackpad, touch)
- 🎯 Multi-select, drag, **resize**, 8-color palette, **duplicate**
- ↩️ **Undo / redo** (full history)
- 💾 **Auto-save** to your browser + **import / export `.json`** + **export PNG**
- ⌨️ Keyboard shortcuts for everything

## Use it

| | How |
|---|---|
| **Fastest** | [Open the live demo](https://nocodework.github.io/offline-whiteboard/) and start drawing. |
| **Offline / air-gapped** | [Download `index.html`](https://raw.githubusercontent.com/nocodework/offline-whiteboard/main/index.html), copy it anywhere (USB stick, locked-down PC), double-click. Done. |
| **Self-host** | Drop `index.html` on any static host (or `git clone` and open). No backend needed. |

## Keyboard shortcuts

| Key | Action | Key | Action |
|---|---|---|---|
| `V` | Select & move | `A` | Arrow (drag item → item) |
| `H` / `Space` | Pan view | double-click | Edit text / new note |
| `N` | Sticky note | `⌫` | Delete selection |
| `R` `O` `T` | Rectangle / ellipse / text | `⌘Z` / `⌘⇧Z` | Undo / redo |
| wheel | Pan | `⌘`+wheel | Zoom |

## Privacy & security

- **No network requests.** Open your browser's DevTools → Network tab, reload — you'll see only the HTML file itself loading. Nothing else.
- **No telemetry, no cookies, no account.** There is no backend to send anything to.
- **Your data lives in `localStorage`** on your device. Clearing site data or using `Clear` wipes it. Use **Export** to back up or move a board as a `.json` file.
- Because it's one self-contained file, it's trivial to audit: open `index.html` and read it.

## How it works

Vanilla JavaScript, no libraries. The board is rendered on a single HTML5 `<canvas>` using a world→screen transform, with a `<textarea>` overlay for text editing (the same approach Excalidraw uses). Because rendering is just canvas code, **PNG export reuses the exact same drawing functions** — what you export is pixel-identical to what you see.

State is a small JSON model (`elements` + `connections`) persisted to `localStorage` and exportable to a `.json` file.

```jsonc
{
  "app": "offline-whiteboard",
  "version": 1,
  "elements": [
    { "id": "n1", "type": "note", "x": 40, "y": 60, "w": 195, "h": 120, "text": "Idea", "color": "#FEF08A" }
  ],
  "connections": [
    { "id": "c1", "from": "n1", "to": "r1" }
  ]
}
```

## Comparison

| | offline-whiteboard | Miro / FigJam | Excalidraw |
|---|:---:|:---:|:---:|
| Works with **zero internet** | ✅ | ❌ | ⚠️ (PWA install) |
| **No account** needed | ✅ | ❌ | ✅ |
| **Single file**, no build | ✅ | ❌ | ❌ |
| Self-host in seconds | ✅ | ❌ | ⚙️ |
| Open source | ✅ | ❌ | ✅ |
| Real-time collaboration | ❌ | ✅ | ✅ |

It's intentionally small: a whiteboard you **fully own and can carry in one file**. If you need live multiplayer, use Excalidraw or Miro.

## Contributing

Issues and PRs welcome — see [CONTRIBUTING.md](CONTRIBUTING.md). The whole app is one readable file; there's no toolchain to set up.

## License

[MIT](LICENSE) © [NoCodeWork](https://nocodework.io) (Mikołaj Brunka). Use it for anything.

---

<div align="center">
Built with vanilla JS and stubbornness. If it's useful, a ⭐ helps others find it.
</div>
