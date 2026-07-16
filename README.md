# IoT Logic Flow Builder — Design Prototype

A pixel-accurate interactive prototype exploring new UI and UX directions for the **IoT Logic** module in the [Telematica](https://www.navixy.com) platform (Navixy). IoT Logic is a visual flow builder that lets users wire up data-processing pipelines for GPS trackers and IoT devices — routing telemetry through conditions, transformations, webhooks, and output endpoints.

## What this is

A **design prototype**, not production code. Single self-contained `index.html` file — all styles, scripts, and icons inlined as base64 SVG. No build step, no npm install, no external requests (no CDN, no Google Fonts). Runs under strict CSP. Open the file directly, or serve any way you like.

## How to run

**Option A — open directly:**

```bash
open index.html
```

**Option B — serve locally (recommended, avoids `file://` quirks):**

```bash
python3 -m http.server 8091
# then open http://localhost:8091
```

Or with Node:

```bash
npx --yes serve -l 8091 .
```

## Prototype variants

Four prototypes ship in the same file. Switch between them via a **hidden dropdown** in the top-right corner (to the left of `SAVE FLOW`). The dropdown is invisible by default — reveal it with **Cmd+Shift+P** (or **Ctrl+Shift+P**). Toggle again to hide.

| Variant | What's different |
|---|---|
| **Prototype 1.0** | Base layout. Horizontal flow. No Flow route panel. |
| **Prototype 1.1** | Flow route panel anchored top-right, aligned with `SAVE FLOW`. Expands downward. |
| **Prototype 1.2** | Flow route panel bottom-right, next to zoom controls. |
| **Prototype 2.0** | Vertical flow. Shaped node icons (circle/diamond/hexagon). Wider Nodes panel with descriptions. |

## Sample flows

Switch via the flow dropdown in the header (next to the flow name):

- **Test flow** — small IF/THEN example
- **QA edited** — mid-size flow with several branches
- **Anti-theft protection** — opens a template modal (with a `Draft with AI Assistant` link that launches the Navixy AI Assistant panel)
- **Status** — includes warning and error node states
- **Long names** — stress-tests long labels
- **Super large** — dense flow with many action nodes
- **Vertical** (Prototype 2.0 only) — top-to-bottom layout

## Interactions

- **Pan** — click and drag on empty canvas
- **Zoom** — scroll wheel or +/− controls; **Center view** with the crosshair button
- **Drag nodes** onto the canvas from the left panel (grip handle on each card)
- **Reveal Prototype dropdown** — Cmd/Ctrl+Shift+P
- **Expand/collapse** left sidebar via the hamburger button
- **Node tooltips** appear on hover (500ms delay, positioned to the right of the panel card)
- **Node active state** — click a canvas node to highlight it with a soft halo
- **Warning / error pills** appear under nodes that have status attached (visible in the Status flow)

## Node types

| Node | Role | Required? |
|---|---|---|
| Data Source | Entry point — selects the IoT device or sensor input | Yes (start) |
| IF/THEN Logic | Conditional branch — splits flow into THEN / ELSE paths | No |
| Initial attributes | Formula node — creates or transforms data attributes | No |
| Device Action | Sends commands back to the device (terminal) | No |
| Webhook | Fires an HTTP POST to an external URL (terminal) | No |
| Output Endpoint | Terminal node — delivers processed data to Navixy | Yes (end) |

## Design specs (for engineers)

Detailed token/spec docs are in [`docs/`](docs/):

- [`docs/nodes-spec.md`](docs/nodes-spec.md) — node card dimensions, icon chip sizes, borders, colors, active/warning/error states, connector styles
- [`docs/node-tooltips-spec.md`](docs/node-tooltips-spec.md) — tooltip timing, positioning, per-node copy
- [`docs/shadows-spec.md`](docs/shadows-spec.md) — the `iot-shadow` token (parameters + where it's applied)

## Tech notes

- Single HTML file, zero dependencies, strict CSP compliant
- All icons are base64-encoded inline SVGs — nothing loads from disk or the network
- Fonts: system stack (`-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, ...`) — no font files, no CDN
- Canvas uses CSS `transform: translate() scale()` for pan/zoom
- Connections are drawn with SVG `<path>` elements (cubic bezier)
- Flow state is in-memory; `SAVE FLOW` is visual-only
- Expand/collapse state for the Flow route panel persists via `localStorage`

## Project context

Built as part of a UX/UI redesign initiative for the IoT Logic module in Telematica. The goal is to explore improved visual hierarchy, clearer node semantics, vertical flow layout as an alternative to the horizontal default, and a streamlined onboarding experience for new users.
