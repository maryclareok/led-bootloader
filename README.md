# STM32 Custom Bootloader — STM32L475VG

A custom bootloader project for the STM32L475 microcontroller, demonstrating how to transfer execution from a bootloader to a user application using vector table relocation, flash memory partitioning, and firmware handoff.

This project is part of a three-part YouTube tutorial series exploring STM32 bootloader development using C and STM32CubeIDE.

## Project Overview

The bootloader executes first when the microcontroller starts, performs its initialization sequence, and transfers control to an application stored at a separate flash memory address.

**Key concepts covered:**

- ARM Cortex-M boot process
- STM32 flash memory partitioning
- Vector Table Offset Register (VTOR)
- Main Stack Pointer (MSP) initialization
- Application reset handler execution
- Interrupt management during firmware handoff
- Embedded firmware development and debugging

## Hardware and Software

| Component | Description |
|---|---|
| Microcontroller | STM32L475VGT6 |
| IDE | STM32CubeIDE |
| Configuration | STM32CubeMX |
| Programming language | C |
| Debugging interface | ST-LINK / SWD |
| Firmware package | STM32Cube FW_L4 V1.18.2 |

## Project Files — Google Drive

The project files are available through the Google Drive folder below.

**[Open STM32 Bootloader Project Folder](https://drive.google.com/drive/folders/1gsx1aJYHLriSP3tHLPW9a-Lhsd-ivweB?usp=sharing)**

This external folder is provided for accessing additional project materials. Its contents have not been independently verified against this repository.

## Flash Memory Layout

The microcontroller's flash memory is divided into two regions:

| Component | Start Address | Description |
|---|---|---|
| Bootloader | `0x08000000` | First 64 KB of flash |
| Application | `0x08010000` | Remaining application flash |

The application vector table begins at `0x08010000`.

The first two entries contain:

- Initial application stack pointer: `0x08010000`
- Application reset handler address: `0x08010004`

## Bootloader Operation

1. The STM32 starts executing the bootloader after reset.
2. The bootloader performs its initialization sequence.
3. The bootloader validates the application entry information.
4. Interrupts and SysTick are disabled before the firmware handoff.
5. The application vector table is configured using VTOR.
6. The application's Main Stack Pointer is loaded.
7. Execution transfers to the application reset handler.

This describes the bootloader design. The original C implementation should be consulted for the exact handoff sequence.

## LED Demonstration

An LED connected to PB14 is used to distinguish the bootloader from the main application.

**Bootloader behavior:**
- LED blinks twice.
- A short pause of approximately 300 ms follows.

**Application behavior:**
- After the bootloader transfers execution, the application toggles the LED approximately every 500 ms.

These behaviors are based on the project demonstration.

## YouTube Tutorial Series

The project accompanies a three-part YouTube tutorial series documenting the STM32 bootloader development process.

### Part 1 — STM32 Bootloader Tutorial

[Watch Part 1 on YouTube](https://youtu.be/UElGZ5fQhmg)

### Part 2 — STM32 Bootloader Tutorial

[Watch Part 2 on YouTube](https://youtu.be/8a7JMIiE7iU)

### Part 3 — STM32 Bootloader Tutorial

Link to be added.

*Note: The third URL originally provided duplicates Part 1.*

## Repository Structure

```text
STM32-Custom-Bootloader/
├── README.md
├── .gitignore
├── cubemx/
│   └── led_bootloader.ioc
└── docs/
    └── source-files-needed.md
```

## Opening the Project Configuration

1. Install STM32CubeIDE.
2. Download or clone this repository.
3. Open `cubemx/led_bootloader.ioc` in STM32CubeIDE or STM32CubeMX.
4. Review the microcontroller configuration and peripheral settings.
5. Use the original STM32CubeIDE project source files to restore the custom bootloader and application implementation.

**Important:** Generating code from the `.ioc` configuration alone does not recreate the custom bootloader handoff logic.

## Project Status

The current repository package includes the STM32CubeMX configuration and project documentation.

The original bootloader C source files, application C source files, linker scripts, and complete STM32CubeIDE project files have not yet been included in the repository package.

Until those files are added, this repository should be treated as project documentation and configuration rather than a complete buildable firmware implementation.

## Future Improvements

- Add the complete bootloader and application source code.
-
