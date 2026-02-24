# STM32F407 Development Environment Setup

## 1. Introduction

This document explains how to set up the complete development environment
for STM32F407 firmware development using STM32CubeIDE.

This guide is intended for:

- Beginners starting with STM32
- Contributors cloning this repository
- Developers setting up a new system

---

## 2. Hardware Requirements

- STM32F407G-DISC1 development board
- USB Type-A to Mini-B cable (for ST-LINK)
- External components (LED, resistor, jumper wires if needed)

---

## 3. Software Requirements

- STM32CubeIDE (Latest Version Recommended)
- STM32CubeF4 Firmware Package
- ST-LINK Drivers (Usually included with IDE)

Operating Systems Supported:
- Windows
- Linux
- macOS

---

## 4. Installing STM32CubeIDE

Step 1:
Download STM32CubeIDE from:
https://www.st.com/en/development-tools/stm32cubeide.html

Step 2:
Run installer and follow setup wizard.

Step 3:
Launch STM32CubeIDE.

Step 4:
Select workspace directory.

---

## 5. Installing STM32CubeF4 Firmware

When creating a new project:

1. File → New → STM32 Project
2. Select Board: STM32F407G-DISC1
3. If firmware package not installed,
   IDE will prompt to download STM32CubeF4.
4. Click Install.

Firmware includes:
- HAL drivers
- LL drivers
- Middleware libraries
- Startup code

---

## 6. Creating a New Project

1. Open STM32CubeIDE
2. Click File → New → STM32 Project
3. Choose:
   Board Selector → STM32F407G-DISC1
4. Name your project
5. Finish

The IDE generates:
- Core/
- Drivers/
- Startup files
- .ioc configuration file

---

## 7. Configuring Peripherals

Open .ioc file.

You can configure:

- GPIO
- Timers
- UART
- SPI
- I2C
- ADC
- Clock system

After configuration:

Click:
Project → Generate Code

---

## 8. Build Process

Click:
Project → Build Project

Or use:
Hammer icon

If successful:
Console shows:
Build Finished

---

## 9. Programming the Board

Step 1:
Connect USB cable to ST-LINK port.

Step 2:
Click Run (Green Play Button)

IDE will:
- Compile code
- Connect to ST-LINK
- Flash firmware
- Start execution

---

## 10. Debugging

Click Debug (Bug icon)

Debug features:
- Breakpoints
- Step Over
- Step Into
- Variable watch
- Memory inspection

---

## 11. ST-LINK Configuration

If connection fails:

- Check USB cable
- Ensure board power LED is ON
- Open:
  Run → Debug Configurations
- Set:
  Debugger → ST-LINK (OpenOCD)
- Try:
  "Connect under reset"

---

## 12. Repository Usage Instructions

If cloning this repository:

1. Clone repository
2. Open STM32CubeIDE
3. File → Import → Existing Projects into Workspace
4. Select project folder
5. Build
6. Flash to board

---

## 13. Recommended IDE Settings

- Enable optimization level: -O0 (Debug) during development
- Use -O2 for release builds
- Enable warnings
- Keep consistent code formatting

---

## 14. Version Control Best Practices

- Do not push:
  - Debug/
  - Release/
  - .settings/
  - Generated binaries

- Commit:
  - Source files
  - .ioc file
  - Documentation

Use meaningful commit messages.

---

## 15. Common Setup Problems

### Problem: Target not found
Solution:
- Check ST-LINK connection
- Try "Under Reset" mode

### Problem: Firmware package missing
Solution:
- Install STM32CubeF4 package

### Problem: Build errors
Solution:
- Clean project
- Rebuild
- Check include paths

---

## 16. Optional Advanced Tools

- STM32CubeProgrammer (Standalone flashing tool)
- OpenOCD (Command-line debugging)
- Doxygen (Documentation generation)
- CMake (Advanced build systems)

---

## 17. Summary

This setup enables:

- Professional STM32 firmware development
- Debugging and flashing
- Modular project organization
- Scalable embedded system design

After completing setup, you are ready to:

- Develop GPIO projects
- Configure timers and interrupts
- Implement communication protocols
- Build real-time embedded systems