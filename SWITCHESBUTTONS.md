# Switches and Buttons

Switches and buttons are user and control interfaces that open, close, or redirect electrical paths. They are simple components, but reliable switching behavior is essential in real systems.

## Core Concept

- Open switch: path is broken, no current flow.
- Closed switch: path is completed, current can flow.

Buttons are usually momentary switches; toggles and rockers often latch in state.

## Common Configurations

- SPST: single-pole single-throw (on/off)
- SPDT: single-pole double-throw (select A or B)
- DPDT: two SPDT sections linked mechanically
- Momentary NO: closes only while pressed
- Momentary NC: opens only while pressed

## Key Parameters

- Contact rating (voltage/current, AC/DC)
- Contact resistance
- Mechanical life (number of cycles)
- Electrical life under load
- Actuation force and travel
- Environmental rating (IP, temperature, vibration)

## Contact Bounce

Mechanical contacts bounce for a short time when actuated, causing multiple rapid transitions.

Typical debounce approaches:

## 1) Software Debounce

- Wait for stable state (for example 5 ms to 30 ms) before accepting change

## 2) RC Hardware Debounce

- Resistor-capacitor network smooths transitions

Simple starting point:

- `10 kohm` with `100 nF` (adjust as needed)

## 3) Schmitt Trigger Input

- Improves noise immunity at threshold crossings

## Pull-Up and Pull-Down Use

Digital inputs must not float.

- Pull-up: default HIGH, switch to ground for LOW when pressed
- Pull-down: default LOW, switch to VCC for HIGH when pressed

Typical values:

- `4.7 kohm` to `100 kohm` depending on power/noise needs

Many MCUs provide configurable internal pull resistors.

## Typical Circuits

## 1) MCU Button Input (Active Low)

- Pin with pull-up enabled
- Button connects pin to ground when pressed

Benefits:

- Simple wiring and good noise tolerance in many designs

## 2) Selector Switch

- SPDT/rotary switch routes signal to one of multiple nodes

## 3) Power Toggle

- Mechanical latching switch in series with power path

## Reliability and Selection Guidance

- For low-level signals, prefer gold-plated contacts where possible.
- For larger loads, check inrush current and arc behavior.
- Consider environmental sealing (IP rating) for outdoor/industrial use.
- For high vibration, choose components with suitable mechanical retention.

## Common Failure Modes

- Oxidized/worn contacts causing intermittent behavior
- Contact welding from overcurrent/inrush
- Broken actuator/mechanics
- False triggering from insufficient debounce or noise pickup

## Troubleshooting Tips

- Use continuity mode to verify contact state changes.
- Scope input node if bounce/noise is suspected.
- Confirm pull resistor presence and value.
- Check cable length/routing for EMI coupling in remote buttons.

## Safety Notes

- Do not use low-voltage signal switches for mains unless specifically rated.
- Ensure panel/door switches used for safety interlocks meet required standards.

## Worked Example

Goal: estimate debounce time from an RC network.

Given:

- `R = 10 kohm`
- `C = 100 nF`

Use:

```
tau = R x C
```

Calculate:

```
tau = 10000 x 100e-9 = 0.001 s = 1 ms
```

Practical interpretation:

- Around `5 x tau` (`5 ms`) gives near-full settling for a simple debounce threshold strategy.

## Related Topics

- See RESISTORS.md for pull-up/pull-down values.
- See MICROCONTROLLERS.md for GPIO input handling context.
- See RELAYS.md for electrical load switching with isolation.
