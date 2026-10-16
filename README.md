# Arch Diagram

A single-file, serverless web app for drawing architecture diagrams.
Open `index.html` in Google Chrome (or Edge). Nothing to install, no build step and no server.

## Features

- **Blocks**: size, fill, border style/color/width, corner radius, a rich-text title (bold, italic, colors, sizes, line breaks), an icon (built-in set or any emoji/text), and a badge plus an optional highlight ring.
- **Links**: **Shift + drag** from a block to another block, or onto empty canvas to leave a free end.
- **Connectors**: placed on a block side automatically and spread evenly when several share a side. Drag a link end to another side, another block, or free space. Drop near a block's center to make the side automatic again. A connector can be simple, a circle or a square, in any color.
- **Link ends**: none, full arrows (normal/narrow/wide), lined arrows (normal/narrow/wide), triangle, circle, square and diamond, in hollow or filled versions.
- **Routing**: curve, straight line or orthogonal polyline.
  - Polylines are routed with A* around blocks and keep a set clearance.
  - Polylines avoid overlapping each other. Parallel segments are spread apart by a set spacing.
  - Polyline corners are rounded with a set radius.
- **Settings**: canvas, grid and snap, routing parameters, and default styles for new blocks and links. You can save them as your personal defaults.
- **Files**: the diagram is stored as JSON. In Chrome the File System Access API reads and writes the local file in place; other browsers fall back to upload/download. Work is also auto-saved in browser storage, and you can drop a `.json` file onto the window to open it.
- **Other**: undo/redo, copy/paste/duplicate, box selection, zoom/pan, export to SVG.

## JSON format

```json
{
  "app": { "name": "arch-diagram", "version": "1.0.0", "github": "https://github.com/avchaykin/arch-diagram" },
  "format": 1,
  "savedAt": "…",
  "settings": { "canvas": {}, "routing": {}, "block": {}, "link": {} },
  "view": { "x": 0, "y": 0, "k": 1 },
  "blocks": [ { "id": "b1", "x": 0, "y": 0, "w": 160, "h": 72, "title": "<b>API</b>", "icon": "server", "badge": "NEW" } ],
  "links":  [ { "id": "l1", "from": { "block": "b1", "side": "auto" }, "to": { "x": 300, "y": 40 }, "route": "poly", "endEnd": "arrow" } ]
}
```

A link end is either attached, `{ "block": id, "side": "auto" | "top" | "right" | "bottom" | "left", "t": 0..1 }`, or free, `{ "x", "y" }`.

## Shortcuts

| Action | Keys |
|---|---|
| New block | double-click canvas |
| Edit title | double-click block / Enter |
| New link | Shift + drag from block |
| Undo / redo | Ctrl/⌘+Z, Ctrl/⌘+Shift+Z |
| Copy / paste / duplicate | Ctrl/⌘+C / V / D |
| Save / save as / open | Ctrl/⌘+S, Ctrl/⌘+Shift+S, Ctrl/⌘+O |
| Pan / zoom | wheel or Space + drag / Ctrl/⌘ + wheel |
| Fit | F |
