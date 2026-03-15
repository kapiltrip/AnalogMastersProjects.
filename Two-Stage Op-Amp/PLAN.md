# Two-Stage CMOS Op-Amp Plan

## Project Goal

Design and analyze a Miller-compensated two-stage CMOS op-amp with gain, unity-gain bandwidth, phase margin, slew rate, output swing, and load trade-off study.

## Working Rule

For every study block:

1. Watch the lecture.
2. Make 1-page handwritten notes.
3. Do 1 derivation or design sheet.
4. Do 1 simulation block.
5. Write what failed and why.

## Suggested Folder Use

- `notes/`: handwritten scan summaries, derivations, viva points
- `design/`: hand calculations, sizing sheets, topology decisions
- `simulations/`: Cadence plots, testbenches, sweeps
- `references/`: PDFs, lecture lists, copied links
- `report/`: report draft, slides, final summary

## Week 1: Op-Amp Intuition First

### Watch

- [Razavi Basic Circuits Lec 38: Introduction to Op Amps](https://www.youtube.com/watch?v=KjQAz-U_-gk)
- [Razavi Electronics 1, Lec 42: Op Amp Circuits 1](https://www.youtube.com/watch?v=WzdmaSUCQGM)
- [Razavi Electronics 1, Lec 43: Op Amp Circuits II](https://www.youtube.com/watch?v=oWMBjDfRacc)

### What You Gain

- What an op-amp is trying to do
- Why high open-loop gain matters
- How feedback makes the circuit useful
- What closed-loop behavior means

### Why It Supports The Project

This gives the system-level purpose of the two-stage op-amp before transistor-level design starts.

### Do Next

Prepare a spec sheet with:

- Supply voltage
- Load capacitance
- Target DC gain
- Target UGB
- Target phase margin
- Output swing
- Slew rate
- Power budget

Freeze the specs before opening Cadence.

## Week 2: Stability And Compensation

### Watch

- [Nyquist Criterion; Phase Margin](https://www.youtube.com/watch?v=hDc4UD2iHio)
- [NPTEL Analog IC Design Playlist](https://www.youtube.com/playlist?list=PLbMVogVj5nJRlMz5diOg9wBizaU6-egJc)
- [Razavi: Stability and Frequency Compensation Part 1](https://www.youtube.com/watch?v=rEM0tW7FzUA)

### Optional Add-On

- [Razavi Electronics 2 Lec 43: Intro to Instability in Feedback](https://www.youtube.com/watch?v=kC8FYL8gr3E)
- [Razavi Electronics 2 Lec 44: Bode's Rules, Stability Condition](https://www.youtube.com/watch?v=UKf4tVoULlo)

### What You Gain

- Why two-stage op-amps are unstable without care
- What phase margin means
- Why Miller compensation is used
- How compensation trades speed for stability

### Why It Supports The Project

This is the core theory needed to make the design stable and to explain the loop behavior properly.

### Do Next

Make a one-page sheet with:

- Open-loop poles
- Pole splitting idea
- Effect of compensation capacitor `Cc`
- Target phase margin
- Expected trade-off: larger `Cc` gives better stability but lower speed

## Week 3: Stage-Level Understanding

### Watch

- [Single Stage Op-Amp Realization](https://www.youtube.com/watch?v=oSYd6sDdlnY)
- [The Two Stage Opamp and Single Supply Operation](https://www.youtube.com/watch?v=ITYwPYcPeIA)

### What You Gain

- What the first stage does
- What the second stage does
- Why single-supply operation changes headroom limits
- How gain and swing begin to fight each other

### Why It Supports The Project

You stop treating the op-amp as a black box and start understanding the role of each block.

### Do Next

Do a first-pass hand design:

- Choose topology
- Estimate stage gains
- Choose rough overdrive voltages
- Estimate current split between first and second stage

## Week 4: Main Two-Stage Miller-Compensated Design

### Watch

- [Two Stage Miller Compensated Opamp-1](https://www.youtube.com/watch?v=sjqObvsIpOA)
- [Two Stage Miller Compensated Opamp-2](https://www.youtube.com/watch?v=EoEx3sFvf58)

### What You Gain

- Standard two-stage architecture
- How Miller compensation is inserted
- How the dominant pole is created
- Why a zero may appear
- How unity-gain behavior is shaped

### Why It Supports The Project

This is the main circuit-design week where the project becomes a real architecture and not just theory.

### Do Next

Create the schematic draft and calculate:

- Initial `Cc`
- First-stage transconductance target
- Expected UGB
- Estimated DC gain
- Expected load limitation

Then start Cadence schematic entry.

## Week 5: Limits, Alternatives, And Explanation Depth

### Watch

- [Two and Three Stage Miller Compensated Opamps; Feedforward Compensated Opamp](https://www.youtube.com/watch?v=obEmLZo2Kww)
- [The Two Stage Opamp (contd)](https://www.youtube.com/watch?v=PCHsptMu12Y)
- [The Two Stage Opamp contd](https://www.youtube.com/watch?v=rvPmI87J12o)
- [Swing Limits of the Two Stage OTA](https://www.youtube.com/watch?v=vIZTDVzG204)

### What You Gain

- Why the standard two-stage op-amp is chosen
- Where swing limits come from
- How it compares with more advanced compensated structures
- Which practical trade-offs define a good design

### Why It Supports The Project

This is the material that makes your explanation mature in viva, review, and interview settings.

### Do Next

Add a comparison page to the report:

- Chosen architecture
- Why it was chosen
- Its known limits
- What a better architecture would be if specs changed

## Week 6: Simulation And Debugging

### Run

- DC operating point
- Open-loop gain and phase
- Unity-gain closed-loop test
- Step response
- Slew rate
- Output swing
- Load capacitance sweep
- Supply sweep
- Corner check if time permits

### What You Gain

You generate the actual project evidence for the final report.

### Why It Supports The Project

This is where theory becomes measured design data.

### Typical Failure Notes

- Low phase margin: increase or re-evaluate `Cc`, check non-dominant poles
- Low gain: revisit output resistance and current levels
- Poor slew rate: check bias current and `Cc` trade-off
- Poor swing: check headroom, not just gain
- Load instability: output pole moved too low

## Final Deliverables

- Spec table
- Hand calculations
- Final schematic
- Gain and phase plot
- Transient and slew-rate plots
- Load sweep
- One trade-off summary slide

## Primary References

- [NPTEL Analog IC Design Course](https://onlinecourses.nptel.ac.in/noc26_ee66/preview)
- [Shanthi Pavan Analog Electronic Circuits Course Details](https://nptel.ac.in/courses/108106188)
- [Razavi Electronics 1, Lec 45: Op Amp Nonidealities II](https://www.youtube.com/watch?v=VN8SeVA8LnU)

## Resume Line

Designed and analyzed a Miller-compensated two-stage CMOS op-amp; evaluated gain, UGB, phase margin, slew rate, and load-capacitance trade-offs.
