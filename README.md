# Basic Electronics

I'm trying to learn (well partly re-learn) about electronics, with the capabilities of microcontrollers such as the Arduino's, ESP32, and Raspberry Pi's (such as the Pico) there's so many oppurtunites for controller electronic devices or getting information from them.

---

## How a Circuit Works

A **circuit** is simply a closed loop that allows electric current to flow from a power source, through one or more components, and back to the source. If the loop is broken at any point, current stops flowing — that's the basis of a switch.

### Key Concepts

| Concept | Symbol | Unit | Plain English |
|---|---|---|---|
| **Voltage** (V) | V | Volt (V) | The "pressure" pushing electrons around the circuit |
| **Current** (I) | I | Ampere / Amp (A) | The amount of electrons actually flowing |
| **Resistance** (R) | R | Ohm (Ω) | How much a component fights against the flow |
| **Power** (P) | P | Watt (W) | The rate at which energy is used |

### Ohm's Law

The single most important relationship in electronics:

```
V = I × R
```

- If you know any two of Voltage, Current, or Resistance, you can calculate the third.
- Example: a 9 V battery driving current through a 470 Ω resistor will allow `I = V / R = 9 / 470 ≈ 19 mA` of current to flow.

### Series vs Parallel

**Series** — components are chained end-to-end. The same current flows through all of them, but voltage is shared (divided) across them.

**Parallel** — components share the same two connection points. They all see the same voltage, but the total current is split between them.

---

## Basic Components

Let's look at a few of the really core components used in electronics projects.

---

## Quick Reference — Schematic Symbols

| Component | Key Feature |
|---|---|
| Resistor | Limits current |
| Capacitor | Stores charge; blocks DC |
| Inductor | Stores energy in magnetic field; blocks AC |
| Diode | One-way current valve |
| LED | Light-emitting diode; needs series resistor |
| NPN Transistor | Small Base current switches large Collector current |
| MOSFET | Gate voltage controls Drain-Source channel |
| Switch | Opens/closes circuit mechanically |
| Relay | Electrically operated switch; isolates circuits |
| IC | Complete circuit on a chip |

---

### Power Source

The power source provides the energy (voltage and current) that drives the circuit. Common examples:

- **Battery** — a self-contained chemical energy store. AA, 9 V PP3, LiPo packs, etc.
- **USB power supply** — provides 5 V DC, the standard for most microcontroller boards.
- **Bench power supply** — an adjustable lab supply useful for development and testing.
- **Voltage regulator** — not a source itself, but converts one voltage to a stable lower one (e.g. 12 V → 5 V). The classic 7805 regulator or modern LDO regulators are common examples.

> The two key ratings of any source are its **voltage** (e.g. 5 V) and maximum **current** it can deliver (e.g. 2 A).

---

### Resistors

A resistor limits (resists) the flow of current. It is one of the most common components in any circuit.

- **Unit:** Ohm (Ω). Larger values are expressed in kΩ (1,000 Ω) or MΩ (1,000,000 Ω).
- **Symbol:** a rectangle (IEC) or a zigzag line (ANSI).
- **Colour bands** on the body encode the resistance value.

**Common uses:**
- Protecting LEDs by limiting current (a "current-limiting resistor").
- Setting signal levels or bias points.
- Pull-up / pull-down resistors to keep a digital pin at a known state (HIGH or LOW) when nothing else is driving it.

**Types:**
- *Fixed resistor* — the most common; value does not change.
- *Potentiometer (pot)* — a variable resistor with a knob or slider; used for volume controls, brightness dimmers, etc.
- *LDR (Light Dependent Resistor)* — resistance decreases as light increases; useful for light sensors.
- *Thermistor* — resistance changes with temperature; useful for temperature sensing.

---

### Capacitors

A capacitor stores electrical charge (energy) temporarily in an electric field between two conductive plates separated by an insulator.

- **Unit:** Farad (F). In practice most capacitors are measured in microfarads (µF), nanofarads (nF), or picofarads (pF).
- Think of it like a very small, fast-charging/discharging rechargeable battery.

**Common uses:**
- **Smoothing / filtering** — placed across a power supply to smooth out ripple (voltage spikes and dips).
- **Decoupling** — placed close to an IC to provide a local reservoir of charge, preventing noise on the supply rail.
- **Timing circuits** — combined with a resistor (RC circuit), the charge/discharge time can be used to create delays or oscillators.
- **Signal coupling / blocking DC** — passes AC signals while blocking DC.

**Types:**
- *Ceramic* — small, cheap, non-polarised; good for decoupling (typical values: pF to low µF).
- *Electrolytic* — larger values (µF to mF); **polarised** — the `+` leg must connect to the higher voltage or the capacitor can be damaged.
- *Tantalum* — polarised, compact, stable; common in precision circuits.
- *Film* — non-polarised, stable and low-loss; used in audio and timing circuits.

---

### Inductors

An inductor stores energy in a magnetic field when current flows through a coil of wire. It is the counterpart to the capacitor.

- **Unit:** Henry (H). In practice, millihenry (mH) and microhenry (µH) are most common.
- An inductor **resists changes in current** — it tries to keep current flowing at the same level.

**Common uses:**
- **Filtering** — blocks high-frequency signals (noise) while passing DC or low-frequency signals.
- **Switching power supplies (boost/buck converters)** — the inductor is the energy storage element that allows voltage to be stepped up or down efficiently.
- **RF tuning circuits** — combined with a capacitor to form a resonant "tank" circuit tuned to a specific frequency.

---

### Diodes

A diode is a one-way gate for current — it allows current to flow in one direction only (from **anode** to **cathode**). In the other direction it blocks current (until the reverse voltage is high enough to cause breakdown).

- **Symbol:** an arrow pointing in the direction of allowed current flow, with a bar at the cathode end.
- A small forward voltage drop is required for the diode to conduct: ~0.6–0.7 V for silicon, ~0.3 V for Schottky diodes.

**Common uses:**
- **Rectification** — converting AC to DC (four diodes arranged as a bridge rectifier).
- **Protection** — a "flyback" diode placed across a relay coil or motor to absorb the voltage spike when inductive loads are switched off.
- **Reverse polarity protection** — placed in series to prevent damage if power is connected the wrong way.

**Types:**
- *Signal diode (e.g. 1N4148)* — small and fast; used for signal clamping and logic circuits.
- *Rectifier diode (e.g. 1N4001–1N4007)* — handles higher currents; used in power supplies.
- *Schottky diode* — very low forward voltage drop (~0.3 V) and fast switching; used in switching power supplies.
- *Zener diode* — designed to conduct in reverse at a specific "zener voltage"; used as a voltage reference or simple voltage regulator.
- *LED (Light Emitting Diode)* — see below.

---

### LEDs (Light Emitting Diodes)

An LED is a diode that emits light when current flows through it. It is polarised — the longer leg is the **anode (+)** and the shorter leg (with a flat on the body) is the **cathode (−)**.

- **Always use a current-limiting resistor** in series with an LED, or it will burn out instantly.
- Typical forward voltage: ~2 V (red/yellow) to ~3.5 V (blue/white).
- Typical operating current: 10–20 mA for standard LEDs.

To calculate the series resistor value:
```
R = (Supply Voltage − LED Forward Voltage) / Desired Current

Example (5 V supply, red LED, 15 mA): R = (5 − 2.0) / 0.015 = 200 Ω → use 220 Ω (nearest standard value)
```

---

### Transistors

A transistor is a semiconductor device that acts as either a **switch** or an **amplifier**. It is the fundamental building block of modern electronics — billions of them exist inside every microcontroller or processor.

The two most common types are:

#### BJT (Bipolar Junction Transistor)

Has three legs: **Base (B)**, **Collector (C)**, and **Emitter (E)**.

- A small current into the Base controls a much larger current flowing from Collector to Emitter.
- **NPN type** (most common): current flows Collector → Emitter when the Base is driven HIGH.
- **PNP type**: current flows Emitter → Collector when the Base is driven LOW.
- As a switch: the transistor is either fully ON (saturated) or fully OFF.
- As an amplifier: the output current is proportional to the Base current, multiplied by the transistor's gain (hFE or β).

Common examples: BC547 (NPN), BC557 (PNP), 2N2222 (NPN).

#### MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor)

Has three legs: **Gate (G)**, **Drain (D)**, and **Source (S)**.

- The voltage on the Gate controls the current flowing from Drain to Source — almost no current is drawn by the Gate itself.
- **N-channel** (most common): conducts when Gate voltage is HIGH relative to Source.
- **P-channel**: conducts when Gate voltage is LOW relative to Source.
- Preferred over BJTs for switching larger loads (motors, lights) because they are more efficient (lower "on" resistance).
- Logic-level MOSFETs (e.g. IRLZ44N) can be driven directly from a 3.3 V or 5 V microcontroller pin.

---

### Switches and Buttons

A switch physically opens or closes a circuit.

- **SPST (Single Pole Single Throw)** — the simplest on/off switch.
- **SPDT (Single Pole Double Throw)** — connects one input to one of two outputs; useful for selecting between two states.
- **Momentary push button** — only closed while held down; the type used on breadboards for reset buttons, etc.
- **Toggle switch** — stays in its last position.

When reading a button with a microcontroller, always use a **pull-up or pull-down resistor** (or enable the internal one) to ensure the pin reads a definite HIGH or LOW when the button is open.

---

### Relays

A relay is an electrically operated switch. A small control current (through an electromagnet coil) switches a separate, mechanically isolated contact that can handle a much larger current.

- Lets a low-voltage/low-current circuit (e.g. a microcontroller GPIO pin) safely switch mains voltage or high-current loads.
- Always place a **flyback diode** across the coil to suppress the voltage spike when the relay is turned off.
- Solid-state relays (SSRs) do the same job using semiconductors — they are silent, faster, and longer-lasting than mechanical relays.

---

### Integrated Circuits (ICs)

An IC is a complete circuit — potentially containing millions of components — etched onto a single piece of semiconductor. They are the workhorses of modern electronics.

**Common categories:**
- *Logic gates (e.g. 74HC series)* — AND, OR, NOT, NAND, NOR, XOR gates; the building blocks of digital logic.
- *555 Timer* — a versatile IC used to create timing delays and oscillators (astable / monostable modes).
- *Op-Amp (Operational Amplifier, e.g. LM358, TL071)* — a high-gain differential amplifier used for signal conditioning, filtering, and comparison.
- *Voltage Regulators (e.g. 7805, LM317)* — produce a stable output voltage from a higher input.
- *Microcontrollers (e.g. ATmega328 on Arduino, RP2040 on Pico)* — a CPU, memory, and I/O all in one chip; the brains of most hobby electronics projects.

---

### Crystals and Oscillators

Many digital circuits need a precise timing reference.

- A **quartz crystal** vibrates at a very precise frequency when voltage is applied, providing an accurate clock source for microcontrollers, real-time clocks (RTCs), and communication interfaces.
- A **ceramic resonator** is a cheaper, slightly less accurate alternative.
- Many modern microcontrollers include an internal oscillator so an external crystal is optional.


---

## Microcontrollers

See the dedicated [Microcontrollers](MICROCONTROLLERS.md) page for an overview of what a microcontroller is, a run-through of popular boards (Arduino, ESP32, Raspberry Pi Pico, STM32, and more), and a guide to choosing the right one for your project.

---

## Tools

Getting a project off the ground requires more than just components. See the dedicated [Tools](TOOLS.md) page for a run-through of the essential equipment — including breadboards, power supplies, multimeters, logic analysers, oscilloscopes, and soldering gear.