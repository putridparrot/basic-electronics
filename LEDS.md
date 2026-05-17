# LEDs (Light Emitting Diodes)

An LED is a diode that emits light when forward biased. LEDs are efficient, long-lived light sources used for indicators, displays, signaling, and illumination.

## Core Concept

- LED current determines brightness (within rated limits).
- LED forward voltage (`Vf`) depends on material, color, and current.
- LEDs require current limiting (resistor or constant-current driver).

Typical `Vf` ranges at nominal current:

- Red/amber: about `1.8 V` to `2.2 V`
- Green: about `2.0 V` to `3.2 V` (varies by chemistry)
- Blue/white: about `2.8 V` to `3.6 V`

## Key Parameters

- Forward voltage (`Vf`) at specific current
- Continuous forward current (`If`)
- Peak/pulse current rating
- Luminous intensity or flux (`mcd` / `lm`)
- Viewing angle
- Wavelength / CCT (for white LEDs)
- Thermal resistance and junction temperature limits

## Basic Resistor Calculation

For simple DC drive:

```
R = (Vsupply - Vf) / Iled
```

Resistor power:

```
Pres = Iled^2 x R
```

Example:

- `5 V` supply, red LED (`2.0 V`), target `10 mA`
- `R = (5 - 2) / 0.01 = 300 ohm`
- Choose standard `330 ohm` for margin.

## LED Wiring Topologies

## 1) Single LED + Series Resistor

- Easiest and most common for indicators

## 2) Multiple LEDs in Series

- Same current through each LED
- More efficient at higher supply voltages

## 3) Multiple LEDs in Parallel

- Use one resistor per LED branch for current sharing
- Avoid directly paralleling unmatched LEDs on a single resistor

## 4) Constant-Current Driver

- Best for power LEDs and consistent brightness
- Preferred over resistor-only drive in many lighting applications

## Dimming Methods

## 1) PWM Dimming

- Switch LED rapidly on/off while changing duty cycle
- Maintains color better than simple analog current reduction

Average LED current approximately scales with duty cycle.

## 2) Analog Current Dimming

- Adjust LED current directly
- Can shift color and reduce efficiency depending on LED type

## Indicator vs Power LEDs

Indicator LEDs:

- Typical current `1 mA` to `20 mA`
- Usually no heatsink needed

Power LEDs:

- Current can be hundreds of mA to amps
- Thermal design is critical (MCPCB, heatsink, airflow)

## Thermal Considerations

- LED performance and lifetime are strongly tied to junction temperature.
- As temperature rises, efficiency drops and long-term degradation accelerates.
- Keep thermal path low resistance using proper PCB copper/heatsinking.

## Common Applications

- Status indicators on boards
- Seven-segment and matrix displays
- Backlighting
- Illumination (white LEDs)
- Optocoupler emitters and infrared signaling

## Common Failure Modes

- Overcurrent causing thermal damage
- Reverse voltage overstress (many LEDs tolerate very little reverse voltage)
- Incorrect polarity
- Insufficient thermal management in power LED designs

## Measurement and Debug Tips

- Measure LED current in series or infer via resistor voltage (`I = V/R`).
- Check polarity: anode to positive through current limiter.
- Verify PWM frequency is high enough to avoid visible flicker in application.

## Safety Notes

- High-brightness LEDs can be uncomfortable or harmful to view directly.
- Blue/UV LEDs require additional eye-safety caution.

## Quick Reference

- Typical MCU indicator LED current: `2 mA` to `10 mA`
- Simple 5 V indicator resistor starting point:
	- Red LED: around `330 ohm`
	- Blue/white LED: around `220 ohm` to `330 ohm`

## Related Topics

- See DIODES.md for diode fundamentals.
- See RESISTORS.md for current-limiting resistor selection.
- See MICROCONTROLLERS.md for PWM control context.
