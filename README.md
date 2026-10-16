# Arch Diagram

A single-file, serverless web app for drawing architecture diagrams.
Open `index.html` in Google Chrome (or Edge). Nothing to install, no build step and no server.

## Features

- **Blocks**: size, fill, border style/color/width, corner radius, a rich-text title (bold, italic, colors, sizes, line breaks), an icon (built-in set or any emoji/text), and a badge plus an optional highlight ring.
- **Links**: **Shift + drag** from a block to another block, or onto empty canvas to leave a free end.
- **Connectors**: placed on a block side automatically and spread evenly when several share a side. The exception is a link whose blocks face each other, or whose free end lies in front of a side. It attaches straight across, with no bends, as long as that crosses no block and adds no crossings with other links. You can switch this per link with "Straight when possible" in the link's sidebar, set the default for new links in Settings, or turn it off for all links in Settings under Link routing. Drag a link end to another side, another block, or free space. Drop near a block's center to make the side automatic again. A connector can be simple, a circle or a square, in any color.
  When you select a block, the sidebar lists all its connectors. Each one shows the block at the other end, lets you change its side, and can be given a name. A "show" toggle turns the name on or off next to the connector.
- **Link ends**: none, full arrows (normal/narrow/wide), lined arrows (normal/narrow/wide), triangle, circle, square and diamond, in hollow or filled versions.
- **Routing**: curve, straight line or orthogonal polyline.
  - Polylines are routed with A* around blocks and keep a set clearance.
  - Polylines avoid overlapping each other. Parallel segments are spread apart by a set spacing.
  - Polyline corners are rounded with a set radius.
  - You can drag any polyline segment to move it. Near the line of the neighbouring segments it snaps into line with them, which removes the step. The route then becomes manual: its bends stay where you put them and follow the ports when blocks move. Double-clicking a segment, or "Reset route" in the sidebar, brings back automatic routing.
- **Flows**: named sequences of numbered steps over blocks and links, such as a request path or a user scenario. They are managed in the **Flows** tab of the sidebar.
  - You can start with an empty flow, record one by clicking elements on the canvas in order, or build one from the current selection.
  - Steps can be added, deleted and dragged to a new order. The same element can appear in a flow several times.
  - A flow has a name, a description and a color, and each step has its own description.
  - Hovering a flow in the list previews its step numbers on the canvas. When a flow is open, its numbers stay visible. Click a number to jump to that step.
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
  "links":  [ { "id": "l1", "from": { "block": "b1", "side": "auto" }, "to": { "x": 300, "y": 40 }, "route": "poly", "endEnd": "arrow" } ],
  "flows":  [ { "id": "f1", "name": "Place an order", "description": "…", "color": "#7c3aed", "steps": [ { "ref": "b1", "description": "…" }, { "ref": "l1", "description": "…" } ] } ]
}
```

A link end is either attached, `{ "block": id, "side": "auto" | "top" | "right" | "bottom" | "left", "t": 0..1 }`, or free, `{ "x", "y" }`.
Any end can also carry a connector name: `"name": "REST /orders", "showName": true`.
A flow step's `ref` is the id of a block or a link.
A manually shaped polyline stores its bend points as `"waypoints": [ { "x", "y" }, … ]`.

## Shortcuts

| Action | Keys |
|---|---|
| New block | double-click canvas |
| Edit title | double-click block / Enter |
| New link | Shift + drag from block |
| Move a polyline segment | drag the segment |
| Reset an adjusted polyline | double-click a segment |
| Stop recording flow steps | Enter / Esc |
| Undo / redo | Ctrl/⌘+Z, Ctrl/⌘+Shift+Z |
| Copy / paste / duplicate | Ctrl/⌘+C / V / D |
| Save / save as / open | Ctrl/⌘+S, Ctrl/⌘+Shift+S, Ctrl/⌘+O |
| Zoom | mouse wheel |
| Pan | drag empty canvas (or Space + drag) |
| Box select | Shift or Ctrl/⌘ + drag on empty canvas |
| Fit | F |
