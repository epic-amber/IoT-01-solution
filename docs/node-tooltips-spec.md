# Node Tooltips — short spec

## When they appear
On hover over a node card in the **Nodes** panel (left side).

## Delay
- **Show:** **500 ms** after the cursor enters the card.
- **Hide:** immediately when the cursor leaves.
- If the user starts dragging the node before 500 ms elapse, the tooltip does not appear.

## Position
To the right of the node card:
- tooltip left edge = card right edge + **8 px**
- tooltip top edge = card top edge

Max width **320 px**, text wraps automatically.

## Texts (one per node type)

**Data Source**
Selects which devices feed data.
e.g. GPS trackers, sensors, dashcams.
Required · every flow starts here.

**IF/THEN Logic**
Splits the flow based on a condition.
e.g. speed > 100 → alert, ELSE continue.
Undefined values go to ELSE.

**Initial attributes**
Creates new values from raw data.
e.g. convert °C → °F, compute avg speed.
Optional · place between nodes.

**Device Action**
Sends a command back to the device.
e.g. lock, unlock, engine block.
Terminal · nothing connects after.

**Webhook**
Sends HTTP POST to external service.
e.g. Slack alert, CRM, Zapier trigger.
Terminal · nothing connects after.

**Output Endpoint**
Sends data to Navixy or external system.
e.g. Default endpoint, MQTT stream.
Required · data won't reach Navixy without it.
