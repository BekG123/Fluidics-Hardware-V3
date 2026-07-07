<img src="assets/cephla-logo.png" alt="Cephla" width="180">

# Fluidics Controller PCB (V3)

A KiCad hardware design for the fluidics controller used on Cephla/Squid
microscopy systems. It drives the pumps, valves, and sensors that move and
monitor liquid through the instrument, all coordinated by an on-board
Teensy 4.1 microcontroller.

## What it does

The board is the single point of electrical control for the instrument's
liquid path. The Teensy firmware talks to each subsystem over the bus noted
below and exposes a serial interface to the host software.

## Subsystems

| Subsystem | Qty | Interface | Notes |
|---|---|---|---|
| Syringe pump | 1 | RS-232 (`J3`, DB15) | Primary fluid actuation |
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

## Fabrication

The ready-to-order package lives in `fab_outs_v3/`

## Attribution

Derived from `Fluidics-Hardware-V2` by Kevin Marx. V3 modifications by
Bekhruz Malikov (<bekhruz.malikov@cephla.com>). Built with KiCad 10.
