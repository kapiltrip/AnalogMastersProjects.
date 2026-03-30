# Learning-Oriented Master's Project Plan: Miller-Compensated Two-Stage CMOS Op-Amp

## Project Statement

Design, size, simulate, verify, and document a Miller-compensated two-stage CMOS op-amp, but treat the project first as a learning project and only then as a final circuit project.

The real goal is not just to "finish an op-amp."

The real goal is to learn, in the correct order:

1. feedback and why open-loop gain is not enough,
2. MOS small-signal behavior and biasing,
3. differential pair operation,
4. frequency response, poles, zeros, and phase margin,
5. why a second stage helps and why it creates a stability problem,
6. how Miller compensation fixes one problem while creating other trade-offs,
7. how to verify an analog design correctly in simulation,
8. how to explain every design choice in a thesis or viva.

## This Is A Learning-Centric Project

This file is written for a learning-centric master's project.

That means:

- resources matter,
- concept order matters,
- what I learned each week matters,
- why I chose one circuit over another matters,
- software choice matters because it affects what I can realistically finish,
- final plots matter, but only after the conceptual chain is solid.

So this plan is built around four questions:

1. What exactly must I learn?
2. Which resource should teach it?
3. What should I do right after watching or reading?
4. Which circuit or simulation task proves that I actually learned it?

## What This Project Should Teach Me

By the end of the project, I should be able to explain all of the following in my own words:

- why a differential amplifier becomes useful only under feedback,
- why a single-stage amplifier is not always enough,
- how gain, bandwidth, phase margin, slew rate, swing, and power are coupled,
- where the dominant pole and non-dominant poles come from in a two-stage op-amp,
- what the Miller capacitor is doing physically,
- why an uncompensated Miller path can create a right-half-plane zero,
- when a nulling resistor is useful,
- how to extract loop gain correctly without breaking DC bias,
- why AC and transient results must agree,
- why layout and parasitics can move poles and change stability.

## Why This Final Circuit Is The Right Choice

The recommended final circuit for this project is still a Miller-compensated two-stage CMOS op-amp.

It is the best learning-centric choice because it forces me to understand:

- differential pair behavior,
- active loads and current mirrors,
- gain staging,
- output swing limits,
- stability and phase margin,
- Miller compensation,
- slew-rate limitation,
- load sensitivity,
- verification discipline.

If the project were only a single-stage op-amp, I would learn less about compensation and stability.

If the project were a very advanced low-voltage, rail-to-rail, gain-boosted, or fully differential op-amp from the start, the learning risk would be too high and the schedule would become fragile.

So the correct strategy is:

1. learn the building blocks,
2. study simpler op-amp forms,
3. then design the final two-stage Miller-compensated op-amp.

## Circuit Choices Before Final Freeze

This section answers the question: what circuit path should I study, and why?

### Option 1: Differential Pair Only

Use this first as a learning block, not as the final project.

Why study it:

- it teaches transconductance,
- it teaches differential versus common-mode behavior,
- it teaches current steering,
- it teaches active-load intuition.

Why it is not enough as the final project:

- gain is limited,
- output swing and drive are limited,
- compensation story is weak,
- thesis story is too small for a strong analog design project.

### Option 2: Single-Stage Op-Amp

Use this as an intermediate learning circuit.

Good sub-options:

- simple differential pair with active load,
- telescopic cascode,
- folded cascode.

Why study it:

- it gives one clean high-gain stage,
- it teaches gain versus swing trade-offs,
- it teaches biasing more clearly than a full two-stage design,
- it is the bridge between basic amplifier stages and the final op-amp.

Why it is not the best final learning target:

- it does not force as deep a compensation story,
- it will not teach multistage stability as strongly as the two-stage design.

### Option 3: Telescopic Cascode

Study this if I want to understand high gain with one stage.

What it teaches:

- high output resistance,
- gain through cascoding,
- limited swing,
- biasing sensitivity,
- why it is often used as a first stage.

From the NPTEL op-amp summary, telescopic cascode is relevant for:

- capacitive loads,
- low swing circuits,
- switched-capacitor circuits,
- first stage of a two-stage op-amp,
- high-gain design in fine-line processes.

### Option 4: Folded Cascode

Study this if I want a wider view of one-stage architectures.

What it teaches:

- swing improvement relative to telescopic,
- a different headroom trade-off,
- why the circuit is usually noisier and slower than telescopic,
- extra internal poles and a more involved bias structure.

From the NPTEL op-amp summary, folded cascode generally gives:

- higher swing,
- higher noise and offset,
- lower speed than telescopic,
- a low-frequency pole at the drain of the input pair.

### Recommended Final Choice

The final project should be:

- a Miller-compensated two-stage CMOS op-amp,
- with a simple and explainable first stage,
- and a common-source second stage.

This choice is strongly supported by the NPTEL Analog IC Design material, which treats the two-stage op-amp as a central block-level architecture and explicitly covers dominant-pole compensation, phase margin, slew rate, swing limits, and two-stage Miller compensation.

## OTA Versus Op-Amp In This Project

At transistor level, this project is closely related to an OTA.

The analog core is basically OTA-like:

- differential input pair,
- gain stage,
- second stage,
- compensation,
- bias circuitry.

But this project is framed as an op-amp project because the learning goals emphasize:

- closed-loop behavior,
- unity-gain stability,
- output swing,
- load drive,
- time-domain settling,
- phase margin.

So the most accurate description is:

- the core is OTA-like,
- the project goal is op-amp behavior under feedback.

## Input Pair Choice: nMOS Or pMOS

This choice should not be guessed.

From the NPTEL op-amp summary:

- nMOS input stage:
  - higher `gm` for the same current,
  - better for larger bandwidths,
  - usually higher flicker noise.
- pMOS input stage:
  - lower `gm` for the same current,
  - usually lower flicker noise,
  - better for low-noise, low-frequency work.

For a learning-centric first project, a practical rule is:

- if speed and easier `gm` per current matter more, start by exploring nMOS input,
- if low-frequency noise intuition matters more, also study the pMOS trade-off,
- do not freeze this choice before I understand common-mode range and noise goals.

## Software Choices

This section answers the question: what software path should I use for this project?

### Path A: University / Commercial Flow

Use this if Cadence is available.

Typical path:

- Cadence Virtuoso for schematic,
- Spectre for simulation,
- ADE for benches and sweeps,
- optional layout and extraction in the Cadence flow.

Why this is strong:

- standard analog IC workflow,
- easier multirun bench management,
- better direct analog design ergonomics,
- easier transition to layout and post-layout work.

Best use case:

- use this for the final project if my lab or university already gives access.

### Path B: Open-Source Full-Custom Flow

Use this if Cadence is not available.

Recommended stack:

- SKY130 PDK,
- open_pdks,
- xschem for schematic entry,
- ngspice for simulation,
- Magic for layout,
- Netgen for LVS,
- KLayout for viewing and checking layout data.

Why this is a valid project path:

- xschem is explicitly aimed at VLSI, ASIC, and analog custom design and emphasizes hierarchy and parametric reuse,
- ngspice is an open-source SPICE simulator and can read foundry-style device libraries,
- the SKY130 open PDK is openly documented and usable for test-chip style learning and initial design verification,
- Magic, Netgen, and KLayout give a complete open layout-verification path.

Best use case:

- use this if I need a serious final flow without commercial tools.

### Path C: Quick Learning Sandbox

Use this only for intuition building, not as the final transistor-level project environment.

Good tools:

- LTspice,
- TINA-TI,
- simple ideal-op-amp SPICE environments.

Why use them:

- they are fast for learning feedback,
- they are fast for learning Bode plots,
- they are fast for learning phase margin, overshoot, and capacitive-load intuition,
- TI Precision Labs explicitly uses TINA-TI in its stability teaching flow.

Why not use them as the final project flow:

- they are not the best place to do a full PDK-based transistor-level IC design project,
- they do not naturally give a clean full-custom analog IC workflow.

### Recommended Software Strategy

Use a two-layer software plan:

1. use LTspice or TINA-TI in the first learning stage for feedback and stability intuition,
2. use Cadence or xschem/ngspice/SKY130 for the real transistor-level project.

If no commercial tools are available, the most realistic learning-first final path is:

- xschem + ngspice + SKY130,
- and only add Magic / Netgen / KLayout if layout becomes part of the deliverables.

## How I Must Learn From Videos

This is the most important rule in the whole project.

Watching videos is not learning.

Learning happens only when every video is followed by active work.

For every lecture, I must do this exact loop:

1. Watch the lecture once without taking long notes.
2. Write a half-page summary in my own words.
3. Write the 3 to 5 equations or ideas that matter most.
4. Draw one circuit or one pole-zero picture from memory.
5. Simulate one tiny example related to the lecture.
6. Write one thing I still do not understand.
7. Rewatch only the needed part and resolve that confusion.

If I do not do steps 2 to 7, the lecture stays passive.

## Resource Backbone

The project should use a small set of strong resources, not random videos.

### Resource 1: NPTEL Analog Electronic Circuits, IIT Madras, Prof. Shanthi Pavan

URL:

https://onlinecourses.nptel.ac.in/noc26_ee65/preview

Why it matters:

- it is intuition-heavy,
- it is explicitly first-principles oriented,
- its Week 8 to Week 11 sequence maps very well to this project.

Most relevant weeks for this project:

- Week 8: differential pair and common-mode rejection,
- Week 9: basic two-stage op-amp and parasitic capacitances,
- Week 10: multistage feedback, stability, phase margin,
- Week 11: dominant-pole compensation and Miller effect.

What I should learn from it:

- intuitive differential-pair thinking,
- the physical meaning of poles and parasitic capacitances,
- why two-stage op-amps are unstable without compensation,
- what dominant-pole compensation is doing.

### Resource 2: NPTEL Analog IC Design, Prof. Nagendra Krishnapura

URLs:

https://archive.nptel.ac.in/content/syllabus_pdf/117106030.pdf
https://archive.nptel.ac.in/content/storage2/courses/117106030/nptel-aic/opampsummary.pdf

Why it matters:

- it is directly aligned to transistor-level analog IC design,
- it explicitly covers feedback, stability, one-stage op-amps, and two-stage Miller-compensated op-amps,
- it also gives architecture comparisons and input-pair trade-offs.

Most relevant lecture blocks from the course listing:

- Differential Amplifiers,
- Negative Feedback,
- Stability of Negative Feedback Systems,
- Dominant Pole Compensation,
- One Stage OpAmps,
- Loop gain and unity loop gain frequency,
- Phase margin,
- Single stage opamp realization,
- Two stage Miller compensated opamp,
- Two and three stage Miller compensated opamps.

What I should learn from it:

- transistor-level equations and architecture logic,
- how to go from gain blocks to a real op-amp,
- how to compare single-stage, telescopic, folded, and two-stage forms,
- how `gm`, `ro`, `Cc`, and current set performance.

### Resource 3: Razavi Path

Use Razavi as the parallel intuition and textbook spine.

Recommended parallel topics:

- basic op-amp intuition,
- op-amp circuits,
- instability in feedback,
- Bode rules and stability,
- stability and frequency compensation,
- op-amp nonidealities.

How to use Razavi correctly:

- do not use Razavi as passive background watching,
- use Razavi to make the concept feel intuitive,
- then use NPTEL Analog IC Design to translate that intuition into transistor-level design steps.

### Resource 4: TI Precision Labs - Op Amp Stability

URLs:

https://www.ti.com/video/4080254925001
https://www.ti.com/video/6216778063001
https://www.ti.com/lit/pdf/slypa06

Why it matters:

- it is very good for stability measurement intuition,
- it connects Bode plots, phase margin, overshoot, and AC peaking,
- it discusses open-loop SPICE simulation and common stability mistakes.

What I should learn from it:

- how to read phase margin from loop gain,
- how overshoot maps back to phase margin,
- why bench setup errors cause fake stability conclusions,
- how to think about capacitive loads and compensation in simulation.

### Resource 5: Open-Source Tool Documentation

Useful official pages:

- xschem: https://github.com/StefanSchippers/xschem
- ngspice: https://ngspice.sourceforge.io/index.html
- SKY130 docs: https://skywater-pdk.readthedocs.io/en/main/
- Magic docs: https://magicvlsi.wordpress.com/documentation/
- KLayout docs: https://www.klayout.de/doc/

Why these matter:

- they tell me what the tools actually do,
- they help me choose a realistic flow,
- they stop me from treating software setup as an afterthought.

## Core Learning Modules

Each module below answers four questions:

- what I must learn,
- which resource teaches it best,
- what I do after watching,
- how I prove that I learned it.

### Module 1: Feedback And Op-Amp Intuition

What I must learn:

- open-loop versus closed-loop behavior,
- why high gain alone is not enough,
- why finite gain and finite bandwidth matter,
- why feedback both helps and creates stability concerns.

Best resources:

- Razavi op-amp intuition lectures,
- NPTEL Analog Electronic Circuits feedback weeks,
- TI phase margin introduction.

What I do right after watching:

- write one page: "Why feedback makes an op-amp useful",
- simulate inverting and non-inverting ideal-op-amp examples,
- show what changes when finite GBW is added,
- connect closed-loop overshoot to insufficient phase margin.

How I prove I learned it:

- I can explain why a closed-loop unity-gain follower can ring even when the op-amp has very high DC gain.

### Module 2: MOS Small-Signal Behavior And Biasing

What I must learn:

- `gm`,
- `ro`,
- overdrive,
- current mirrors,
- saturation constraints,
- body effect,
- how current and length change gain and bandwidth.

Best resources:

- NPTEL Analog Electronic Circuits Weeks 2 to 7,
- NPTEL Analog IC Design MOSFET, current mirror, active load, and one-stage op-amp material,
- Razavi MOS and basic amplifier chapters.

What I do right after watching:

- derive `gm` and `ro` relations used in first-pass sizing,
- simulate one common-source stage,
- simulate one current mirror,
- write what improves when current is increased and what gets worse.

How I prove I learned it:

- I can predict, before simulation, whether a size or current change should increase gain, speed, or headroom.

### Module 3: Differential Pair And Active Load

What I must learn:

- differential-to-single-ended conversion,
- transconductance from the pair,
- common-mode behavior,
- active-load impact on gain,
- tail current role.

Best resources:

- NPTEL Analog Electronic Circuits Week 8,
- NPTEL Analog IC Design differential amplifier lectures,
- Razavi differential pair and current mirror material.

What I do right after watching:

- build a differential pair with active load,
- run small differential stimulus,
- observe gain,
- sweep common-mode input,
- identify where the pair stops behaving correctly.

How I prove I learned it:

- I can point to which devices set gain, which devices set headroom, and which node becomes high impedance.

### Module 4: Frequency Response, Poles, Zeros, And Phase Margin

What I must learn:

- how poles and zeros shape Bode plots,
- why gain crossover matters,
- what phase margin means physically,
- why overshoot and ringing correlate with phase margin,
- why rate of closure can warn about stability risk.

Best resources:

- NPTEL Analog Electronic Circuits Week 10,
- NPTEL Analog IC Design negative feedback and phase margin lectures,
- TI phase margin video and compensation PDF.

What I do right after watching:

- draw Bode plots by hand for one-pole and two-pole systems,
- simulate a closed-loop amplifier with different phase margins,
- compare overshoot, AC peaking, and loop-gain phase margin,
- write one page on why AC and transient must agree.

How I prove I learned it:

- I can look at overshoot or AC peaking and give a reasonable phase-margin estimate directionally.

### Module 5: One-Stage Op-Amp As A Precursor

What I must learn:

- why one-stage op-amps are useful,
- why cascodes improve gain,
- why telescopic and folded cascodes differ,
- when one-stage is enough and when it is not.

Best resources:

- NPTEL Analog IC Design one-stage op-amp lectures,
- NPTEL op-amp summary PDF,
- Razavi one-stage op-amp sections.

What I do right after watching:

- study at least one simple one-stage op-amp,
- compare telescopic and folded in notes,
- write why telescopic is faster and why folded gives more swing,
- decide which one is worth using only as a learning precursor.

How I prove I learned it:

- I can explain why the final project is not stopping at a one-stage op-amp.

### Module 6: Two-Stage Op-Amp And Miller Compensation

What I must learn:

- why a second stage is added,
- why the second stage adds another pole,
- what the Miller capacitor does,
- where the RHP zero comes from,
- when a series resistor helps,
- how `Cc`, `gm1`, `gm2`, and `CL` interact.

Best resources:

- NPTEL Analog Electronic Circuits Week 11,
- NPTEL Analog IC Design lectures on dominant-pole compensation and two-stage Miller compensated op-amps,
- TI stability resources,
- Razavi compensation material.

What I do right after watching:

- draw the two-stage architecture and label the nodes,
- derive `gm1 ~= 2*pi*UGB*Cc`,
- derive `SR ~= I/Cc`,
- explain in writing why increasing `Cc` helps phase margin but hurts speed,
- build the first transistor-level two-stage schematic.

How I prove I learned it:

- I can explain the final compensation capacitor choice in terms of poles, zeros, bandwidth, and slew rate, not just "simulation worked."

### Module 7: Verification Method And Measurement Correctness

What I must learn:

- how to measure loop gain,
- how to preserve DC bias while breaking the loop,
- how to compare loop gain, closed-loop step response, slew rate, and swing,
- why a wrong bench can produce fake phase margin.

Best resources:

- TI Precision Labs phase margin and SPICE-stability resources,
- NPTEL Analog IC Design loop-gain and phase-margin lectures.

What I do right after watching:

- document one correct loop-break method,
- run AC and transient on the same load condition,
- write a short note when the results disagree,
- refuse to tune the circuit until the bench setup is trusted.

How I prove I learned it:

- I can explain exactly how phase margin was measured in my project.

### Module 8: Trade-Offs, Reporting, And Optional Layout

What I must learn:

- how to tell a gain-bandwidth-stability-power story,
- how to compare theory versus simulation honestly,
- why layout and parasitics matter even for a learning project.

Best resources:

- NPTEL Analog IC Design layout and mismatch topics,
- SKY130, Magic, KLayout, and Netgen documentation if layout is attempted.

What I do right after watching:

- run `Cc`, `CL`, and current sweeps,
- summarize what improved and what degraded,
- if layout is in scope, lay out only the most educational core pieces,
- rerun the main AC and transient benches post-layout.

How I prove I learned it:

- I can explain one major trade-off clearly in the final report.

## Recommended Learning-To-Design Sequence

Do not jump straight to the final op-amp.

Use this exact circuit sequence:

1. ideal op-amp feedback examples,
2. common-source amplifier,
3. current mirror,
4. differential pair with active load,
5. one-stage op-amp or one-stage precursor study,
6. final two-stage Miller-compensated op-amp,
7. compensation sweeps,
8. optional layout and post-layout.

This order matters because each circuit teaches the next one.

## Detailed 20-Week Learning Plan

### Weeks 1 To 2: Feedback Foundation

Study:

- Razavi op-amp intuition material,
- NPTEL feedback content,
- TI phase margin introduction.

Learn:

- open-loop versus closed-loop,
- finite bandwidth,
- overshoot, ringing, and phase margin.

Do:

- simulate ideal-op-amp inverting and non-inverting amplifiers,
- simulate a finite-GBW op-amp follower,
- write one page on why feedback is the real story.

Output:

- feedback note,
- first Bode plot,
- first overshoot example.

### Weeks 3 To 4: MOS Basics, Biasing, And Single Stages

Study:

- MOS amplifier and biasing material from NPTEL and Razavi.

Learn:

- `gm`,
- `ro`,
- overdrive,
- current mirrors,
- gain and swing basics.

Do:

- simulate a common-source amplifier,
- simulate a current mirror,
- estimate gain before simulation,
- compare hand estimate and SPICE.

Output:

- small-signal note,
- current mirror note,
- discrepancy log v1.

### Weeks 5 To 6: Differential Pair And Active Load

Study:

- differential amplifier material from NPTEL Analog Electronic Circuits and Analog IC Design.

Learn:

- differential gain,
- common-mode behavior,
- active-load gain increase,
- high-impedance node intuition.

Do:

- build and simulate a differential pair,
- test differential excitation,
- test common-mode input change,
- note where the pair loses proper biasing.

Output:

- differential pair schematic,
- gain note,
- common-mode note.

### Weeks 7 To 8: Frequency Response And Stability Basics

Study:

- NPTEL stability lectures,
- TI phase margin material.

Learn:

- dominant pole,
- non-dominant poles,
- loop gain,
- phase margin,
- overshoot relation.

Do:

- draw one-pole and two-pole Bode plots by hand,
- simulate closed-loop systems with different phase margins,
- create one page mapping overshoot to phase margin.

Output:

- stability summary note,
- Bode sketch sheet,
- AC versus transient comparison note.

### Weeks 9 To 10: One-Stage Op-Amp Study

Study:

- NPTEL one-stage op-amp lectures,
- NPTEL op-amp summary for telescopic and folded cascode comparison.

Learn:

- what a single-stage op-amp can do well,
- where swing gets limited,
- why telescopic and folded trade off speed, swing, and noise.

Do:

- compare architectures in notes,
- decide whether the first stage of the final two-stage op-amp should conceptually resemble a simple differential pair, telescopic, or folded precursor.

Output:

- architecture comparison note,
- chosen first-stage learning direction.

### Weeks 11 To 12: Final Two-Stage Architecture And First-Pass Sizing

Study:

- NPTEL two-stage Miller-compensated op-amp lectures,
- Razavi compensation material.

Learn:

- first-stage role,
- second-stage role,
- Miller capacitor role,
- `Cc`, `gm1`, `SR`, and `CL` relations.

Do:

- freeze provisional specs,
- choose first-pass `Cc`,
- compute `gm1`,
- compute current from slew-rate target,
- draw the full architecture with labeled nodes.

Output:

- sizing sheet v1,
- architecture diagram,
- provisional spec note.

### Weeks 13 To 14: Schematic And DC Bring-Up

Learn:

- how transistor-level reality differs from hand estimates.

Do:

- enter the transistor-level schematic,
- run DC operating point,
- verify region of operation,
- correct current and headroom issues before any serious AC work.

Output:

- schematic v0,
- operating-point table,
- bias-debug note.

### Weeks 15 To 16: Loop Gain, Step Response, Slew Rate, Swing

Learn:

- how to verify the actual circuit correctly.

Do:

- build the loop-gain bench,
- extract gain, `UGB`, and phase margin,
- run unity-gain closed-loop step,
- run slew-rate test,
- run swing test,
- compare all results back to theory.

Output:

- gain/phase plot,
- step response,
- slew-rate plot,
- swing note.

### Weeks 17 To 18: Compensation And Trade-Off Exploration

Learn:

- how compensation choices reshape the full design.

Do:

- sweep `Cc`,
- sweep `CL`,
- evaluate `Rc`,
- sweep second-stage current,
- explain every trend in words.

Output:

- compensation plot set,
- final `Cc` decision note,
- optional `Rc` decision note.

### Weeks 19 To 20: Final Story, Optional Layout, And Viva Prep

Learn:

- how to present the design as a coherent engineering story.

Do:

- assemble final result set,
- write theory-versus-simulation summary,
- optionally do a compact layout study,
- prepare viva answers.

Output:

- final plot package,
- final summary note,
- viva sheet,
- optional layout note.

## What I Should Produce After Every Resource Block

After any major lecture block, I should produce exactly these four things:

- one concept note,
- one derivation or equation sheet,
- one small simulation,
- one confusion log entry.

This rule prevents passive accumulation of videos without understanding.

## Core Equations That Must Keep Reappearing

These equations must repeatedly appear in my notes, sizing sheets, and report:

- `Av0 ~ (gm1*ro1)*(gm2*ro2)`
- `gm1 ~ 2*pi*UGB*Cc`
- `SR ~ I/Cc`
- uncompensated RHP zero `~ gm2/Cc`
- larger `Cc` usually improves phase margin but lowers `UGB` and slew rate
- larger current usually improves speed but raises power
- larger `CL` usually makes stability harder

## Final Deliverables For A Learning-Centric Version

The final project should include:

- a learning log,
- a resource-to-concept map,
- concept notes for feedback, differential pair, stability, and compensation,
- a first-pass sizing sheet,
- the final schematic,
- the loop-gain method note,
- gain, `UGB`, phase margin, slew rate, swing, and load plots,
- at least one trade-off sweep set,
- one theory-versus-simulation discrepancy note,
- optional layout and post-layout comparison if scope and tools allow.

## Questions I Must Be Ready To Answer

- Why is a two-stage op-amp better than a single-stage op-amp for this project?
- Why does a second stage create a stability problem?
- What exactly does the Miller capacitor do?
- Why does increasing `Cc` usually help phase margin but hurt speed?
- What sets `UGB` in a first-pass design?
- Why can slew rate be estimated from `I/Cc`?
- When is `Rc` useful?
- Why might AC and transient give conflicting conclusions?
- Why would I choose nMOS or pMOS input devices?
- Why was this software flow chosen instead of another one?
