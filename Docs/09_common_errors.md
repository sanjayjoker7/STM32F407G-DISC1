# Common STM32F407 Errors and Debugging Guide

## 1. Introduction

Embedded systems debugging requires understanding hardware, software, clock configuration, memory, and interrupts.

This document lists the most common errors encountered while developing on STM32F407 and how to fix them.

---

# 2. Programming & Connection Errors

## Error: "Target Not Found"

Cause:
- USB cable not connected
- ST-LINK driver issue
- Wrong debug configuration
- Power supply issue

Solution:
- Check USB cable
- Verify power LED is ON
- Try "Connect under reset"
- Open STM32CubeProgrammer and test connection

---

## Error: ST-LINK not detected

Cause:
- Driver missing
- Faulty cable
- Board not powered

Solution:
- Reinstall STM32CubeIDE
- Install ST-LINK driver
- Try different USB cable

---

# 3. Build Errors

## Error: Undefined Reference

Cause:
- Function declared but not defined
- Missing source file

Solution:
- Check function implementation
- Verify file included in project

---

## Error: Multiple Definition

Cause:
- Same variable defined in multiple files

Solution:
- Use extern in header files
- Define variable only once

---

# 4. GPIO Errors

## LED Not Blinking

Possible Causes:
- GPIO clock not enabled
- Wrong pin number
- Incorrect port
- LED connected incorrectly
- Missing resistor

Solution:
- Enable RCC clock
- Check pin configuration
- Verify hardware wiring

---

## Button Not Working

Cause:
- No pull-up/pull-down resistor
- Wrong EXTI configuration

Solution:
- Enable internal pull-up
- Verify interrupt configuration

---

# 5. Clock Configuration Errors

## UART Baud Rate Incorrect

Cause:
- Wrong system clock
- Wrong APB1/APB2 frequency

Solution:
- Check Clock Configuration tab
- Verify SYSCLK = 168 MHz
- Verify APB1 = 42 MHz

---

## USB Not Working

Cause:
- 48 MHz clock not configured properly

Solution:
- Ensure PLL configuration provides 48 MHz

---

# 6. HardFault Error

## What is HardFault?

HardFault occurs when:

- Invalid memory access
- Stack overflow
- Divide by zero
- Corrupted pointer
- Incorrect clock setup

---

## Debugging HardFault

Steps:

1. Check call stack in debugger
2. Inspect SCB registers:
   SCB->HFSR
   SCB->CFSR
3. Check stack pointer
4. Verify memory addresses
5. Ensure Flash latency matches clock

---

# 7. Interrupt Errors

## Interrupt Not Triggering

Cause:
- NVIC not enabled
- Interrupt flag not cleared
- Wrong IRQ handler name

Solution:
- Call HAL_NVIC_EnableIRQ()
- Verify ISR function name
- Check vector table

---

## Interrupt Repeating Continuously

Cause:
- Interrupt flag not cleared

Solution:
- Clear flag manually (register-level)
- Use HAL handler correctly

---

# 8. DMA Errors

## DMA Not Transferring Data

Cause:
- DMA clock not enabled
- Wrong channel selection
- Interrupt not enabled

Solution:
- Enable DMA clock
- Verify stream/channel
- Check NVIC configuration

---

# 9. Stack Overflow

Symptoms:
- Random crashes
- HardFault
- Unexpected resets

Cause:
- Stack size too small
- Deep recursion
- Large local arrays

Solution:
- Increase stack size in linker script
- Avoid recursion
- Use static buffers

---

# 10. Memory Access Errors

## Using Wrong Address

Cause:
- Writing to incorrect register
- Invalid pointer

Solution:
- Verify base address
- Check memory map documentation

---

# 11. Infinite Loop / Code Not Executing

Cause:
- MCU stuck in HardFault
- Interrupt blocking execution
- Debugger paused at breakpoint

Solution:
- Check debug status
- Resume execution
- Inspect fault handlers

---

# 12. HAL Delay Not Working

Cause:
- SysTick not configured
- Clock misconfiguration

Solution:
- Verify SysTick running
- Check SystemCoreClock value

---

# 13. Floating Inputs

Symptom:
- Random readings on input pins

Cause:
- No pull-up or pull-down resistor

Solution:
- Enable internal pull-up/down

---

# 14. Optimization Issues

Symptom:
- Variables not updating in debugger

Cause:
- Compiler optimization enabled

Solution:
- Use -O0 during debugging
- Mark shared variables as volatile

---

# 15. Debugging Best Practices

- Use breakpoints
- Inspect registers
- Check call stack
- Monitor memory
- Print debug via UART
- Use logic analyzer if needed

---

# 16. Golden Debug Rule

When something fails:

1. Check power
2. Check clock
3. Check peripheral enable
4. Check wiring
5. Check interrupt flags
6. Check memory

Most issues are one of these.

---

# 17. Summary

Common STM32 errors usually come from:

- Clock misconfiguration
- Missing peripheral clock enable
- Wrong GPIO configuration
- Interrupt misconfiguration
- Stack overflow

Systematic debugging approach solves most issues.