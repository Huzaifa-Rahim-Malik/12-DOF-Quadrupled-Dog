# Quadruped Robot — 12-DOF Electronics Design

Electronics and power-distribution design for a 12-degree-of-freedom quadruped robot (6 servos driving the front legs, 6 driving the back legs), controlled by a Raspberry Pi 4B.

![Block diagram](images/Block_Diagram.png)

## System Overview

- **Compute:** Raspberry Pi 4B as the main controller, communicating with a dedicated servo controller over I2C (SDA/SCL) and PWM.
- **Actuation:** 12 servo motors total — 6 for front-leg control, 6 for back-leg control — driven via a servo controller with two PWM banks (channels 0–5 front, 6–10 back).
- **Power architecture:** a single 14.8V / 7200 mAh battery pack feeds three buck converters:
  - Buck 1 — 6.5V @ 15A for the front 6 servos
  - Buck 2 — 6.5V @ 15A for the back 6 servos
  - Buck 3 — 5V @ 3.5A for the Raspberry Pi 4 (with a 3.3V rail for logic)
- **Load calculation:** worst-case current draw was modeled for two candidate servo options (MG996R ~11kg·cm vs DS3218MG ~20kg·cm) across idle, typical gait, and all-six-stalled scenarios, to size the buck converters and battery draw (peak ≈ 16–17A reflected at the battery). Full working is in `docs/Load_Calculation.docx`.

## Repository Structure

```
hardware/altium/   Altium project — schematic, block diagram, schematic library, PCB project files
docs/               Block diagram & schematic PDF exports, load calculation, source Visio diagram
images/             Block diagram render for this README
```

## Hardware Design

The schematic and block diagram were designed in Altium Designer (`hardware/altium/`):
- `Block Diagram.SchDoc` — system-level power and signal architecture (servo rails, controller, Pi)
- `Schematic.SchDoc` — detailed circuit schematic
- `Schlib2.SchLib` — custom schematic symbol library used in the design

PDF exports of both are in `docs/` for quick viewing without Altium installed.

## Author

Muhammad Huzaifa Rahim Malik — AITEC NCP, Islamabad.
