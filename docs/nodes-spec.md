# Nodes — design spec

All visual values are pulled from Figma. Everything below is what's currently implemented in [index.html](../index.html) and matches the Figma source of truth.

## Sources of truth

- [Node types + canvas node](https://www.figma.com/design/2aOoOXwPIRtLIntpb4FX39/IoT-UI-Update?node-id=3537-18192)
- [Nodes panel layout](https://www.figma.com/design/2aOoOXwPIRtLIntpb4FX39/IoT-UI-Update?node-id=3557-22012)
- [Active state](https://www.figma.com/design/2aOoOXwPIRtLIntpb4FX39/IoT-UI-Update?node-id=3546-19899)

## Design tokens

| Token | Value | Where |
|---|---|---|
| `blue-accent-4` | `#2962FF` | Data Source accent |
| `deep-purple-accent-2` | `#7C4DFF` | IF/THEN Logic, Initial attributes accent |
| `purple-accent-3` | `#D500F9` | Device Action, Webhook accent |
| `cyan` | `#00BCD4` | Output Endpoint accent |
| `grey` | `#9E9E9E` | Neutral connectors, `+` buttons |
| `green-accent-4` | `#00C853` | Then (accept) branch on IF/THEN Logic |
| `red-darken-3` | `#E53935` | Else (reject) branch on IF/THEN Logic |
| `opacity/13` | `rgba(0, 0, 0, 0.13)` | Active-node halo outline |
| `surface/bright` | `#FFFFFF` | Card fill |
| Icon-chip fill | accent @ 10% opacity | e.g. Data Source chip `rgba(41, 98, 255, 0.1)` |
| `text-label-medium` | Roboto Medium 12 / 16, letter-spacing 0.25 | Node label |
| `ga-1` / `ga-2` / `ga-4` | 4 / 8 / 16 px | Spacing scale |
| `radius/4` | `4px` | Card corners AND icon chip corners |

## Node types

| Type | Accent color | Icon-chip fill | Left connector | Right connector | Role |
|---|---|---|---|---|---|
| Data Source | `#2962FF` | `rgba(41, 98, 255, 0.1)` | — | `+` | Required · flow starts here |
| IF/THEN Logic | `#7C4DFF` | `rgba(124, 77, 255, 0.1)` | arrow | then / else | Optional |
| Initial attributes | `#7C4DFF` | `rgba(124, 77, 255, 0.1)` | arrow | `+` | Optional |
| Device Action | `#D500F9` | `rgba(213, 0, 249, 0.1)` | arrow | — | Optional, terminal |
| Webhook | `#D500F9` | `rgba(213, 0, 249, 0.1)` | arrow | — | Optional, terminal |
| Output Endpoint | `#00BCD4` | `rgba(0, 188, 212, 0.1)` | arrow | — | Required · endpoint |

Border color = accent color. Icon color = accent color.

## Canvas node card

| Property | Value |
|---|---|
| Width | `180px` (fixed) |
| Min height | `52px` |
| Background | `#FFFFFF` |
| Border | `1.5px solid <accent>` |
| Border radius | `4px` |
| Padding | `8px 16px` (vertical / horizontal) |
| Gap (icon ↔ label) | `8px` |
| Transform | `scale(1.2)` (canvas zoom baseline) |

CSS class: `.canvas-node > .cn-body` in [index.html](../index.html).

## Panel node card

| Property | Value |
|---|---|
| Width | fills panel column (~192px) |
| Height | `46px` |
| Background | `#FFFFFF` |
| Border | `1px solid #DEDEDE` (neutral, does NOT use accent color) |
| Border radius | `4px` |
| Padding | `8px` |
| Gap (icon ↔ label) | `8px` |

CSS class: `.node-card` in [index.html](../index.html). Panel keeps neutral gray border by design — only the icon chip carries the accent color.

## Icon chip

Same on canvas and in panel except for size:

| Property | Canvas | Panel |
|---|---|---|
| Size | `36 × 36` | `30 × 30` |
| Border radius | `4px` | `4px` |
| Background | accent @ 10% opacity | accent @ 10% opacity |
| Icon inside | 20 × 20, accent color | 20 × 20, accent color |

## Label

| Property | Value |
|---|---|
| Font | Roboto |
| Weight | 500 (Medium) |
| Size / line-height | `12px / 16px` |
| Letter-spacing | `0.25` |
| Color | `#000000` |
| Wrap | max 2 lines (canvas), single line ellipsis (panel) |

## Connectors between nodes

| Style | Color | Notes |
|---|---|---|
| Default flow line | `#9E9E9E`, `2px` stroke | Bezier |
| Then edge | `#00C853`, `2px` stroke | With `then` label above line |
| Else edge | `#E53935`, `2px` stroke | With `else` label above line |
| `+` add-connector button | `#9E9E9E` circle stroke + fill | Right side of source-type nodes |
| Arrow-in connector | `#9E9E9E` circle stroke + fill | Left side of downstream nodes |

Then / else status circles on IF/THEN Logic:
- Accept (then): green `#00C853` ring with checkmark
- Reject (else): red `#E53935` ring with cross

## Active state (selected node)

Trigger: user clicks a canvas node. One node active at a time.

| Property | Value |
|---|---|
| Base border | unchanged — stays `1.5px solid <accent>` |
| Halo outline | `box-shadow: 0 0 0 3px rgba(0, 0, 0, 0.13)` |
| Layout impact | none (box-shadow doesn't reserve space) |

Above the active card: **Delete** and **Edit** action buttons (`.cn-actions`, shown via `.canvas-node.active .cn-actions { display: flex }`).

CSS: `.canvas-node.active .cn-body` in [index.html](../index.html).

## Drag ghost

While the user drags a node from the panel onto the canvas:

| Property | Value |
|---|---|
| Icon chip size | `30 × 30` |
| Border radius | `4px` |
| Background | `#F3F3F3` |
| Label | Roboto Medium 12, color `#9E9E9E` |

CSS: `.gn-icon`, `.drag-ghost .dg-icon` in [index.html](../index.html).

## Warning / error state (Figma `3546:19843`, `3537:18227`)

When a node is in warning or error, `addNodeStatus()` wraps the body in `.cn-body-wrap`, changes the card border, and appends a pill below the card.

### Card border

| Variant | Border |
|---|---|
| Warning | `1.5px solid #FF5722` |
| Error | `1.5px solid #FF0000` |

### Pill

Rendered below the card via `.cn-body-wrap`.

| Variant | Text/icon color | Background | Border |
|---|---|---|---|
| Warning | `#FF5722` | `#FFF3E0` | `1px solid #FF5722` |
| Error | `#FF0000` | `#FFEBEE` | `1px solid #FF0000` |

Both:
- Radius `4px`, height `29px`, padding `5px 10px`, gap `8px`
- Font: Roboto Medium `12/16`, letter-spacing `0.03px`
- Icon: Material Symbols `error` (filled) at `19 × 19`, tinted via `currentColor` (same glyph for warning and error, differs only in state color)
- Texts: `See warning details` / `See error details`

## Tooltips (node cards in panel)

See [node-tooltips-spec.md](./node-tooltips-spec.md).

## Where to find things in [index.html](../index.html)

| What | Approx. line |
|---|---|
| Panel `.node-card` / `.node-icon` / `.node-label` | 208–221 |
| Node tooltip CSS | 223–232 |
| `.canvas-node.active .cn-body` (halo) | 625 |
| `.cn-actions` / `.cn-act-btn` (Delete/Edit) | 626–640 |
| `.cn-warning` / `.cn-error` | 650–665 |
| `.cn-body` / `.cn-icon` / `.cn-label` | 666–682 |
| `.gn-icon` / `.drag-ghost .dg-icon` | 254, 710 |
| `NODE_TYPES` (accent colors + connector config) | 1422–1429 |
| Connector SVG generators (`plusSvg`, `arrowSvg`, `thenSvg`, `elseSvg`) | ~1454–1466 |
| `TOOLTIP_DATA` | 1646–1653 |

## Not covered here

- **Prototype 2.0** (`.v2-panel`, `.v2-canvas`) — separate visual system, own tokens.
- **Flow route panel** — see the Flow route spec if needed; not a node.
- **Onboarding placeholders** — visual only, inherit nothing from the node system.
