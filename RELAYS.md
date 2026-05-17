# Relays

A relay is an electrically controlled switch that allows a low-power control circuit to switch a separate load circuit. Relays are widely used for isolation, high-voltage switching, and interfacing low-voltage logic to larger loads.

## Core Concept

Most relays use an electromagnetic coil:

- Energize coil -> magnetic field moves contacts
- De-energize coil -> spring returns contacts

This provides galvanic isolation between control and switched sides.

## Common Relay Contact Terms

- COM: common terminal
- NO (Normally Open): open when coil is off, closes when coil is on
- NC (Normally Closed): closed when coil is off, opens when coil is on
- SPST, SPDT, DPDT: pole/throw configurations

## Relay Types

## 1) Electromechanical Relay (EMR)

- Mechanical contacts, audible click
- Can switch AC or DC loads depending on rating

Best use:

- General switching with isolation requirements

## 2) Solid-State Relay (SSR)

- Semiconductor switching, no moving contacts
- Silent and fast, often longer switching life

Best use:

- High cycle count, low acoustic noise applications

## 3) Reed Relay

- Small, fast, low coil power
- Usually lower current switching capacity

Best use:

- Signal-level switching and instrumentation

## Critical Parameters

- Coil voltage and coil current/power
- Contact rating (voltage/current/type of load)
- Contact form (NO/NC/SPDT etc.)
- Contact resistance
- Operate/release time
- Mechanical/electrical lifetime
- Isolation voltage

Important:

- Inductive loads (motors, solenoids) are harder on contacts than resistive loads.

## Driving a Relay from a Microcontroller

A GPIO pin usually cannot drive a relay coil directly.

Typical interface:

- Transistor or MOSFET coil driver
- Flyback diode across coil
- Optional base/gate resistor and status LED

Flyback diode rule:

- Diode is reverse-biased during normal coil energization and clamps voltage spike when coil turns off.

## Contact Protection

To extend contact life with inductive or noisy loads:

- Use RC snubber (often for AC)
- Use flyback diode or TVS on DC inductive loads
- Keep within inrush and steady-state ratings

## Common Applications

- Switching mains appliances from low-voltage control
- Motor and solenoid control
- Signal routing/isolation
- Safety interlocks and fail-safe control

## Common Failure Modes

- Contact pitting/welding from inrush or arcing
- Coil burnout from overvoltage or overheating
- Mechanical wear and contact bounce issues
- PCB damage from missing flyback suppression

## Selection Checklist

1. Control voltage available for coil/input.
2. Load type (resistive/inductive/capacitive) and rating.
3. Needed contact configuration.
4. Isolation/safety requirements.
5. Switching speed, noise, and lifetime targets.

## Safety Notes

- Mains switching requires proper creepage/clearance and enclosure safety.
- Never exceed relay contact ratings or ignore load derating curves.
- Treat exposed mains wiring as hazardous.

## Worked Example

Goal: estimate relay coil current and driver suitability.

Given:

- Coil voltage: `5 V`
- Coil resistance: `70 ohm`

Use:

```
Icoil = V / R
Pcoil = V x I
```

Calculate:

```
Icoil ~= 5 / 70 ~= 71 mA
Pcoil ~= 5 x 0.071 ~= 0.36 W
```

Result: a typical MCU GPIO cannot supply `71 mA`, so use a transistor/MOSFET driver plus flyback diode.

## Related Topics

- See DIODES.md for flyback diode fundamentals.
- See TRANSISTORS.md for relay driver stage design.
- See SWITCHESBUTTONS.md for basic control interfaces.
