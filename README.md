# Fluidics Controller PCB (V3)

A KiCad hardware design for the fluidics controller used on Cephla/Squid
microscopy systems. It drives the pumps, valves, and sensors that move and
monitor liquid through the instrument, all coordinated by an on-board
Teensy 4.1 microcontroller.

**V3** is a minimal, purpose-built variant derived from Kevin Marx's
[`Fluidics-Hardware-V2`](https://github.com/kmarx-kmarx-kmarx/Fluidics-Hardware-V2):
the solenoid-valve, disc-pump, and SPI pressure-sensor subsystems were stripped
out, a 6th selector-valve channel was added, and a GPIO-driven solenoid driver
was introduced. See [`V3_CHANGES.md`](V3_CHANGES.md) for the full change log.

## What it does

The board is the single point of electrical control for the instrument's
liquid path. The Teensy firmware talks to each subsystem over the bus noted
below and exposes a serial interface to the host software.

## Subsystems

| Subsystem | Qty | Interface | Notes |
|---|---|---|---|
| Syringe pump | 1 | RS-232 (`J3`, DB15) | Primary fluid actuation |
| Peristaltic pump | 1 | RS-485 | ⚠️ transceiver not yet on board (see Roadmap) |
| Solenoid valves | up to 7 | GPIO → `U1` TPL7407 → `J5` screw terminal | Low-side driver + per-channel status LEDs |
| Selector valves (IDEX) | 6 | Isolated I²C (5 V) | Addresses set on each valve module |
| Flow sensors | 3 | I²C @ 0x08 | One per I²C port (`J15`/`J17`/`J20`) — fixed address forces separate buses |
| Bubble sensors | 2 | Digital, level-shifted (`J2`/`J4`) | Not I²C |

Isolation and bus conditioning are handled by ADuM1250 / ISO7021 isolators,
a PCA9615 differential-I²C link, and UART/logic level shifters.

## Board specs

- **MCU:** Teensy 4.1 (footprint `U2`, on-board)
- **Stack-up:** 4-layer — `F.Cu` / `In1.Cu` (GND) / `In2.Cu` (+24 V & +5 V planes) / `B.Cu`
- **Power:** +24 V input; Pololu DC-DC regulators for +5 V; on-board LDO (`U3`) for +3.3 V
- **Mounting:** 4 corner plated holes (`H1`–`H4`), chassis GND

## Repository layout

```
fluidics-v2/            KiCad project (schematic, PCB, project-local libraries)
  fluidics-v2.kicad_pro   project file — open this in KiCad
  fluidics-v2.kicad_sch   root schematic (hierarchical child sheets alongside)
  fluidics-v2.kicad_pcb   board layout
fab_outs_v3/            generated fabrication package (gerbers, drill, BOM, CPL, STEP)
fluidics-v3-schematic.pdf  rendered schematic
V3_CHANGES.md           detailed V3 change log vs. upstream V2
```

## Fabrication

The ready-to-order package lives in `fab_outs_v3/`:

- **`fluidics-v3-gerbers.zip`** — upload this to JLCPCB (or any fab). Contains
  all 4 copper layers, masks, pastes, silkscreens, `Edge.Cuts`, and the drill files.
- `positions.csv` / `bom.csv` — CPL and BOM, needed only for SMT assembly
  (LCSC part numbers are not yet filled in).
- `fluidics-v3.step` — 3D model for enclosure fit checks.

To bare-board fabricate: upload the gerber zip, select a **4-layer** stack-up
at 1.6 mm, and order. The Teensy, connectors, and screw terminals are
through-hole / hand-soldered rather than machine-assembled.

To regenerate the package after a board change, re-export with `kicad-cli`
(gerbers + drill + pos + bom + step), then re-zip the gerber folder.

## Roadmap

- **Add an RS-485 transceiver** for the peristaltic pump (currently only the
  RS-232 path for the syringe pump exists).
- Physical layout compaction / final outline confirmation against the enclosure.

## Attribution

Derived from `Fluidics-Hardware-V2` by Kevin Marx. V3 modifications by
Bekhruz Malikov (<bekhruz.malikov@cephla.com>). Built with KiCad 10.
