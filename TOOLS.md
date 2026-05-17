# Tools

This page covers the basic tools useful for getting a basic electronics project up and running — from measuring and debugging to building and soldering.

_Note: The tools are listed in no particular order apart from the last two which are more likely for those more advanced requirements._

---

## Breadboard

A **breadboard** is a reusable, solderless prototyping board that lets you build and test circuits quickly without any permanent connections.

- Rows of holes are internally connected in groups. Component legs and jumper wires simply push in and out.
- The two long rails running down each side are the **power rails** (typically connected to VCC and GND).
- Essential for experimenting — if something is wrong, you just rearrange the wires rather than desolder anything.

---

## Jumper Wires

Short wires used to connect components and pins on a breadboard or to headers on a microcontroller board.

- **Male–Male** — the most common; both ends are pins that push into breadboard holes.
- **Male–Female** — one pin end, one socket end; useful for connecting a breadboard to a GPIO header (e.g. Raspberry Pi Pico).
- **Female–Female** — both ends are sockets; used between header pins.

---

## Bench Power Supply

An adjustable DC power supply lets you set an exact voltage and current limit, making it much safer than a battery when developing circuits.

- Set the **current limit** low when testing a new circuit — if something is wired wrong the supply will current-limit rather than burning out a component.
- Ideal voltage ranges for hobby work: 0–30 V, 0–5 A covers almost everything.

---

## Multimeter

A **multimeter** (or DMM — Digital Multi Meter) is the single most useful tool on an electronics workbench. It can measure voltage, current, resistance, and often several other quantities, all in one handheld device.

### Anatomy of a Multimeter

- **Display** — shows the measured value.
- **Rotary dial** — selects the measurement mode and range.
- **COM port** — the common (negative / ground) probe socket; the black probe always goes here.
- **VΩmA port** — the positive probe socket for voltage, resistance, and small current measurements.
- **10 A port** — a separate socket (where present) for measuring large currents; always move the red probe here when measuring currents above ~200 mA.

> **Safety first:** Always check which socket the red probe is in before taking a measurement. Measuring voltage with the probe in the current socket will blow the meter's internal fuse or damage the circuit.

---

### Measuring Voltage (V)

1. Set the dial to **DC Voltage (V—)** for battery/circuit work, or **AC Voltage (V~)** for mains.
2. Select a range *higher* than the voltage you expect, or use auto-ranging if available.
3. Touch the **black probe to ground (negative)** and the **red probe to the point you want to measure**.
4. Read the display.

**Typical uses:**
- Checking a battery is at its rated voltage (e.g. a "9 V" battery below ~7 V is nearly flat).
- Confirming the output of a voltage regulator.
- Verifying that a GPIO pin is actually going HIGH (3.3 V or 5 V) or LOW (0 V).
- Tracing where voltage "disappears" in a faulty circuit.

---

### Measuring Resistance (Ω)

> **Power must be OFF.** Measuring resistance in a live circuit will damage the meter and give wrong readings.

1. Set the dial to **Resistance (Ω)**.
2. Touch the probes across the component (or the two points) you want to measure.
3. Read the display.

**Typical uses:**
- Confirming a resistor's value matches its colour bands.
- Checking a potentiometer sweeps smoothly from zero to its rated value.
- Checking for a short circuit (near 0 Ω) or open circuit (OL / overload).

---

### Continuity Test

Most meters have a **continuity / beep mode** (usually shares the resistance dial, indicated by a diode or sound-wave symbol).

- When resistance is very low (a good connection), the meter **beeps**.
- No beep means the path is broken.

**Typical uses:**
- Checking that a wire or PCB trace is not broken.
- Confirming a switch or relay contact opens and closes correctly.
- Verifying that solder joints are properly connected.
- Checking that two points that *should not* be connected are not shorted.

> Continuity mode is probably the most-used function when debugging circuits on a breadboard.

---

### Measuring Current (A)

Current measurement is different — the meter must be placed **in series** (in-line) with the circuit, not across it. This means you have to break the circuit and insert the meter into the break.

> Breaking an existing circuit to measure current can be disruptive; it is often easier to measure voltage across a known resistor and use Ohm's Law (`I = V / R`) to calculate current indirectly.

1. **Power OFF** the circuit.
2. Move the red probe to the **mA / µA socket** (or 10 A socket for large currents).
3. Set the dial to **DC Current (A— or mA)**.
4. Break the circuit at the point you want to measure and connect the meter in the gap (current flows through the meter).
5. **Power ON** and read the display.

**Typical uses:**
- Measuring how much current an LED circuit actually draws (to verify your resistor calculation).
- Checking the idle current of a battery-powered device.
- Confirming a motor or component is not drawing more than expected.

---

### Diode / LED Test

Most meters have a **diode test mode** (diode symbol: ▷|).

- Place the **red probe on the anode** and the **black probe on the cathode**.
- A good silicon diode will show ~0.5–0.7 V (its forward voltage drop).
- An LED will typically show 1.8–3.5 V and may glow faintly.
- A reading of **0 V** means the diode is shorted; **OL** means it is open (broken).
- Reversing the probes should give **OL** (no conduction in reverse) for a healthy diode.

---

### Quick Multimeter Reference

| Measurement | Dial Setting | Probe Placement | Power |
|---|---|---|---|
| Voltage (DC) | V— | Red to point, Black to GND | ON |
| Voltage (AC) | V~ | Red to point, Black to neutral | ON |
| Resistance | Ω | Across component | **OFF** |
| Continuity | ))) or diode | Across path | **OFF** |
| Current (small) | mA | In series (red in mA port) | ON |
| Current (large) | A | In series (red in 10 A port) | ON |
| Diode test | ▷| | Red to anode, Black to cathode | **OFF** |

---

## Soldering Iron

Once a circuit moves beyond the breadboard prototype stage, soldering is needed to make permanent connections.

- **Temperature-controlled stations** (e.g. Hakko FX-888D, TS100/TS80 portable irons) are far better than cheap fixed-temperature irons.
- Typical soldering temperature for electronics: **320–380 °C** depending on solder type.
- **Lead-free solder** (e.g. Sn99/Ag0.3/Cu0.7) is the modern standard; requires slightly higher temperatures than leaded solder.
- Use **flux** to clean the joint and improve solder flow, and **solder wick** or a **solder sucker** to remove mistakes.

---

## Wire Strippers and Cutters

- **Wire strippers** remove insulation cleanly without nicking the conductor.
- **Side cutters (flush cutters)** trim component leads close to the PCB after soldering.
- **Long-nose (needle-nose) pliers** help bend component leads and hold small parts.

---

## Helping Hands / PCB Vice

Holds the PCB or component still while you solder — essential for anything beyond the simplest connections. A small bench vice or a "helping hands" stand with crocodile clips works well.

---

## Logic Analyser

A logic analyser captures and displays digital signals over time, making it invaluable for debugging serial communication (UART, SPI, I²C, PWM).

- Budget USB options (e.g. the 8-channel Saleae clone) work well with the open-source **PulseView / sigrok** software.
- Can decode protocols automatically — you can see human-readable bytes being sent over I²C or UART without manually counting bits.
- Ideal when a multimeter just shows "something is toggling" but you need to see exactly what.

---

## Oscilloscope

_Note: This one is not essential for most basic electronics projects, but it can still be very useful._

An oscilloscope plots voltage over time as a waveform on a screen. It shows you what is actually happening in an analogue or digital signal.

- **Bandwidth** — the highest frequency it can accurately display. 50–100 MHz covers most hobby needs.
- Budget digital oscilloscopes (e.g. Rigol DS1054Z, Fnirsi) are reasonably affordable and very capable.
- Use it to: measure signal frequency and duty cycle, check for noise/ripple on a power supply, debug PWM signals, visualise audio waveforms.
- A logic analyser is better for decoding digital protocols; an oscilloscope is better for analogue signal shapes.

---

## Worked Example: Debugging a Non-Blinking LED Circuit

Scenario: an LED connected to a microcontroller pin does not blink as expected.

Step-by-step workflow:

1. Multimeter (voltage mode): confirm board supply rail is present.
2. Multimeter (continuity mode, power off): confirm LED resistor path is connected and not shorted.
3. Diode mode (power off): verify LED polarity and health.
4. Multimeter (voltage mode, running): check GPIO pin swings between LOW and HIGH.
5. Oscilloscope (if needed): confirm actual waveform timing and duty cycle.

Typical root causes found:

- LED installed backwards
- Wrong resistor value
- GPIO configured as input instead of output
- Missing ground reference between modules

## Related Topics

- See LEDS.md for LED resistor sizing.
- See RESISTORS.md for resistor verification and values.
- See MICROCONTROLLERS.md for GPIO and PWM behavior.
