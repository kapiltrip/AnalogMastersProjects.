# Two-Stage CMOS Op-Amp Plan

## Project Goal

Design and analyze a Miller-compensated two-stage CMOS op-amp with gain, unity-gain bandwidth, phase margin, slew rate, output swing, and load trade-off study.

## If I Am Starting From Zero

I should clear these basics before Week 1. If any of them are unclear, I should spend a day or two on them first.

- Voltage, current, resistance, capacitance, and power
- Ohm's law, KCL, and KVL
- RC charging, time constants, and the idea of a pole
- MOSFET basics: `VGS`, threshold voltage, saturation region, and overdrive
- Why `gm` and `ro` matter in analog design
- How to read Bode plots and step responses at a basic level
- How to run operating-point, AC, and transient simulations in the tool I use

## What I Must Learn Before I Finish

- What an op-amp is supposed to do in a feedback system
- Difference between open-loop and closed-loop behavior
- Why DC gain, `UGB`, phase margin, slew rate, swing, and load cannot be treated separately
- What loop gain, poles, zeros, gain crossover, and phase margin mean
- Why multistage op-amps become unstable
- Why Miller compensation is used
- What `Cc` does and when `Rc` may help
- Why a right-half-plane zero can appear
- How `UGB` relates to first-stage transconductance and `Cc`
- How slew rate relates to available current and `Cc`
- How a differential pair, current mirrors, and active loads set gain and biasing
- How the second gain stage affects gain, swing, and pole locations
- Why common-mode range and output swing are architecture-dependent
- What CMRR, PSRR, offset, and noise mean in a practical op-amp
- What overdrive voltage means and why it matters in sizing
- How AC and transient results should be cross-checked
- How load capacitance changes stability
- Why corners, mismatch, and layout can shift a design that looked fine schematically
- How to document trade-offs and limitations clearly

## Working Rule

For every study block:

1. Watch the lecture or read the note.
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

### Watch / Read

- Video: `Razavi Basic Circuits Lec 38: Introduction to Op Amps` by `Behzad Razavi (Long Kong)`. Link: `https://www.youtube.com/watch?v=KjQAz-U_-gk`
- Why this video: it gives the simplest system-level intuition for what an op-amp is supposed to do before transistor details start.
- Video: `Razavi Electronics 1, Lec 42, Op Amp Circuits 1` by `Behzad Razavi (Long Kong)`. Link: `https://www.youtube.com/watch?v=WzdmaSUCQGM`
- Why this video: it starts connecting ideal op-amp use to real circuit behavior and feedback usage.
- Video: `Razavi Electronics 1, Lec 43, Op Amp Circuits II` by `Behzad Razavi (Long Kong)`. Link: `https://www.youtube.com/watch?v=oWMBjDfRacc`
- Why this video: it extends the first lecture into practical closed-loop behavior and prepares me for nonidealities.
- [Basic Linear Design, Chapter 1 - The Op Amp](https://www.analog.com/media/en/training-seminars/design-handbooks/basic-linear-design/chapter1.pdf)
- [Analog Electronic Circuits syllabus - NPTEL](https://archive.nptel.ac.in/content/syllabus_pdf/108106188.pdf)

### What To Learn This Week

- What an op-amp is trying to do in a larger system
- Why open-loop gain matters even though op-amps are almost always used with feedback
- What negative feedback gives me and what it does not give me
- Why ideal-op-amp intuition is useful but incomplete
- What closed-loop behavior means physically
- What the main design specs are: DC gain, `UGB`, phase margin, slew rate, output swing, load capacitance, power
- Why the spec table must be frozen before transistor sizing begins

### What Else I Learn In Parallel

- Why system-level specifications should be frozen before transistor sizing
- Why gain, bandwidth, and stability must be discussed together
- Why the op-amp should be treated as a feedback block, not just a transistor stack

### Why This Supports My Project

This gives the system-level purpose of the two-stage op-amp before transistor-level design starts.

### What I Must Do Next

Prepare a spec sheet with:

- Supply voltage
- Load capacitance
- Target DC gain
- Target UGB
- Target phase margin
- Output swing
- Slew rate
- Power budget

I should freeze the specs before opening Cadence.

### Move On Only When I Can Explain

- Why op-amps are useful only because of feedback
- Why gain, bandwidth, and phase margin must be specified together

## Week 2: Stability And Compensation

### Watch / Read

- Video: `Nyquist criterion; Phase margin` by `nptelhrd`. Link: `https://www.youtube.com/watch?v=hDc4UD2iHio`
- Why this video: it gives the formal stability language needed to understand why a two-stage op-amp needs compensation.
- [TI Precision Labs - Op Amps](https://www.ti.com/video/series/precision-labs/ti-precision-labs-op-amps.html)
- [Stability - Introduction - TI](https://www.ti.com/video/4080235259001)
- [Circuit stability analysis and compensation schemes - TI](https://www.ti.com/lit/pdf/slypa06)
- [Compensation of Op Amps-I - P. E. Allen](https://www.pallen.ece.gatech.edu/Academic/ECE_6412/Spring_2004/L120-CompOpAmpsI%282UP%29.pdf)

### What To Learn This Week

- Why multiple poles make a feedback amplifier unstable
- What Nyquist and Bode stability viewpoints are each trying to tell me
- What gain crossover and phase margin mean
- How overshoot, ringing, and settling connect to phase margin
- Why a two-stage op-amp needs compensation
- What dominant-pole compensation is doing physically
- Why Miller compensation trades speed for stability
- Why compensation is a design choice and not just a capacitor added at the end

### What Else I Learn In Parallel

- Why Bode-plot intuition matters even before transistor-level design
- How overshoot, ringing, and phase margin connect
- Why compensation is a design choice, not just a capacitor added at the end

### Why This Supports My Project

This is the core theory I need to make the design stable and to explain the loop behavior properly.

### What I Must Do Next

Make a one-page sheet with:

- Open-loop poles
- Pole splitting idea
- Effect of compensation capacitor `Cc`
- Target phase margin
- Expected trade-off: larger `Cc` gives better stability but lower speed

### Move On Only When I Can Explain

- Why a two-stage op-amp becomes unstable without compensation
- What phase margin means physically in the time domain

## Week 3: Stage-Level Understanding

### Watch / Read

- Video: `Single stage opamp realization` by `nptelhrd`. Link: `https://www.youtube.com/watch?v=oSYd6sDdlnY`
- Why this video: it helps me understand what a single gain stage can and cannot do before moving to a multistage amplifier.
- Video: `The two Stage Opamp and Single Supply Operation` by `NPTEL-NOC IITM`. Link: `https://www.youtube.com/watch?v=ITYwPYcPeIA`
- Why this video: it connects stage roles, supply limitations, and headroom issues in the actual two-stage structure.
- [Integrated Circuit Operational Amplifiers - NPTEL summary PDF](https://archive.nptel.ac.in/content/storage2/courses/117106030/nptel-aic/opampsummary.pdf)
- [MT-035: Op Amp Inputs, Outputs, Single-Supply, and Rail-to-Rail Issues](https://www.analog.com/media/en/training-seminars/tutorials/mt-035.pdf)

### What To Learn This Week

- What the first stage of a two-stage op-amp is supposed to do
- What the second stage is supposed to do
- How a differential pair creates transconductance
- How current mirrors and active loads raise gain
- Why output resistance matters to total gain
- Why single-supply operation creates headroom limits
- Why gain, common-mode range, and output swing compete with each other
- Why the first transistor-level architecture decision already affects later stability and swing

### What Else I Learn In Parallel

- Why input common-mode range and output swing are not separate from architecture choice
- Why differential pair behavior matters for the first stage
- Why current mirrors and active loads shape both gain and bias stability

### Why This Supports My Project

I stop treating the op-amp as a black box and start understanding the role of each block.

### What I Must Do Next

Do a first-pass hand design:

- Choose topology
- Estimate stage gains
- Choose rough overdrive voltages
- Estimate current split between first and second stage

### Move On Only When I Can Explain

- What the first stage is doing that the second stage is not
- Why gain and swing begin to fight each other in a real transistor-level design

## Week 4: Main Two-Stage Miller-Compensated Design

### Watch / Read

- Video: `Two stage miller compensated opamp-1` by `nptelhrd`. Link: `https://www.youtube.com/watch?v=sjqObvsIpOA`
- Why this video: it introduces the standard compensated two-stage architecture and the role of the Miller capacitor.
- Video: `Two stage miller compensated opamp-2` by `nptelhrd`. Link: `https://www.youtube.com/watch?v=EoEx3sFvf58`
- Why this video: it continues the compensated design discussion and is useful for linking dominant-pole design to expected frequency behavior.
- [Analog IC Design - NPTEL course page](https://archive.nptel.ac.in/courses/117/106/117106030/)
- [NPTEL Analog IC Design syllabus](https://archive.nptel.ac.in/content/syllabus_pdf/117106030.pdf)
- [Integrated Circuit Operational Amplifiers - NPTEL summary PDF](https://archive.nptel.ac.in/content/storage2/courses/117106030/nptel-aic/opampsummary.pdf)

### What To Learn This Week

- The standard Miller-compensated two-stage CMOS op-amp structure
- Where `Cc` is connected and why
- How pole splitting is produced
- Why an `RHP` zero can appear
- When a nulling resistor `Rc` is useful
- How first-stage `gm` and `Cc` set the rough `UGB`
- How available current and `Cc` set the rough slew rate
- Why the load capacitance matters to the output pole
- How to convert these ideas into a first-pass hand design

### What Else I Learn In Parallel

- How `UGB`, `gm1`, and `Cc` are related
- Why slew rate depends on available charging current
- Why stage partitioning affects both gain and stability

### Why This Supports My Project

This is the main circuit-design week where the project becomes a real architecture and not just theory.

### What I Must Do Next

Create the schematic draft and calculate:

- Initial `Cc`
- First-stage transconductance target
- Expected UGB
- Estimated DC gain
- Expected load limitation

Then start Cadence schematic entry.

### Move On Only When I Can Explain

- Why `Cc` changes both stability and speed
- Why `UGB` and slew rate are tied to `gm`, current, and `Cc`

## Week 5: Limits, Alternatives, And Explanation Depth

### Watch / Read

- Video: `Two and three stage miller compensated opamps; Feedforward compensated opamp` by `nptelhrd`. Link: `https://www.youtube.com/watch?v=obEmLZo2Kww`
- Why this video: it puts the standard two-stage design in context and shows what more advanced compensation paths look like.
- Video: `The two Stage Opamp (contd)` by `NPTEL-NOC IITM`. Link: `https://www.youtube.com/watch?v=PCHsptMu12Y`
- Why this video: it adds continuation on the real two-stage structure and helps deepen the architecture-level explanation.
- Video: `The Two Stage Opamp contd` by `NPTEL-NOC IITM`. Link: `https://www.youtube.com/watch?v=rvPmI87J12o`
- Why this video: it reinforces the same architecture from another continuation and is useful when writing a clearer final explanation.
- Video: `Swing Limits of the Two Stage OTA` by `NPTEL-NOC IITM`. Link: `https://www.youtube.com/watch?v=vIZTDVzG204`
- Why this video: it directly addresses one of the most common practical misunderstandings, which is output swing versus gain.
- [MT-033: Voltage Feedback Op Amp Gain and Bandwidth](https://www.analog.com/media/en/training-seminars/tutorials/mt-033.pdf)
- [MT-042: Op Amp Common-Mode Rejection Ratio (CMRR)](https://www.analog.com/media/en/training-seminars/tutorials/mt-042.pdf)
- [MT-043: Op Amp Power Supply Rejection Ratio (PSRR) and Supply Voltages](https://www.analog.com/media/en/training-seminars/tutorials/MT-043.pdf)

### What To Learn This Week

- Why a standard two-stage op-amp is often the best learning architecture
- Where swing limits come from
- How gain, swing, stability, and power trade against each other
- What CMRR and PSRR mean once the amplifier core exists
- Why offset and noise matter even if they are not the first simulation priority
- How a two-stage op-amp compares with one-stage, folded-cascode, or feedforward-compensated alternatives
- What a realistic limitations section should say if specs tighten later
- How to explain architecture choice clearly in viva or review

### What Else I Learn In Parallel

- Why CMRR and PSRR matter once the core amplifier is working
- Why architecture choice affects explanation quality in viva and report
- Why a design can meet gain and still fail the real application

### Why This Supports My Project

This is the material that makes my explanation mature in viva, review, and interview settings.

### What I Must Do Next

Add a comparison page to the report:

- Chosen architecture
- Why it was chosen
- Its known limits
- What a better architecture would be if specs changed

### Move On Only When I Can Explain

- Why the standard two-stage architecture is good enough for this project
- Which limitations come from architecture choice and which come from sizing

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

### Read Also

- [Stability - Lab - TI](https://www.ti.com/video/4080346918001)
- [TI Precision Labs - Op Amps](https://www.ti.com/video/series/precision-labs/ti-precision-labs-op-amps.html)
- [Circuit stability analysis and compensation schemes - TI](https://www.ti.com/lit/pdf/slypa06)

### What To Learn This Week

- How to check the DC operating point and transistor regions
- How to measure open-loop gain and phase correctly
- How to run a unity-gain closed-loop test
- How to compare AC phase margin with transient overshoot and ringing
- How to measure slew rate and output swing
- How to run load-capacitance and supply sweeps
- How to tell whether a failure comes from compensation, bias current, headroom, or load
- How to document a design iteration so the next change is based on evidence
- When corners or mismatch checks are worth adding for a stronger final report

### What Else I Learn In Parallel

- How to document design iterations clearly
- Why load sweeps matter even if the nominal design looks stable
- How to write a defensible limitations section

### Why This Supports My Project

This is where theory becomes measured design data.

### Typical Failure Notes

- Low phase margin: increase or re-evaluate `Cc`, check non-dominant poles
- Low gain: revisit output resistance and current levels
- Poor slew rate: check bias current and `Cc` trade-off
- Poor swing: check headroom, not just gain
- Load instability: output pole moved too low

### Move On Only When I Can Explain

- Whether a bad result came from compensation, biasing, headroom, or load
- Why AC and transient results must agree before I trust the design

## Final Deliverables

- Spec table
- Hand calculations
- Final schematic
- Gain and phase plot
- Transient and slew-rate plots
- Load sweep
- One trade-off summary slide

## Expanded Sources

### Official Course Sources

- [Analog IC Design - NPTEL course page](https://archive.nptel.ac.in/courses/117/106/117106030/)
- [NPTEL Analog IC Design syllabus](https://archive.nptel.ac.in/content/syllabus_pdf/117106030.pdf)
- [Analog Electronic Circuits syllabus - NPTEL](https://archive.nptel.ac.in/content/syllabus_pdf/108106188.pdf)
- [Integrated Circuit Operational Amplifiers - NPTEL summary PDF](https://archive.nptel.ac.in/content/storage2/courses/117106030/nptel-aic/opampsummary.pdf)

### Stability And Compensation Sources

- [TI Precision Labs - Op Amps](https://www.ti.com/video/series/precision-labs/ti-precision-labs-op-amps.html)
- [Stability - Introduction - TI](https://www.ti.com/video/4080235259001)
- [Stability - Lab - TI](https://www.ti.com/video/4080346918001)
- [Circuit stability analysis and compensation schemes - TI](https://www.ti.com/lit/pdf/slypa06)
- [Compensation of Op Amps-I - P. E. Allen](https://www.pallen.ece.gatech.edu/Academic/ECE_6412/Spring_2004/L120-CompOpAmpsI%282UP%29.pdf)

### Op-Amp Device And Spec Notes

- [Basic Linear Design, Chapter 1 - The Op Amp](https://www.analog.com/media/en/training-seminars/design-handbooks/basic-linear-design/chapter1.pdf)
- [MT-033: Voltage Feedback Op Amp Gain and Bandwidth](https://www.analog.com/media/en/training-seminars/tutorials/mt-033.pdf)
- [MT-035: Op Amp Inputs, Outputs, Single-Supply, and Rail-to-Rail Issues](https://www.analog.com/media/en/training-seminars/tutorials/mt-035.pdf)
- [MT-042: Op Amp Common-Mode Rejection Ratio (CMRR)](https://www.analog.com/media/en/training-seminars/tutorials/mt-042.pdf)
- [MT-043: Op Amp Power Supply Rejection Ratio (PSRR) and Supply Voltages](https://www.analog.com/media/en/training-seminars/tutorials/MT-043.pdf)

## Resume Line

Designed and analyzed a Miller-compensated two-stage CMOS op-amp; evaluated gain, UGB, phase margin, slew rate, load-capacitance trade-offs, and stability behavior with supporting simulations.
