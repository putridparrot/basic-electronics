# Diodes

A diode is a two-terminal semiconductor that conducts current primarily in one direction. Diodes are used for rectification, protection, clamping, switching, and light emission (LEDs).

## Core Concept

- Forward bias: diode conducts when anode is sufficiently above cathode.
- Reverse bias: diode blocks current until breakdown conditions are reached.

Practical forward voltage (`Vf`) examples:

- Silicon diode: about `0.6 V` to `0.8 V`
- Schottky diode: about `0.2 V` to `0.5 V`
- LED: typically `1.8 V` to `3.5 V+` depending on color/type

## Key Parameters

- `Vf` (forward voltage) at a given current
- `If` (average forward current rating)
- `Ifsm` (surge forward current)
- `Vr` or `Vrrm` (maximum reverse voltage)
- Reverse leakage current (`Ir`)
- Reverse recovery time (`trr`) for switching behavior
- Junction capacitance (`Cj`) for high-frequency performance
- Power dissipation and thermal resistance

## Common Diode Types

## 1) Rectifier Diodes

- Designed for power conversion, generally slower switching
- Common family: `1N400x`

Best use:

- AC to DC rectifiers, polarity protection in low-speed paths

## 2) Fast and Ultra-Fast Diodes

- Shorter reverse recovery than standard rectifiers

Best use:

- Switching power supplies and fast commutation paths

## 3) Schottky Diodes

- Low forward voltage and fast switching
- Higher reverse leakage than many silicon PN diodes

Best use:

- Low-loss rectification, OR-ing supplies, clamp paths

## 4) Zener Diodes

- Intended to operate in reverse breakdown at specified voltage (`Vz`)

Best use:

- Reference/clamp circuits and basic overvoltage protection

## 5) TVS Diodes

- Transient Voltage Suppressors for ESD and surge events

Best use:

- Protecting interfaces and supply rails from short transients

## 6) Signal/Small-Switching Diodes

- Small currents, fast switching, low capacitance
- Common part: `1N4148`

Best use:

- Logic steering, signal shaping, detector circuits

## 7) LEDs (Light Emitting Diodes)

- Emit light in forward conduction
- Require current limiting

Best use:

- Indicators, lighting, optocouplers

## Core Circuits

## 1) Half-Wave Rectifier

- One diode passes one half-cycle of AC waveform.

## 2) Bridge Rectifier

- Four diodes convert full AC cycle to pulsating DC.
- Full-wave ripple frequency is twice mains frequency.

## 3) Flyback Protection for Coils

- Diode placed across relay/motor coil to absorb inductive kick when switch opens.
- Orientation is reverse-biased during normal operation.

## 4) Reverse Polarity Protection

- Series diode: simple but drops voltage by `Vf`.
- Parallel diode plus fuse: protects by shorting wrong polarity condition.

## 5) Clamping and Level Shifting

- Diodes limit voltage excursions and protect inputs.

## Diode Equation (Conceptual)

The I-V curve is exponential in forward bias:

```
I = Is x (exp(Vd / (n x Vt)) - 1)
```

In most practical design work, datasheet curves are used instead of direct equation solving.

## Power and Thermal Checks

Approximate conduction loss:

```
P ~= Vf x I
```

Higher current and temperature raise junction temperature; ensure thermal limits are respected.

## Selection Checklist

1. Maximum reverse voltage margin.
2. Average and surge forward current requirements.
3. Acceptable forward voltage drop and efficiency impact.
4. Recovery speed requirements for switching frequency.
5. Leakage limits at operating temperature.
6. Package thermal performance.

## Common Failure Modes

- Overcurrent leading to thermal runaway and short/open failure
- Reverse overvoltage breakdown damage
- Repetitive surge overstress
- Incorrect orientation in circuit

## Measurement Tips

- Use multimeter diode mode: forward drop should be reasonable, reverse should show open.
- In-circuit readings may be affected by parallel paths.
- For switching supplies, scope reverse recovery and ringing behavior where needed.

## Safety Notes

- Mains rectifier circuits can retain dangerous voltage in capacitors after power-off.
- Use correctly rated isolation and creepage/clearance distances in high-voltage designs.

## Worked Example

Goal: estimate loss in a series polarity-protection diode.

Given:

- Load current: `0.5 A`
- Diode forward drop: `0.7 V`

Use:

```
P ~= Vf x I
```

Calculate:

```
P ~= 0.7 x 0.5 = 0.35 W
```

Implication: choose a diode/package that can safely dissipate at least `0.35 W` with thermal margin, or use a lower-drop Schottky/MOSFET ideal-diode approach for efficiency.

## Related Topics

- See LEDS.md for LED-specific guidance.
- See RELAYS.md for flyback protection context.
- See POWERSOURCE.md for rectification and supply design basics.
