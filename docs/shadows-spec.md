# Shadows — short spec

One shared shadow token for all UI overlays sitting above the canvas. Nodes and connectors on the canvas do NOT use it.

## Token: `iot-shadow`

Source: Figma [nodes-panel 3560:50064](https://www.figma.com/design/2aOoOXwPIRtLIntpb4FX39/IoT-UI-Update?node-id=3560-50064) → effect `iot-shadow`.

Two drop-shadow layers:

| Layer | X | Y | Blur | Spread | Color | Opacity |
|---|---|---|---|---|---|---|
| 1 (ambient) | 0 | 0 | 4 | 0 | `#000000` | 5% |
| 2 (directional) | 0 | 4 | 8 | 1 | `#000000` | 5% |

CSS:

```css
--overlay-shadow: 0 0 4px 0 rgba(0,0,0,0.05), 0 4px 8px 1px rgba(0,0,0,0.05);
```

Defined once as a CSS variable in `:root` in [index.html](../index.html), used via `box-shadow: var(--overlay-shadow)`.

## Where it's applied

Only interface elements floating above the canvas:

| Element | Selector |
|---|---|
| Top header | `.header` |
| Nodes panel | `.np-body`, `.np-toggle` |
| Flow route panel | `.fp` |
| Zoom controls | `.ctrl-zoom`, `.ctrl-btn` |

## Where it's NOT applied

- Canvas nodes (`.cn-body`) and their active-state halo — the active halo uses its own `box-shadow: 0 0 0 3px rgba(0,0,0,0.13)`
- Connectors, `+` buttons, then/else circles
- Drag ghost during a drag
- Warning / error pills
- Dropdown menus, modals, tooltips — they carry their own shadows
