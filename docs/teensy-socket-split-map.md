# Teensy socket split (Route B) — pin/net map

Generated from `fluidics-v3/fluidics-v2.kicad_pcb`. U2 origin **(178.23, 51.33)**, rotation 0.

## Parts

| Part | Covers | Footprint | PCB position | PCB rotation |
|---|---|---|---|---|
| **J6** (left socket) | old U2 pins **1–24** | `teensy4.1:PinSocket_1x24_P2.54mm_Vertical_SMD_DualLand` | 170.61, 51.33 | 0° |
| **J7** (right socket) | old U2 pins **25–48** | same footprint | 185.85, 51.33 | 180° |

Both sockets are the same part (Harwin M20-786 series, 1×24 SMT). J7 is J6 rotated 180°, which is why J7 pin *n* lands on old U2 pin *n+24*. Schematic rotation is irrelevant — only the **PCB** rotation above matters.

> Note: auto-annotation reused the designators **J6/J7**, which belonged to the 1×02 terminal blocks removed in commit `5ce1d61`. Renaming them to J26/J27 avoids confusion when comparing against older fab packages, but is optional.

## How to connect (summary)

| Method | Count | Pins (U2 numbering) |
|---|---:|---|
| Label | 34 | 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 16, 17, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45 |
| **GND power symbol** | 3 | 1, 34, 47 |
| **No-connect flag** | 4 | 2, 3, 15, 46 |
| **Label both ends** | 7 | 18, 19, 20, 21, 22, 23, 48 |

Label text **never includes the leading `/`** — that is the sheet path, not part of the name. `~{...}` is overbar markup and must be typed exactly as shown.

## Full map

| U2 pin | Teensy function | Current net | Socket | Socket pin | Label text to place | Method |
|---:|---|---|---|---:|---|---|
| 1 | GND_1 | `GND` | J6 | 1 | `GND` | **GND power symbol** |
| 2 | 0_RX1_CRX2_CS1_2 | *(auto)* | J6 | 2 | — | **No-connect flag** |
| 3 | 1_TX1_CTX2_MISO1_3 | *(auto)* | J6 | 3 | — | **No-connect flag** |
| 4 | 2_OUT2_4 | `/VALVES_~{RST}` | J6 | 4 | `VALVES_~{RST}` | Label |
| 5 | 3_LRCLK2_5 | `/VALVES_PWM` | J6 | 5 | `VALVES_PWM` | Label |
| 6 | 4_BCLK2_6 | `/GPIO_9` | J6 | 6 | `GPIO_9` | Label |
| 7 | 5_IN2_7 | `/GPIO_8` | J6 | 7 | `GPIO_8` | Label |
| 8 | 6_OUT1D_8 | `/~{INVALID}_SYRPUMP` | J6 | 8 | `~{INVALID}_SYRPUMP` | Label |
| 9 | 7_RX2_OUT1A_9 | `/UART_TX_SYRPUMP` | J6 | 9 | `UART_TX_SYRPUMP` | Label |
| 10 | 8_TX2_IN1_10 | `/UART_RX_SYRPUMP` | J6 | 10 | `UART_RX_SYRPUMP` | Label |
| 11 | 9_OUT1C_11 | `/SPI_~{CS}_PRESS` | J6 | 11 | `SPI_~{CS}_PRESS` | Label |
| 12 | 10_CS_MQSR_12 | `/SPI_~{CS}_VALVES` | J6 | 12 | `SPI_~{CS}_VALVES` | Label |
| 13 | 11_MOSI_CTX1_13 | `/SPI_MOSI` | J6 | 13 | `SPI_MOSI` | Label |
| 14 | 12_MISO_MQSL_14 | `/SPI_MISO` | J6 | 14 | `SPI_MISO` | Label |
| 15 | 3V3_15 | *(auto)* | J6 | 15 | — | **No-connect flag** |
| 16 | 24_A10_TX6_SCL2_16 | `/SCL2` | J6 | 16 | `SCL2` | Label |
| 17 | 25_A11_RX6_SDA2_17 | `/SDA2` | J6 | 17 | `SDA2` | Label |
| 18 | 26_A12_MOSI1_18 | `/Bubble Sensors/2B 3.3V` | J6 | 18 | `BUB_2B` | **Label both ends** |
| 19 | 27_A13_SCK1_19 | `/Bubble Sensors/2A 3.3V` | J6 | 19 | `BUB_2A` | **Label both ends** |
| 20 | 28_RX7_20 | `/Bubble Sensors/1B 3.3V` | J6 | 20 | `BUB_1B` | **Label both ends** |
| 21 | 29_TX7_21 | `/Bubble Sensors/1A 3.3V` | J6 | 21 | `BUB_1A` | **Label both ends** |
| 22 | 30_CRX3_22 | `/Bubble Sensors/Calib 2 3.3V` | J6 | 22 | `BUB_CALIB2` | **Label both ends** |
| 23 | 31_CTX3_23 | `/Bubble Sensors/Calib 1 3.3V` | J6 | 23 | `BUB_CALIB1` | **Label both ends** |
| 24 | 32_OUT1B_24 | `/PG-12V` | J6 | 24 | `PG-12V` | Label |
| 25 | 33_MCLK2_25 | `/PG-5V` | J7 | 1 | `PG-5V` | Label |
| 26 | 34_RX8_26 | `/~{CS}3` | J7 | 2 | `~{CS}3` | Label |
| 27 | 35_TX8_27 | `/~{CS}2` | J7 | 3 | `~{CS}2` | Label |
| 28 | 36_CS_28 | `/~{CS}1` | J7 | 4 | `~{CS}1` | Label |
| 29 | 37_CS_29 | `/~{CS}0` | J7 | 5 | `~{CS}0` | Label |
| 30 | 38_CS1_IN1_30 | `/GPIO_7` | J7 | 6 | `GPIO_7` | Label |
| 31 | 39_MISO1_OUT1A_31 | `/GPIO_6` | J7 | 7 | `GPIO_6` | Label |
| 32 | 40_A16_32 | `/GPIO_5` | J7 | 8 | `GPIO_5` | Label |
| 33 | 41_A17_33 | `/POT_ANALOG` | J7 | 9 | `POT_ANALOG` | Label |
| 34 | GND_34 | `GND` | J7 | 10 | `GND` | **GND power symbol** |
| 35 | 13_SCK_LED_35 | `/SPI_SCK` | J7 | 11 | `SPI_SCK` | Label |
| 36 | 14_A0_TX3_SPDIF_OUT_36 | `/UART_RX_DISCPUMP` | J7 | 12 | `UART_RX_DISCPUMP` | Label |
| 37 | 15_A1_RX3_SPDIF_IN_37 | `/UART_TX_DISCPUMP` | J7 | 13 | `UART_TX_DISCPUMP` | Label |
| 38 | 16_A2_RX4_SCL1_38 | `/SCL1` | J7 | 14 | `SCL1` | Label |
| 39 | 17_A3_TX4_SDA1_39 | `/SDA1` | J7 | 15 | `SDA1` | Label |
| 40 | 18_A4_SDA_40 | `/SCL` | J7 | 16 | `SCL` | Label |
| 41 | 19_A5_SCL_41 | `/SDA` | J7 | 17 | `SDA` | Label |
| 42 | 20_A6_TX5_LRCLK1_42 | `/GPIO_4` | J7 | 18 | `GPIO_4` | Label |
| 43 | 21_A7_RX5_BCLK1_43 | `/GPIO_3` | J7 | 19 | `GPIO_3` | Label |
| 44 | 22_A8_CTX1_44 | `/GPIO_2` | J7 | 20 | `GPIO_2` | Label |
| 45 | 23_A9_CRX1_MCLK1_45 | `/GPIO_1` | J7 | 21 | `GPIO_1` | Label |
| 46 | 3V3_46 | *(auto)* | J7 | 22 | — | **No-connect flag** |
| 47 | GND_47 | `GND` | J7 | 23 | `GND` | **GND power symbol** |
| 48 | VIN_48 | `Net-(D21-K)` | J7 | 24 | `VIN` | **Label both ends** |

## The 7 pins that need care

- **U2.18** (26_A12_MOSI1_18) — `/Bubble Sensors/2B 3.3V`: named inside the *Bubble Sensors* subsheet; label the root-sheet wire too. Put `BUB_2B` on the existing U2 pin wire **and** on J6.18. This renames the net to `/BUB_2B` in the PCB (cosmetic).
- **U2.19** (27_A13_SCK1_19) — `/Bubble Sensors/2A 3.3V`: named inside the *Bubble Sensors* subsheet; label the root-sheet wire too. Put `BUB_2A` on the existing U2 pin wire **and** on J6.19. This renames the net to `/BUB_2A` in the PCB (cosmetic).
- **U2.20** (28_RX7_20) — `/Bubble Sensors/1B 3.3V`: named inside the *Bubble Sensors* subsheet; label the root-sheet wire too. Put `BUB_1B` on the existing U2 pin wire **and** on J6.20. This renames the net to `/BUB_1B` in the PCB (cosmetic).
- **U2.21** (29_TX7_21) — `/Bubble Sensors/1A 3.3V`: named inside the *Bubble Sensors* subsheet; label the root-sheet wire too. Put `BUB_1A` on the existing U2 pin wire **and** on J6.21. This renames the net to `/BUB_1A` in the PCB (cosmetic).
- **U2.22** (30_CRX3_22) — `/Bubble Sensors/Calib 2 3.3V`: named inside the *Bubble Sensors* subsheet; label the root-sheet wire too. Put `BUB_CALIB2` on the existing U2 pin wire **and** on J6.22. This renames the net to `/BUB_CALIB2` in the PCB (cosmetic).
- **U2.23** (31_CTX3_23) — `/Bubble Sensors/Calib 1 3.3V`: named inside the *Bubble Sensors* subsheet; label the root-sheet wire too. Put `BUB_CALIB1` on the existing U2 pin wire **and** on J6.23. This renames the net to `/BUB_CALIB1` in the PCB (cosmetic).
- **U2.48** (VIN_48) — `Net-(D21-K)`: net is unnamed today; label U2.48 *and* the socket pin. Put `VIN` on the existing U2 pin wire **and** on J7.24. This renames the net to `/VIN` in the PCB (cosmetic).

## Verification

After Update PCB and a zone refill, DRC must match the current baseline: **6 unconnected** (5 intentional GPIO_8/9 + SPI no-connects, 1 pre-existing +5V stub gap near U13/U4), 0 shorts / clearance / isolated copper / starved thermals. A higher count means a mismapped pin.
