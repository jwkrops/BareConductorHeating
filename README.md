# Bare conductor heating

Web calculator for induced-current heating of bare conductor meander loops with connectors under test (conductor typically 125 °C): heating and start current from a desired heat-up time, compensation transformers with capacitor-can wiring diagrams, and heating transformers.

**Live:** https://jwkrops.github.io/BareConductorHeating/

Everything runs in the browser; nothing is sent anywhere. After the first visit it also works offline. On Android, "Add to Home screen" in Chrome installs it with its own icon.

> Engineering aid. Verify the setup and the measured temperatures before relying on the results. Provided "as is" under the MIT License, without warranty.

## Files

| File | What it is |
|---|---|
| `index.html` | The calculator |
| `sw.js` | Offline cache (service worker) |
| `manifest.webmanifest`, `icon.svg`, `icon-192.png`, `icon-512.png` | App icon for "Add to Home screen" |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |
| `QR_labels_L6011_1-140.pdf` | QR labels for the 1:140 transformers (Avery L6011, 63.5 × 29.6 mm, 27 per A4 sheet) |
| `L6011_alignment_test.pdf` | Print on plain paper first to check alignment against a label sheet |
| `LICENSE` | MIT License |

## QR labels and preset links

Scanning a label opens the calculator with both transformer ratios set to 1:140 (`?t=140`). `?t=80` and `?t=40` work too, and other settings can be preset the same way, for example `?nc=140&nh=80&uh=230`. Print the labels at 100 % ("fit to page" off).

## Method

- **Heating current:** heat balance for a bare conductor in still indoor air: natural convection and radiation as in CIGRE TB 601 (no sun, no wind), emissivity 0.3 for new conductor. AC resistance with skin effect per IEC 60287-1-1. Heat-loss correction 0.93, calibrated on one heat run (95 mm² aluminium, 355 A at 125 °C). Diameter estimated as √(4A/π) × 1.13 unless entered.
- **Start current:** from the desired heat-up time (conductor heat capacity, resistance and losses stepped through time from room temperature), or as a fixed overcurrent percentage. The heat-up time is for the conductor; connectors follow a few minutes later.
- **Loop reactance:** the meander (legs, end links and return conductor) split into straight segments; self and mutual partial inductances of all segments added (Grover / Neumann). Checked against Grover's rectangle formula.
- **Connections:** 20 µΩ per joint, 3 joints per leg (test connector and both leg ends).
- **Capacitors:** BSMJ0.4-50-1 cans, 400 V, 2 × 497.5 µF. One or two cans per transformer give 11 values from 124 to 1990 µF; the app draws the wiring for each.
- **Transformer limits:** 1:80 and 1:140 max 230 V, 1:40 max 400 V.
- **Aims:** *Full compensation*, *Heating input voltage* (deliberate under- or over-compensation for finer autotransformer regulation) or *Fewest transformers* (compensation + heating together). Candidates that exceed a voltage limit at the start current are rejected.

## Calibration

The heat-loss correction (under *Advanced*) is the measured current² divided by the current² the app gives with the correction at 1.0, both at the same steady temperature. Heat runs on further cross-sections will show whether 0.93 holds across the range.

## Updating

1. Replace the changed file(s) in the repository.
2. Raise `VERSION` in `sw.js` (for example `v1.0` → `v1.1`), otherwise phones that used the site offline keep the old files for longer.
3. Update the version number in the footer of `index.html`.

## Version history

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2026-11-05 | First published version |

See also: [Loop heating setup](https://jwkrops.github.io/LoopHeatingCalculator/) for heat cycle loops of MV/HV cable.
