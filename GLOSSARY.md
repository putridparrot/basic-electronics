# Acronyms and Terms

This page is a quick reference for common acronyms and names used in electronics and embedded systems.

## Core Embedded Terms

| Term | Full Name | Brief Description |
|---|---|---|
| MCU | Microcontroller Unit | A small computer-on-a-chip with CPU, memory, and peripherals for control tasks. |
| MPU | Microprocessor Unit | CPU-focused chip that usually needs external RAM, storage, and peripherals. |
| SoC | System on Chip | Integrates CPU, memory interfaces, and peripherals into one chip. |
| SBC | Single-Board Computer | Complete computer on one board (for example Raspberry Pi), usually running Linux. |
| RTOS | Real-Time Operating System | OS designed to respond to events within predictable timing limits. |
| Bare metal | (No acronym) | Firmware running directly on hardware without an operating system. |
| Firmware | (No acronym) | Low-level software programmed into a device's non-volatile memory. |
| Bootloader | (No acronym) | Small program that starts firmware and often supports flashing updates. |

## Memory and Storage

| Term | Full Name | Brief Description |
|---|---|---|
| RAM | Random Access Memory | Volatile working memory used while code is running. |
| SRAM | Static Random Access Memory | Fast RAM that does not need refresh cycles; common inside MCUs. |
| DRAM | Dynamic Random Access Memory | Dense RAM that needs refresh; common in larger systems. |
| ROM | Read-Only Memory | Non-volatile memory traditionally used for fixed data/code. |
| Flash | Flash Memory | Rewritable non-volatile memory used for firmware storage. |
| EEPROM | Electrically Erasable Programmable Read-Only Memory | Non-volatile memory for small data that needs occasional updates. |

## Communication Protocols

| Term | Full Name | Brief Description |
|---|---|---|
| UART | Universal Asynchronous Receiver/Transmitter | Serial communication interface using TX/RX lines. |
| I2C | Inter-Integrated Circuit | Two-wire bus (SDA/SCL) for multiple chips on one board. |
| SPI | Serial Peripheral Interface | High-speed synchronous serial bus using clock and separate data lines. |
| CAN | Controller Area Network | Robust differential bus commonly used in automotive and industrial systems. |
| USB | Universal Serial Bus | Standard interface for data, power delivery, and device connectivity. |
| BLE | Bluetooth Low Energy | Low-power wireless protocol for short-range communication. |

## Power and Signal Terms

| Term | Full Name | Brief Description |
|---|---|---|
| GPIO | General Purpose Input/Output | Configurable digital pins used for input or output. |
| ADC | Analogue-to-Digital Converter | Converts an analogue voltage into a digital value. |
| DAC | Digital-to-Analogue Converter | Converts a digital value into an analogue voltage/current output. |
| PWM | Pulse Width Modulation | Controls average power by changing pulse duty cycle. |
| VCC | Voltage at Common Collector | Positive supply rail label used in many schematics. |
| GND | Ground | Reference node for voltages and current return path. |
| LDO | Low Dropout Regulator | Linear regulator that works with a small input-to-output voltage difference. |
| SMPS | Switched-Mode Power Supply | Efficient power converter using high-frequency switching. |

## Timing and Reliability

| Term | Full Name | Brief Description |
|---|---|---|
| PLL | Phase-Locked Loop | Circuit that locks one clock/signal to another frequency reference. |
| RTC | Real-Time Clock | Low-power clock/calendar block that keeps time when main power is off. |
| EMI | Electromagnetic Interference | Unwanted electromagnetic noise that can affect circuit operation. |
| ESD | Electrostatic Discharge | Sudden static electricity discharge that can damage components. |
| TVS | Transient Voltage Suppressor | Device used to clamp short voltage spikes for protection. |

## Exam-Focused Extras

| Term | Full Name | Brief Description |
|---|---|---|
| PID | Proportional-Integral-Derivative | Feedback control method that combines present, accumulated, and rate-of-change error terms. |
| ESR | Equivalent Series Resistance | Internal series resistance of a capacitor that causes loss and ripple heating. |
| PSRR | Power Supply Rejection Ratio | How well a circuit (often an op-amp/regulator) rejects supply voltage noise. |
| SNR | Signal-to-Noise Ratio | Ratio of wanted signal power to unwanted noise power. |
| THD | Total Harmonic Distortion | Measure of harmonic distortion content relative to the fundamental signal. |
| CMRR | Common-Mode Rejection Ratio | Ability of a differential amplifier/op-amp to reject common-mode signals. |
| Nyquist rate | (No acronym) | Minimum sampling rate of at least twice the highest input frequency component. |
| Bode plot | (No acronym) | Frequency response plot showing gain and phase versus frequency. |
| Vgs(th) | MOSFET Gate Threshold Voltage | Gate-source voltage where a MOSFET just begins to conduct (not fully on). |
| Rds(on) | MOSFET On-Resistance | Drain-source resistance when MOSFET is on; drives conduction loss. |
| Qg | MOSFET Total Gate Charge | Charge needed to drive the MOSFET gate; affects switching speed and drive current. |

## Quick A-Z Index

- A: ADC
- B: BLE, Bootloader, Bode plot
- C: CAN, CMRR
- D: DAC, DRAM
- E: EEPROM, EMI, ESD, ESR
- F: Firmware, Flash
- G: GND, GPIO
- I: I2C
- L: LDO
- M: MCU, MPU
- N: Nyquist rate
- P: PID, PLL, PSRR, PWM
- Q: Qg
- R: RAM, Rds(on), ROM, RTC, RTOS
- S: SBC, SMPS, SNR, SoC, SPI, SRAM
- T: THD, TVS
- U: UART, USB
- V: VCC, Vgs(th)

## Related Topics

- See [Microcontrollers](MICROCONTROLLERS.md) for platform choices and board families.
- See [ICs](IC.md) for integrated circuit categories and selection checks.
- See [Tools](TOOLS.md) for measurement and debugging workflows.
