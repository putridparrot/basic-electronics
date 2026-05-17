# Power Source

The power source is the foundation of every electronic system. Good power design improves stability, safety, noise performance, and component lifetime.

## Core Concept

A source must provide:

- Correct voltage (`V`)
- Enough current (`I`)
- Acceptable ripple/noise
- Safe operation under faults

Power relation:

```
P = V x I
```

## Common Power Source Types

## 1) Batteries

- Primary (non-rechargeable): alkaline, lithium primary
- Secondary (rechargeable): Li-ion/LiPo, NiMH, lead-acid

Benefits:

- Portable, low noise

Considerations:

- Capacity (Ah/mAh), internal resistance, discharge curve, safety

## 2) USB Power

- Commonly `5 V`
- Convenient for low to medium power projects

Considerations:

- Cable drop, source current limits, connector reliability

## 3) Bench DC Supply

- Adjustable voltage and current limit
- Best for development and fault-safe bring-up

Best practice:

- Start with low current limit for first power-on.

## 4) AC Mains Adapters

- Isolated AC-DC supplies provide regulated DC output

Considerations:

- Safety certifications, ripple, transient behavior

## 5) Solar and Energy Harvesting

- Used with charge controllers and storage elements

Considerations:

- Highly variable input, MPPT and storage management needs

## Regulation Methods

## 1) Linear Regulators (LDO)

- Simple, low noise
- Dissipate excess voltage as heat

Loss estimate:

```
Ploss ~= (Vin - Vout) x Iout
```

## 2) Switching Regulators (Buck/Boost/Buck-Boost)

- Higher efficiency
- More complex, introduces switching ripple/EMI

Best use:

- Medium to high power, battery-operated efficiency-critical systems

## Design Checks

## Voltage Margin

- Ensure minimum source voltage always exceeds regulator headroom and load needs.

## Current Budget

- Sum all load currents and include startup/transient peaks.
- Add margin for future expansion and temperature effects.

## Ripple and Noise

- Sensitive analog and RF circuits often need extra filtering and low-noise rails.
- Use local decoupling at IC pins.

## Protection Features to Include

- Reverse polarity protection
- Overcurrent protection (fuse/PTC/current limit)
- Overvoltage/transient suppression (TVS where needed)
- Inrush control for large capacitive loads
- Brown-out monitoring/reset for digital systems

## Grounding and Distribution

- Use low-impedance ground return paths.
- Separate noisy switching returns from sensitive analog references when possible.
- Keep high-current loops short.

## Common Failure Symptoms

- Random resets: voltage droop or brown-out
- Hot regulators: excessive power dissipation or thermal path issues
- Communication noise/errors: ripple/ground bounce/EMI coupling
- Unstable analog readings: poor decoupling or shared noisy supply

## Selection Checklist

1. Input source type and range.
2. Required output rails and current per rail.
3. Efficiency and thermal targets.
4. Noise/ripple requirements.
5. Protection and safety needs.
6. PCB space, cost, and assembly constraints.

## Safety Notes

- Mains-powered designs require isolation, clearances, and certified parts.
- Large capacitors can remain charged after power-off.
- Lithium battery systems require proper charging/protection ICs.

## Worked Example

Goal: check regulator heat in a linear supply.

Given:

- `Vin = 12 V`
- `Vout = 5 V`
- `Iout = 0.3 A`

Use:

```
Ploss ~= (Vin - Vout) x Iout
```

Calculate:

```
Ploss ~= (12 - 5) x 0.3 = 2.1 W
```

Result: `2.1 W` is substantial for a small package; consider heatsinking or switching regulator.

## Related Topics

- See CAPACITORS.md for decoupling and smoothing.
- See INDUCTORS.md for switching regulator magnetics.
- See DIODES.md for rectification and protection paths.
