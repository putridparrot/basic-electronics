# Inductors

An inductor stores energy in a magnetic field when current flows through its winding. Inductors resist changes in current, making them central to filters, switching regulators, and resonant circuits.

## Core Concept

Ideal inductor relationship:

```
V = L x (dI/dt)
```

Energy stored:

```
E = 0.5 x L x I^2
```

Where:

- `L` = inductance (henry)
- `I` = current (amp)

Practical behavior:

- Current through an inductor cannot change instantaneously.
- Voltage across an inductor can change quickly to enforce current continuity.

## Units and Typical Values

- `1 H` (henry)
- `1 mH` = `10^-3 H`
- `1 uH` = `10^-6 H`

Common ranges:

- RF tuning/chokes: `nH` to low `uH`
- Buck/boost power stages: around `0.1 uH` to `100 uH`
- Audio/crossover/filtering: `uH` to `mH`

## Real-World Parameters

- Inductance tolerance
- DCR (DC resistance) of winding
- Saturation current (`Isat`)
- RMS current rating (thermal limit)
- Core material and core losses
- Self-resonant frequency (SRF)
- Q factor and AC loss behavior

Important:

- Above `Isat`, effective inductance drops and ripple/current stress rise sharply.

## Common Inductor Types

## 1) Air-Core

- No magnetic core, very linear, no core saturation
- Lower inductance per turn and larger size

Best use:

- RF, high-linearity applications

## 2) Ferrite-Core

- High permeability, compact, widely used in switching supplies

Best use:

- SMPS power inductors, chokes, EMI filtering

## 3) Iron Powder / Composite Core

- Better distributed air-gap behavior and DC bias handling

Best use:

- Power conversion where ripple and DC bias are significant

## 4) Toroidal Inductors

- Ring core reduces external magnetic field leakage
- Can provide low EMI and good efficiency

Best use:

- Power filtering and converter stages

## 5) Coupled Inductors / Common-Mode Chokes

- Multiple windings on shared core
- Used for differential/common-mode noise control or transformer-like coupling

Best use:

- EMI suppression and specialized converter topologies

## Core Applications

## 1) Buck/Boost Converters

- Inductor stores and transfers energy each switching cycle.
- Value affects ripple current, transient response, and efficiency.

## 2) LC Filters

- With capacitors, inductors form low-pass, high-pass, band-pass, or notch filters.

Resonant frequency:

```
f0 = 1 / (2 x pi x sqrt(L x C))
```

## 3) Energy Storage and Smoothing

- Inductor smoothing reduces current ripple after switching nodes.

## 4) EMI Suppression

- Common-mode and differential chokes attenuate conducted noise.

## Selection Checklist

1. Required inductance at operating current and frequency.
2. Peak current below saturation with margin.
3. RMS current below thermal rating.
4. DCR low enough for acceptable copper loss.
5. Core loss suitable for switching frequency.
6. Package and thermal design compatibility.

## Losses and Heating

Major contributors:

- Copper loss: approximately `I^2 x DCR`
- Core loss: frequency and flux-density dependent

Both must be checked for expected operating point and temperature.

## Common Failure Modes

- Overcurrent saturation causing overheating and stress elsewhere
- Insulation breakdown at excessive voltage stress
- Core cracking from mechanical or thermal stress
- Excess EMI from poor layout or wrong component choice

## Layout and Measurement Tips

- Keep high di/dt loops small in switch-mode supplies.
- Separate noisy switch nodes from sensitive analog traces.
- Measure inductor ripple current with proper current probe or low-ohm shunt and differential probing.

## Safety Notes

- Inductors in power circuits can generate high transient voltages when current paths are interrupted.
- Ensure clamp/snubber/flyback paths are correctly designed.

## Worked Example

Goal: find resonant frequency of an LC network.

Given:

- `L = 10 uH`
- `C = 100 nF`

Use:

```
f0 = 1 / (2 x pi x sqrt(L x C))
```

Calculate:

```
L x C = 10e-6 x 100e-9 = 1e-12
sqrt(L x C) = 1e-6
f0 ~= 1 / (2 x pi x 1e-6) ~= 159 kHz
```

Result: resonance is approximately `159 kHz`.

## Related Topics

- See POWERSOURCE.md for converter and filtering context.
- See CAPACITORS.md for LC and ripple interactions.
- See FORMULAE.md for resonance and timing equations.
