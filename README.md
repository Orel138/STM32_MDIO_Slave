<a name="readme-top"></a>

<h1 align="center">
  <br> STM32_MDIO_Slave <br>
</h1>

<div align="center">

[![Orel138 - STM32_MDIO_Slave](https://img.shields.io/static/v1?label=Orel138&message=STM32_MDIO_Slave&color=blue&logo=github)](https://github.com/Orel138/STM32_MDIO_Slave "Go to GitHub repo")
[![stars - STM32_MDIO_Slave](https://img.shields.io/github/stars/Orel138/STM32_MDIO_Slave?style=social)](https://github.com/Orel138/STM32_MDIO_Slave)
[![forks - STM32_MDIO_Slave](https://img.shields.io/github/forks/Orel138/STM32_MDIO_Slave?style=social)](https://github.com/Orel138/STM32_MDIO_Slave)

[![Open in Visual Studio Code](https://img.shields.io/static/v1?logo=visualstudiocode&label=&message=Open%20in%20Visual%20Studio%20Code&labelColor=2c2c32&color=007acc&logoColor=007acc)](https://open.vscode.dev/Orel138/STM32_MDIO_Slave)
[![license](https://custom-icon-badges.demolab.com/github/license/Orel138/STM32_MDIO_Slave?logo=law&logoColor=white)](https://github.com/Orel138/STM32_MDIO_Slave/blob/main/LICENSE "license MIT")
[![issues](https://custom-icon-badges.demolab.com/github/issues-raw/Orel138/STM32_MDIO_Slave?logo=issue)](https://github.com/Orel138/STM32_MDIO_Slave/issues "issues")

[![STM32](https://img.shields.io/badge/STM32-message?style=flat&logo=stmicroelectronics&color=%2303234B)](https://st.com "STM32")
[![FreeRTOS](https://img.shields.io/badge/FreeRTOS-message?style=flat&logo=freertos&color=%23000000)](https://freertos.org/ "FreeRTOS")

</div>

<div align="center">
  <h4>
    <a href="#about">About</a> |
    <a href="#key-goals">Key Goals</a> |
    <a href="#architecture-overview">Architecture</a> |
    <a href="#requirements">Requirements</a> |
    <a href="#installation">Installation</a> |
    <a href="#usage">Usage</a> |
    <a href="#references">References</a> |
    <a href="#license">License</a>
  </h4>
</div>

<div align="center">
  <sub>Built by
  <a href="https://orel138.github.io">Orel138</a> and
  <a href="https://github.com/orel138/STM32_MDIO_Slave/graphs/contributors">contributors</a>
</div>
<br>

## About

**STM32 MDIO Slave Example** is an implementation example of an MDIO Slave device using STM32 microcontrollers with the FreeRTOS kernel. This project demonstrates how to configure and use the MDIOS peripheral in slave mode to emulate a PHY device, allowing communication with an MDIO master (such as an Ethernet MAC).

The implementation is based on STM32Cube HAL and integrates with FreeRTOS for task management, logging, and CLI interface. It supports read/write operations on PHY registers and handles interrupts for efficient data exchange.

## Table of Contents

- [About](#about)
- [Key Goals](#key-goals)
- [Architecture Overview](#architecture-overview)
- [Project Structure](#project-structure)
- [Design Principles](#design-principles)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [References](#references)
- [Contributing](#contributing)
- [License](#license)

## Key Goals

- Demonstrate MDIO Slave functionality on STM32 devices
- Provide a FreeRTOS-integrated example with logging and CLI
- Ensure compatibility with STM32Cube HAL and BSP
- Offer a foundation for custom PHY emulation in embedded systems

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Architecture Overview

### High-Level Architecture

```
STM32 MDIOS Peripheral (Slave Mode)
        │
        ▼
FreeRTOS Tasks (Heartbeat, CLI, Logging)
```

### Project Structure

```
.
├── Drivers/
│   ├── CMSIS/               # ARM Cortex-M CMSIS headers
│   └── STM32H7xx_HAL_Driver/ # STM32 HAL drivers
│
├── Middlewares/
│   └── Third_Party/
│       └── FreeRTOS/        # FreeRTOS kernel
│
├── Projects/
│   ├── Common/
│   │   ├── cli/             # Command Line Interface utilities
│   │   └── config/          # Common configuration files
│   └── NUCLEO-H723ZG/       # Board-specific projects
│       └── Applications/
│           └── ETH_MDIO_Slave/  # Main application
│
└── README.md                # This file
```

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Design Principles

- HAL-based peripheral initialization
- FreeRTOS task-based architecture
- Interrupt-driven MDIOS operations
- Shadow register management for PHY emulation
- Logging and CLI for debugging and interaction

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Requirements

### Hardware

- NUCLEO-H723ZG or NUCLEO-H743ZI
- MDIO master device (e.g., Ethernet controller) : see https://github.com/Orel138/STM32_MDIO_Master

### Software

- STM32CubeIDE or compatible toolchain
- FreeRTOS kernel
- STM32Cube HAL for H7 series

### Development Environment

- Git
- STM32CubeIDE or VS Code with STM32 extension

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Installation

Clone the repository:

```bash
git clone https://github.com/Orel138/STM32_MDIO_Slave.git
```

Enter the project directory:

```bash
cd STM32_MDIO_Slave
```

Open the project in STM32CubeIDE:

- Import the project from `Projects/NUCLEO-H723ZG/Applications/ETH_MDIO_Slave`
- Build and flash to the target board

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Usage

### Running the Example

1. Flash the firmware to the STM32 Nucleo board
2. Connect an MDIO master (e.g., via Ethernet interface)
3. Use the UART CLI for interaction and monitoring
4. Observe LED heartbeat and MDIO transactions

### CLI Commands

The project includes a CLI for system interaction. Available commands include:

- `ps` - List running tasks
- `kill` - Signal tasks
- `heapstat` - Display heap statistics
- `uptime` - Show system uptime
- `reset` - Reboot the system
- `mdios` - Perform MDIO Slave operations (write/read registers)

### MDIO Operations

The MDIO slave emulates a PHY with 32 registers. Write operations update shadow registers, and read operations return the current values. Interrupts handle transaction completion.

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## References

- [STM32Cube MCU Overall Offer](https://github.com/STMicroelectronics/STM32Cube_MCU_Overall_Offer)
- [FreeRTOS Kernel](https://github.com/FreeRTOS/FreeRTOS-Kernel)
- [STM32 MDIOS Peripheral Documentation](https://www.st.com/resource/en/reference_manual/rm0433-stm32h742-stm32h743-753-and-stm32h750-value-line-advanced-arm-based-32-bit-mcus-stmicroelectronics.pdf)
- [MDIO Protocol Specification](https://en.wikipedia.org/wiki/Management_Data_Input/Output)

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## Contributing

Contributions are welcome.

To contribute:

1. Fork the repository
2. Create a feature branch
3. Commit your changes with clear messages
4. Open a pull request

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

## License

This project is released under the [MIT License](LICENSE).

© [Orel138](https://github.com/Orel138)

<p align="right"><a href="#readme-top">~~~~~ back to top ~~~~~</a></p>

> [!TIP]
> If you find this project useful, consider giving it a ⭐.
> It is the simplest way to show support and helps the project grow.