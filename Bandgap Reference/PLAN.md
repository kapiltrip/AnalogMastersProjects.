# Learning-Centric Master's Plan: Bandgap Voltage Reference

## 5-Week Learning Plan

### Week 1: Understand PTAT And CTAT

- Learn: why `VBE` is `CTAT` and why `DeltaVBE` is `PTAT`.
- Learn: why adding a `PTAT` term to a `CTAT` term can reduce temperature drift.
- Why: this is the core idea of the bandgap reference, so the rest of the project depends on understanding this clearly.

### Week 2: Learn The Bandgap Equation

- Learn: how `Vref = VBE + k*DeltaVBE` is formed.
- Learn: how resistor ratio sets `k` and how area ratio sets `ln(N)`.
- Why: this explains where the reference voltage comes from and what design choices control it.

### Week 3: Learn The Real Circuit Structure

- Learn: the difference between a concept-level PTAT-CTAT block, a Brokaw-style bandgap, and lower-voltage variants.
- Learn: why startup is needed and why the zero-current state is a real issue.
- Why: this helps choose a practical final structure instead of staying only at equation level.

### Week 4: Learn How Theory Becomes A Schematic

- Learn: how hand-derived ratios become resistor values, area ratios, bias currents, and a first schematic.
- Learn: how to read the temperature trend and judge whether the `PTAT` term is too strong or too weak.
- Why: this is where theory turns into circuit intuition.

### Week 5: Learn What Makes The Reference Usable

- Learn: line regulation, load regulation, `PSRR`, corners, Monte Carlo, and mismatch in the bandgap context.
- Learn: why layout and matching can disturb a design that looks correct on paper.
- Why: a bandgap is useful only if it stays credible across variation, not just at one nominal point.

## Software Learning Plan

### Week 1: Learn The Basic Simulation Flow

- Learn: how to draw simple BJT, diode, and resistor circuits in LTspice, TINA-TI, Cadence, or xschem/ngspice.
- Learn: how to run operating-point, DC, and temperature sweeps.
- Why: this is the minimum needed to see `VBE` and `DeltaVBE` behavior directly in simulation.

### Week 2: Learn Parameter Sweeps

- Learn: how to vary area ratio, resistor ratio, and bias conditions and compare the results.
- Learn: how to check whether the simulated trend matches the expected `PTAT` or `CTAT` direction.
- Why: bandgap design depends on ratios, so the software should help verify cause and effect clearly.

### Week 3: Learn Full Schematic Entry

- Learn: how to enter the full bandgap core in the main tool.
- Learn: how to bias it properly and confirm the intended operating point exists.
- Why: this is the step where the theory becomes a real circuit.

### Week 4: Learn Practical Tests

- Learn: how to run startup tests with different supply ramps and temperatures.
- Learn: how to run basic line-regulation and load-regulation sweeps.
- Why: a bandgap is only useful if it starts correctly and behaves properly when conditions change.

### Week 5: Learn Robustness Checks

- Learn: how to run corners, Monte Carlo, and result comparisons if the tool flow supports them.
- Learn: how to keep a simple simulation log with the change made, the reason, and the result.
- Why: this turns software use into real design learning instead of random trial and error.
