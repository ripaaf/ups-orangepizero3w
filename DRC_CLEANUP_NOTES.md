# Phase 6B.1c — pre-routing DRC cleanup

## Fixes applied

1. **Fine-pitch copper clearances**
   - Added a project custom-rule file (`OrangePi_Zero3W_UPS_RevA.kicad_dru`).
   - U1, U2, and U3 use a local 0.15 mm copper-clearance exception only around those footprints.
   - The rest of the PCB keeps its normal netclass clearances.

2. **Imported solder-mask expansions**
   - Removed local `solder_mask_margin 0.102` overrides from the embedded PCB footprints.
   - Normalized the included imported `.kicad_mod` source copies as well.
   - This targets the 27 `solder_mask_bridge` violations in the uploaded DRC report.

3. **TPS61088 thermal vias**
   - Added a local 0.20 mm drill exception only for U5 thermal vias.
   - The board-wide minimum through-hole size remains 0.30 mm elsewhere.

4. **USB-C edge clearance**
   - Added a local 0.25 mm board-edge exception only for J3.
   - The board-wide 0.30 mm copper-to-edge constraint remains unchanged elsewhere.

5. **Orange Pi antenna keepout**
   - Removed only the `footprints not_allowed` flag so the unavoidable top-right mounting-hole footprint no longer triggers DRC.
   - Tracks, vias, pads, and copper pours remain forbidden in the antenna keepout.

6. **Netclass matching**
   - Corrected hierarchical net patterns to include their leading `/`, e.g. `/BAT_POS`, `/USB_VBUS_SAFE`, `/BOOST_SW`, and `/I2C_SDA`.

## Recheck locally

Open the project in KiCad 9, press **B**, then run DRC again.
The previous report is retained as `DRC-terbaru_BEFORE_DRC_cleanup.rpt`.

Expected remaining entries at this stage:
- **Unconnected Items**: expected until routing and planes are added.
- The 64 non-routing violations from the uploaded report should be resolved by these changes, but this must be confirmed in KiCad because `kicad-cli` is unavailable in this environment.
