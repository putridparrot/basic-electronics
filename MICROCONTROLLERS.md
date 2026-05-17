# Microcontrollers

## What is a Microcontroller?

A **microcontroller (MCU)** is a compact integrated circuit that contains a processor (CPU), memory (both program flash and working RAM), and programmable input/output peripherals — all on a single chip. Think of it as a tiny, self-contained computer designed to run one dedicated program and interact with the physical world.

Compared to a full computer or single-board computer (SBC) like a Raspberry Pi:

| | Microcontroller | SBC (e.g. Raspberry Pi) |
|---|---|---|
| OS | Bare metal (no OS, or RTOS) | Full Linux OS |
| Boot time | Instant (microseconds) | Seconds |
| Power use | Very low (mA or µA) | Higher (hundreds of mA) |
| Best for | Real-time control, sensors, low power | Complex software, networking, display |

Key peripheral types built into most microcontrollers:

- **GPIO (General Purpose Input/Output)** — digital pins you can set HIGH/LOW or read as a button/sensor input.
- **ADC (Analogue-to-Digital Converter)** — reads analogue voltages (e.g. from a potentiometer or sensor) and converts them to a number.
- **PWM (Pulse Width Modulation)** — rapidly switches a pin on and off to simulate a variable voltage; used to dim LEDs or control motors.
- **UART / SPI / I²C** — serial communication interfaces for talking to other chips and modules.
- **Timers / Interrupts** — let the MCU react to events precisely without constantly checking ("polling") a pin.

---

## Popular Microcontrollers

### Arduino Uno (ATmega328P)
- **Core:** 8-bit AVR @ 16 MHz
- **Flash / RAM:** 32 KB / 2 KB
- **I/O:** 14 digital pins (6 PWM), 6 analogue inputs
- **Voltage:** 5 V logic
- The classic beginner board. Huge community, libraries for almost every sensor and module imaginable. Programmed in C/C++ via the Arduino IDE.
- Ideal for: learning, simple sensors, driving servos and LEDs.

### Arduino Nano
- Essentially an Uno shrunk to a small DIP-style board; fits directly on a breadboard. Same ATmega328P chip.
- Ideal for: compact projects where a full Uno is too large.

### Arduino Mega 2560
- **Core:** 8-bit AVR @ 16 MHz
- **I/O:** 54 digital pins (15 PWM), 16 analogue inputs
- More pins and more memory than the Uno. Used when a project outgrows the Uno.
- Ideal for: larger projects with many sensors, motors, or displays.

### ESP8266 (e.g. NodeMCU, Wemos D1 Mini)
- **Core:** 32-bit Xtensa @ 80/160 MHz
- **Flash / RAM:** 1–4 MB / ~80 KB
- **Connectivity:** Wi-Fi built in
- **Voltage:** 3.3 V logic
- Cheap and capable Wi-Fi MCU. Can be programmed via the Arduino IDE or with MicroPython. The low cost made it enormously popular for IoT projects.
- Ideal for: Wi-Fi connected sensors, home automation, simple web servers.

### ESP32 (e.g. ESP32-DevKitC, ESP32-WROOM)
- **Core:** Dual-core 32-bit Xtensa @ up to 240 MHz
- **Flash / RAM:** 4 MB+ / 520 KB
- **Connectivity:** Wi-Fi + Bluetooth (Classic & BLE) built in
- **Voltage:** 3.3 V logic
- The spiritual successor to the ESP8266 — significantly more powerful. Has more GPIO, touch inputs, a DAC, hall-effect sensor, and hardware encryption. Variants like the ESP32-S3 add USB OTG and AI acceleration.
- Ideal for: IoT devices, Bluetooth sensors, audio, camera projects (ESP32-CAM).

### Raspberry Pi Pico / Pico W (RP2040)
- **Core:** Dual-core ARM Cortex-M0+ @ 133 MHz
- **Flash / RAM:** 2 MB / 264 KB
- **Connectivity:** Pico W adds Wi-Fi + BLE (CYW43439 chip)
- **Voltage:** 3.3 V logic
- Designed by the Raspberry Pi Foundation. Programmed with MicroPython or C/C++. The RP2040 has a unique "PIO" (Programmable I/O) system that can emulate custom serial protocols in hardware.
- Ideal for: learning MicroPython, USB HID devices, precise timing/PIO tasks.

### STM32 (e.g. STM32F103 "Blue Pill", Nucleo boards)
- **Core:** 32-bit ARM Cortex-M (M0 to M7 depending on variant) @ 48–480 MHz
- Professional-grade MCUs with a wide range of peripherals. Steeper learning curve but very capable. Often used in commercial products.
- Ideal for: advanced projects, motor control, DSP, USB.

### ATtiny (e.g. ATtiny85)
- **Core:** 8-bit AVR (same family as the Uno's ATmega328P) but in a tiny 8-pin package.
- Minimal flash and RAM, very few pins — but extremely small and cheap.
- Can be programmed via an Arduino acting as an ISP programmer.
- Ideal for: embedding a tiny bit of intelligence inside a small product or where space is critical.

---

## Worked Example: Choosing an MCU

Goal: choose a controller for a battery-powered sensor node that needs Wi-Fi and deep sleep.

Requirements:

- Wi-Fi connectivity
- Low sleep current
- Small board size
- Enough GPIO for a sensor and status LED

Reasoning:

- Arduino Uno/Nano: simple, but no native Wi-Fi and less suited to low-power IoT.
- ESP8266: has Wi-Fi and low cost; suitable for simple connected sensors.
- ESP32: adds more features (BLE, more GPIO, dual-core), useful if future expansion is likely.

Practical decision:

- Start with `ESP8266` for minimal cost/complexity.
- Choose `ESP32` if you need BLE, more peripherals, or more processing headroom.

## Related Topics

- See POWERSOURCE.md for battery and regulator planning.
- See CRYSTALSOSCILLATORS.md for timing source considerations.
- See TOOLS.md for debugging hardware interfaces.
