# SHROTA PRO — Handheld Rocket Recovery Ground Station

Custom-engineered handheld ground station PCB developed for **Team Sammard** to track, receive telemetry from, and recover high-powered sounding rockets post-touchdown. Built around an **STM32H743VIT6** microcontroller, the board computes real-time relative distance and azimuth bearing between the recovery team and the landed rocket.

![SHROTA PRO PCB](docs/assembled_board.jpg)

---

## System Specifications

| Subsystem | Component / Specification |
| :--- | :--- |
| **Microcontroller** | STMicroelectronics **STM32H743VITx** (`LQFP-100`, 25 MHz HSE + 32.768 kHz LSE) |
| **Primary Power Input** | Dual **7.4V 18650** Li-ion battery holders (`BT1`, `BT3`) + **USB-C** (`GCT USB4105`) |
| **Power Regulation** | Dual **TPS563200** synchronous buck converters (`5V` & `3.3V`) + **AMS1117-5.0 / 3.3** LDOs |
| **Navigation & Heading** | **Quectel L89** GNSS, **u-blox NEO-M8N** GNSS, **Bosch BMM150** 3-axis magnetometer |
| **Telemetry & RF Links** | **LLCC68** LoRa, **REYAX RYLR998** LoRa, **RFD900x** long-range radio modem interface |
| **UI & Peripherals** | SPI Screen + microSD slot (`SCREENSD`), **WS2812B** RGB status LED, pushbuttons, SWD/UART debug |
| **EDA & Fabrication** | KiCad 2-layer PCB (`Shrota Pro Verified`) with `SMA` & `U.FL` RF connectors |

---

## Hardware Architecture

1. **Multi-Stage Power Distribution & Protection:**
   - Powered from dual **7.4V** battery cells (`BT1`, `BT3`) with **SS14** Schottky OR-ing/reverse-current diodes and **SMAJ7.5CA** TVS transient suppression.
   - High-efficiency **TPS563200** step-down switching regulators generate the main `5V` and `3.3V` rails, isolated via ferrite beads (`FB1–FB5`) to keep RF and GNSS supplies clean.
   - **USB-C** receptacle with `5.1k` CC pull-downs (`R6`, `R7`) and **ESD9L5.0ST5G** ESD protection handles serial debugging and firmware flashing.
2. **Dual-GNSS & Geomagnetic Heading Suite:**
   - Combines **Quectel L89** and **u-blox NEO-M8N** GNSS receivers with a **BMM150** 3-axis geomagnetic compass so the handheld unit calculates both rocket coordinates and user heading without external phone connectivity.
3. **Multi-Band Long-Range Telemetry Block:**
   - Supports **LLCC68** and **RYLR998** LoRa modules alongside a dedicated **RFD900x** UART radio modem header, routed to onboard **SMA** and **U.FL** coaxial connectors.
4. **Field Interface & Debug:**
   - Drives an onboard display and SD card interface (`SCREENSD`), tactile navigation switches (`SW1`, `SW5–SW7`), a **WS2812B** status indicator, and dedicated **ST-LINK SWD** and **UART** headers.

---

## Repository Contents

- `hardware/kicad/` — Verified KiCad schematic (`Shrota Pro Verified.kicad_sch`), PCB layout (`Shrota Pro Verified.kicad_pcb`), and project files.
- `hardware/manufacturing/` — Complete Gerber layers and drill files (`ShrotaPRO_Gerbers_and_Drill.zip`).
- `hardware/bom/` — Full 64-line-item Bill of Materials (`ShrotaPRO_BOM.csv`).
- `docs/` — Schematic PDF and board renders.
