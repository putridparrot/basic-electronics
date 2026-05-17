# Crystals and Oscillators

Crystals and oscillators provide the timing reference (clock) that keeps digital systems synchronized. The clock determines instruction timing, serial communication accuracy, PWM precision, and real-time timekeeping quality.

## Core Concept

Digital systems need a periodic signal (clock) to sequence operations.

- Frequency (`f`) is measured in hertz (Hz).
- Period (`T`) is the inverse of frequency.

```
T = 1 / f
f = 1 / T
```

Example:

- `16 MHz` clock has period `62.5 ns`.

## Common Clock Sources

## 1) Internal RC Oscillator

- Built into many MCUs
- Very low cost and simple (no external parts)
- Lower absolute accuracy and higher drift than crystal-based clocks

Best use:

- Non-critical timing tasks, low-cost designs, fast startup

## 2) Quartz Crystal

- Passive resonator requiring load capacitors and oscillator circuitry
- High frequency stability and good long-term accuracy
- Common frequencies: `32.768 kHz`, `8 MHz`, `16 MHz`, `25 MHz`

Best use:

- MCU system clocks, RTC timing, communication interfaces

## 3) Ceramic Resonator

- Similar usage to crystals, usually lower cost
- Less accurate and less stable than quartz crystal

Best use:

- General timing where moderate accuracy is acceptable

## 4) Crystal Oscillator Module (XO)

- Active device providing ready-to-use clock output
- Includes internal oscillator circuit and crystal
- Typically 4-pin parts (VCC, GND, output, enable/NC)

Best use:

- Systems needing simple clock integration and predictable startup

## 5) Temperature-Compensated / Oven-Controlled Oscillators

- TCXO: improved stability across temperature
- OCXO: very high stability using heated controlled environment

Best use:

- Precision radios, instrumentation, telecom timing

## Key Parameters to Check

- Nominal frequency (e.g. `16 MHz`)
- Frequency tolerance (initial error at reference conditions)
- Frequency stability over temperature and aging
- Load capacitance (`CL`) for crystals
- ESR (equivalent series resistance) of crystal
- Drive level (maximum excitation power)
- Startup time
- Supply voltage and output logic level (for oscillator modules)
- Output waveform type: CMOS, clipped sine, differential (LVDS/LVPECL, etc.)

## 32.768 kHz RTC Crystal Note

`32.768 kHz` is widely used for real-time clocks because:

```
32768 = 2^15
```

Simple binary divider chains can generate 1 Hz from this frequency efficiently.

## Load Capacitor Selection (Typical Crystal Circuit)

For a crystal with specified load capacitance `CL`, two capacitors to ground are commonly used.

Approximation:

```
CL ~= (C1 x C2) / (C1 + C2) + Cstray
```

If `C1 = C2 = C`, then:

```
CL ~= C/2 + Cstray
```

Practical point:

- Include PCB and pin stray capacitance (`Cstray`, often a few pF) when choosing `C1` and `C2`.

## Typical Applications

- MCU system clock generation
- UART baud-rate accuracy improvement
- USB/Ethernet timing references
- RTC timekeeping
- RF synthesizers and PLL references

## Layout Guidelines

- Place crystal as close as possible to oscillator pins.
- Keep traces short, symmetric, and away from noisy high-current nodes.
- Avoid routing clock lines under switching regulators where possible.
- Use solid ground reference near clock network.

## Common Failure or Debug Symptoms

- No startup: incorrect load caps, excessive ESR, poor layout
- Frequency offset: wrong load capacitance, drift, temperature effect
- Intermittent operation: vibration/shock, poor solder joints
- Communication errors: clock accuracy too poor for protocol margin

## Selection Checklist

1. Required frequency and tolerance.
2. Temperature range and stability target.
3. Startup behavior and power budget.
4. Package size and mounting method.
5. Crystal (`CL`, ESR, drive level) compatibility with MCU oscillator.
6. Need for module oscillator (XO/TCXO) instead of passive crystal.

## Quick Reference

- `16 MHz` crystal: common 8-bit MCU external clock
- `8 MHz` crystal: common low-power MCU options
- `25 MHz` crystal/XO: common Ethernet and networking
- `32.768 kHz`: RTC and low-power timekeeping

## Worked Example

Goal: determine load capacitors for a `16 MHz` crystal with `CL = 18 pF`.

Assume:

- `C1 = C2 = C`
- Stray capacitance `Cstray = 3 pF`

Use:

```
CL ~= C/2 + Cstray
```

Calculate:

```
18 ~= C/2 + 3
C/2 ~= 15
C ~= 30 pF
```

Practical choice: start around `27 pF` to `33 pF`, then verify frequency error and startup margin in hardware.

## Related Topics

- See MICROCONTROLLERS.md for MCU clock context.
- See FORMULAE.md for frequency and timing equations.
