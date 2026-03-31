# Bandgap Reference Plan

## Project Goal

Design and analyze a bandgap reference using PTAT and CTAT components, with temperature sweep, line sensitivity discussion, startup awareness, and optional low-voltage extension.

## If I Am Starting From Zero

I should clear these basics before Week 1. If any of them are unclear, I should spend a day or two on them first.

- Voltage, current, resistance, and power
- Ohm's law, KCL, and KVL
- What a diode does and why its voltage is not constant
- Basic BJT idea: emitter, base, collector, and why `VBE` matters
- What temperature coefficient means
- How to read a plot: slope, intercept, operating point, and sweep
- How to run a simple DC sweep and temperature sweep in the simulator I use

## What I Must Learn Before I Finish

- What a voltage reference is supposed to do in a real system
- Why `VBE` is `CTAT`
- Why `DeltaVBE` is `PTAT`
- How `Vref = VBE + k * DeltaVBE` is formed
- How resistor ratio sets the PTAT scaling
- How emitter area ratio or current-density ratio sets `DeltaVBE`
- Why first-order temperature cancellation works
- Why curvature remains even after first-order cancellation
- How the Brokaw bandgap works as a practical circuit
- Why startup is necessary and why zero-current equilibrium can exist
- How supply voltage headroom limits standard bandgap operation
- What changes in low-voltage or sub-1 V references
- What tempco, line regulation, load regulation, and PSRR mean
- What thermal voltage and current density mean in this context
- How startup, settling, and transient disturbances should be checked
- Why mismatch, resistor TC, corners, and Monte Carlo matter
- Why layout and matching can disturb a seemingly correct schematic
- How to document limitations and future work honestly

## Working Rule

For every study block:

1. Watch the lecture or read the note.
2. Make 1-page handwritten notes.
3. Do 1 derivation or design sheet.
4. Do 1 simulation block.
5. Write what failed and why.

## Suggested Folder Use

- `notes/`: temperature theory, derivations, viva points
- `design/`: circuit choice, resistor ratios, device ratios
- `simulations/`: temperature sweeps, startup, line regulation
- `references/`: lecture links, PDFs, source notes
- `report/`: report draft, slides, final summary

## Week 1: Bandgap Intuition First

### Watch / Read

- Video: `The Bandgap Reference - Part 1` by `NPTEL-NOC IITM`. Link: `https://www.youtube.com/watch?v=VyWFaDfAoHw`
- Why this video: it gives the first clean intuition for why references drift and why temperature cancellation is needed.
- [Power Management Integrated Circuits - NPTEL course page](https://archive.nptel.ac.in/noc/courses/noc20/SEM1/noc20-ee08/)
- [Chapter 14: Voltage References - Analog Devices](https://wiki.analog.com/university/courses/electronics/text/chapter-14)
- [What is a voltage reference? - TI](https://www.ti.com/video/5784629312001)

### What To Learn This Week

- What a voltage reference does inside a larger analog or mixed-signal system
- Why ordinary device voltages drift with temperature
- Why the silicon bandgap voltage is a useful reference point
- Why `VBE` has a negative temperature coefficient
- Why a temperature-independent reference cannot come from a single junction alone
- What the words `CTAT`, `PTAT`, tempco, and drift actually mean
- Why a good reference must eventually be judged across temperature, supply, and load, not just at room temperature

### What Else I Learn In Parallel

- Difference between a voltage reference concept and a complete reference product
- Why output accuracy, drift, and startup are separate concerns
- Why a good room-temperature number does not mean a good reference

### Why This Supports My Project

This gives me the principle-level story before formulas and circuit implementation details.

### What I Must Do Next

Write a one-page concept note on:

- What CTAT means
- What PTAT means
- Why summing them can flatten temperature dependence
- Why `VBE` by itself is not enough

### Move On Only When I Can Explain

- Why a single junction voltage is not a good long-term reference by itself
- The difference between `CTAT`, `PTAT`, and a temperature-independent target

## Week 2: PTAT And CTAT Explicitly

### Watch / Read

- Video: `#7 Current Regulator Applications | Introduction to Bandgap Voltage References PTAT & CTAT Voltage` by `NPTEL-NOC IITM`. Link: `https://www.youtube.com/watch?v=NhA1vHVKjNc`
- Why this video: it explains where the PTAT and CTAT terms physically come from, which is the key idea for the derivation.
- Video: `#8 Adding PTAT & CTAT Voltages | Power Management Integrated Circuits` by `NPTEL-NOC IITM`. Link: `https://www.youtube.com/watch?v=BLmW2zjKZF8`
- Why this video: it connects the separate PTAT and CTAT pieces into the actual summed reference equation.
- [Bandgap Reference Calculator Tutorial - Analog Devices](https://www.analog.com/en/resources/design-notes/bandgap-reference-calculator-tutorial.html)
- [EECS Berkeley Lecture 8: References](https://rfic.eecs.berkeley.edu/courses/ee240sp06/pdf/lect8.pdf)

### What To Learn This Week

- How the temperature behavior of `VBE` produces the `CTAT` term
- How two devices with different current densities or emitter areas produce `DeltaVBE`
- Why `DeltaVBE` is proportional to absolute temperature
- Where thermal voltage fits into the derivation
- How `Vref = VBE + k * DeltaVBE` is built mathematically
- Why resistor ratio controls the PTAT scaling factor `k`
- How the chosen ratio decides the zero-tempco operating point
- Why first-order cancellation is only an approximation over a temperature range

### What Else I Learn In Parallel

- Why `DeltaVBE` depends on current density or area ratio
- How thermal voltage enters the derivation
- Why first-order cancellation is useful but not perfect

### Why This Supports My Project

This is the mathematical core I need to justify the resistor and device choices.

### What I Must Do Next

Derive a symbolic form such as:

`Vref = VCTAT + k * VPTAT`

Then calculate the first-pass scaling factor `k`, and write what physical design parameter sets it.

### Move On Only When I Can Explain

- Why `DeltaVBE` becomes `PTAT`
- What physical circuit parameter controls `k`

## Week 3: Actual Bandgap Circuit Choice

### Watch / Read

- Video: `#9 Bandgap Voltage Reference Circuit | Brokaw Bandgap Circuit | Power Management Integrated Circuits` by `NPTEL-NOC IITM`. Link: `https://www.youtube.com/watch?v=-EMza3bf4a8`
- Why this video: it turns the PTAT-CTAT idea into the actual Brokaw-style circuit structure that I can implement and defend.
- [EE5390 Analog Integrated Circuit Design - Introduction](https://www.ee.iitm.ac.in/~nagendra/EE539/201001/handouts/ee539-intro.pdf)
- [EE5390 Assignment 7: Bandgap Reference](https://www.ee.iitm.ac.in/~nagendra/EE539/201001/assignments/assignment07.pdf)
- [AN-82: Understanding and Applying Voltage References](https://www.analog.com/en/resources/app-notes/an-82f.html)

### What To Learn This Week

- The structure of a practical Brokaw-style bandgap
- How the loop forces the required relationship between device voltages or currents
- How the resistor network turns `DeltaVBE` into a usable PTAT term
- How area ratio and resistor ratio map into an actual circuit
- Why the Brokaw cell is a better project choice than a pure equation-only block
- Why startup is not optional in a practical reference
- What the zero-current operating point is and why it is dangerous
- When an op-amp-assisted bandgap is worth considering and when it is unnecessary complexity

### What Else I Learn In Parallel

- Why startup is a real design issue
- Why loop behavior matters if an op-amp-assisted structure is used
- Why ratio choices matter more than arbitrary absolute values

### Why This Supports My Project

This is the point where the project becomes a real circuit implementation.

### What I Must Do Next

Freeze the main architecture:

- Standard bandgap or Brokaw bandgap
- Whether to use an op-amp-assisted loop
- Whether startup is already in scope

For a first implementation, I should use Brokaw bandgap as the main structure unless the supply requirement forces a different path.

### Move On Only When I Can Explain

- Why the Brokaw-style structure is a practical first choice
- Why startup must be part of the real circuit and not an afterthought

## Week 4: Low-Voltage Extension

### Watch / Read

- Video: `#10 Sub 1 | Volt Bandgap Circuit | Power Management Integrated Circuits` by `NPTEL-NOC IITM`. Link: `https://www.youtube.com/watch?v=Shg9rhlCBQ0`
- Why this video: it shows what breaks when supply voltage becomes small and why low-voltage references are a harder extension topic.
- [Power Management Integrated Circuits syllabus](https://archive.nptel.ac.in/content/syllabus_pdf/108106159.pdf)
- [Precision Techniques - Berkeley](https://people.eecs.berkeley.edu/~boser/courses/240B/lectures/M12%20Precision%20Techniques.pdf)
- [Voltage Reference Introduction PDF - TI](https://www.ti.com/content/dam/videos/external-videos/de-de/3/3816841626001/5783793652001.mp4/subassets/voltage-reference-overview-presentation.pdf)

### What To Learn This Week

- Why a normal bandgap struggles when supply voltage is low
- How headroom limits devices, loop operation, and startup
- What a fractional or sub-1 V bandgap tries to change
- Why low-voltage bandgaps are usually harder to stabilize and verify
- Why low-voltage operation changes the trade-off between simplicity and usefulness
- When low-voltage discussion belongs in future work instead of the main design
- Why curvature correction and low-voltage design should not be mixed into the first implementation without a strong reason

### What Else I Learn In Parallel

- Why headroom affects both startup and accuracy
- Why future-work sections matter in a report
- How to separate a core design goal from an optional extension

### Why This Supports My Project

This gives me an advanced extension section that strengthens the report even if the main design is not sub-1 V.

### What I Must Do Next

Keep this as:

- Future work
- Advanced discussion
- Comparison section

I should not use it as the first implementation unless my guide requires it.

### Move On Only When I Can Explain

- Why low supply voltage creates a different design problem
- Why low-voltage discussion belongs in extension work unless the spec forces it

## Week 5: Turn It Into A Real Design Project

### Use This Evaluation Checklist

- [IIT Madras EE539 Assignment 7](https://www.ee.iitm.ac.in/~nagendra/EE539/201001/assignments/assignment07.pdf)
- [AN-82: Understanding and Applying Voltage References](https://www.analog.com/en/resources/app-notes/an-82f.html)
- [Voltage reference overview for ADC - TI](https://www.ti.com/video/5783793652001)

### What To Learn This Week

- What a proper bandgap verification checklist looks like
- How to extract `dVBE/dT` and use it in first-pass design decisions
- How to choose resistor values for a first-pass near-zero-tempco target
- What temperature sweep results should look like
- What supply sweep results should look like
- Why startup and transient response deserve their own benches
- Why line regulation, load regulation, and PSRR are separate checks
- Why corners, mismatch, and resistor temperature coefficient should not be ignored in the report
- How to convert lecture knowledge into a defendable design workflow

### What Else I Learn In Parallel

- How to define proof of learning, not just proof of simulation
- Why line sensitivity, tempco, and startup must all be checked separately
- What a defendable design flow looks like in a master's project

### Why This Supports My Project

This prevents the project from staying at the level of lecture notes and pushes it into a proper design workflow.

### What I Must Do Next

Prepare the simulation checklist:

- Temperature sweep
- Supply sweep
- Line sensitivity
- Transient or startup check
- Optional loop gain if an amplifier is included

### Move On Only When I Can Explain

- Why tempco, line regulation, startup, and mismatch are different checks
- What evidence would make the project look complete to a reviewer

## Week 6: Implementation And Refinement

### Run

- `Vref` versus temperature
- `Vref` versus supply
- Startup and settling
- Output loading effect if relevant
- Parameter tuning for near-zero TC around room temperature

### Read Also

- [Chapter 14: Voltage References - Analog Devices](https://wiki.analog.com/university/courses/electronics/text/chapter-14)
- [AN-82: Understanding and Applying Voltage References](https://www.analog.com/en/resources/app-notes/an-82f.html)
- [Bandgap Reference Calculator Tutorial - Analog Devices](https://www.analog.com/en/resources/design-notes/bandgap-reference-calculator-tutorial.html)

### What To Learn This Week

- How to build and run the main simulation benches for the project
- How to interpret `Vref` versus temperature correctly
- Which parameter changes mainly shift the output value and which mainly change the slope
- How startup behavior should be tested and reported
- How output loading can disturb a reference
- How supply sensitivity shows up in the plots
- How to separate topology errors from tuning errors
- How to write a useful limitations section if the first design is not perfect
- How to decide whether corners, Monte Carlo, and layout matching are necessary additions for the time I have

### What Else I Learn In Parallel

- How to write a useful limitations section
- How startup, loading, and supply rejection expose hidden weaknesses
- How to separate topology problems from tuning problems

### Why This Supports My Project

This gives me the data needed for temperature coefficient, robustness, and practical usability.

### Typical Failure Notes

- Slope not flat: PTAT and CTAT weighting is wrong
- Too much supply dependence: poor supply rejection or loop behavior
- Startup issue: document it honestly and add startup discussion
- Low-voltage failure: usually a headroom limitation

### Move On Only When I Can Explain

- Which tuning changes mainly affect output value and which mainly affect temperature slope
- Whether my final weakness is a topology problem, a sizing problem, or a verification gap

## Final Deliverables

- Final schematic
- PTAT and CTAT derivation sheet
- Temperature sweep plots
- Supply sweep plots
- Startup or transient plots
- Near-zero TC tuning summary
- One limitations and future-work slide

## Expanded Sources

### Official Course Sources

- [Power Management Integrated Circuits - NPTEL course page](https://archive.nptel.ac.in/noc/courses/noc20/SEM1/noc20-ee08/)
- [Power Management Integrated Circuits syllabus](https://archive.nptel.ac.in/content/syllabus_pdf/108106159.pdf)
- [EE5390 Analog Integrated Circuit Design - Introduction](https://www.ee.iitm.ac.in/~nagendra/EE539/201001/handouts/ee539-intro.pdf)
- [EE5390 Assignment 7: Bandgap Reference](https://www.ee.iitm.ac.in/~nagendra/EE539/201001/assignments/assignment07.pdf)

### Design And Application Notes

- [Chapter 14: Voltage References - Analog Devices](https://wiki.analog.com/university/courses/electronics/text/chapter-14)
- [AN-82: Understanding and Applying Voltage References](https://www.analog.com/en/resources/app-notes/an-82f.html)
- [Bandgap Reference Calculator Tutorial - Analog Devices](https://www.analog.com/en/resources/design-notes/bandgap-reference-calculator-tutorial.html)
- [What is a voltage reference? - TI](https://www.ti.com/video/5784629312001)
- [Voltage reference overview for ADC - TI](https://www.ti.com/video/5783793652001)
- [Voltage Reference Introduction PDF - TI](https://www.ti.com/content/dam/videos/external-videos/de-de/3/3816841626001/5783793652001.mp4/subassets/voltage-reference-overview-presentation.pdf)

### Extra Academic Reading

- [EECS Berkeley Lecture 8: References](https://rfic.eecs.berkeley.edu/courses/ee240sp06/pdf/lect8.pdf)
- [Precision Techniques - Berkeley](https://people.eecs.berkeley.edu/~boser/courses/240B/lectures/M12%20Precision%20Techniques.pdf)

## Resume Line

Designed a PTAT/CTAT-based bandgap reference and evaluated temperature behavior, supply sensitivity, startup/transient characteristics, and practical reference trade-offs.
