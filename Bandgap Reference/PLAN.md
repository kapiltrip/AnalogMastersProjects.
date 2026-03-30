# Molecular Project Plan: Bandgap Voltage Reference

## End State

The project is complete only when the following exist:

- a frozen numeric spec table,
- a justified topology choice,
- a clean derivation of `Vref = VBE + k*DeltaVBE`,
- a convergent schematic with explicit startup behavior,
- a full verification suite across temperature, supply, load, corners, and mismatch,
- optional layout and post-layout closure if layout is in scope,
- a final pass/fail table and thesis-ready plot package.

## Operating Rules

- Do not commit to a topology until `VDD` range, target `Vref`, temperature range, and trim policy are frozen.
- Do not call the reference "good" based only on room-temperature `Vref`.
- Startup is mandatory from the first serious schematic revision onward.
- Every design change must be logged with what changed, why it changed, expected effect, and measured effect.
- Every phase must end with one artifact and one pass/fail gate.
- If temperature behavior looks right but line regulation or PSRR is weak, keep the design in debug. Do not declare success early.

## Core Design Anchors

Use these relations repeatedly during derivation and review:

- `VBE` is CTAT
- `DeltaVBE = VT*ln(N)` is PTAT
- `Vref = VBE + k*DeltaVBE`
- first-order temperature cancellation requires `dVref/dT ~= 0` near the chosen reference temperature
- resistor ratio sets `k`
- emitter area ratio or current-density ratio sets `ln(N)`
- startup, resistor mismatch, finite beta, offset, and supply sensitivity disturb the ideal result

## Spec Freeze Sheet

Fill this before detailed design.

| Item | Target | Status | Verification Method |
| --- | --- | --- | --- |
| Process / PDK | TBD | open | confirm BJT devices, resistor options, corners |
| Supply range | TBD | open | DC sweep from `VDDmin` to `VDDmax` |
| Nominal `Vref` | TBD | open | operating-point result at nominal corner |
| Temperature range | TBD | open | `Vref(T)` sweep |
| Tempco target | TBD | open | tempco extraction from sweep |
| Line regulation | TBD | open | `Vref(VDD)` sweep |
| Load regulation | TBD | open | load current or resistance sweep |
| PSRR | TBD | open | AC supply injection |
| Output noise | TBD | open | noise analysis |
| Startup | must pass | open | transient with multiple ramp rates |
| Quiescent current | TBD | open | nominal and worst-corner operating point |
| Load range | TBD | open | load sweep |
| Trim policy | none / 1-point / 2-point | open | trim plan note |
| Layout required | yes / no | open | DRC/LVS/PEX plan |

## Phase 0: Workspace, Scope, and Spec Freeze

### Objective

Remove ambiguity in project scope before any topology is chosen.

### Tasks

0.1 Create folders for `notes`, `derivations`, `schematics`, `benches`, `plots`, `report`, and `logs`.

0.2 Choose the simulation flow and record tool versions.

0.3 Record the exact PDK and available BJT and resistor devices.

0.4 Freeze the intended `VDD` range.

0.5 Freeze the target `Vref`.

0.6 Freeze the required temperature range.

0.7 Freeze the expected output load range.

0.8 Decide whether trimming is allowed.

0.9 Decide whether layout is mandatory.

0.10 Decide whether the project is classic bandgap, buffered bandgap, curvature-corrected extension, or low-voltage branch.

0.11 Write a one-page spec note with all numeric targets and all open assumptions.

0.12 Freeze the signoff conditions for tempco, line regulation, load regulation, PSRR, startup, and current.

### Outputs

- folder structure,
- tool note,
- frozen spec table v1,
- scope note for trim and layout.

### Exit Gate

You can state all major targets numerically and the topology branch is no longer ambiguous.

## Phase 1: Theory Lock-In

### Objective

Make the first schematic a result of derivation rather than guesswork.

### Tasks

1.1 Write one page explaining why `VBE` alone is not a stable reference.

1.2 Derive `DeltaVBE = VT*ln(N)` from unequal current density or emitter area.

1.3 Derive `Vref = VBE + k*DeltaVBE`.

1.4 Derive the first-order zero-tempco condition around the chosen reference temperature.

1.5 Choose a first-pass area ratio `N`.

1.6 Compute a first-pass `DeltaVBE` at room temperature.

1.7 Compute the resistor ratio needed for first-order cancellation.

1.8 Build a sensitivity table for resistor ratio error, BJT mismatch, finite beta, offset, and supply variation.

1.9 Write one note on why startup is a real issue in bandgap loops.

1.10 Write one note on what limits PSRR and line regulation in the chosen topology class.

### Outputs

- derivation note,
- first-pass `N` choice,
- first-pass resistor-ratio target,
- sensitivity table.

### Exit Gate

You can explain each term in `Vref = VBE + k*DeltaVBE` and how nonidealities disturb it.

## Phase 2: Topology Freeze

### Objective

Choose the simplest topology that can meet the frozen spec.

### Tasks

2.1 Compare at least three candidates: canonical bandgap, Brokaw-style cell, op-amp-assisted bandgap, or low-voltage branch if required.

2.2 Reject any topology that cannot meet `VDDmin` with realistic headroom.

2.3 Reject any topology that adds complexity without helping the frozen spec.

2.4 Decide whether an output buffer is required.

2.5 Decide whether trimming hooks are required now or only as future work.

2.6 Decide whether curvature correction is in scope or explicitly out of scope.

2.7 Draw a block diagram with PTAT path, CTAT path, summing mechanism, startup path, and output path.

2.8 Write one paragraph explaining why the chosen topology is lower risk than the rejected options.

### Outputs

- topology decision memo,
- block diagram,
- scope boundary note.

### Exit Gate

The topology is fixed and all later changes are sizing or implementation changes, not architecture changes.

## Phase 3: First-Pass Hand Design

### Objective

Translate the derivation into first-pass device and resistor choices.

### Tasks

3.1 Choose the area ratio implementation method using available devices.

3.2 Choose resistor types that are available and layout-friendly.

3.3 Convert the required PTAT gain into resistor ratio targets.

3.4 Estimate nominal branch currents.

3.5 Check whether resistor values are practical for area and noise.

3.6 Check whether branch currents are practical for power and startup.

3.7 Estimate the nominal output voltage at room temperature.

3.8 Estimate the slope direction if the PTAT term is too strong.

3.9 Estimate the slope direction if the PTAT term is too weak.

3.10 Decide which quantities will be tuned first during simulation: area ratio, resistor ratio, or current level.

3.11 Record all assumptions before opening the schematic editor.

### Outputs

- hand-design worksheet,
- resistor-ratio sheet,
- branch-current estimate sheet.

### Exit Gate

You have numeric first-pass values for ratios, currents, and expected `Vref`.

## Phase 4: Baseline Schematic Entry

### Objective

Enter the core reference loop and verify that it lands in the correct operating region.

### Tasks

4.1 Enter the baseline schematic without startup extras first.

4.2 Label PTAT, CTAT, and output nodes clearly.

4.3 Run a room-temperature operating-point simulation.

4.4 Record node voltages and branch currents.

4.5 Confirm that the PTAT term is positive and in the expected range.

4.6 Confirm that the CTAT term is present and in the expected range.

4.7 Check that the output `Vref` is in the correct ballpark.

4.8 If the circuit biases to a zero-current state, document it instead of hiding it.

4.9 Adjust only the minimum number of parameters needed to land close to the hand-design target.

4.10 Freeze schematic v0 once the core loop operates correctly at nominal conditions.

### Outputs

- schematic v0,
- room-temperature operating-point table,
- first discrepancy log.

### Exit Gate

The baseline loop produces a valid nominal `Vref` and the PTAT and CTAT terms behave in the expected direction.

## Phase 5: Startup and Load Readiness

### Objective

Make the reference practical rather than nominally correct.

### Tasks

5.1 Add explicit startup circuitry.

5.2 Define multiple supply ramp profiles: slow, nominal, and fast.

5.3 Run startup transient at nominal temperature.

5.4 Run startup transient at hot temperature.

5.5 Run startup transient at cold temperature.

5.6 Run startup transient at supply extremes.

5.7 Decide whether an output buffer is needed for the intended load.

5.8 If a buffer is needed, add it and rerun operating-point checks.

5.9 Define the output load model.

5.10 Run the first load-regulation sweep.

5.11 Record startup pass/fail rules and load-regulation extraction rules.

### Outputs

- startup note,
- startup transient set,
- load model note,
- first load-regulation plot.

### Exit Gate

The circuit starts reliably from all defined ramp cases and can support the intended load model.

## Phase 6: Temperature Bring-Up

### Objective

Tune the reference against temperature before building the rest of the signoff flow.

### Tasks

6.1 Run a coarse temperature sweep.

6.2 Plot `Vref(T)`.

6.3 Extract the slope near room temperature.

6.4 Decide whether the PTAT term is too strong or too weak.

6.5 Adjust resistor ratio or branch scaling in the smallest useful increment.

6.6 Rerun the temperature sweep after each controlled change.

6.7 Record the direction and reason for every tuning change.

6.8 Run a finer temperature sweep once the coarse trend is acceptable.

6.9 Extract tempco using one documented method and keep that method fixed.

### Outputs

- `Vref(T)` plot set,
- tempco result,
- temperature-tuning log.

### Exit Gate

The reference has a controlled and documented temperature trend, not an accidental one.

## Phase 7: Full Pre-Layout Verification

### Objective

Build the complete evidence package before layout starts.

### Tasks

7.1 Run the final temperature sweep on the pre-layout schematic.

7.2 Run the full `VDD` sweep and extract line regulation.

7.3 Run the full load sweep and extract load regulation.

7.4 Run PSRR analysis over frequency.

7.5 Record PSRR at the main report frequencies you will use later.

7.6 Run output-noise analysis if noise is in scope.

7.7 Run process corners.

7.8 Run corner-plus-temperature combinations if supported.

7.9 Run Monte Carlo for mismatch.

7.10 Extract `mean`, `sigma`, and yield-style summaries from Monte Carlo.

7.11 Identify the top three failure mechanisms from the full bench set.

7.12 Build a pass/fail table against the frozen spec.

### Outputs

- pre-layout signoff plot set,
- line-regulation result,
- load-regulation result,
- PSRR plot,
- optional noise plot,
- corner table,
- Monte Carlo histogram,
- pass/fail summary.

### Exit Gate

Every frozen spec item has a measured result or a written justification for why it is outside scope.

## Phase 8: Optimization and Freeze

### Objective

Make targeted fixes and freeze the pre-layout design.

### Tasks

8.1 Rank the failures by impact: startup, tempco, line regulation, load regulation, PSRR, mismatch, current.

8.2 Change one parameter family at a time: ratio, current, buffer strength, or startup path.

8.3 Rerun only the affected benches after each small change.

8.4 When a change helps one metric and hurts another, write the trade-off explicitly.

8.5 Decide whether trim hooks are necessary based on mismatch and tempco results.

8.6 If trim is added, define the trim granularity and the bench used to evaluate it.

8.7 Freeze schematic v1 only after the main metrics are stable.

8.8 Archive the final pre-layout netlist, benches, and result set.

### Outputs

- schematic v1,
- optimization log,
- final pre-layout archive list.

### Exit Gate

The pre-layout design is frozen and reproducible.

## Phase 9: Layout and Matching Execution

### Objective

Implement the physical design without destroying the ratio accuracy and sensitivity assumptions.

### Tasks

9.1 Mark ratio-critical devices and resistor groups.

9.2 Build a matching map for BJTs, resistors, mirrors, and any trim arrays.

9.3 Choose unit-device decomposition for ratio-critical structures.

9.4 Use common-centroid or interdigitated structures where gradients matter.

9.5 Add dummies where matching quality depends on edge effects.

9.6 Keep PTAT and CTAT routing balanced where symmetry matters.

9.7 Keep noisy or high-current routes away from `Vref`.

9.8 Complete layout placement.

9.9 Complete routing.

9.10 Pass DRC.

9.11 Pass LVS.

9.12 Extract parasitics.

### Outputs

- floorplan sketch,
- matching checklist,
- layout screenshots,
- DRC and LVS reports,
- extracted netlist.

### Exit Gate

The extracted design matches the intended schematic and the physical implementation is clean enough to trust the post-layout benches.

## Phase 10: Post-Layout Closure

### Objective

Repeat the exact verification flow on the extracted design and quantify the delta.

### Tasks

10.1 Rerun temperature sweep post-layout.

10.2 Rerun line-regulation sweep post-layout.

10.3 Rerun load-regulation sweep post-layout.

10.4 Rerun startup tests post-layout.

10.5 Rerun PSRR post-layout.

10.6 Rerun noise if it is in scope.

10.7 Rerun corners.

10.8 Rerun Monte Carlo if the project scope requires post-layout mismatch evidence.

10.9 Build a pre-layout versus post-layout delta table.

10.10 If post-layout degradation is severe, make one focused layout fix at a time and remeasure.

### Outputs

- post-layout plot set,
- post-layout pass/fail table,
- delta summary note.

### Exit Gate

Post-layout behavior is either signed off or tied to a specific physical cause with written evidence.

## Required Result Set

Do not call the project complete unless these exist:

- frozen spec table,
- derivation note,
- topology decision note,
- hand-design worksheet,
- room-temperature operating-point table,
- startup transient set,
- `Vref(T)` plot and tempco result,
- `Vref(VDD)` plot and line-regulation result,
- load-regulation plot,
- PSRR plot,
- optional noise plot,
- corner table,
- Monte Carlo histogram,
- final pass/fail table,
- optional DRC/LVS/PEX evidence.

## 26-Week Molecular Schedule

| Week | Focus | Required Output |
| --- | --- | --- |
| 1 | workspace setup and spec freeze | folders, tool note, frozen spec sheet |
| 2 | PTAT / CTAT fundamentals | concept note and bibliography start |
| 3 | derive `DeltaVBE` and first-pass ratios | derivation note and first-pass ratio sheet |
| 4 | topology decision | topology memo and block diagram |
| 5 | hand design and nominal current estimates | branch-current and resistor worksheet |
| 6 | baseline schematic entry | schematic v0 and operating-point table |
| 7 | coarse temperature sweep and first tuning | `Vref(T)` plot v1 |
| 8 | startup circuit and ramp tests | startup plot set |
| 9 | load model and load sweep | load-regulation plot |
| 10 | `VDD` sweep and line regulation | `Vref(VDD)` plot |
| 11 | PSRR bench | PSRR plot and key-frequency table |
| 12 | noise bench if in scope | noise result |
| 13 | corners | corner summary table |
| 14 | Monte Carlo | histogram and `mean/sigma` summary |
| 15 | targeted tuning | optimization log |
| 16 | freeze pre-layout schematic | schematic v1 and signoff table |
| 17 | layout planning and matching map | floorplan and matching checklist |
| 18 | ratio-critical placement | placement review snapshot |
| 19 | routing and DRC cleanup | routed layout and DRC report |
| 20 | LVS and extraction | LVS report and PEX netlist |
| 21 | post-layout temp and line-regulation reruns | post-layout sweep set |
| 22 | post-layout startup, load, and PSRR reruns | post-layout dynamic plots |
| 23 | post-layout corners and optional Monte Carlo | worst-case summary |
| 24 | final layout fixes or freeze | delta note and freeze decision |
| 25 | report figure cleanup | final plot package |
| 26 | thesis / viva packaging | final tables, summary sheet, archive |

## Weekly Operating Loop

Repeat this every week:

1. Read only the material needed for the active phase.
2. Write one short note in your own words.
3. Update one derivation, ratio sheet, or schematic.
4. Run one new bench or sweep.
5. Save one plot or table with a clear filename.
6. Write one failure note and one next-step note.

## Viva Preparation Questions

Be able to answer these directly:

- Why is `VBE` alone not a stable reference?
- Why is `DeltaVBE` PTAT?
- How do area ratio and resistor ratio set `Vref`?
- Why is startup a real problem in bandgap loops?
- What causes line-regulation error?
- What limits PSRR at low and high frequency?
- Why can a good room-temperature `Vref` still be a bad reference?
- What does Monte Carlo show that corners do not?
- Why can layout disturb bandgap accuracy?
- Why was this topology chosen instead of a low-voltage or curvature-corrected alternative?
