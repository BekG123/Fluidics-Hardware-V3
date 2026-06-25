# Fluidics Controller — V3 Change Notes

Author: Bekhruz Malikov (<bekhruz.malikov@cephla.com>)
Base: Kevin Marx's `Fluidics-Hardware-V2`
Tooling: KiCad 10 (project migrated from the V2 / KiCad 7 format)

## Summary

V3 strips the V2 fluidics controller down to a minimal build and extends the
selector-valve bank by one channel. Net result: **177 → 86 footprints**, with
**DRC reporting 0 unconnected items**.

## Target configuration

| Subsystem | V2 | V3 | Change |
|---|---|---|---|
| Solenoid valves (on/off, 1× MCZ33996) | 16 | 0 | removed |
| Selector valves (IDEX, isolated I²C) | 5 | 6 | +1 channel |
| Pressure sensors (Honeywell HSC, **SPI**) | 4 | 0 | removed |
| Flow sensors (**I²C**) | 4 | 3 | −1 |
| Bubble sensors | 2 | 2 | unchanged |
| Pumps | disc + syringe | syringe only | disc removed |

## Removed

- **Disc-pump driver** — `U1` (TTP Ventus driver module connector) + `M1`
  (pump mount). The disc pump was UART-controlled; the syringe pump (RS-232)
  is retained.
- **Solenoid-valve subsystem** (whole sheet) — `IC1` (MCZ33996 16-ch low-side
  driver), `D5–D20` (16 flyback indicators), `R6–R21` (16 gate resistors),
  `C3/C4/JP6/R55`, and connector `J5`.
- **All SPI pressure sensors** — `IC3–IC6` (HSCDRRN001BDSA3) and their
  decoupling caps / pull-ups (`C31/C32/C33/C34`, `C36/C37/C38/C39`,
  `R56–R59`).
- **One I²C flow-sensor channel** — connector `J17`.
- **Wenzel-lab pressure-controller daughter board** interface — `J6`
  (SPI/GPIO breakout), `J8` (3.3/5/12/24 V power), `J7` (ICSP) + `JP3`. This
  external module (I²C ADC at 0x48) was paired with the now-removed disc pump.
- **Manual-control block** (whole sheet) — switches `S1–S4`, push-button
  `SW1`, potentiometer `VR1`, GPIO expander `U7` (TCA9539), pull-ups
  `R24–R38`, `C10/C11/JP1/JP2`.
- **24 V → 12 V converter** — `U5` (Pololu D36V28Fx) + 12 V indicator
  `D1/R2` + power-good pull-up `R52`. No 12 V load remained once the
  solenoids and daughter board were removed.

## Added

- **6th IDEX selector-valve channel** — connector pair `J24` (0705430001,
  power: GND / +24 V) and `J25` (87832-1010, signal: SDA 5 V / SCL 5 V / GND),
  tied to the shared **isolated-I²C** bus (ADUM1250 + LTC4311 front-end).
  Placed in the board area freed by the solenoid block; +24 V connects via the
  In2.Cu power plane, GND via the board ground pours. The valve's I²C address
  is set on the IDEX module itself (no on-board addressing hardware).

## Fixed

- **Library path portability** — `fp-lib-table` and `sym-lib-table` referenced
  the original author's hardcoded absolute paths
  (`/home/octopi-codex/Documents/kmarx/...`), which fail on any other machine
  (this blocked adding new footprints). All 140 entries were rewritten to
  `${KIPRJMOD}/../`-relative URIs so the libraries resolve anywhere.
- **`.gitignore`** added for KiCad lock/autosave/cache and editor-history
  files (the V2 repo had several `*.lck` files committed).

## Notes / retained

- The board is 4-layer: F.Cu / In1.Cu (GND) / In2.Cu (+24 V & +5 V planes) /
  B.Cu, with GND poured on the outer layers.
- Mounting holes `H1–H4` (corner, plated, chassis-GND) are unchanged.
- The SPI bus is retained (Teensy + connector `J9`) even though no SPI sensor
  remains; the freed Teensy SPI pins are simply unused.
- `pctrl.kicad_sch` is an orphaned sheet (not instantiated in the design) and
  can be deleted in a follow-up.

## Known TODO

- **Board not yet physically resized.** The outline (Edge.Cuts) is still the
  V2 ~127 mm square — removing parts only freed space, it did not shrink the
  board. A resize requires compacting the remaining parts, redrawing the
  outline, repositioning the mounting holes, and re-pouring the zones, and
  depends on whether the enclosure / mounting-hole pattern is fixed.

## Verification method

Changes were applied in the KiCad GUI (schematic edit → "Update PCB from
Schematic" → cleanup → DRC). After each step the netlist was diffed and DRC
re-run via `kicad-cli` to confirm exactly the intended parts changed and that
connectivity stayed intact. Final state: 86 footprints, 0 unconnected.
