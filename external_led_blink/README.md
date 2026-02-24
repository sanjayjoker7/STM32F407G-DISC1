# External LED Blinking – STM32F407

## Project Overview

This project demonstrates how to control an external LED using GPIO on the STM32F407G-DISC1 development board.

An external LED is connected to GPIO pin PA5 and toggled every 500 milliseconds using STM32 HAL drivers.

This project validates:

- GPIO configuration
- Clock initialization
- External hardware interfacing
- HAL-based firmware structure
- Basic embedded debugging

---

## Hardware Used

- Board: STM32F407G-DISC1
- MCU: STM32F407VGT6 (ARM Cortex-M4)
- External LED
- 220Ω–330Ω resistor
- Jumper wires

---

## External LED Connections

### Wiring Diagram

PA5  ----  330Ω Resistor  ----  LED (Anode / Long Leg)  
LED (Cathode / Short Leg)  ----  GND  

### Connection Table

| STM32 Pin | Connect To |
|------------|------------|
| PA5        | One side of resistor |
| Resistor   | LED Anode (long leg) |
| LED Cathode| GND |

### Important Notes

- Always use a resistor to limit current.
- Do NOT connect LED directly to GPIO pin.
- STM32 GPIO operates at 3.3V.
- Ensure LED GND is connected to board GND.

---

## GPIO Configuration (STM32CubeIDE)

Inside the `.ioc` file:

- Select PA5
- Mode: GPIO_Output
- Output Type: Push-Pull
- Pull: No Pull
- Speed: Low

Generate code after configuration.

---

## HAL Implementation

Inside `main.c`:

```c
while (1)
{
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
    HAL_Delay(500);
}
```

### Code Explanation

- `HAL_GPIO_TogglePin()` toggles the LED state (ON ↔ OFF)
- `HAL_Delay(500)` waits 500 milliseconds
- `while(1)` ensures infinite execution

Result:  
The external LED blinks every 0.5 seconds.

---

## Register-Level Implementation (Advanced)

Clock enable:

```c
RCC->AHB1ENR |= (1 << 0);
```

Configure PA5 as output:

```c
GPIOA->MODER |= (1 << 10);
```

Toggle LED:

```c
GPIOA->ODR ^= (1 << 5);
```

This method provides faster execution and deeper hardware control.

---

## Build and Flash Instructions

1. Open project in STM32CubeIDE  
2. Connect USB to ST-LINK port  
3. Click **Build**  
4. Click **Run (▶)**  
5. Observe LED blinking  

---

## Troubleshooting

If the LED does not blink:

- Check LED polarity
- Verify resistor connection
- Confirm PA5 is configured as output
- Ensure GPIOA clock is enabled
- Check board power LED
- Verify correct GND connection

---

## Learning Outcomes

After completing this project, you understand:

- GPIO configuration in STM32
- Clock enable requirement
- HAL driver usage
- External hardware interfacing
- Basic embedded debugging concepts
