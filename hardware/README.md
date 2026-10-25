# Hardware Design

This directory is reserved for the project's optional custom hardware design. We will use KiCad for the schematic, PCB layout, and related design files.

## Project status and priority

Our immediate goal is to complete and validate the firmware prototype in approximately one week. We will build that prototype with the STM32 NUCLEO-F303K8 development board and an external TJA1051T/3 CAN transceiver module (Adafruit 5708). This lets us develop and test the core firmware without waiting for a custom PCB.

The custom hardware is a later, non-blocking part of the project. We may postpone it until after the prototype is working, and its schedule is not part of the one-week firmware target. The firmware should remain useful and testable on the development hardware even if the custom board is delayed.

## Planned custom board

When we are ready to begin the hardware work, we plan to design a board around an STM32G4-series microcontroller and a TCAN1044AV-Q1 CAN transceiver. The design will build on what we learn from the firmware prototype and bench testing. Before committing to a layout, we will confirm the exact component choices, interfaces, power requirements, and connector pinout.

## Expected contents

As the hardware work progresses, this directory may contain:

- KiCad project, schematic, and PCB layout files.
- Project-specific symbols, footprints, and 3D models, where needed.
- A bill of materials and notes on component selection.
- Manufacturing outputs, such as Gerber files and drill files, when the design is ready for fabrication.
- Assembly, bring-up, and hardware validation notes.

Until the custom design is underway, this directory may contain only this overview. The development-board prototype and its firmware do not depend on KiCad files being present.
