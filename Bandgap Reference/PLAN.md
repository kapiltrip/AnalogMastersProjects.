# Bandgap Reference Plan

## Project Goal

Design and analyze a bandgap reference using PTAT and CTAT components, with temperature sweep, line sensitivity discussion, startup awareness, and optional low-voltage extension.

## Working Rule

For every study block:

1. Watch the lecture.
2. Make 1-page handwritten notes.
3. Do 1 derivation or design sheet.
4. Do 1 simulation block.
5. Write what failed and why.

## Suggested Folder Use

- `notes/`: temperature theory, derivations, viva points
- `design/`: circuit choice, resistor ratios, device ratios
- `simulations/`: temperature sweeps, startup, line regulation
- `references/`: lecture links, assignment PDFs, source notes
- `report/`: report draft, slides, final summary

## Week 1: Bandgap Intuition First

### Watch

- [The Bandgap Reference - Part 1](https://www.youtube.com/watch?v=VyWFaDfAoHw)
- [Shanthi Pavan Analog Electronic Circuits Course Details](https://nptel.ac.in/courses/108106188)

### What You Gain

- Why references drift with temperature
- Why bandgap references are needed
- How temperature cancellation is possible

### Why It Supports The Project

This gives the principle-level story before formulas and circuit implementation details.

### Do Next

Write a one-page concept note on:

- What CTAT means
- What PTAT means
- Why summing them can flatten temperature dependence

## Week 2: PTAT And CTAT Explicitly

### Watch

- [Introduction to Bandgap Voltage References, PTAT and CTAT Voltage](https://www.youtube.com/watch?v=NhA1vHVKjNc)
- [Adding PTAT and CTAT Voltages](https://www.youtube.com/watch?v=BLmW2zjKZF8)

### What You Gain

- Where the CTAT term comes from
- Where the PTAT term comes from
- How resistor ratios or scaling combine them
- How the zero-temperature-coefficient point is chosen

### Why It Supports The Project

This is the mathematical core needed to justify the resistor and device choices.

### Do Next

Derive a symbolic form such as:

`Vref = VCTAT + k * VPTAT`

Then calculate the first-pass scaling factor `k`.

## Week 3: Actual Bandgap Circuit Choice

### Watch

- [Bandgap Voltage Reference Circuit | Brokaw Bandgap Circuit](https://www.youtube.com/watch?v=-EMza3bf4a8)

### What You Gain

- The Brokaw bandgap structure
- Role of the amplifier or loop
- How device area ratio and resistors create the PTAT term
- How the final reference is formed

### Why It Supports The Project

This is the point where the project becomes a real circuit implementation.

### Do Next

Freeze the main architecture:

- Standard bandgap or Brokaw bandgap
- Whether to use an op-amp-assisted loop

For a first implementation, use Brokaw bandgap as the main structure.

## Week 4: Low-Voltage Extension

### Watch

- [Sub 1 Volt Bandgap Circuit](https://www.youtube.com/watch?v=Shg9rhlCBQ0)

### What You Gain

- Why standard bandgaps are harder at low supply voltage
- What changes in low-voltage reference design
- What additional constraints appear

### Why It Supports The Project

This gives you an advanced extension section that strengthens the report even if the main design is not sub-1 V.

### Do Next

Keep this as:

- Future work
- Advanced discussion
- Comparison section

Do not use it as the first implementation unless your guide requires it.

## Week 5: Turn It Into A Real Design Project

### Use This Evaluation Checklist

- [IIT Madras EE539 Assignment 7](https://www.ee.iitm.ac.in/~nagendra/EE539/201001/assignments/assignment07.pdf)

### What You Gain

- A real academic design checklist
- `dVBE/dT` extraction target
- Resistor choice method for near-zero TC
- Temperature sweep and transient expectations
- Loop behavior checkpoints if an amplifier is used

### Why It Supports The Project

This prevents the project from staying at the level of lecture notes and pushes it into a proper design workflow.

### Do Next

Prepare the simulation checklist:

- Temperature sweep
- Supply sweep
- Line sensitivity
- Transient or startup check
- Optional loop gain if an amplifier is included

## Week 6: Implementation And Refinement

### Run

- `Vref` versus temperature
- `Vref` versus supply
- Startup and settling
- Output loading effect if relevant
- Parameter tuning for near-zero TC around room temperature

### What You Gain

You generate the proof that the reference works over operating conditions.

### Why It Supports The Project

This gives you the data needed for temperature coefficient, robustness, and practical usability.

### Typical Failure Notes

- Slope not flat: PTAT and CTAT weighting is wrong
- Too much supply dependence: poor supply rejection or loop behavior
- Startup issue: document it honestly and add startup discussion
- Low-voltage failure: usually a headroom limitation

## Final Deliverables

- Final schematic
- PTAT and CTAT derivation sheet
- Temperature sweep plots
- Supply sweep plots
- Startup or transient plots
- Near-zero TC tuning summary
- One limitations and future-work slide

## Primary References

- [NPTEL Power Management Integrated Circuits Course](https://onlinecourses.nptel.ac.in/noc20_ee08/preview)
- [Shanthi Pavan Analog Electronic Circuits Course Details](https://nptel.ac.in/courses/108106188)
- [IIT Madras EE539 Intro Handout](https://www.ee.iitm.ac.in/~nagendra/EE539/201101/handouts/ee539-intro.pdf)

## Resume Line

Designed a PTAT/CTAT-based bandgap reference and evaluated temperature behavior, supply sensitivity, and startup/transient characteristics.
