# Phase 6B.1b – PCB cleanup notes

Changes are intentionally limited to PCB presentation and DRC noise cleanup. No nets, pads, tracks, vias, zones, footprint positions, or schematic connectivity were changed.

- Kept readable top-silkscreen references for J1–J3, U1–U6, L1–L2, and SW1 at 0.8 mm / 0.15 mm.
- Hid dense passive references from production silkscreen; they remain available in KiCad and fabrication/assembly data.
- Removed imported U2/U6 QFN corner-silkscreen segments that crossed exposed pads; pin-1 markers remain.
- Consolidated front section labels into one bottom-silkscreen functional legend.
- Normalized the decorative bottom legend for PCBWay-readable text dimensions.
- Set only `lib_footprint_mismatch` to Ignore because local footprint presentation overrides are intentional. Electrical, clearance, solder-mask, courtyard, routing, and connectivity checks remain enabled.
- Preserved the previous PCB as `OrangePi_Zero3W_UPS_RevA_before_silkscreen_cleanup.kicad_pcb`.

Run KiCad DRC again locally after opening and saving the project. Any remaining violations should be reviewed rather than bulk-ignored.
