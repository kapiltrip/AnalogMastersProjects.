# Learning-Oriented Master's Project Plan: Miller-Compensated Two-Stage CMOS Op-Amp

## Project Statement

Design, size, simulate, verify, and document a Miller-compensated two-stage CMOS op-amp, with explicit evidence for gain, unity-gain bandwidth, phase margin, slew rate, output swing, load-drive behavior, and the trade-offs created by compensation.

## Executive Summary

This project is strong for a master's portfolio because it forces a full analog IC design chain:

1. feedback and stability intuition,
2. MOS small-signal modeling,
3. transistor-level hand design,
4. compensation strategy,
5. simulation-driven verification,
6. interpretation of trade-offs,
7. optional layout and post-layout closure.

The project should never be framed as "I drew an op-amp schematic."

The defensible finish line is:

- a frozen spec table,
- a clear architecture justification,
- first-pass equations and sizing logic,
- a reproducible testbench suite,
- measured trends that match the equations,
- one clear trade-off story,
- optional layout/post-layout evidence if time allows.

## Why This Plan Exists

This file is meant to serve as:

1. a learning roadmap,
2. a design execution checklist,
3. a weekly project tracker,
4. a simulation signoff checklist,
5. a thesis-writing backbone,
6. a viva preparation guide.

At the end of each major week, I should be able to answer:

1. What concept did I learn?
2. What design decision did that concept unlock?
3. What exact equation or estimate did I derive?
4. What simulation did I run?
5. What mismatch or failure remains between theory and behavior?

## Why This Topology Is A Strong Master's Project

A Miller-compensated two-stage CMOS op-amp is a strong project because it naturally exposes the most important analog design dependencies:

- high gain is useful only through feedback,
- more gain stages create more poles,
- more poles make stability a real design problem,
- Miller compensation solves one problem while creating other measurable penalties,
- every specification ties back to transistor-level quantities such as `gm`, `ro`, bias current, overdrive voltage, and capacitance.

That makes the project ideal for a resume because it demonstrates not just design, but diagnosis and reasoning.

## Current Assumptions And Unknowns

These must be frozen early because they change the entire sizing path.

- Process node / PDK is not yet fixed.
- Supply voltage is not yet fixed.
- Load capacitance is not yet fixed.
- Required output swing is not yet fixed.
- Input common-mode range is not yet fixed.
- Power budget is not yet fixed.
- Whether layout is required is not yet fixed.
- Whether noise and offset are mandatory measured outputs is not yet fixed.

Until those are frozen, all sizing should be treated as provisional.

## Main Technical Story Of The Project

The final project should clearly explain this sequence:

1. An op-amp becomes useful when high open-loop gain is controlled by feedback.
2. A single stage may not simultaneously provide enough gain, output swing, and load drive.
3. A second stage increases gain and drive capability, but adds another pole.
4. Multi-pole feedback loops can become unstable, so compensation is required.
5. Miller compensation creates a dominant pole and splits poles, but also changes bandwidth, slew rate, and zero location.
6. Therefore the project is not "gain only"; it is a controlled trade-off among gain, speed, stability, swing, load, and power.

## Core Equations And Anchor Relations

These are the equations that must appear repeatedly in the project report and viva.

- `Av ~ A1 * A2`
- `Av0 ~ (gm1*ro1)*(gm2*ro2)` as a first-pass small-signal view
- `wu ~ gm1/Cc`
- `gm1 ~ wu*Cc = 2*pi*UGB*Cc` when `UGB` is in hertz
- `SR ~ I/Cc`
- an uncompensated Miller path can create an `RHP zero ~ gm2/Cc`
- a series resistor `Rc` can push that zero away, remove it, or move it to the LHP

These relations imply:

- increasing `gm1` usually raises `UGB`,
- increasing `Cc` usually improves phase margin but lowers `UGB` and slew rate,
- increasing bias current improves speed and slew rate but costs power,
- increasing `ro` improves gain but often costs headroom or speed,
- increasing `CL` makes stability harder,
- ignoring the RHP zero can make AC and transient results look inconsistent.

## Success Criteria

A strong project outcome is:

- one well-justified two-stage architecture,
- one stable compensation strategy,
- one correct loop-gain measurement method,
- one clear sizing sheet,
- one reproducible simulation bundle,
- one trade-off sweep set,
- one short discrepancy log comparing equations and simulations.

Novelty is optional. Clarity and correctness are not.

## Weekly Micro-Loop

This project should be run in a fixed weekly loop.

Each week:

1. Watch the selected lectures or read the selected notes.
2. Write a 1-page summary in my own words.
3. Produce one derivation sheet or sizing sheet.
4. Update one design sheet with actual numbers.
5. Run one new simulation or build one new testbench.
6. Write one short failure note explaining what did not match expectation.

### Recommended Time Split Per Week

- lectures and notes: `4 to 6` hours
- derivations and sizing math: `2 to 4` hours
- simulation and debug: `4 to 8` hours
- documentation and plot cleanup: `1 to 2` hours

## Week 0 Decision Gates

Before deep transistor-level work begins, freeze the following.

### System-Level Questions

- What is `VDD`?
- What is the target load capacitance `CL`?
- What is the target DC gain?
- What is the target unity-gain bandwidth or gain-bandwidth?
- What phase margin is required?
- What slew rate is required?
- What output swing is required?
- What quiescent power budget is acceptable?
- What input common-mode range is required?
- Is noise in scope?
- Is offset in scope?
- Is layout required?

### Why These Questions Matter

- `CL` directly affects compensation choice and non-dominant pole behavior.
- `UGB` and `Cc` immediately set a `gm1` target.
- `SR` and `Cc` immediately set a current target.
- gain and swing compete through `ro`, current, and headroom.
- if layout is required, routing and parasitics must be planned early.

### Week 0 Deliverable

Produce a 1-page spec freeze note containing:

- supply voltage,
- target `CL`,
- target DC gain,
- target `UGB`,
- target phase margin,
- target slew rate,
- target output swing,
- power budget,
- input common-mode assumption,
- whether layout is included.

## Reusable Specification Template

Fill this table before the schematic is treated as real.

| Item | Target | How It Will Be Verified |
| --- | --- | --- |
| Process / PDK | TBD | identify device models and minimum lengths |
| `VDD` | TBD | DC operating point and swing checks |
| Load capacitance `CL` | TBD | transient and AC load sweep |
| DC gain | TBD | open-loop AC / loop-gain result |
| `UGB` | TBD | loop gain 0 dB crossing |
| Phase margin | TBD | loop-gain phase at crossover |
| Slew rate | TBD | large-signal transient |
| Output swing | TBD | DC sweep or transient output limits |
| Power / `Iq` | TBD | DC operating point currents |
| Input common-mode range | TBD | DC bias sweep if included |
| CMRR / PSRR | optional / TBD | AC injection if in scope |
| Noise | optional / TBD | output noise simulation |
| Offset | optional / TBD | mismatch / Monte Carlo if in scope |
| Layout requirement | yes / no | DRC/LVS/PEX and post-layout reruns |

## Knowledge Map: What Must Be Learned Before What

The project should be learned in dependency order, not random topic order.

### Layer 1: Feedback And Stability

Must understand:

- Bode plots,
- loop gain,
- poles and zeros,
- gain crossover,
- phase margin,
- why transient ringing and phase margin are linked.

Without this layer, compensation becomes guesswork.

### Layer 2: MOS Small-Signal Behavior

Must understand:

- `gm`,
- `ro`,
- node capacitances,
- current mirrors,
- overdrive voltage,
- saturation constraints.

Without this layer, transistor sizing becomes blind tuning.

### Layer 3: Two-Stage Architecture

Must understand:

- what the first stage does,
- what the second stage does,
- where the high-impedance nodes are,
- which node becomes dominant after compensation,
- why the second stage adds a pole.

### Layer 4: Miller Compensation

Must understand:

- where `Cc` is connected,
- what pole splitting means physically,
- how the compensation capacitor shapes the loop,
- where the RHP zero comes from,
- when a series resistor `Rc` is useful.

### Layer 5: Verification Method

Must understand:

- how to measure loop gain correctly,
- how to preserve DC bias while breaking the loop,
- how to cross-check AC phase margin with transient ringing,
- how to extract slew rate, gain, `UGB`, and swing consistently.

### Layer 6: Optional Physical Design

Must understand:

- why parasitics move poles,
- why routing symmetry matters,
- why layout can degrade gain, phase margin, and settling.

## Reading And Video Stack

Use a short, deliberate stack rather than too many resources.

### Primary Structured Sources

- NPTEL Analog IC Design course
- NPTEL Analog Electronic Circuits course
- Razavi lecture sequence on op-amps, feedback, stability, and nonidealities

### Practical Stability Sources

- TI Precision Labs material on Bode plots and phase margin
- a compact gain/phase margin explainer for sanity checks

### Design-Oriented Sizing Sources

- P. E. Allen style two-stage op-amp design flow
- compensation notes that explicitly discuss `Cc`, `SR`, `gm1`, and `Rc`

### Use Of Resources

Do not watch everything at once.

Use resources in this order:

1. feedback and phase margin,
2. two-stage architecture,
3. Miller compensation and zero behavior,
4. swing and nonidealities,
5. sizing and simulation.

## Curated Lecture Stack

These are good anchors for the learning path already started in this project.

### Op-Amp Intuition And Feedback

- Razavi Basic Circuits Lec 38: Introduction to Op Amps
- Razavi Electronics 1 Lec 42: Op Amp Circuits 1
- Razavi Electronics 1 Lec 43: Op Amp Circuits II

### Stability And Compensation

- Nyquist Criterion; Phase Margin
- Razavi: Stability and Frequency Compensation Part 1
- Razavi Electronics 2 Lec 43: Intro to Instability in Feedback
- Razavi Electronics 2 Lec 44: Bode's Rules, Stability Condition

### Two-Stage Architecture

- Single Stage Op-Amp Realization
- The Two Stage Opamp and Single Supply Operation
- Two Stage Miller Compensated Opamp-1
- Two Stage Miller Compensated Opamp-2

### Nonidealities And Swing Limits

- The Two Stage Opamp (contd)
- The Two Stage Opamp contd
- Swing Limits of the Two Stage OTA
- Two and Three Stage Miller Compensated Opamps; Feedforward Compensated Opamp
- Razavi Electronics 1 Lec 45: Op Amp Nonidealities II

## Tooling Paths

The project is credible only if the measurement method is credible.

### If Cadence Is Available

Recommended flow:

- schematic capture,
- operating-point and AC analyses,
- STB or loop-gain style analysis,
- transient tests,
- optional layout and extraction.

Key rule:

- if using loop stability analysis, break the loop in a way that preserves DC bias and actually breaks all relevant paths.

### If Commercial EDA Is Not Available

A strong student project can still be done with:

- SKY130 or another open PDK,
- xschem for schematic entry,
- ngspice for simulation,
- Magic or KLayout for layout verification if layout is in scope.

### Measurement Correctness Checklist

Before trusting any phase margin number, confirm:

- which loop is being measured,
- where the loop is broken,
- whether DC bias is preserved,
- whether all feedback paths are interrupted,
- whether AC and transient interpretations agree.

If AC says high phase margin but the unity-gain transient rings badly, assume the measurement setup is wrong until proven otherwise.

## Project Phases

Use the project in phases rather than one long open-ended loop.

## Phase 1: Environment And Measurement Correctness

Goal:

- remove tool and testbench uncertainty before circuit complexity is added.

Tasks:

- create project folders for notes, sizing sheets, schematics, simulations, plots, and report assets,
- run a simple DC and AC check on a known amplifier block,
- define the loop-gain extraction method,
- write a short note on how phase margin will be measured.

Outputs:

- project folder structure,
- first successful DC and AC simulation,
- loop-gain method note,
- file naming convention for plots and benches.

## Phase 2: Spec Freeze And Architecture Justification

Goal:

- choose a target that is ambitious enough to be meaningful but simple enough to finish.

Recommended learning-oriented starting point:

- `CL` in the pF range,
- `UGB` in the MHz range,
- phase margin around `60 deg`,
- swing and slew targets consistent with the supply and current budget.

Tasks:

- fill the spec template,
- justify why a two-stage Miller-compensated op-amp is the right topology,
- write a one-paragraph explanation of why a second stage helps and why it creates a compensation problem.

Outputs:

- frozen spec table v1,
- architecture decision note,
- assumptions list.

## Phase 3: Stability Fundamentals Lock-In

Goal:

- make phase margin predictive rather than descriptive.

Tasks:

- sketch expected Bode magnitude and phase shapes,
- explain how poles and zeros change those shapes,
- connect crossover frequency to phase margin,
- write a short note on why a two-stage loop needs compensation.

Outputs:

- hand-drawn Bode sketches,
- stability summary note,
- first estimate of dominant and non-dominant pole roles.

## Phase 4: First-Pass Hand Design

Goal:

- produce a first transistor-level design that has a reasonable chance of converging.

### Recommended First-Pass Sizing Rules

Use simple, defensible starting rules.

- choose `Cc` relative to `CL`, for example a baseline such as `Cc >= 0.2*CL`
- use slew rate to back-calculate a required charging current: `I >= SR*Cc`
- use target `UGB` and `Cc` to estimate `gm1`: `gm1 ~ 2*pi*UGB*Cc`
- allocate enough second-stage transconductance and output resistance to support gain and output-pole placement
- if using a nulling resistor, document whether it is for RHP-zero removal or LHP-zero placement

### Critical Schematic Decisions To Document

- where `Cc` is connected,
- which node is the first-stage high-impedance node,
- which node is the output node,
- how bias currents are generated,
- whether `Rc` is present,
- what the assumed `Vov` values are for key devices.

Outputs:

- sizing sheet v1,
- node-labeled architecture diagram,
- transistor-level schematic v0.

## Phase 5: First Verification Pass

Goal:

- prove that the first-pass sizing is at least directionally correct.

Tasks:

- run DC operating point,
- verify all critical transistors are in the intended region,
- run loop gain / open-loop AC,
- extract DC gain and `UGB`,
- run a unity-gain closed-loop step response,
- compare ringing to phase margin.

Outputs:

- operating-point table,
- first gain/phase plot,
- first step response plot,
- first discrepancy note between expectation and result.

## Phase 6: Compensation And Trade-Off Exploration

Goal:

- turn the op-amp from a schematic into a measured trade-off system.

Minimum sweeps to run:

- sweep `Cc`,
- sweep second-stage bias current,
- sweep `CL`,
- add and remove `Rc`,
- vary `Rc` if used.

For each sweep, explain:

- what improved,
- what degraded,
- why the trend follows the equations.

Outputs:

- trade-off plot set,
- design decision memo for final `Cc`,
- design decision memo for `Rc`,
- updated schematic v1.

## Phase 7: Final Verification Suite

Goal:

- generate the evidence that will appear in the report and viva.

Tasks:

- final loop-gain measurement,
- final unity-gain transient,
- final slew-rate measurement,
- output swing check,
- load-capacitance sweep,
- supply sensitivity check,
- optional noise and offset work if in scope,
- optional corner analysis if models support it.

Outputs:

- final measured spec table,
- pass/fail table against targets,
- final calculation-versus-simulation note.

## Phase 8: Optional Layout And Post-Layout Closure

Goal:

- prove awareness that analog design does not end at the schematic.

Minimal high-value layout scope:

- input pair,
- current mirrors,
- second stage,
- compensation network,
- bias core.

Tasks:

- create layout of the core analog block,
- run DRC and LVS,
- extract parasitics,
- rerun gain, `UGB`, phase margin, and step response.

Outputs:

- DRC-clean evidence,
- LVS-clean evidence,
- post-layout AC and transient comparison,
- post-layout delta note.

## Required Simulation Matrix

The project should not be considered finished unless every relevant row below has an output.

| Test | Why It Matters | Minimum Output |
| --- | --- | --- |
| DC operating point | verifies currents, regions, headroom | node voltages and branch currents |
| Loop gain / open-loop AC | gives DC gain, `UGB`, and phase margin | gain-phase plot and extracted values |
| Unity-gain closed-loop step | cross-checks stability in time domain | transient plot and ringing comment |
| Slew rate | verifies large-signal speed | rising and falling SR values |
| Output swing | checks headroom and stage saturation | swing range result |
| `CL` sweep | exposes load sensitivity | plot of PM or step response versus `CL` |
| `Cc` sweep | shows compensation trade-off | PM, `UGB`, SR trends |
| Bias current sweep | shows power-speed trade-off | gain / speed / power comparison |
| `Rc` sweep | shows zero control | phase trend and zero-mitigation comment |
| Supply sweep | checks operating robustness | gain or swing sensitivity versus `VDD` |
| Noise | optional but useful | output noise result |
| Offset / mismatch | optional advanced extension | MC histogram or offset estimate |
| Corners | optional if model support exists | worst-case table |

## Measurement And Extraction Rules

Consistency matters more than having many plots.

### DC Gain

Report:

- low-frequency gain,
- units in dB,
- exact setup used.

### Unity-Gain Bandwidth

Report:

- crossover frequency,
- whether it was obtained from loop gain or closed-loop gain,
- phase at the same crossing.

### Phase Margin

Report:

- the phase margin number,
- the exact loop-break method,
- one sentence cross-checking the transient response.

### Slew Rate

Report:

- rising and falling slew rates separately,
- input step size used,
- whether the amplifier is in unity gain during the test.

### Output Swing

Report:

- linear output range,
- supply conditions,
- load condition.

## First-Pass Design Worksheet

This worksheet should exist as a real spreadsheet or notebook page.

### Inputs

- `VDD`
- target `CL`
- target `UGB`
- target phase margin
- target slew rate
- target DC gain
- target power

### Derived Starting Quantities

- choose `Cc`
- compute required current from `SR*Cc`
- compute required `gm1` from `2*pi*UGB*Cc`
- estimate first-stage gain
- estimate second-stage gain
- estimate total gain
- estimate dominant-pole and non-dominant-pole tendencies
- estimate whether `Rc` is necessary

### Device-Level Choices To Record

- device lengths selected for gain,
- overdrive voltages selected for swing and efficiency,
- first-stage and second-stage current allocation,
- expected `gm`, `ro`, and node capacitances,
- expected output resistance at the output node.

## Trade-Off Story That Must Be Demonstrated

The final report should explicitly show at least these three trends.

### `Cc` Sweep

Expected trend:

- larger `Cc` -> higher phase margin
- larger `Cc` -> lower `UGB`
- larger `Cc` -> lower slew rate

This is one of the main equations-to-plots stories in the project.

### Second-Stage Bias Current Sweep

Expected trend:

- larger second-stage current -> potentially better speed and drive
- larger second-stage current -> higher power
- pole locations and zero behavior can shift

### `Rc` Inclusion Or Sweep

Expected trend:

- correct `Rc` can mitigate the RHP-zero penalty
- phase response should improve if the zero was previously harmful

If adding `Rc` changes very little, explain whether the zero was already far away or whether the setup is not measuring the effect properly.

## Common Failure Modes And Diagnosis Map

Use this as the debug checklist before changing device sizes blindly.

### Phase Margin Looks Wrong

Possible causes:

- loop broken at the wrong place,
- DC bias disturbed by the test method,
- the measured loop is not the actual feedback loop,
- `Cc` too small,
- `CL` too large,
- RHP zero too close to crossover.

What to check first:

- loop-break correctness,
- AC versus transient consistency,
- `Cc`,
- effect of adding or tuning `Rc`.

### Phase Margin Looks Fine But Transient Rings Too Much

Possible causes:

- wrong loop measured,
- closed-loop bench differs from AC bench conditions,
- load in transient is not the same as load in AC,
- extra poles not captured by the chosen measurement method.

### Slew Rate Is Lower Than Expected

Possible causes:

- bias current lower than intended,
- `Cc` too large,
- devices not biased in the expected region,
- large-signal current limited by internal mirrors or second stage.

Check against:

- `SR ~ I/Cc`

### Gain Is Good But Swing Is Poor

Possible causes:

- headroom constraint,
- excessive overdrive,
- second-stage saturation,
- current-source saturation limits.

This is a DC headroom problem first, not a compensation problem.

### Stable At Small `CL` But Unstable At Larger `CL`

Possible causes:

- output pole moved down too much,
- `Cc` too small for the load,
- `CL` is now comparable to the compensation capacitor,
- compensation was chosen for the wrong load.

This is why `CL` sweep is mandatory.

### Calculation And Simulation Disagree Strongly

Possible causes:

- parasitic capacitances ignored in the hand estimate,
- `ro` overestimated,
- real device `gm/Id` or region assumptions were wrong,
- testbench or measurement setup not equivalent to the assumed model.

Required action:

- write the discrepancy down,
- explain the likely missing effect,
- do not hide the mismatch.

## Layout Awareness Checklist

Even if layout is optional, note what would matter physically.

- keep the input pair well matched,
- keep current mirrors symmetrical,
- minimize parasitic at the first-stage high-impedance node,
- route the compensation path deliberately,
- avoid accidental coupling into the compensation node,
- keep output routing realistic for the assumed load,
- expect parasitics to reduce phase margin and shift `UGB`.

## Signoff Checklist

Before the project is called complete, confirm:

- spec table frozen,
- architecture justified,
- `Cc` choice justified,
- `Rc` decision justified,
- sizing sheet completed,
- loop-gain method documented,
- DC operating point verified,
- gain / `UGB` / phase margin extracted,
- transient step response verified,
- slew rate measured,
- output swing measured,
- `CL` sweep completed,
- `Cc` sweep completed,
- bias sweep completed,
- discrepancy log written,
- optional layout results added if layout is in scope.

## Detailed 26-Week Execution Plan

This is the recommended deep version of the project schedule.

### Weeks 1 To 4: Foundations And Spec Freeze

#### Week 1

Objective:

- set up folders, naming scheme, and simulation environment.

Outputs:

- project folder structure,
- tool-flow note,
- first DC and AC sanity simulation.

#### Week 2

Objective:

- study op-amp feedback intuition and closed-loop thinking.

Outputs:

- one-page open-loop versus closed-loop note,
- ideal-versus-real assumption table,
- short note on why high gain alone is not enough.

#### Week 3

Objective:

- study poles, zeros, phase margin, and compensation.

Outputs:

- hand Bode sketch,
- dominant versus non-dominant pole note,
- phase-margin interpretation sheet.

#### Week 4

Objective:

- freeze provisional specs and justify the two-stage architecture.

Outputs:

- spec table v1,
- topology justification paragraph,
- list of assumed load and supply conditions.

### Weeks 5 To 8: Architecture And First-Pass Sizing

#### Week 5

Objective:

- understand first-stage and second-stage roles,
- assign qualitative responsibilities to each stage.

Outputs:

- node-labeled architecture sketch,
- current allocation note,
- first list of target `gm` and `ro` values.

#### Week 6

Objective:

- choose `Cc` and derive first-pass current and `gm1`.

Outputs:

- compensation sheet,
- `SR` to current estimate,
- `UGB` to `gm1` estimate.

#### Week 7

Objective:

- build hand calculations for stage gains and expected total gain.

Outputs:

- gain calculation sheet,
- headroom assumptions sheet,
- `Vov` targets for critical transistors.

#### Week 8

Objective:

- enter transistor-level schematic v0.

Outputs:

- schematic v0,
- labeled nodes for AC and transient probing,
- first DC operating-point report.

### Weeks 9 To 12: First Verification Pass

#### Week 9

Objective:

- verify operating region and bias currents.

Outputs:

- branch-current table,
- node-voltage table,
- note on any saturation failures.

#### Week 10

Objective:

- build and validate the loop-gain measurement setup.

Outputs:

- loop-break method note,
- first gain/phase plot,
- extracted DC gain and `UGB`.

#### Week 11

Objective:

- measure phase margin and cross-check with unity-gain transient.

Outputs:

- phase-margin result,
- unity-gain step response,
- AC-versus-transient consistency note.

#### Week 12

Objective:

- measure slew rate and output swing.

Outputs:

- SR rising and falling results,
- output swing result,
- note on which devices limit swing.

### Weeks 13 To 16: Trade-Off Sweeps And Refinement

#### Week 13

Objective:

- sweep `Cc`.

Outputs:

- `Cc` versus PM/UGB/SR plot set,
- selected `Cc` rationale,
- note on compensation trade-off.

#### Week 14

Objective:

- sweep load capacitance `CL`.

Outputs:

- stability-versus-load plot,
- maximum safe `CL` note,
- explanation of output-pole movement.

#### Week 15

Objective:

- evaluate `Rc` use and zero management.

Outputs:

- with/without `Rc` comparison,
- `Rc` sweep if used,
- note on RHP-zero mitigation.

#### Week 16

Objective:

- sweep second-stage current or key bias currents.

Outputs:

- power versus speed trade-off plot,
- updated schematic v1,
- current allocation decision note.

### Weeks 17 To 20: Final Verification Package

#### Week 17

Objective:

- rerun gain, `UGB`, and phase margin on the refined design.

Outputs:

- final AC plot,
- final extracted gain / `UGB` / PM table,
- comparison against targets.

#### Week 18

Objective:

- rerun transient, slew, and swing on the refined design.

Outputs:

- final step response,
- final slew-rate plot,
- final swing result.

#### Week 19

Objective:

- run supply sweep and optional common-mode sweep.

Outputs:

- supply robustness note,
- optional ICMR plot,
- note on remaining weak points.

#### Week 20

Objective:

- run optional noise, mismatch, or corner checks if models and time support it.

Outputs:

- optional noise result,
- optional offset / mismatch note,
- optional worst-case table.

### Weeks 21 To 24: Optional Layout And Physical Awareness

#### Week 21

Objective:

- create a compact layout plan for the analog core.

Outputs:

- block floorplan sketch,
- matching note for input pair and mirrors,
- parasitic-risk checklist.

#### Week 22

Objective:

- complete core placement and critical routing.

Outputs:

- layout screenshot,
- routing note around the compensation node,
- DRC progress log.

#### Week 23

Objective:

- finish DRC and run LVS.

Outputs:

- DRC-clean report,
- LVS-clean report,
- note on any extracted parasitic concern.

#### Week 24

Objective:

- run post-layout AC and transient comparison.

Outputs:

- pre-layout versus post-layout comparison plots,
- delta note for gain / `UGB` / PM,
- delta note for step response.

### Weeks 25 To 26: Reporting And Viva Preparation

#### Week 25

Objective:

- draft report sections and clean all final figures.

Outputs:

- intro and theory section draft,
- design methodology draft,
- final cleaned plots.

#### Week 26

Objective:

- finalize the project package and viva summary.

Outputs:

- final report package,
- one-page viva sheet,
- final measured spec table,
- short "what improved / what got worse / why" summary.

## Required Final Deliverables

By the end of the project, assemble:

- frozen spec table,
- architecture justification note,
- stability measurement method note,
- hand calculation sheets for gain, `UGB`, `Cc`, and `SR`,
- complete schematic,
- node-labeled architecture diagram,
- gain and phase plots,
- unity-gain step response plots,
- slew-rate plots,
- swing result,
- `Cc` sweep results,
- `CL` sweep results,
- bias sweep results,
- discrepancy log comparing theory and simulation,
- optional DRC/LVS/post-layout evidence,
- final viva summary sheet.

## Good Questions To Be Ready For In The Viva

- Why was a two-stage op-amp chosen instead of a single-stage op-amp?
- Why does adding a second stage create a stability problem?
- What exactly does Miller compensation do?
- What sets the unity-gain bandwidth?
- Why does increasing `Cc` improve phase margin but hurt speed?
- Why can an RHP zero reduce phase margin?
- Why might a series resistor with `Cc` help?
- Why does slew rate scale with available current and `Cc`?
- Why can an amplifier have good gain but poor output swing?
- Why does larger `CL` often degrade stability?
- How did your hand calculations compare with simulation?
- What would you change first if the phase margin were too low?

## Primary Reference Package

At minimum, the report and notes should cite or rely on:

- NPTEL Analog IC Design material for sequence and transistor-level perspective,
- NPTEL Analog Electronic Circuits material for op-amp background,
- Razavi lectures for intuition and stability examples,
- TI stability material for Bode and phase-margin interpretation,
- a design-oriented two-stage sizing flow such as Allen-style lecture notes,
- a documented loop-gain method for the chosen simulator,
- open PDK / open-tool documentation if the project uses SKY130, xschem, ngspice, Magic, or KLayout.

## Resume Line

Designed and verified a Miller-compensated two-stage CMOS op-amp with transistor-level sizing, loop-stability analysis, compensation trade-off exploration, and simulation-based validation of gain, unity-gain bandwidth, phase margin, slew rate, output swing, and load sensitivity.
