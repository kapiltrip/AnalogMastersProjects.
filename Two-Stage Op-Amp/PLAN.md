# Molecular Project Plan: Miller-Compensated Two-Stage CMOS Op-Amp

## End State

The project is complete only when the following exist:

- a frozen numeric spec table,
- a justified two-stage topology choice,
- a first-pass hand-design sheet,
- a transistor-level schematic,
- a verified loop-gain measurement method,
- final AC and transient evidence for gain, `UGB`, phase margin, slew rate, output swing, and load behavior,
- a compensation trade-off story backed by sweeps,
- optional layout and post-layout comparison if layout is in scope.

## Operating Rules

- Do not size transistors before `VDD`, `CL`, gain, `UGB`, phase margin, slew rate, and power are frozen.
- Do not trust any phase-margin result until the loop-break method is cross-checked against transient behavior.
- Every design change must be logged with four fields: what changed, why it changed, what was expected, what actually happened.
- Every phase must end with one artifact and one pass/fail gate.
- If DC bias is wrong, stop and fix bias first. Do not tune compensation before bias is correct.
- If AC and transient conclusions disagree, assume the measurement setup is wrong until proven otherwise.

## Core Design Anchors

Use these relations repeatedly during sizing and review:

- `Av0 ~= (gm1*ro1)*(gm2*ro2)`
- `gm1 ~= 2*pi*UGB*Cc`
- `SR ~= I/Cc`
- `RHP zero ~= gm2/Cc` when no nulling resistor is used
- larger `Cc` usually increases phase margin and reduces `UGB` and slew rate
- larger `CL` usually reduces phase margin and slows settling
- larger bias current usually improves speed and slew rate but increases power

## Spec Freeze Sheet

Fill this before detailed sizing.

| Item | Target | Status | Verification Method |
| --- | --- | --- | --- |
| Process / PDK | TBD | open | device models and minimum lengths confirmed |
| `VDD` | TBD | open | DC bias and swing checks |
| Load capacitance `CL` | TBD | open | load sweep |
| DC gain | TBD | open | loop gain / AC |
| `UGB` | TBD | open | loop gain crossover |
| Phase margin | TBD | open | loop gain phase at crossover |
| Slew rate | TBD | open | large-signal transient |
| Output swing | TBD | open | DC or transient swing bench |
| Power / `Iq` | TBD | open | operating-point current |
| Input common-mode range | TBD | open | DC sweep if in scope |
| CMRR / PSRR | optional | open | AC injection |
| Noise | optional | open | noise analysis |
| Offset | optional | open | Monte Carlo / mismatch |
| Layout required | yes / no | open | DRC/LVS/PEX plan |

## Phase 0: Workspace, Tools, and Spec Freeze

### Objective

Remove ambiguity in the tool flow and freeze the project target before transistor sizing starts.

### Tasks

0.1 Create folders for `notes`, `sizing`, `schematics`, `benches`, `plots`, `report`, and `logs`.

0.2 Choose the simulation flow: Cadence or open-source flow such as xschem + ngspice.

0.3 Record the exact PDK, model files, simulator version, and default corner.

0.4 Decide whether the project is schematic-only or includes layout and extraction.

0.5 Choose a provisional `VDD`.

0.6 Choose a provisional `CL`.

0.7 Choose target DC gain, `UGB`, phase margin, slew rate, output swing, and power.

0.8 Decide whether noise, offset, PSRR, and CMRR are in scope.

0.9 Write a one-page spec note with all numeric targets and all open assumptions.

0.10 Write one paragraph explaining why a two-stage op-amp is required instead of a single-stage op-amp for these targets.

0.11 Define the signoff conditions up front: what will count as pass, fail, and acceptable tolerance.

0.12 Freeze the spec sheet. No silent target changes after this point.

### Outputs

- folder structure,
- tool-flow note,
- frozen spec table v1,
- scope note for optional metrics.

### Exit Gate

You can state all target numbers without using placeholders such as "high gain" or "fast."

## Phase 1: Theory Lock-In

### Objective

Make the compensation and sizing steps predictable instead of trial-and-error.

### Tasks

1.1 Write a short note on open-loop gain versus closed-loop usefulness.

1.2 Draw a single-pole amplifier Bode plot from memory.

1.3 Draw a two-pole amplifier Bode plot from memory.

1.4 Write the link between phase margin and transient ringing in one page.

1.5 Mark the first-stage high-impedance node and the output node in a conceptual two-stage diagram.

1.6 Write where the Miller capacitor `Cc` is connected and what physical effect it creates.

1.7 Derive `gm1 ~= 2*pi*UGB*Cc`.

1.8 Derive `SR ~= I/Cc` for the chosen large-signal scenario.

1.9 Write a short note explaining where the right-half-plane zero comes from.

1.10 Write when and why a series resistor `Rc` is useful.

### Outputs

- feedback note,
- stability note,
- one-page compensation note,
- derivation sheet for `gm1`, `Cc`, and `SR`.

### Exit Gate

You can explain phase margin, pole splitting, and slew-rate limitation without looking up formulas.

## Phase 2: Measurement Infrastructure

### Objective

Prove that the benches and extraction methods are correct before the final design depends on them.

### Tasks

2.1 Define file naming rules for schematics, benches, and plots.

2.2 Create a bench template for DC operating point.

2.3 Create a bench template for AC or loop-gain analysis.

2.4 Create a bench template for closed-loop unity-gain transient response.

2.5 Create a bench template for slew-rate measurement.

2.6 Create a bench template for output-swing measurement.

2.7 Build a simple known amplifier test case and verify that the AC bench behaves as expected.

2.8 Document exactly where the loop will be broken and how DC bias will be preserved.

2.9 Define how DC gain, `UGB`, and phase margin will be extracted from the plots.

2.10 Define the transient step amplitude that will be used for small-signal settling tests.

2.11 Define the larger input step that will be used for slew-rate tests.

### Outputs

- bench templates,
- extraction rules,
- loop-break method note,
- one sanity-check result on a simple amplifier.

### Exit Gate

The same bench setup can be reused later without redefining the measurement method.

## Phase 3: Architecture Freeze

### Objective

Freeze the exact op-amp structure before device sizing begins.

### Tasks

3.1 Choose the input pair type: NMOS or PMOS.

3.2 Choose the active load and current-mirror structure for the first stage.

3.3 Choose the second-stage topology and output node structure.

3.4 Mark all high-impedance internal nodes.

3.5 Mark the expected dominant pole location after compensation.

3.6 Mark the expected non-dominant pole locations.

3.7 Decide whether a nulling resistor `Rc` will be omitted initially or included from the start.

3.8 Decide how bias currents will be generated and mirrored.

3.9 Draw a node-labeled architecture sketch with signal path and bias path separated.

3.10 Write one paragraph explaining the role of each stage.

### Outputs

- architecture sketch,
- node map,
- topology decision note.

### Exit Gate

The schematic topology is fixed and all remaining work is parameter sizing, not architecture guessing.

## Phase 4: First-Pass Hand Design

### Objective

Generate a first design that is numerically defensible before entering the schematic.

### Tasks

4.1 Choose a starting `Cc` using the target `CL` and phase-margin goal.

4.2 Compute the minimum current needed from `SR*Cc`.

4.3 Compute the first-stage `gm1` target from `2*pi*UGB*Cc`.

4.4 Allocate current between stage 1, stage 2, and bias branches.

4.5 Choose first-pass overdrive voltages for key devices.

4.6 Estimate first-stage gain from `gm1*ro1`.

4.7 Estimate second-stage gain from `gm2*ro2`.

4.8 Estimate total open-loop gain.

4.9 Check whether the estimated gain can meet the target at realistic device lengths.

4.10 Check swing headroom at the output node.

4.11 Check common-mode headroom at the input pair.

4.12 Decide whether longer channel devices are needed for gain.

4.13 Estimate whether the RHP zero will be close enough to matter.

4.14 Record all assumptions in a sizing sheet before opening the schematic editor.

### Outputs

- sizing sheet v1,
- gain estimate sheet,
- headroom sheet,
- compensation assumptions note.

### Exit Gate

You have numeric targets for currents, `gm`, estimated gains, and key device dimensions.

## Phase 5: Schematic Entry and DC Bring-Up

### Objective

Turn the paper design into a convergent transistor-level schematic.

### Tasks

5.1 Enter the full transistor-level schematic.

5.2 Label all critical nodes for probing.

5.3 Add bias circuitry and confirm current directions.

5.4 Run a DC operating-point simulation.

5.5 Record all node voltages and all branch currents.

5.6 Check that every key transistor is in the intended region.

5.7 Fix any mirror compliance or saturation failures.

5.8 Check the differential pair tail current against the sizing sheet.

5.9 Check the second-stage current against the sizing sheet.

5.10 Check the output common-mode bias point.

5.11 Update the sizing sheet with actual simulated currents and voltages.

5.12 Freeze schematic v0 only after DC convergence is clean.

### Outputs

- schematic v0,
- DC operating-point table,
- first discrepancy log.

### Exit Gate

The design is biased correctly and no key device is accidentally in triode or cutoff during nominal operation.

## Phase 6: Stability Bring-Up

### Objective

Establish the correct compensation behavior and the correct stability measurement flow.

### Tasks

6.1 Attach `Cc` and rerun DC to confirm no bias breakage.

6.2 Run the loop-gain or equivalent AC analysis.

6.3 Extract low-frequency gain.

6.4 Extract `UGB`.

6.5 Extract phase margin.

6.6 Run a unity-gain closed-loop step response with the same load condition used in AC.

6.7 Compare ringing or overshoot against the measured phase margin.

6.8 If the results disagree, debug the bench before resizing the circuit.

6.9 If phase margin is too low, increase `Cc` or revisit the non-dominant pole assumptions.

6.10 If gain is too low, revisit channel lengths, current allocation, or device operating point.

6.11 If `UGB` is too low, revisit `gm1`, current, and `Cc`.

6.12 Record the exact loop-break setup in the notes so it is reproducible later.

### Outputs

- first gain/phase plot,
- first unity-gain step response,
- stability interpretation note.

### Exit Gate

AC and transient results tell the same stability story within reasonable consistency.

## Phase 7: Large-Signal and Swing Verification

### Objective

Verify the main time-domain and headroom specifications before tuning trade-offs.

### Tasks

7.1 Run a large-signal rising slew-rate test.

7.2 Run a large-signal falling slew-rate test.

7.3 Record the input step size used in the slew-rate tests.

7.4 Check whether slew rate matches the `I/Cc` expectation directionally.

7.5 Run an output-swing bench at nominal load.

7.6 Identify which device limits positive swing.

7.7 Identify which device limits negative swing.

7.8 Run a closed-loop settling test with a small input step.

7.9 Record overshoot, settling trend, and any long tail due to secondary poles.

7.10 Update the discrepancy log with theory-versus-simulation gaps.

### Outputs

- slew-rate plots,
- output-swing result,
- settling observation note.

### Exit Gate

The design has first-pass results for gain, `UGB`, phase margin, slew rate, settling, and swing.

## Phase 8: Controlled Trade-Off Sweeps

### Objective

Turn the design from a working schematic into a documented engineering trade-off.

### Tasks

8.1 Sweep `Cc` across at least three to five values.

8.2 Plot phase margin versus `Cc`.

8.3 Plot `UGB` versus `Cc`.

8.4 Plot slew rate versus `Cc`.

8.5 Sweep `CL` across the expected load range.

8.6 Plot stability trend versus load.

8.7 Add or remove `Rc` and compare phase response.

8.8 If `Rc` is used, sweep `Rc` and record which value gives the best trade-off.

8.9 Sweep second-stage current and record gain, speed, and power changes.

8.10 Sweep first-stage current if `UGB` or noise behavior must be explored.

8.11 Record one paragraph for each sweep explaining why the trend makes sense physically.

8.12 Choose the final `Cc`, final `Rc`, and final current allocation.

### Outputs

- trade-off plots,
- final compensation choice note,
- updated schematic v1.

### Exit Gate

The final parameter choices are justified by measured trends, not by a single lucky simulation.

## Phase 9: Final Pre-Layout Signoff

### Objective

Produce the full evidence package that can go into the report and viva.

### Tasks

9.1 Rerun DC operating point on the final schematic.

9.2 Rerun final loop-gain measurement.

9.3 Rerun final unity-gain transient.

9.4 Rerun final slew-rate tests.

9.5 Rerun final output-swing test.

9.6 Run `CL` sweep on the final schematic.

9.7 Run `VDD` sweep if supply sensitivity is in scope.

9.8 Run common-mode sweep if ICMR is in scope.

9.9 Run noise analysis if noise is in scope.

9.10 Run corners or mismatch if models and scope allow it.

9.11 Build a pass/fail table against every frozen target.

9.12 Build a theory-versus-simulation summary table.

### Outputs

- final pre-layout plot set,
- final measured spec table,
- final pass/fail summary,
- discrepancy log vfinal.

### Exit Gate

Every frozen target has either a passing result or a written explanation for the miss.

## Phase 10: Optional Layout and Post-Layout Closure

### Objective

Capture the physical-design portion without losing schematic reproducibility.

### Tasks

10.1 Mark matching-critical devices: input pair, active loads, mirrors, bias devices.

10.2 Plan the floorplan with the first-stage high-impedance node treated as sensitive.

10.3 Route the compensation path deliberately and keep parasitics controlled.

10.4 Complete layout placement and routing.

10.5 Pass DRC.

10.6 Pass LVS.

10.7 Extract parasitics.

10.8 Rerun gain, `UGB`, phase margin, and transient benches on the extracted netlist.

10.9 Compare pre-layout and post-layout results in one delta table.

10.10 If post-layout fails badly, make one targeted fix at a time and remeasure.

### Outputs

- layout screenshot set,
- DRC and LVS reports,
- extracted-netlist results,
- pre-layout versus post-layout delta note.

### Exit Gate

The post-layout circuit either passes or has a specific documented physical cause for the remaining gap.

## Required Result Set

Do not call the project complete unless these exist:

- frozen spec table,
- sizing sheet,
- architecture sketch,
- DC operating-point table,
- gain/phase plot,
- unity-gain step response,
- slew-rate plots,
- output-swing result,
- `Cc` sweep,
- `CL` sweep,
- bias-current sweep,
- `Rc` comparison or explicit no-`Rc` justification,
- final pass/fail table,
- optional DRC/LVS/PEX evidence.

## 26-Week Molecular Schedule

| Week | Focus | Required Output |
| --- | --- | --- |
| 1 | workspace setup and tool sanity | folders, tool note, first DC/AC sanity run |
| 2 | feedback and closed-loop basics | one-page feedback note |
| 3 | poles, zeros, phase margin | stability note and Bode sketches |
| 4 | freeze specs and architecture | frozen spec sheet and topology note |
| 5 | node map and stage-role study | labeled architecture sketch |
| 6 | choose `Cc` and derive current / `gm1` | compensation sheet |
| 7 | estimate gains and headroom | gain and swing worksheet |
| 8 | enter schematic v0 | transistor-level schematic |
| 9 | clean DC bias | operating-point table |
| 10 | build loop-gain bench | first AC plot |
| 11 | cross-check AC with transient | first step response and PM note |
| 12 | measure slew rate and swing | SR and swing plots |
| 13 | `Cc` sweep | PM / `UGB` / SR versus `Cc` plots |
| 14 | `CL` sweep | load-sensitivity plots |
| 15 | `Rc` study | zero-control comparison note |
| 16 | current-allocation sweep | power-speed trade-off plots |
| 17 | freeze refined schematic | schematic v1 and decision log |
| 18 | rerun final AC/transient suite | final gain, PM, step results |
| 19 | rerun final slew and swing suite | final SR and swing results |
| 20 | supply / ICMR / optional noise | extended verification plots |
| 21 | layout planning | floorplan and matching checklist |
| 22 | layout implementation | placed-and-routed core |
| 23 | DRC and LVS | clean verification reports |
| 24 | extraction and post-layout reruns | post-layout result set |
| 25 | report figure cleanup | final plot package |
| 26 | thesis / viva packaging | final tables, summary sheet, archive |

## Weekly Operating Loop

Repeat this every week:

1. Read or watch only the material needed for the current phase.
2. Write one short note in your own words.
3. Produce one calculation sheet or design update.
4. Run one new bench or sweep.
5. Save one plot or table with a clear filename.
6. Write one failure note and one next-step note.

## Viva Preparation Questions

Be able to answer these directly:

- Why was a two-stage op-amp necessary?
- Why does the second stage create a stability problem?
- What exactly does Miller compensation change?
- What sets `UGB`?
- Why does a larger `Cc` improve phase margin but reduce speed?
- Why can an RHP zero hurt phase margin?
- Why might `Rc` help?
- Why does slew rate scale with available current and `Cc`?
- Why can gain be good while output swing is poor?
- Why does larger `CL` often reduce stability margin?
