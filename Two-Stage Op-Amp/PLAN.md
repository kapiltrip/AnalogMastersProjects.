# Learning-Centric Master's Plan: Miller-Compensated Two-Stage CMOS Op-Amp

## 5-Week Learning Plan

### Week 1: Understand Feedback And Stability

- Learn: open-loop versus closed-loop behavior, loop gain, gain crossover, and phase margin.
- Learn: why a high-gain amplifier can still behave badly in feedback.
- Why: stability is the main reason a two-stage op-amp is interesting and worth studying carefully.

### Week 2: Learn The Core Analog Blocks

- Learn: `gm`, `ro`, overdrive, current mirrors, and differential pair behavior.
- Learn: how gain, headroom, and bias current affect amplifier behavior.
- Why: these are the building blocks of the final op-amp, so they must be understood before compensation is studied in detail.

### Week 3: Learn The Two-Stage Structure

- Learn: why a second stage is added, why it creates extra poles, and what Miller compensation is doing.
- Learn: what `Cc` does, why an `RHP` zero appears, and why `Rc` may help.
- Why: this is the main design idea behind the final circuit.

### Week 4: Learn How The Design Becomes A Schematic

- Learn: how gain, `UGB`, phase margin, slew rate, and load connect to first-pass sizing.
- Learn: how the full transistor-level schematic is built and biased.
- Why: this is where the project moves from theory into actual design work.

### Week 5: Learn What Makes The Op-Amp Practically Usable

- Learn: how to judge gain, `UGB`, phase margin, slew rate, swing, and load behavior together.
- Learn: why AC and transient results must agree before the design can be trusted.
- Why: a usable op-amp is judged by closed-loop behavior, not only by one good plot.

## Software Learning Plan

### Week 1: Learn The Basic Simulation Flow

- Learn: how to build simple amplifier circuits in LTspice, TINA-TI, Cadence, or xschem/ngspice.
- Learn: how to run operating-point, AC, and transient simulations.
- Why: this is the minimum needed to study gain, poles, and time-domain behavior.

### Week 2: Learn AC And Transient Checking

- Learn: how to generate Bode plots, phase-margin plots, and step responses.
- Learn: how to compare overshoot and ringing against phase margin.
- Why: stability learning is strongest when AC and transient results are checked together.

### Week 3: Learn Full Schematic Entry

- Learn: how to enter the full two-stage op-amp schematic and bias network in the main tool.
- Learn: how to verify the intended operating point and device regions.
- Why: this is where the full design becomes testable.

### Week 4: Learn Compensation And Load Sweeps

- Learn: how to sweep `Cc`, `Rc`, and `CL` and compare the effect on gain, `UGB`, and phase margin.
- Learn: how to test slew rate and output swing in transient simulation.
- Why: compensation is understood properly only when parameter changes are tied to clear response changes.

### Week 5: Learn Robustness And Documentation

- Learn: how to compare multiple simulation runs and keep a clean design log.
- Learn: how to summarize what changed, why it changed, and what result improved or became worse.
- Why: this turns software use into structured analog design learning instead of random tuning.
