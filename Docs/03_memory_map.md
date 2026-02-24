# STM32F407 Memory Map

## 1. Introduction

The STM32F407VGT6 follows a 32-bit memory architecture based on the ARM Cortex-M4 core.  
The processor uses a fixed memory map where different regions are reserved for Flash, SRAM, peripherals, and system memory.

Understanding the memory map is critical for:

- Debugging
- Bootloader development
- Register-level programming
- Interrupt handling
- Embedded firmware design

---

## 2. Complete Memory Regions Overview

| Region              | Start Address | Description |
|---------------------|--------------|-------------|
| Flash Memory        | 0x08000000   | Program storage |
| SRAM                | 0x20000000   | Data memory |
| Peripheral Memory   | 0x40000000   | Peripheral registers |
| System Memory       | 0x1FFF0000   | ST Bootloader |
| Option Bytes        | 0x1FFFC000   | Configuration |
| Cortex-M4 System    | 0xE0000000   | NVIC, SCB, SysTick |

---

## 3. Flash Memory (Program Memory)

### Base Address:
0x08000000

### Size:
1 MB

Flash is divided into sectors:

- Sector 0 – 16 KB
- Sector 1 – 16 KB
- Sector 2 – 16 KB
- Sector 3 – 16 KB
- Sector 4 – 64 KB
- Sector 5–11 – 128 KB each

Flash is used for:
- Application code
- Interrupt vector table
- Constant data

---

## 4. SRAM (Data Memory)

### Base Address:
0x20000000

### Total Size:
192 KB

Used for:
- Stack
- Heap
- Global variables
- Local variables
- Buffers

---

## 5. Peripheral Memory Region

### Base Address:
0x40000000

All peripheral registers are memory-mapped.

Example:

GPIOA base address:
0x40020000

USART1 base address:
0x40011000

Accessing peripherals means reading/writing memory addresses.

Example (Register-level):

GPIOA->ODR writes to memory address of output data register.

---

## 6. Cortex-M4 System Region

### Base Address:
0xE0000000

Contains:

- NVIC (Interrupt controller)
- SysTick timer
- System Control Block (SCB)
- Debug registers

Example:
NVIC registers start at 0xE000E100

---

## 7. Vector Table

Located at:

0x08000000 (Default)

Structure:

| Address        | Purpose |
|---------------|----------|
| 0x08000000    | Initial Stack Pointer |
| 0x08000004    | Reset Handler |
| Next entries  | Interrupt handlers |

At reset:

1. Stack pointer loaded from first word
2. Reset handler address loaded from second word
3. Execution jumps to Reset_Handler()

---

## 8. Boot Memory Options

Boot configuration depends on BOOT0 pin.

BOOT0 = 0:
→ Boot from Flash (0x08000000)

BOOT0 = 1:
→ Boot from System Memory (0x1FFF0000)

System memory contains:
- ST factory bootloader

---

## 9. Stack and Heap Placement

Stack grows downward in SRAM.

Typical memory layout:

High Address
↓
Stack
Heap
Global Variables
Low Address

Mismanagement can cause:
- Stack overflow
- HardFault

---

## 10. Memory Access Types

The Cortex-M4 supports:

- Byte access (8-bit)
- Half-word (16-bit)
- Word access (32-bit)

Unaligned access may cause fault.

---

## 11. Memory Protection Unit (MPU)

Optional feature:

- Protect memory regions
- Prevent illegal access
- Used in RTOS systems

---

## 12. Why Memory Map Knowledge Is Important

Understanding memory map helps with:

- Debugging HardFault
- Writing bootloaders
- Register-level programming
- Interrupt configuration
- Optimizing RAM usage

---

## 13. Practical Example

Toggling GPIOA Pin 5 (Register-Level):

GPIOA base: 0x40020000  
ODR offset: 0x14  

ODR Address:
0x40020014

Writing to this address changes output pin state.

---

## 14. Summary

The STM32F407 memory architecture separates:

- Code (Flash)
- Data (SRAM)
- Peripherals (Memory-mapped registers)
- System Control (NVIC, SCB)

This structured memory model enables deterministic real-time embedded system behavior.