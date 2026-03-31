# Learning-Centric Master's Plan: Bandgap Voltage Reference

## Project Goal

- Learn PTAT, CTAT, bandgap derivation, startup, regulation, mismatch, and verification in the right order.
- Build one defensible bandgap reference at the end.
- Treat the project as a learning project first and a final-circuit project second.

## Working Rules

- Do not move to the next week if the current week has no artifact.
- Do not commit to a topology before freezing provisional `VDD`, `Vref`, temperature range, and load assumption.
- Do not treat room-temperature `Vref` as success.
- Do not postpone startup until the end.
- Change only one major ratio or block at a time during tuning.
- Keep one design log with: change made, reason, expected effect, measured effect.
- Keep layout optional until the pre-layout schematic is credible.

## Final Circuit Choice

- Final target: Brokaw-style or equivalent closed-loop PTAT-CTAT bandgap reference.
- Core output target: classic bandgap-level reference unless `VDD` forces a sub-1-V branch.
- Add explicit startup.
- Add output buffer only if load requirements force it.
- Keep trim and curvature correction optional until the base design is working.

## Why This Circuit

- Teaches why `VBE` is CTAT.
- Teaches why `DeltaVBE = VT*ln(N)` is PTAT.
- Teaches resistor-ratio and area-ratio design.
- Teaches startup behavior and false zero-current equilibrium.
- Teaches line regulation, load regulation, PSRR, and noise.
- Teaches corners and Monte Carlo in a ratio-sensitive analog block.
- Teaches layout matching in a way that is easier to justify than random layout work.

## What I Must Learn

- Why `VBE` alone is not a good reference.
- Why `DeltaVBE` is PTAT.
- How `Vref = VBE + k*DeltaVBE` is built.
- How resistor ratio sets `k`.
- How emitter-area ratio or current-density ratio sets `ln(N)`.
- What first-order temperature cancellation means.
- Why startup is a real design problem.
- Why a reference can have good tempco and still have poor line regulation or PSRR.
- Why corners and Monte Carlo tell different things.
- Why layout can disturb ratios and degrade accuracy.

## Topology Options To Study

### PTAT + CTAT Concept Block

- Use first to understand the equation.
- Learn: `VBE`, `DeltaVBE`, resistor ratio, area ratio.
- Do not use as the final project by itself.

### Brokaw-Style Bandgap

- Recommended default final choice.
- Learn: canonical bandgap loop, startup, practical robustness.
- Use when `VDD` is comfortably above the bandgap voltage.

### Op-Amp-Assisted Bandgap

- Use only if regulation or buffering becomes a central project goal.
- Learn: control of internal operating points, offset sensitivity, PSRR trade-offs.
- Do not choose first if the goal is a finishable learning project.

### Sub-1-V / Fractional Bandgap

- Use only if `VDDmin` forces it.
- Learn: low-voltage operation, headroom limits, harder startup.
- Do not choose by default.

### Recommended Final Structure

- Brokaw-style core.
- Explicit startup branch.
- Optional output buffer.
- Optional trim only after the base design is stable.

## Software Learning Plan

- Main idea: use software to understand the bandgap, not just to produce final plots.

### Week 1: Learn The Basic Simulation Flow

- Learn: how to draw simple BJT, diode, and resistor circuits in LTspice, TINA-TI, Cadence, or xschem/ngspice.
- Learn: how to run operating-point, DC, and temperature sweeps.
- Why: this is the minimum needed to see `VBE` and `DeltaVBE` behavior instead of treating the equations as theory only.

### Week 2: Learn Parameter Sweeps And Equation Checking

- Learn: how to change area ratio, resistor ratio, and bias conditions and compare the results.
- Learn: how to check whether the simulated trend matches the expected `PTAT` or `CTAT` direction.
- Why: bandgap design depends on ratios, so the software must help you verify cause and effect clearly.

### Week 3: Learn How To Build The Full Schematic

- Learn: how to enter the full bandgap core in your main tool.
- Learn: how to bias it properly and check whether the intended operating point exists.
- Why: this is the step where the theory becomes a real circuit rather than a set of disconnected notes.

### Week 4: Learn How To Test Startup And Practical Behavior

- Learn: how to run transient startup tests with different supply ramps and temperatures.
- Learn: how to run basic line-regulation and load-regulation sweeps.
- Why: a bandgap is only useful if it starts correctly and stays stable when supply or load changes.

### Week 5: Learn How To Judge Robustness

- Learn: how to run corners, Monte Carlo, and comparison plots if your tool flow supports them.
- Learn: how to keep a simple simulation log with the change made, the reason, and the result.
- Why: this is what turns software use into real design learning instead of random trial and error.

## How To Learn From Videos

For every lecture:

1. Watch once for the main idea.
2. Write a half-page summary.
3. Extract 3 to 5 equations or design rules.
4. Redraw one circuit or one derivation step from memory.
5. Simulate one small related example.
6. Write one confusion point.
7. Revisit only that confusion.

## Resource Stack

### Resource Reliability Note

- Several NPTEL lecture links are mirror links.
- If a mirror link fails, use the official course page or the lecture title in the `References` section and search that exact lecture title.
- If a Razavi search link shifts, use the search phrase already written in the file.
- Do not let one broken mirror block progress; the lecture title and topic sequence are the real anchors.

### NPTEL + Razavi: Bandgap Fundamentals

- NPTEL Power Management ICs, Introduction to Bandgap Voltage References, PTAT and CTAT voltage: `https://www.digimat.in/nptel/courses/video/108106159/L07.html`
- NPTEL Power Management ICs, Adding PTAT and CTAT Voltages: `https://kristujayanti.digimat.in/nptel/courses/video/108106159/L08.html`
- NPTEL Power Management ICs, Bandgap Voltage Reference Circuit, Brokaw Bandgap Circuit: `https://hits.digimat.in/nptel/courses/video/108106159/L09.html`
- NPTEL Power Management ICs, Sub-1-volt Bandgap Circuit: `https://kristujayanti.digimat.in/nptel/courses/video/108106159/L10.html`
- NPTEL Analog Electronic Circuits, The Bandgap Reference - Part 1: `https://www.digimat.in/nptel/courses/video/108106188/L59.html`
- NPTEL Analog Electronic Circuits, The Bandgap Reference - Part 2: `https://www.digimat.in/nptel/courses/video/108106188/L60.html`
- Razavi bandgap search: `https://www.youtube.com/results?search_query=Razavi+bandgap+reference`
- Razavi voltage reference search: `https://www.youtube.com/results?search_query=Razavi+voltage+reference`

### NPTEL: PTAT, Supply Sensitivity, Fractional Bandgap

- NPTEL Analog IC Design, Generating PTAT and constant MOS gm bias currents: `https://www.digimat.in/nptel/courses/video/117106030/L53.html`
- NPTEL Analog IC Design, Reducing supply sensitivity; Bandgap voltage reference: `https://www.digimat.in/nptel/courses/video/117106030/L54.html`
- NPTEL Analog IC Design, Fractional bandgap reference; Low dropout regulator: `https://www.digimat.in/nptel/courses/video/117106030/L55.html`

### Reliable Non-Video Resources

- Analog Devices, Chapter 14: Voltage References: `https://wiki.analog.com/university/courses/electronics/text/chapter-14`
- Analog Devices, AN-82: Understanding and Applying Voltage References: `https://www.analog.com/en/resources/app-notes/an-82f.html`
- Analog Devices, Bandgap Reference Calculator Tutorial: `https://www.analog.com/en/resources/design-notes/bandgap-reference-calculator-tutorial.html`
- Analog Devices, The Band-Gap Voltage Reference activity: `https://wiki.analog.com/university/courses/eps/band-gap-regulator`
- TI, What is a voltage reference?: `https://www.ti.com/video/5784629312001`
- TI application report with Brokaw bandgap discussion: `https://www.ti.com/lit/an/slla065/slla065.pdf`
- TI voltage reference e-book landing page: `https://www.ti.com/lit/pdf/slpy003`

### Tool Links

- xschem simulation manual: `https://xschem.sourceforge.io/stefan/xschem_man/simulation.html`
- ngspice docs: `https://ngspice.sourceforge.io/docs.html`
- SKY130 docs: `https://skywater-pdk.readthedocs.io/en/main/`
- Magic docs: `https://magicvlsi.wordpress.com/documentation/`
- KLayout docs: `https://www.klayout.de/doc/`
- Open-source analog flow: `https://www.opencircuitdesign.com/analog_flow/`

## Learning Modules

### Module 1: PTAT And CTAT Basics

- Learn:
  - why `VBE` falls with temperature,
  - why `DeltaVBE` rises with temperature,
  - why adding them can flatten temperature dependence.
- Use:
  - NPTEL PMIC lectures 7 and 8,
  - NPTEL Bandgap Reference Part 1,
  - Razavi bandgap search links.
- Do after learning:
  - derive `DeltaVBE = VT*ln(N)`,
  - write the sign of each temperature coefficient,
  - simulate two BJTs or diode-connected devices with area ratio.
- Proof of learning:
  - explain why `DeltaVBE` is PTAT without reading notes.

### Module 2: First-Order Bandgap Derivation

- Learn:
  - `Vref = VBE + k*DeltaVBE`,
  - resistor ratio selection,
  - area ratio selection,
  - first-order cancellation.
- Use:
  - NPTEL Bandgap Reference Part 1 and Part 2,
  - ADI Chapter 14,
  - AN-82,
  - Bandgap Calculator Tutorial.
- Do after learning:
  - derive a first-pass resistor ratio,
  - choose first-pass area ratio `N`,
  - estimate nominal `Vref`.
- Proof of learning:
  - compute `k` and explain where it comes from physically.

### Module 3: Topology Choice

- Learn:
  - Brokaw-style topology,
  - op-amp-assisted topology,
  - sub-1-V branch,
  - when each is justified.
- Use:
  - NPTEL PMIC lecture 9,
  - NPTEL Analog IC Design lecture 54,
  - NPTEL Analog IC Design lecture 55.
- Do after learning:
  - choose the final topology,
  - write what is being rejected,
  - write what risk is avoided by not choosing the harder branch.
- Proof of learning:
  - justify why the chosen topology is the best learning-first path.

### Module 4: Startup

- Learn:
  - why zero-current state can be stable,
  - how startup circuitry breaks that false equilibrium,
  - why ramp-rate testing matters.
- Use:
  - NPTEL Bandgap Reference Part 2,
  - Brokaw-bandgap resources,
  - ADI Voltage References chapter.
- Do after learning:
  - sketch one startup path,
  - predict what happens with and without startup,
  - run slow and fast ramp tests.
- Proof of learning:
  - explain why startup cannot be left for the end.

### Module 5: Temperature Tuning

- Learn:
  - how resistor ratio and current density affect slope,
  - why zero slope at one point is not perfect over all temperature,
  - what first-order cancellation misses.
- Use:
  - NPTEL PMIC lectures 7 to 9,
  - NPTEL Analog IC Design lecture 54,
  - Bandgap Calculator Tutorial.
- Do after learning:
  - run `Vref(T)`,
  - decide whether PTAT term is too strong or too weak,
  - retune ratio in small steps.
- Proof of learning:
  - explain the direction of tuning before rerunning simulation.

### Module 6: Line Regulation, Load Regulation, PSRR, Noise

- Learn:
  - why good tempco is not enough,
  - how supply sensitivity appears,
  - how load affects a reference,
  - why PSRR and noise matter in a usable reference.
- Use:
  - NPTEL Analog IC Design lecture 54,
  - TI voltage reference intro,
  - AN-82.
- Do after learning:
  - run `Vref(VDD)` sweep,
  - run load sweep,
  - set up PSRR bench,
  - set up noise bench if supported.
- Proof of learning:
  - explain which mechanism dominates each error trend.

### Module 7: Corners, Monte Carlo, And Layout

- Learn:
  - corners versus mismatch,
  - why resistor and BJT mismatch matter,
  - why matching layout matters more than cosmetic layout.
- Use:
  - ADI Voltage References chapter,
  - NPTEL PTAT/bandgap lectures,
  - tool documentation if layout is attempted.
- Do after learning:
  - run corners,
  - run Monte Carlo,
  - identify dominant spread source,
  - only then consider trim or larger device area.
- Proof of learning:
  - explain why corners and Monte Carlo answer different questions.

## 5-Week Learning Plan

### Week 1: Understand PTAT And CTAT Properly

- Learn: why `VBE` is `CTAT` and why `DeltaVBE` is `PTAT`.
- Learn: why adding a `PTAT` term to a `CTAT` term can flatten temperature dependence.
- Why: this is the basic idea behind every bandgap reference, so nothing else will make sense until this is clear.

### Week 2: Learn The Bandgap Equation And The Ratios

- Learn: how `Vref = VBE + k*DeltaVBE` is formed.
- Learn: how resistor ratio sets `k` and how device area ratio sets `ln(N)`.
- Why: this is the main design logic of the circuit, and it explains where the reference voltage actually comes from.

### Week 3: Learn The Real Circuit Structure

- Learn: the difference between a concept-level `PTAT + CTAT` block, a Brokaw-style bandgap, and lower-voltage variants.
- Learn: why startup is necessary and why zero-current equilibrium is a real problem.
- Why: this helps you choose a topology that is simple enough to learn from but still realistic enough to defend.

### Week 4: Learn How Theory Becomes A Working Schematic

- Learn: how the hand-derived ratios turn into resistor values, area ratios, bias currents, and a first schematic.
- Learn: how to read the temperature trend and decide whether the `PTAT` contribution is too strong or too weak.
- Why: this is the stage where bandgap design stops being a derivation exercise and starts becoming circuit intuition.

### Week 5: Learn What Makes The Reference Practically Usable

- Learn: the meaning of line regulation, load regulation, `PSRR`, corners, and Monte Carlo in a bandgap context.
- Learn: what layout and mismatch can disturb even when the ideal equation looks correct.
- Why: a reference is not judged only by one room-temperature output value; it is judged by whether it stays credible across variation and use conditions.

## What To Produce After Every Major Resource Block

- One concept note.
- One derivation sheet.
- One small simulation.
- One confusion log entry.

## Core Equations

- `DeltaVBE = VT*ln(N)`
- `Vref = VBE + k*DeltaVBE`
- first-order target: `dVref/dT ~= 0`
- `k` is usually set by resistor ratio
- area ratio or current-density ratio sets `ln(N)`
- startup must remove the zero-current operating point

## Final Deliverables

- Learning log.
- PTAT/CTAT note.
- Bandgap derivation note.
- Topology decision note.
- Spec note.
- Hand-design worksheet.
- Final schematic.
- Startup note and startup plots.
- `Vref(T)` plot and tempco note.
- `Vref(VDD)` plot and line-regulation note.
- Load-regulation plot.
- PSRR plot.
- Optional noise plot.
- Corner table.
- Monte Carlo histogram and spread note.
- Optional layout/post-layout note.

## Reliability Checks

- After Week 4: the provisional spec and topology must be frozen enough to prevent random branch changes.
- After Week 6: the baseline schematic must produce a meaningful nominal `Vref`.
- After Week 8: startup must already work for the chosen stress cases.
- After Week 10: line regulation and load behavior must already be known.
- After Week 13: mismatch spread must already be quantified.
- After Week 16: the pre-layout design must be frozen and reproducible.
- After Week 20: the project must read like one coherent reference-design story, not a pile of separate benches.

## References

### NPTEL Bandgap And PMIC Links

- `https://onlinecourses.nptel.ac.in/noc24_ee24/preview`
- `https://onlinecourses.nptel.ac.in/noc23_ee77/preview`
- `https://onlinecourses.nptel.ac.in/noc26_ee66/preview`
- `https://www.digimat.in/nptel/courses/video/108106159/L07.html`
- `https://kristujayanti.digimat.in/nptel/courses/video/108106159/L08.html`
- `https://hits.digimat.in/nptel/courses/video/108106159/L09.html`
- `https://kristujayanti.digimat.in/nptel/courses/video/108106159/L10.html`
- `https://www.digimat.in/nptel/courses/video/108106188/L59.html`
- `https://www.digimat.in/nptel/courses/video/108106188/L60.html`
- `https://www.digimat.in/nptel/courses/video/117106030/L53.html`
- `https://www.digimat.in/nptel/courses/video/117106030/L54.html`
- `https://www.digimat.in/nptel/courses/video/117106030/L55.html`

### Razavi Search Links

- `https://www.youtube.com/results?search_query=Razavi+bandgap+reference`
- `https://www.youtube.com/results?search_query=Razavi+voltage+reference`

### Other Reliable Resources

- `https://wiki.analog.com/university/courses/electronics/text/chapter-14`
- `https://www.analog.com/en/resources/app-notes/an-82f.html`
- `https://www.analog.com/en/resources/design-notes/bandgap-reference-calculator-tutorial.html`
- `https://wiki.analog.com/university/courses/eps/band-gap-regulator`
- `https://www.ti.com/video/5784629312001`
- `https://www.ti.com/lit/an/slla065/slla065.pdf`
- `https://www.ti.com/lit/pdf/slpy003`

### Tool Links

- `https://xschem.sourceforge.io/stefan/xschem_man/simulation.html`
- `https://ngspice.sourceforge.io/docs.html`
- `https://skywater-pdk.readthedocs.io/en/main/`
- `https://magicvlsi.wordpress.com/documentation/`
- `https://www.klayout.de/doc/`
- `https://www.opencircuitdesign.com/analog_flow/`
