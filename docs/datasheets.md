# Hardware documentation

Vendor documents are not stored in this repository (copyright, large binary files).
Below are links to the official sources. You can keep local copies in `docs/datasheets/`, which is ignored by git.

## Microcontroller: STM32F303K8

| Document | Description |
|---|---|
| [STM32F303K8 product page](https://www.st.com/en/microcontrollers-microprocessors/stm32f303k8.html) | Datasheet DS9866, errata, documentation |
| [RM0316 reference manual](https://www.st.com/resource/en/reference_manual/rm0316-stm32f303xbcde-stm32f303x68-stm32f328x8-stm32f358xc-stm32f398xe-advanced-armbased-mcus-stmicroelectronics.pdf) | Peripheral registers: RCC, bxCAN, USART, GPIO |
| [PM0214 programming manual](https://www.st.com/resource/en/programming_manual/pm0214-stm32-cortexm4-mcus-and-mpus-programming-manual-stmicroelectronics.pdf) | Cortex-M4 core: NVIC, SysTick, instruction set |

## Board: NUCLEO-F303K8

| Document | Description |
|---|---|
| [NUCLEO-F303K8 product page](https://www.st.com/en/evaluation-tools/nucleo-f303k8.html) | Schematics, board files |
| [UM1956 STM32 Nucleo-32 user manual](https://www.st.com/resource/en/user_manual/um1956-stm32-nucleo32-boards-mb1180-stmicroelectronics.pdf) | Pinout, solder bridges, ST-LINK, VCP, MCO |

## CAN transceiver: Adafruit CAN Pal (5708), TJA1051T/3

| Document | Description |
|---|---|
| [Adafruit 5708 product page](https://www.adafruit.com/product/5708) | On-board 5 V boost converter, 120 Ω termination switch |
| [Adafruit Learn: CAN Pal guide](https://learn.adafruit.com/adafruit-can-pal) | Pinout, schematic, examples |
| [NXP TJA1051 datasheet](https://www.nxp.com/docs/en/data-sheet/TJA1051.pdf) | Electrical characteristics, VIO pin (/3 variant), Silent mode |

## Standards (paid, references only)

- ISO 11898-1 / -2: CAN data link layer / high-speed physical layer
- ISO 15765-2: ISO-TP (transport protocol over CAN)
- ISO 15765-4 / SAE J1979: OBD-II over CAN, service modes and PIDs