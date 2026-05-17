# Transistors

Transistors are semiconductor devices used mainly as switches and amplifiers. They are the foundation of modern electronics, from simple LED drivers to CPUs.

## Core Concept

Two broad families are common in basic electronics:

- BJT (Bipolar Junction Transistor): current-controlled device
- MOSFET (Metal-Oxide-Semiconductor FET): voltage-controlled device

## BJT Basics

Main terminals:

- NPN: Base (B), Collector (C), Emitter (E)
- PNP: Base (B), Collector (C), Emitter (E)

Switching behavior (NPN low-side example):

- Base current drives transistor into conduction
- Collector current flows through load to emitter/ground

Approximate relation in active region:

```
Ic ~= beta x Ib
```

For switching, design with forced beta margin (do not rely on nominal beta).

## MOSFET Basics

Main terminals:

- Gate (G), Drain (D), Source (S)

Key ideas:

- Gate voltage relative to source controls channel conduction.
- Very low gate current in steady state.
- On-state loss depends on `Rds(on)`.

Conduction loss estimate:

```
P ~= I^2 x Rds(on)
```

## Choosing BJT vs MOSFET

BJT strengths:

- Simple small-signal amplification
- Low cost for light loads

MOSFET strengths:

- Better efficiency for switching loads
- Scales well to higher current
- Common choice for MCU-driven power switching (logic-level devices)

## Key Parameters to Check

BJT:

- `Vceo` maximum voltage
- `Ic` maximum current
- Gain (`hFE` or `beta`) range
- `Vce(sat)` at target current
- Power dissipation and thermal limits

MOSFET:

- `Vds` maximum voltage
- Continuous and pulsed current ratings
- `Rds(on)` at actual gate drive voltage
- Gate threshold (`Vgs(th)`) is not full-on voltage
- Total gate charge (`Qg`) for switching speed considerations

## Typical Switch Topologies

## 1) BJT Low-Side Switch

- Load to positive rail, transistor between load and ground
- Base resistor limits base current
- Flyback diode required for inductive loads

## 2) N-MOSFET Low-Side Switch

- Most common efficient load switch
- Gate resistor and gate pull-down often used

## 3) P-MOSFET High-Side Switch

- Useful when load must connect/disconnect from positive rail
- Often needs level shifting/gate driver for full enhancement

## Example: BJT Base Resistor Sizing (Switch)

Given:

- `Iload = 100 mA`
- Force `beta = 10` for saturation margin
- MCU output `5 V`
- `Vbe ~= 0.7 V`

Then:

```
Ib = Iload / 10 = 10 mA
Rb = (5 - 0.7) / 0.01 = 430 ohm
```

Choose nearest standard value with practical drive considerations.

## Example: MOSFET Suitability Check

- Confirm `Rds(on)` is specified at your gate drive voltage (for example `Vgs = 2.5 V` or `4.5 V` for logic-level use).
- Calculate conduction loss and estimated temperature rise.

## Switching and Thermal Considerations

- Fast switching reduces transition loss but can increase EMI.
- Slow switching increases heat during transitions.
- Check SOA (safe operating area) for linear operation cases.
- Use proper heatsinking/copper area for sustained power.

## Common Failure Modes

- Exceeding voltage or current ratings
- Missing flyback diode on inductive loads
- MOSFET not fully enhanced (hot operation)
- Thermal runaway due to inadequate cooling
- ESD damage at MOSFET gate

## Layout and Protection Tips

- Keep high-current loops short and wide.
- Add flyback diode for relays, solenoids, motors.
- Use gate/source protection where transients are possible.
- Separate power ground and sensitive signal return as needed.

## Selection Checklist

1. Voltage and current margin.
2. Drive capability from control source.
3. Loss and thermal budget.
4. Switching speed and EMI constraints.
5. Package and assembly requirements.

## Related Topics

- See RELAYS.md for load switching examples.
- See DIODES.md for flyback and protection components.
- See RESISTORS.md for base/gate resistor selection.
