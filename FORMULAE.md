# Useful Formulae

A reference for the most common formulae in basic electronics, with use cases and worked examples.

---

## Quick Reference

| Formula | Use |
|---|---|
| $V = IR$ | Ohm's Law — voltage, current, resistance |
| $P = VI$ | Power dissipation |
| $R_s = R_1 + R_2$ | Series resistance |
| $R_p = (R_1 R_2)/(R_1+R_2)$ | Parallel resistance (two) |
| $V_{out} = V_{in} \cdot R_2/(R_1+R_2)$ | Voltage divider |
| $\tau = RC$ | RC time constant |
| $Q = CV$ | Capacitor charge |
| $f_0 = 1/(2\pi\sqrt{LC})$ | LC resonant frequency |
| $R = (V_s - V_f)/I_f$ | LED resistor |
| $\text{dB} = 20\log(V_{out}/V_{in})$ | Voltage gain in decibels |
| $V_{avg} = V_s \times D$ | PWM average voltage |

---

## Ohm's Law

$$V = I \times R$$

| Solve for | Formula |
|---|---|
| Voltage | $V = I \times R$ |
| Current | $I = V / R$ |
| Resistance | $R = V / I$ |

**When to use it:** Any time you need to relate voltage, current, and resistance in a resistive circuit.

**Example — finding current through an LED resistor:**
A 5 V supply, 220 Ω resistor. How much current flows?

$$I = V / R = 5 / 220 \approx 22.7 \text{ mA}$$

**Example — choosing a resistor for an LED:**
Supply = 5 V, LED forward voltage = 2 V, desired current = 20 mA.
Voltage across resistor = 5 − 2 = 3 V.

$$R = V / I = 3 / 0.020 = 150 \text{ Ω} \quad \text{(use 150 Ω or next standard value up)}$$

---

## Power

$$P = V \times I$$

| Solve for | Formula |
|---|---|
| Power | $P = V \times I$ |
| Power (from V & R) | $P = V^2 / R$ |
| Power (from I & R) | $P = I^2 \times R$ |

**When to use it:** Checking whether a component (resistor, transistor, regulator) will overheat; sizing power supplies.

**Example — resistor power rating:**
A 100 Ω resistor carries 50 mA.

$$P = I^2 \times R = (0.05)^2 \times 100 = 0.25 \text{ W}$$

Use at least a 0.5 W rated resistor (double the calculated dissipation is a safe rule of thumb).

**Example — supply current from power and voltage:**
An LED strip consumes 12 W at 12 V.

$$I = P / V = 12 / 12 = 1 \text{ A}$$

---

## Series Resistance

$$R_{total} = R_1 + R_2 + R_3 + \ldots$$

**When to use it:** Components chained end-to-end; the same current flows through all of them.

**Example:**
Three resistors: 100 Ω, 220 Ω, 470 Ω in series.

$$R_{total} = 100 + 220 + 470 = 790 \text{ Ω}$$

---

## Parallel Resistance

$$\frac{1}{R_{total}} = \frac{1}{R_1} + \frac{1}{R_2} + \frac{1}{R_3} + \ldots$$

For **two resistors** only, the product-over-sum shortcut applies:

$$R_{total} = \frac{R_1 \times R_2}{R_1 + R_2}$$

**When to use it:** Components sharing the same two nodes; they all see the same voltage but share the current.

**Example:**
Two resistors: 1 kΩ and 1 kΩ in parallel.

$$R_{total} = \frac{1000 \times 1000}{1000 + 1000} = 500 \text{ Ω}$$

**Example — three resistors:**
470 Ω, 1 kΩ, 2.2 kΩ in parallel.

$$\frac{1}{R_{total}} = \frac{1}{470} + \frac{1}{1000} + \frac{1}{2200} \approx 0.002128 + 0.001 + 0.000455 = 0.003583$$

$$R_{total} \approx 279 \text{ Ω}$$

---

## Voltage Divider

$$V_{out} = V_{in} \times \frac{R_2}{R_1 + R_2}$$

Where $R_2$ is the lower resistor (connected to ground) and $R_1$ is the upper resistor.

**When to use it:** Scaling a voltage down — e.g. feeding a 5 V signal into a 3.3 V ADC pin, or reading a potentiometer.

**Example:**
$V_{in}$ = 5 V, $R_1$ = 10 kΩ, $R_2$ = 10 kΩ.

$$V_{out} = 5 \times \frac{10000}{10000 + 10000} = 2.5 \text{ V}$$

**Example — level shifting 5 V → 3.3 V:**
Use $R_1$ = 2.2 kΩ, $R_2$ = 3.3 kΩ.

$$V_{out} = 5 \times \frac{3300}{2200 + 3300} = 5 \times 0.6 = 3.0 \text{ V} \quad \text{(close enough for most ADC inputs)}$$

---

## Capacitance — Charge Stored

$$Q = C \times V$$

| Symbol | Meaning | Unit |
|---|---|---|
| $Q$ | Charge | Coulombs (C) |
| $C$ | Capacitance | Farads (F) |
| $V$ | Voltage | Volts (V) |

**When to use it:** Estimating how long a capacitor can sustain a load, or how much charge is released during a pulse.

**Example:**
A 100 µF capacitor charged to 5 V.

$$Q = 100 \times 10^{-6} \times 5 = 500 \text{ µC}$$

---

## RC Time Constant

$$\tau = R \times C$$

- After **1τ** the capacitor has charged to ~63% of supply voltage.
- After **5τ** it is considered fully charged (~99%).

**When to use it:** Designing filters, debounce circuits, timing delays, and smoothing supplies.

**Example:**
R = 10 kΩ, C = 100 µF.

$$\tau = 10{,}000 \times 100 \times 10^{-6} = 1 \text{ s}$$

The capacitor reaches ~63% charge in 1 second and is essentially full in 5 seconds.

---

## Capacitors in Series and Parallel

**Series** (total capacitance *decreases*):

$$\frac{1}{C_{total}} = \frac{1}{C_1} + \frac{1}{C_2} + \ldots$$

**Parallel** (total capacitance *adds*):

$$C_{total} = C_1 + C_2 + \ldots$$

**When to use it:** Series is rarely intentional (except to share voltage); parallel capacitors are stacked to increase total capacitance or combine different types (e.g. bulk electrolytic + ceramic bypass cap).

---

## Inductors in Series and Parallel

**Series:**

$$L_{total} = L_1 + L_2 + \ldots$$

**Parallel:**

$$\frac{1}{L_{total}} = \frac{1}{L_1} + \frac{1}{L_2} + \ldots$$

(Same pattern as resistance, assuming no mutual inductance between coils.)

---

## Resonant Frequency (LC Circuit)

$$f_0 = \frac{1}{2\pi\sqrt{LC}}$$

| Symbol | Meaning | Unit |
|---|---|---|
| $f_0$ | Resonant frequency | Hertz (Hz) |
| $L$ | Inductance | Henrys (H) |
| $C$ | Capacitance | Farads (F) |

**When to use it:** Designing or analysing filters, oscillators, and RF circuits.

**Example:**
L = 10 mH, C = 10 µF.

$$f_0 = \frac{1}{2\pi\sqrt{0.01 \times 10 \times 10^{-6}}} = \frac{1}{2\pi\sqrt{10^{-7}}} \approx \frac{1}{2\pi \times 3.16 \times 10^{-4}} \approx 503 \text{ Hz}$$

---

## LED Current-Limiting Resistor

$$R = \frac{V_{supply} - V_f}{I_f}$$

| Symbol | Meaning | Typical value |
|---|---|---|
| $V_{supply}$ | Supply voltage | 3.3 V, 5 V |
| $V_f$ | LED forward voltage | ~2 V (red), ~3.2 V (blue/white) |
| $I_f$ | Desired LED current | 10–20 mA |

**Example:**
5 V supply, red LED ($V_f$ = 2 V), target current 15 mA.

$$R = \frac{5 - 2}{0.015} = \frac{3}{0.015} = 200 \text{ Ω} \quad \text{(use 220 Ω)}$$

---

## Decibels (dB)

$$\text{dB} = 20 \log_{10}\!\left(\frac{V_{out}}{V_{in}}\right) \quad \text{(voltage ratio)}$$

$$\text{dB} = 10 \log_{10}\!\left(\frac{P_{out}}{P_{in}}\right) \quad \text{(power ratio)}$$

**When to use it:** Expressing amplifier gain, filter attenuation, or signal levels.

**Common reference points:**

| dB | Voltage ratio | Power ratio | Meaning |
|---|---|---|---|
| 0 | 1× | 1× | No change |
| +6 | ~2× | ~4× | Double the voltage |
| +20 | 10× | 100× | Ten times the voltage |
| −3 | ~0.707× | 0.5× | Half power (filter cut-off point) |
| −20 | 0.1× | 0.01× | One tenth the voltage |

---

## PWM Duty Cycle

$$\text{Duty cycle} = \frac{t_{on}}{T} \times 100\%$$

Where $T = t_{on} + t_{off}$ is the total period.

**Average output voltage:**

$$V_{avg} = V_{supply} \times \frac{\text{Duty cycle}}{100}$$

**When to use it:** Calculating the effective voltage delivered to an LED (brightness), motor (speed), or servo.

**Example:**
5 V supply, 75% duty cycle.

$$V_{avg} = 5 \times 0.75 = 3.75 \text{ V}$$
