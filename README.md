# SimpleFOC Dual ESC

This repository contains the hardware design files for a compact dual-motor BLDC controller built around the SimpleFOC ecosystem.  
The board is designed to run two 3-phase motors independently with field-oriented control (FOC) using an STM32G4 microcontroller.

## What the device does

The controller takes a single high-voltage DC input and drives two BLDC motors through two independent 3-phase power stages.  
Each motor stage uses a dedicated gate driver and current-sense path so firmware can regulate torque/current, speed, and position.

At a high level, the board:

- Converts a DC supply (up to 36 V, per current spec draft) into PWM-driven 3-phase outputs for **Motor 1** and **Motor 2**
- Uses dual DRV8323-based driver stages for 6-PWM control of each motor
- Measures phase/motor current for closed-loop control and protection
- Interfaces with Hall sensors for rotor position feedback
- Exposes control/debug interfaces including I2C, SPI headers, USB-C, reset, and programming pins

## Hardware highlights

- **MCU:** STM32G474CBTx (FOC-capable Cortex-M4)
- **Power input:** XT60 connector footprint, board marked **36V MAX**
- **Motor outputs:** Two MR60 3-phase motor connectors
- **Board outline:** 50 mm × 50 mm (from KiCad PCB edge cuts)
- **Power stage:** Dual 3-phase inverter architecture (6 MOSFETs per motor stage)

## Repository layout

- `specifications.md`  
  Project specification draft (electrical, control, thermal, and interface targets).
- `KiCad/simpleFOC Dual Motor Controller.kicad_pro`  
  Top-level KiCad project.
- `KiCad/simpleFOC Dual Motor Controller.kicad_sch`  
  Top-level schematic with MCU, power, interfaces, and two motor-driver hierarchical sheets.
- `KiCad/DriverStage.kicad_sch`  
  Per-motor driver stage (reused for Motor Driver 1 and Motor Driver 2).
- `KiCad/simpleFOC Dual Motor Controller.kicad_pcb`  
  PCB layout and silkscreen connector labels.

## Current status

This repo currently provides hardware design and specification files.  
Firmware implementation and full bring-up documentation are not yet included here.
