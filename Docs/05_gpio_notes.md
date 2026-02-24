# STM32F407 GPIO (General Purpose Input Output) Notes

## 1. Introduction

GPIO (General Purpose Input Output) pins allow the microcontroller to interact with external hardware.

GPIO is used for:

- Controlling LEDs
- Reading buttons
- Driving relays
- Interfacing sensors
- Communicating with peripherals (alternate functions)

Understanding GPIO is fundamental to embedded development.

---

## 2. GPIO Ports Overview

The STM32F407 provides the following GPIO ports:

- GPIOA
- GPIOB
- GPIOC
- GPIOD
- GPIOE
- GPIOF
- GPIOG
- GPIOH
- GPIOI

Each port contains up to 16 pins (Pin 0 – Pin 15).

Example:
PA5 → Port A, Pin 5  
PD12 → Port D, Pin 12

---

## 3. GPIO Operating Modes

Each GPIO pin can operate in one of four modes:

### 3.1 Input Mode
Used to read external signals.

Example:
- Push button
- Sensor output

---

### 3.2 Output Mode
Used to drive external devices.

Example:
- LED
- Relay
- Transistor

---

### 3.3 Alternate Function Mode
Used when pin is controlled by a peripheral.

Example:
- UART TX/RX
- SPI
- I2C
- Timer PWM

---

### 3.4 Analog Mode
Used for:
- ADC input
- DAC output
- Reducing power consumption

---

## 4. Output Configuration

When configured as output, two options exist:

### 4.1 Output Type

- Push-Pull
- Open-Drain

Push-Pull:
Drives HIGH and LOW actively.

Open-Drain:
Can only pull LOW, requires external pull-up resistor.

---

### 4.2 Output Speed

- Low speed
- Medium speed
- High speed
- Very high speed

Higher speed:
- Faster transitions
- More power consumption
- More EMI noise

---

## 5. Pull-Up and Pull-Down Resistors

Each pin can enable internal:

- Pull-Up resistor
- Pull-Down resistor
- No pull

Used to avoid floating inputs.

Example:
Button input → enable Pull-Up

---

## 6. GPIO Electrical Characteristics

Operating voltage:
3.3V (Typical)

Maximum recommended current per pin:
< 20 mA

Important:

Never connect 5V directly to GPIO pin.  
Use level shifting if required.

Always use resistor when connecting LED.

Example:
330Ω resistor for LED.

---

## 7. GPIO Registers (Register-Level View)

Each GPIO port has several registers:

- MODER   → Mode register
- OTYPER  → Output type
- OSPEEDR → Output speed
- PUPDR   → Pull-up/pull-down
- IDR     → Input data register
- ODR     → Output data register
- BSRR    → Bit set/reset register

Example (Register-Level LED toggle):

GPIOA->ODR ^= (1 << 5);

---

## 8. Clock Enable Requirement

Before using any GPIO port:

Its clock must be enabled.

Example:

RCC->AHB1ENR |= (1 << 0);  // Enable GPIOA clock

Without enabling clock:
GPIO will not work.

---

## 9. HAL Example

Using HAL:

```c
HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);