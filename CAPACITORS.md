# Capacitors

Capacitors store electrical energy in an electric field. They are used for filtering, timing, coupling/decoupling, energy storage, snubbing, and frequency selection.

## Core Concept

A capacitor has two conductive plates separated by a dielectric (insulator).

- Charge-voltage relationship: $Q = C \cdot V$
- Current-voltage relationship: $I = C \cdot \frac{dV}{dt}$
- Energy stored: $E = \frac{1}{2} C V^2$

Where:

- $Q$ = charge (coulombs)
- $C$ = capacitance (farads)
- $V$ = voltage (volts)
- $I$ = current (amps)

## Units and Common Values

- 1 F (farad) is very large in most electronics.
- Typical values:
	- pF (picofarad) = $10^{-12}$ F
	- nF (nanofarad) = $10^{-9}$ F
	- uF (microfarad) = $10^{-6}$ F
	- mF (millifarad) = $10^{-3}$ F

Common practical ranges:

- RF tuning: 1 pF to 100 pF
- General signal coupling: 1 nF to 1 uF
- Decoupling/bypass: 100 nF (very common), plus 1 uF to 10 uF nearby
- Power smoothing/bulk: 10 uF to 4700 uF+

## Important Real-World Parameters

Real capacitors are non-ideal.

- Tolerance: e.g. +/-1%, +/-5%, +/-10%, +/-20%
- Rated voltage: maximum continuous voltage (never exceed)
- ESR (equivalent series resistance): causes heat/ripple losses
- ESL (equivalent series inductance): limits high-frequency behavior
- Leakage current: small DC current through dielectric
- Temperature coefficient: capacitance drift with temperature
- Dielectric absorption: capacitor "memory" effect after discharge
- Lifetime (especially electrolytic): usually given in hours at temperature and ripple conditions

## Major Capacitor Types

## 1) Ceramic (MLCC)

- Typical range: pF to tens/hundreds of uF (value depends on package/voltage)
- Usually non-polarized
- Low ESR/ESL, excellent for high-frequency decoupling
- Dielectric classes:
	- C0G/NP0: very stable, low loss, small capacitance values
	- X7R/X5R: higher capacitance, moderate stability
	- Y5V/Z5U: high variation, less precision
- Limitation: DC bias can significantly reduce effective capacitance (especially X5R/X7R at high electric field)

Best use:

- Fast bypass near IC power pins
- RF/oscillator (C0G/NP0)

## 2) Aluminum Electrolytic

- Typical range: 1 uF to thousands of uF
- Polarized (must observe polarity)
- Good for bulk energy storage and low-frequency ripple smoothing
- Higher ESR and leakage than ceramics
- Finite lifetime; temperature and ripple current strongly affect longevity

Best use:

- Power supply input/output bulk capacitance
- DC bus smoothing

## 3) Tantalum (including polymer tantalum)

- Polarized (most types)
- Better volumetric efficiency than many aluminum parts
- Generally lower leakage and more stable capacitance than standard electrolytics
- Can fail short if overstressed; derating is important

Best use:

- Compact power rails where stable capacitance is needed

## 4) Film (Polyester, Polypropylene, etc.)

- Non-polarized
- Good stability, low loss, good pulse handling (especially polypropylene)
- Larger physical size for same capacitance vs electrolytic/ceramic

Best use:

- Audio coupling, timing networks, snubbers, AC applications, precision analog

## 5) Supercapacitors (EDLC)

- Very high capacitance (farads to kilofarads)
- Low voltage per cell (often around 2.7 V max)
- High leakage compared with conventional capacitors

Best use:

- Short-term backup, hold-up power, energy buffering

## Polarized vs Non-Polarized

Polarized capacitors (most electrolytic/tantalum):

- Must be connected with correct polarity
- Reverse voltage can cause damage, leakage, heating, or venting

Non-polarized capacitors (ceramic/film):

- Can be connected either way in DC/AC circuits (subject to voltage/current limits)

## Typical Circuit Applications

## 1) Decoupling and Bypass

Goal: reduce supply noise and provide local transient current.

- Place 100 nF ceramic as close as possible to each IC power pin pair.
- Add nearby bulk capacitor (1 uF to 47 uF, depending on load transients).
- Keep traces short and ground return low impedance.

## 2) Smoothing Rectified DC

After rectification, a bulk capacitor reduces ripple.

Approximate ripple relation:

$$
\Delta V \approx \frac{I_{load}}{f_{ripple} C}
$$

Where $f_{ripple}$ is typically $2 \times$ mains frequency for full-wave rectifiers.

## 3) RC Timing and Filtering

Time constant:

$$
	au = RC
$$

- After 1 tau: ~63% of final step response
- After 5 tau: ~99% settled

For first-order RC low-pass/high-pass:

$$
f_c = \frac{1}{2\pi RC}
$$

## 4) AC Coupling (DC Blocking)

Series capacitor blocks DC and passes AC above cutoff frequency.

Pick $C$ with load/input resistance to set acceptable low-frequency response:

$$
f_c = \frac{1}{2\pi R_{in} C}
$$

## 5) Snubbers and Transient Suppression

RC snubbers reduce switching spikes and ringing across switches/inductive loads.

- Use film capacitors for pulse/high dV/dt stress where possible.
- Ensure voltage and pulse ratings are sufficient.

## Series and Parallel Combinations

Parallel:

$$
C_{total} = C_1 + C_2 + \cdots
$$

Series:

$$
\frac{1}{C_{total}} = \frac{1}{C_1} + \frac{1}{C_2} + \cdots
$$

Notes:

- Parallel increases capacitance and can reduce effective ESR.
- Series increases voltage capability, but may require balancing resistors for electrolytics due to leakage mismatch.

## Selection Checklist

1. Required capacitance at operating conditions (include tolerance and DC bias effects).
2. Required voltage rating with derating margin.
3. Temperature range and expected drift.
4. Ripple current and ESR heating.
5. Frequency behavior (ESR/ESL, self-resonant frequency).
6. Size/package and mounting constraints.
7. Lifetime/reliability requirements.

Practical derating guidance:

- Use at least 1.25x to 2x voltage margin where practical.
- For tantalum, conservative derating (often around 50% voltage use) improves reliability.

## Reading Common Markings

Through-hole and some SMD parts may use 3-digit EIA codes:

- First two digits are significant figures, third is multiplier in pF.
- Example: `104` = $10 \times 10^4$ pF = 100000 pF = 100 nF = 0.1 uF.
- Example: `472` = $47 \times 10^2$ pF = 4700 pF = 4.7 nF.

Electrolytic cans often print direct values and voltage (e.g. `470uF 25V`).

## Common Failure Modes

- Overvoltage: dielectric breakdown
- Reverse polarity (polarized caps): gas generation, leakage, venting
- Excess ripple current: overheating, ESR increase, lifetime reduction
- Thermal stress and aging: value drift, reduced capacitance
- Mechanical cracking in MLCCs from PCB flexing

## Measurement and Testing Tips

- Use LCR meter at relevant frequency (e.g. 100 Hz/1 kHz/10 kHz depending on part and application).
- Measure ESR for power applications (in-circuit ESR meter can help diagnostics).
- For leakage tests, apply rated/working voltage through a resistor and monitor steady-state current.
- Always discharge capacitors safely before handling or measuring.

## Safety Notes

- Large electrolytics and supercapacitors can store dangerous energy after power is removed.
- Use a resistor for controlled discharge; do not short large capacitors directly.
- Observe polarity and voltage ratings.
- In mains-connected circuits, use safety-rated capacitors:
	- X-class across line
	- Y-class line-to-earth

## Quick Reference Values

- MCU decoupling: 100 nF ceramic per VCC pin + 1 uF to 10 uF nearby
- LDO output stability: follow regulator datasheet ESR/capacitance recommendations
- Audio coupling starting point: 1 uF to 10 uF depending on input impedance
- Simple debounce RC (switch): 1 kohm to 100 kohm with 1 nF to 100 nF (tune experimentally)

## Worked Example

Goal: choose a smoothing capacitor for a rectified supply.

Given:

- Load current: `0.2 A`
- Full-wave ripple frequency: `100 Hz`
- Allowable ripple: `1 V`

Use:

```
Delta V ~= Iload / (fripple x C)
```

Rearrange:

```
C ~= Iload / (fripple x Delta V)
```

Calculate:

```
C ~= 0.2 / (100 x 1) = 0.002 F = 2000 uF
```

Practical choice: `2200 uF` with suitable voltage rating and ripple current margin.

## Related Topics

- See FORMULAE.md for additional circuit equations.
- See POWERSOURCE.md for power supply context.