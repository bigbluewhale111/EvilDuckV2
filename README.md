# EvilDuck V2

A custom RP2040-based USB HID research board developed as part of a thesis on **BadUSB / HID injection detection and protection**.

The project is intended for controlled laboratory research, defensive security testing, firmware experimentation, and evaluation of host-side protections against malicious or abnormal USB Human Interface Device (HID) behavior.

---

## 1. Project Overview

EvilDuck V2 is a compact custom USB development board designed around the **Raspberry Pi RP2040**.

The PCB is intended to provide a small, self-contained platform for:

- USB HID research
- Keyboard-emulation experiments
- Host-side HID injection detection testing
- USB behavior logging and evaluation
- Firmware prototyping
- microSD-based storage
- SWD/UART debugging
- Thesis experiments involving BadUSB defenses

The design uses **two USB connectors**, one on each end of the PCB, to simplify development and testing.

---

## 2. Thesis Context

This board is being developed for a thesis focused on protecting users from **BadUSB-style HID injection attacks**.

The broader research investigates host-side mechanisms for identifying suspicious keyboard-like behavior, including characteristics such as:

- Unrealistically fast key intervals
- Typing-rate anomalies
- Timing distributions
- Burst behavior
- Pause structure
- Statistical deviation from normal human input
- Device-specific behavioral profiles

The hardware provides a reproducible USB HID test platform for evaluating these defensive mechanisms.

---

## 3. PCB Specifications

| Property | Value |
|---|---|
| PCB size | **80 mm x 20 mm** |
| Main MCU | **RP2040** |
| USB connector 1 | USB-A |
| External storage | microSD |
| Debug interfaces | SWD / UART |
| Flash | External QSPI flash |
| Main supply | USB 5 V |
| Logic supply | 3.3 V |
| PCB target | 2-layer board |

The board has one USB connector mounted at each short end:

---

## 4. Hardware Architecture

Main functional blocks include:

- RP2040 microcontroller
- External QSPI flash
- 12 MHz crystal oscillator
- USB-A interface
- USB power input
- 3.3 V LDO regulator
- microSD card socket
- RUN / BOOT controls
- Status LEDs
- SWD programming/debug interface
- UART debug interface

---

## 5. Main Components

### RP2040

The RP2040 is the main MCU and handles:

- USB communication
- HID firmware
- microSD communication
- GPIO
- timing measurements
- firmware logic
- debug interfaces

### External QSPI Flash

The RP2040 boots from external QSPI flash. The flash should be placed close to the RP2040 to keep QSPI traces short, especially the clock line.

### microSD Card

The microSD interface provides removable storage for:

- experiment configuration
- test data
- logging
- firmware resources
- non-sensitive test scripts
- research datasets

### USB Interfaces

The board contains:

- **USB-A connector on one end**

The connectors are mechanically placed at the edges of the PCB so that their mating faces point outward.

### Power Supply

USB 5 V power is converted to 3.3 V using an LDO regulator.

Power-related circuitry includes:

- USB input protection
- Schottky ORing diodes
- fuse/protection element
- bulk capacitance
- 3.3 V regulator
- local decoupling capacitors

---

## 6. Component Orientation Guidelines

### USB-A

- Place at the **left edge**
- Mating side faces outward
- Body extends toward the PCB center

### RP2040

Place the RP2040 near the center of the board.

Choose the orientation that keeps these routing groups short:

- USB D+ / D-
- QSPI flash
- crystal
- microSD SPI
- 3.3 V power

Always verify the **pin-1 marker** on the actual EasyEDA footprint before routing.

### QSPI Flash

Place immediately beside the RP2040.

Keep:

- QSPI clock short
- QSPI traces compact
- decoupling capacitor directly beside the flash supply pin

### Crystal

Place the crystal and load capacitors immediately beside the RP2040 oscillator pins.

Avoid routing high-speed or noisy signals through the oscillator area.

### Decoupling Capacitors

Place decoupling capacitors beside the power pins they support. Do not group them together purely for visual neatness.

---

## 7. Dual-USB Design Note

The two USB connectors require special consideration.

Power from the two connectors may be isolated or combined using suitable protection circuitry, but **USB D+ and D- should not simply form an uncontrolled T-junction between two active hosts**.

Use an intentional USB data-path strategy, for example:

- only one connector active at a time
- solder-jumper selection
- 0-ohm resistor selection
- a USB 2.0 analog switch / multiplexer
- another controlled switching method

The board should not be connected to two independent USB hosts simultaneously unless the hardware has specifically been designed for that operating mode.

---

## 8. PCB Routing Priorities

Recommended routing order:

1. RP2040 power and decoupling
2. Crystal oscillator
3. QSPI flash
4. USB D+ / D-
5. Main 5 V power path
6. 3.3 V distribution
7. microSD SPI
8. SWD / UART
9. Buttons and LEDs
10. Ground pours and stitching vias

### USB Routing

The USB differential pair should:

- remain together
- use consistent trace width and spacing
- avoid unnecessary vias
- avoid large length mismatch
- avoid routing over ground-plane gaps
- avoid sharp 90-degree corners
- maintain a continuous ground reference

Final trace width and spacing should be calculated from the actual PCB manufacturer's stack-up.

---

## 9. Initial Board Bring-Up

Recommended sequence:

1. Inspect the unpowered PCB for solder bridges and assembly defects.
2. Check resistance between 5 V and GND.
3. Check resistance between 3.3 V and GND.
4. Apply current-limited USB power.
5. Confirm the 3.3 V regulator output.
6. Confirm RP2040 power rails.
7. Test SWD connectivity.
8. Test BOOTSEL / firmware programming.
9. Flash a minimal firmware image.
10. Verify USB enumeration.
11. Verify status LEDs.
12. Verify microSD communication.
13. Verify UART.
14. Proceed with thesis-specific HID experiments only after basic hardware validation.

---

## 10. Research and Ethical Use

This project is intended for:

- academic research
- defensive cybersecurity research
- authorized penetration testing
- USB security education
- controlled laboratory experiments
- development and evaluation of HID-injection defenses

Do not use the hardware to access, modify, disrupt, or test systems without explicit authorization.

Experiments should be performed on dedicated laboratory systems or systems for which the researcher has permission.

---

## 11. Documentation Goals

This repository should eventually contain enough information to reproduce the research hardware, including:

- schematic
- PCB layout
- bill of materials
- fabrication files
- assembly information
- firmware source
- hardware bring-up procedure
- experiment methodology
- measurement results
- known limitations

---


## 12. Project Information

**Project:** EvilDuck V2  
**Type:** Custom USB HID research hardware  
**Purpose:** Thesis research on BadUSB / HID injection detection and protection  
**PCB:** 80 mm x 20 mm  
**MCU:** RP2040

---

## Disclaimer

This project is a research prototype. Schematics, PCB files, firmware, and documentation may contain errors and should be independently reviewed before fabrication or deployment.

The author assumes no responsibility for damage resulting from incorrect assembly, electrical faults, misuse, or unauthorized security testing.

---

## Reference

- [EvilDuck](https://github.com/cifertech/EvilDuck)
- [RP2040 Datasheet](https://pip-assets.raspberrypi.com/categories/814-rp2040/documents/RP-008371-DS-1-rp2040-datasheet.pdf)
- [RP2040 Dev-Board](https://github.com/abhinav937/RP2040-Dev-Board)