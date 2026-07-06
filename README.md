# IoT Logic Flow Builder — Design Prototype

A pixel-accurate interactive prototype exploring new UI and UX directions for the **IoT Logic** module in the [Telematica](https://www.navixy.com) platform (Navixy). IoT Logic is a visual flow builder that lets users wire up data-processing pipelines for GPS trackers and IoT devices — routing telemetry through conditions, transformations, webhooks, and output endpoints.

## What this is

This is a **design prototype**, not production code. It is a single self-contained HTML file (`index.html`) with all styles, scripts, and icons inlined — no build step, no dependencies, no external requests. It runs under a strict Content Security Policy and can be opened directly in a browser or served with any static file server.

The prototype demonstrates two design iterations side by side:

| | Prototype 1.0 | Prototype 2.0 |
|---|---|---|
| **Node panel** | Compact 234px panel, 30x30 icons with colored backgrounds, no descriptions | Wider 310px panel, 54x54 shaped icons (circle, diamond, hexagon) with short descriptions |
| **Canvas nodes** | Rectangular inline cards with icon + label | Shaped icon nodes matching the panel style |
| **Flow direction** | Horizontal (left-to-right) | Vertical (top-to-bottom) |
| **Flows** | 3 sample flows: Test, QA edited, Anti-theft | 1 sample flow: Vertical test flow |
| **Onboarding** | Ghost-node placeholders with descriptions | Ghost-node placeholders + "Build with AI" CTA |

Switch between prototypes using the dropdown in the bottom-right corner of the canvas.

## How to use

**Option A — open directly:**

```
open index.html
```

**Option B — serve locally:**

```
npx serve -p 8090
```

Then visit `http://localhost:8090`.

## Interactions

- **Pan** the canvas by clicking and dragging on empty space
- **Zoom** with the scroll wheel or the +/- controls
- **Center view** with the crosshair button
- **Switch flows** via the dropdown in the header (next to the flow name)
- **Switch prototypes** via the "Prototype 1.0 / 2.0" dropdown (bottom-right)
- **Drag nodes** from the left panel onto the canvas (drag handle on the right side of each card)
- **Expand/collapse** the left sidebar by clicking the hamburger menu

## Node types

| Node | Role | Required? |
|---|---|---|
| Data Source | Entry point — selects the IoT device or sensor input | Yes (start) |
| IF/THEN Logic | Conditional branch — splits flow into THEN / ELSE paths | No |
| Initial attributes | Formula node — creates or transforms data attributes | No |
| Device Action | Sends commands back to the device | No |
| Webhook | Fires an HTTP POST to an external URL | No |
| Output Endpoint | Terminal node — delivers processed data to Navixy | Yes (end) |

## Tech notes

- Single HTML file, zero dependencies, strict CSP compliant
- All icons are base64-encoded inline SVGs
- Canvas uses CSS `transform: translate() scale()` for pan/zoom
- Connections are drawn with SVG `<path>` elements (cubic bezier curves)
- Horizontal flows use S-curve beziers; vertical flows use vertical S-curve beziers
- Flow state is stored in-memory; "SAVE FLOW" button is visual-only

## Project context

This prototype was built as part of a UX/UI redesign initiative for the IoT Logic module in Telematica. The goal is to explore improved visual hierarchy, clearer node semantics through shaped icons, vertical flow layout as an alternative to the current horizontal layout, and a streamlined onboarding experience for new users.
