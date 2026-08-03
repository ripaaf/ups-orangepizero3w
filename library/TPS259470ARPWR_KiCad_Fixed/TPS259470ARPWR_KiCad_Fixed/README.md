# TPS259470ARPWR corrected KiCad library

This package fixes two independent issues found in common third-party downloads:

1. **Invalid footprint identifier** — KiCad requires `library_nickname:footprint_name`, not only a footprint name.
2. **Incorrect 14-pin logical model** — TI specifies RPW0010A as a **10-pin** package. The four small copper pieces used to complete the L-shaped corner lands are not pins 11–14. In this fixed footprint they reuse the correct electrical pad numbers: **1, 4, 7 and 10**.

## Install inside the project

Copy the included `libraries` folder into the root of the KiCad project so the result is:

```
<project>/libraries/TPS25947_fixed.kicad_sym
<project>/libraries/TPS25947_fixed.pretty/TPS259470ARPWR_RPW0010A.kicad_mod
<project>/libraries/TPS25947_fixed.3dshapes/TPS259470ARPWR.stp
```

In **Preferences → Manage Symbol Libraries → Project Specific Libraries**, add:

- Nickname: `TPS25947_fixed`
- Path: `${KIPRJMOD}/libraries/TPS25947_fixed.kicad_sym`

In **Preferences → Manage Footprint Libraries → Project Specific Libraries**, add:

- Nickname: `TPS25947_fixed`
- Path: `${KIPRJMOD}/libraries/TPS25947_fixed.pretty`

The symbol already points to this valid identifier:

```
TPS25947_fixed:TPS259470ARPWR_RPW0010A
```

## Recommended replacement workflow

Delete the current 14-pin symbol instance and place `TPS25947_fixed:TPS259470ARPWR` instead. Do not mix the old 14-pin symbol with this corrected 10-pin footprint.

Pin mapping:

| Pin | Function |
|---:|---|
| 1 | EN/UVLO |
| 2 | OVLO |
| 3 | AUXOFF |
| 4 | FLT (active low, open drain) |
| 5 | IN |
| 6 | OUT |
| 7 | DVDT |
| 8 | GND |
| 9 | ILM |
| 10 | ITIMER |

After placement, open **Symbol Properties** and confirm the Footprint field is exactly:

```
TPS25947_fixed:TPS259470ARPWR_RPW0010A
```

Then preview the footprint and verify that KiCad reports only logical pad numbers 1 through 10. There are 14 physical pad primitives because pins 1, 4, 7 and 10 each use two touching copper shapes.
