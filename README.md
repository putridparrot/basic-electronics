# Basic Electronics

This repository is a practical reference for learning electronics fundamentals, especially for microcontroller-based projects.

## How to Use This Repo

- Start with [Formulae](FORMULAE.md) for core equations.
- Use [Glossary](GLOSSARY.md) when you need quick definitions of common electronics and embedded abbreviations.
- Read component pages as needed while building circuits.
- Use [Tools](TOOLS.md) as a bench and debugging checklist.
- Use [Microcontrollers](MICROCONTROLLERS.md) when selecting a controller platform.

## Documentation Index

| Page | Difficulty | Focus |
|---|---|---|
| [Formulae](FORMULAE.md) | Beginner | Core equations and worked calculations |
| [Glossary](GLOSSARY.md) | Beginner | Common abbreviations and quick definitions |
| [Resistors](RESISTORS.md) | Beginner | Current limiting, dividers, tolerance, power |
| [Capacitors](CAPACITORS.md) | Beginner | Decoupling, timing, filtering, capacitor types |
| [Diodes](DIODES.md) | Beginner | Rectification, protection, diode families |
| [LEDs](LEDS.md) | Beginner | LED drive, resistor sizing, dimming |
| [Transistors](TRANSISTORS.md) | Intermediate | BJT and MOSFET switching and selection |
| [Inductors](INDUCTORS.md) | Intermediate | Energy storage, filtering, converter inductors |
| [Power Source](POWERSOURCE.md) | Intermediate | Power rails, regulation, protection, grounding |
| [Relays](RELAYS.md) | Beginner | Isolated switching, coil drive, contact protection |
| [Switched and Buttons](SWITCHESBUTTONS.md) | Beginner | Switch types, pull resistors, debounce |
| [ICs](IC.md) | Intermediate | IC categories, datasheet checks, integration tips |
| [Crystals and Oscillators](CRYSTALSOSCILLATORS.md) | Intermediate | Clock sources, load caps, timing accuracy |
| [Microcontrollers](MICROCONTROLLERS.md) | Beginner | MCU basics and board family comparison |
| [Tools](TOOLS.md) | Beginner | Measurement, soldering, debug workflow |

## Conventions Used in These Docs

- Resistance values are written as `ohm`, `kohm`, and `Mohm`.
- Capacitance values are written as `pF`, `nF`, and `uF`.
- Inductance values are written as `uH` and `mH`.
- Equations are shown in simple text form for easy copy/use.

## Quick Start Checklist

1. Confirm supply voltage and current limits before power-on.
2. Add decoupling (`100 nF` near each IC supply pin).
3. Add current limiting for LEDs.
4. Add flyback protection for relay/motor coils.
5. Check resistor power ratings with margin.
6. Verify polarity and orientation before energizing a circuit.
