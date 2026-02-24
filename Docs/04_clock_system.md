# STM32F407 Clock System

## 1. Introduction

The STM32F407 clock system is responsible for generating and distributing clock signals to the CPU and all peripherals.

A correct clock configuration is essential for:

- System performance
- Peripheral timing accuracy
- UART baud rate correctness
- ADC sampling speed
- USB functionality
- Power optimization

The clock system is configured using the RCC (Reset and Clock Control) peripheral.

---

## 2. Clock Sources

The STM32F407 provides multiple clock sources.

### 2.1 HSI – High-Speed Internal

- 16 MHz internal oscillator
- No external components required
- Moderate accuracy

Used as:
- Default clock after reset
- Backup clock

---

### 2.2 HSE – High-Speed External

- External crystal or oscillator
- 8 MHz on STM32F407G-DISC1 board
- More accurate than HSI

Preferred for:
- USB
- Precise communication
- Stable system timing

---

### 2.3 PLL – Phase Locked Loop

The PLL multiplies input clock frequency.

Used to achieve:
Maximum system clock = 168 MHz

PLL input:
HSI or HSE

PLL output:
SYSCLK

---

## 3. Clock Tree Overview

Clock flow:

Clock Source → PLL → SYSCLK → AHB → APB1 / APB2 → Peripherals

Hierarchy:

- SYSCLK → CPU core
- AHB → High-speed bus
- APB1 → Low-speed peripherals
- APB2 → High-speed peripherals

---

## 4. System Clock (SYSCLK)

Maximum frequency: 168 MHz

SYSCLK can be selected from:
- HSI
- HSE
- PLL

Typical professional configuration:

HSE (8 MHz) → PLL → 168 MHz SYSCLK

---

## 5. AHB Bus

AHB connects:

- CPU
- SRAM
- DMA
- Flash
- GPIO

AHB maximum frequency:
168 MHz

AHB prescaler can divide SYSCLK if needed.

---

## 6. APB1 Bus

Used for low-speed peripherals.

Examples:
- USART2
- I2C
- SPI2
- TIM2–TIM7

Maximum frequency:
42 MHz

If SYSCLK = 168 MHz,
APB1 prescaler must divide clock.

---

## 7. APB2 Bus

Used for high-speed peripherals.

Examples:
- USART1
- SPI1
- ADC
- TIM1
- TIM8

Maximum frequency:
84 MHz

---

## 8. Peripheral Clock Enable

Each peripheral clock must be enabled manually.

Example:

To enable GPIOA clock:

RCC->AHB1ENR |= (1 << 0);

Without enabling clock,
peripheral will not work.

---

## 9. Flash Latency

When running at high frequencies:

Flash memory requires wait states.

For 168 MHz:
Flash latency must be configured correctly.

Incorrect latency causes:
- HardFault
- System instability

---

## 10. USB Clock Requirement

USB requires:

48 MHz clock

Derived from PLL.

Improper PLL configuration:
USB will not function.

---

## 11. Clock Configuration in STM32CubeIDE

Inside .ioc file:

Clock Configuration Tab → Graphical clock tree

You can:

- Select HSE
- Enable PLL
- Set SYSCLK to 168 MHz
- Verify APB1 = 42 MHz
- Verify APB2 = 84 MHz

CubeIDE prevents invalid configurations.

---

## 12. Low Power Considerations

Lower clock frequency:
- Reduces power consumption
- Reduces performance

High frequency:
- Higher performance
- Higher power usage

Embedded systems must balance both.

---

## 13. Common Clock Mistakes

- Forgetting to enable HSE
- Wrong PLL multiplier
- Exceeding APB1 limit (42 MHz)
- Wrong Flash latency
- Forgetting peripheral clock enable

---

## 14. Typical Professional Configuration

HSE = 8 MHz  
PLL input = 8 MHz  
PLL output = 168 MHz  

SYSCLK = 168 MHz  
AHB = 168 MHz  
APB1 = 42 MHz  
APB2 = 84 MHz  

This is the standard high-performance setup.

---

## 15. Why Clock System Knowledge Is Critical

Understanding clock tree is essential for:

- Debugging UART baud rate errors
- Fixing timer frequency issues
- Running USB correctly
- Achieving real-time performance
- Designing low-power systems

Clock misconfiguration is one of the most common beginner errors.