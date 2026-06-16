---
name: doflow
description: Turn a described process, funnel, flow or simple diagram into a visual board and open it in offline-whiteboard for editing. Use when the user wants to "draw a funnel / process / flow / diagram", "map these steps", "make a flowchart", or sketch out logic on a whiteboard. Generates a board JSON and opens it preloaded. Works offline.
---

# doflow — generate a process/funnel and open it in offline-whiteboard

[offline-whiteboard](https://github.com/nocodework/offline-whiteboard) is a single-file, offline whiteboard (sticky notes, shapes, arrows). This skill builds a board from a described process or funnel and opens it preloaded, so the user can rearrange and edit it.

The board lives in the browser's local storage once opened. It does not write a file on disk; the user can Export from the app to save.

## 1. Build the board JSON

Produce an object with `elements` and `connections`:

```jsonc
{
  "app": "offline-whiteboard",
  "version": 1,
  "elements": [
    // type: "rect" | "ellipse" | "note" | "text"
    // x,y = top-left in world units; w,h = size; text = label; color = fill hex
    { "id": "t",  "type": "text", "x": 40,  "y": -20, "w": 320, "h": 40, "text": "Sales funnel", "color": "#FFFFFF", "fontSize": 30 },
    { "id": "s1", "type": "rect", "x": 110, "y": 60,  "w": 280, "h": 80, "text": "Visitors",  "color": "#BFDBFE" },
    { "id": "s2", "type": "rect", "x": 145, "y": 200, "w": 210, "h": 80, "text": "Leads",     "color": "#DDD6FE" },
    { "id": "s3", "type": "rect", "x": 180, "y": 340, "w": 140, "h": 80, "text": "Customers", "color": "#BBF7D0" }
  ],
  "connections": [
    { "from": "s1", "to": "s2" },
    { "from": "s2", "to": "s3" }
  ]
}
```

Rules:
- Give every element a unique `id`. `connections` reference element ids (`from` → `to`); the arrow snaps to the boxes automatically.
- Coordinates are free; the app frames the board for you on open. Keep boxes from overlapping.
- Layout by shape of the idea:
  - **Funnel** — rectangles stacked top→bottom (y increasing by ~130–150), each a bit narrower, each connected to the next.
  - **Process / steps** — boxes left→right (x increasing by ~280) or top→bottom, connected in order; branches = extra connections.
  - **Mind map** — a central node with satellites around it, connections from the centre out.
- Colours (fills): blue `#BFDBFE`, purple `#DDD6FE`, green `#BBF7D0`, yellow `#FEF08A`, pink `#FBCFE8`, orange `#FED7AA`, grey `#E5E7EB`, white `#FFFFFF`. Use a `text` element (with `fontSize`) for a title.
- Notes (`note`) are good for comments; `rect`/`ellipse` for steps; `ellipse` reads well as start/end.

## 2. Open it

Write the JSON to a temp file, base64-encode it (UTF-8), and open the whiteboard with the board in the URL hash:

```bash
# macOS
B64=$(base64 < /tmp/board.json | tr -d '\n')
open "https://nocodework.github.io/offline-whiteboard/#board64=$B64"
```

```bash
# Linux
B64=$(base64 -w0 < /tmp/board.json)
xdg-open "https://nocodework.github.io/offline-whiteboard/#board64=$B64"
```

```powershell
# Windows (PowerShell)
$B64 = [Convert]::ToBase64String([IO.File]::ReadAllBytes("board.json"))
Start-Process "https://nocodework.github.io/offline-whiteboard/#board64=$B64"
```

There is also `#board=<uri-encoded JSON>` if you prefer not to base64.

## Fully offline

Download the whiteboard once and open the local file instead of the hosted URL:

```bash
curl -O https://raw.githubusercontent.com/nocodework/offline-whiteboard/main/index.html
B64=$(base64 < /tmp/board.json | tr -d '\n')
open "file://$(pwd)/index.html#board64=$B64"
```

## Caveats

- Editing in the browser doesn't change any file on disk; the user exports from the app to save.
- Very large boards can exceed the OS command-line length for the URL; for big diagrams, open the whiteboard and use Import (the JSON file) instead.
