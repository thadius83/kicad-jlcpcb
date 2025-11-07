# JLCPCB 4-Layer PCB Template (3313 Stackup)

Production-ready KiCad 9.0 template for 4-layer PCBs manufactured by JLCPCB using the 3313 prepreg stackup.

## Features

- Pre-configured layer stack matching JLCPCB JLC04161H-3313 specification
- Comprehensive design rules (.kicad_dru) for JLCPCB manufacturing capabilities
- Custom netclasses for impedance-controlled routing
- Ready-to-use track widths and via sizes
- I2C and SPI bus aliases for multi-wire routing

## Stack-up Specification

| Layer | Material | Thickness | Notes |
|-------|----------|-----------|-------|
| F.Cu | Copper | 0.035 mm (1 oz) | Top signal layer |
| Dielectric 1 | Prepreg 3313 | 0.0994 mm | εr = 4.1 |
| In1.Cu | Copper | 0.0152 mm | Inner layer (recommend GND) |
| Dielectric 2 | Core FR-4 | 1.265 mm | εr = 4.1 |
| In2.Cu | Copper | 0.0152 mm | Inner layer (power/GND) |
| Dielectric 3 | Prepreg 3313 | 0.0994 mm | εr = 4.1 |
| B.Cu | Copper | 0.035 mm (1 oz) | Bottom signal layer |

**Total board thickness:** 1.58 mm

## Custom Netclasses

Pre-configured netclasses with appropriate track widths, clearances, and via sizes:

| Netclass | Track Width | Clearance | Via (Ø/drill) | Purpose |
|----------|-------------|-----------|---------------|---------|
| `SIGNAL` | 0.2 mm | 0.2 mm | 0.6/0.3 mm | Standard signal traces |
| `HS_50R_MICROSTRIP` | 0.1565 mm | 0.2 mm | 0.5/0.25 mm | 50Ω single-ended (RF, high-speed) |
| `HS_90R_DIFF_EC` | 0.1582 mm | 0.2 mm | 0.5/0.25 mm | 90Ω differential (USB 2.0 HS, etc.) |
| `SIGNAL_FINE` | 0.12 mm | 0.12 mm | 0.5/0.25 mm | Fine-pitch signals |
| `SENSE_KELVIN` | 0.2 mm | 0.25 mm | 0.5/0.25 mm | Kelvin sense traces |
| `RELAY_SSR_CTRL` | 0.25 mm | 0.25 mm | 0.7/0.35 mm | Relay/SSR control |
| `PWR_1A` | 0.6 mm | 0.3 mm | 0.8/0.4 mm | Power (up to 1A) |
| `PWR_2A` | 1.0 mm | 0.35 mm | 1.0/0.5 mm | Power (up to 2A) |
| `VBAT_HIGH` | 1.5 mm | 0.4 mm | 1.0/0.5 mm | High-current battery traces |

### Differential Pairs

- **HS_90R_DIFF_EC:** 0.1582 mm trace width, 0.2032 mm edge-to-edge gap (≈90Ω differential)
- Optimized for USB 2.0 High-Speed and similar protocols

## Design Rules Summary

| Parameter | Value | Notes |
|-----------|-------|-------|
| Min track width/spacing | 0.09 mm | JLCPCB 4-6 layer, 1 oz capability |
| Standard via | 0.6/0.3 mm | Diameter/drill (no extra fee) |
| Min annular ring | 0.075 mm | Via and PTH |
| Min hole-to-hole | 0.5 mm | Different nets |
| Edge clearance | 0.3 mm | Traces to board edge |
| Silkscreen clearance | 0.15 mm | Pads to silkscreen |

## Usage

1. Copy this template to your KiCad templates directory
2. Create a new project from template in KiCad
3. Assign your nets to the appropriate netclasses for automatic DRC compliance
4. Route your design following the impedance-controlled guidelines
5. Run DRC to verify JLCPCB manufacturing compliance

## Best Practices

- Keep In1.Cu as a continuous ground plane under high-speed traces
- Use 45° miters or rounded corners for impedance-controlled traces
- Minimize via stubs on high-speed differential pairs
- Avoid splits or antipads under controlled-impedance routes
- Use Kelvin connections for precise voltage/current sensing

## Requirements

- KiCad 9.0 or later
- JLCPCB 4-layer PCB fabrication service

## Important Manufacturing Notes

### Via Types
- Only through-hole vias are supported (no blind/buried or microvias)

### Hole Constraints
- **PTH (Plated Through-Hole):** 0.2-6.3 mm diameter
- **NPTH (Non-Plated Through-Hole):** Min 0.5 mm diameter
- **Castellated Holes:** Min 0.6 mm diameter
- **Plated Slots:** Min 0.5 mm width (drawn with pad)
- **Non-Plated Slots:** Min 1.0 mm width (draw outline in Edge.Cuts layer)

### NPTH with Copper Pads
If using NPTH with surrounding copper pads, the inner diameter of the pad should be 0.4-0.5 mm larger than the NPTH drill diameter. JLCPCB will remove copper 0.2-0.25 mm around the hole to prevent it from becoming plated.

### Small Via Warning
Avoid vias with holes < 0.3 mm and diameter ≤ 0.4 mm, as these trigger an expensive 4-Wire Kelvin Test. If necessary, ensure annular ring ≥ 0.125 mm.

### Board Constraints
- Minimum board size: 10 × 10 mm
- Hole to board edge: ≥ 1 mm

## License

This template is provided as-is for use with JLCPCB manufacturing services. Modify as needed for your specific design requirements.

## Credits & References

### Custom Design Rules
The `.kicad_dru` file is based on JLCPCB manufacturing capabilities and was inspired by:
- Original repository: [Cimos/KiCad-CustomDesignRules](https://github.com/Cimos/KiCad-CustomDesignRules)
- [darkxst's JLCPCB DRC rules](https://gist.github.com/darkxst/f713268e5469645425eed40115fb8b49)
- [denniskupec's JLCPCB DRC rules](https://gist.github.com/denniskupec/e163d13b0a64c2044bd259f64659485e)

### Documentation
- [JLCPCB PCB Capabilities](https://jlcpcb.com/capabilities/pcb-capabilities)
- [KiCad Custom Design Rules Documentation](https://docs.kicad.org/master/en/pcbnew/pcbnew_advanced.html#custom_design_rules)
