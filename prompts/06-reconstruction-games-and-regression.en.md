# Feature Reconstruction, Games, Versions, and Regression

[简体中文](06-reconstruction-games-and-regression.md) | **English**

[Back to the main index](../README.en.md)

REA provides investigation, comparison, and evidence evaluation. Ordinary development tools implement code, build WASM, and run project tests. Implementing from behavior alone does not automatically establish a strict organizational clean-room process.

References: [Evidence workflows](https://github.com/morluto/rea/blob/main/.agents/skills/reverse-engineer-anything/references/evidence-workflows.md), [Process capture](https://github.com/morluto/rea/blob/main/docs/process-capture.md), [Recorded crashes](https://github.com/morluto/rea/blob/main/docs/recorded-crashes.md).

## On this page

- [F01 · A behavioral specification for one feature](#f01)
- [F02 · Build a minimal implementation from a specification](#f02)
- [F03 · Stage a reconstruction across multiple features](#f03)
- [F04 · Verify a finite specification](#f04)
- [F05 · One mechanic in an offline game](#f05)
- [F06 · Game assets and save-file compatibility](#f06)
- [F07 · Data entry points for single-player mods](#f07)
- [F08 · Assess WASM port feasibility](#f08)
- [F09 · Implement a logic core for the browser](#f09)
- [F10 · Choose a version comparison by target type](#f10)
- [F11 · Behavioral regression for a command-line program](#f11)
- [F12 · From crash evidence to candidate root causes](#f12)
- [F13 · CTF and self-owned validation-algorithm exercises](#f13)

## F01

**A behavioral specification for one feature**

```text
Use REA to investigate <one feature> in <program>. Record triggers, inputs, outputs, state changes, errors, and edge cases in <output directory>/SPEC.md.
Link every specification item to evidence. Separate confirmed original behavior, implementation choices, and unknowns. Perform only static investigation; list pending tests when runtime evidence is missing.
Do not copy original code, assets, or branding, or include unexamined features in a promise of “complete reconstruction.”

Use REA for investigation and evidence, and ordinary development tools for implementation and testing. Preserve the original materials in the specified output directory, cite evidence for each rule, and explicitly mark unverified parts.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F02

**Build a minimal implementation from a specification**

```text
Use REA to verify the evidence references in <SPEC.md>, then implement <bounded feature> in <language/framework> inside <new project directory>.
Test normal inputs, boundaries, errors, and state transitions using <original input/output samples> I provide. Design the implementation yourself without copying target code.
Do not run the original program. Provide run instructions, tests actually passed, untested areas, and differences. One matching example does not establish global equivalence.
Expected results must come from original samples or the cited specification; outputs produced by the new implementation cannot serve as its own correctness oracle. Add specification-derived tests for uncovered branches and label them separately, without claiming they passed comparison against the original.

Use REA for investigation and evidence, and ordinary development tools for implementation and testing. Preserve the original materials in the specified output directory, cite evidence for each rule, and explicitly mark unverified parts.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F03

**Stage a reconstruction across multiple features**

```text
Use REA to investigate <explicit feature list> in <application> in stages. Begin with a table of “feature—entry point—evidence—unknowns—acceptance cases.”
Select one minimal end-to-end slice and write its behavioral specification and implementation plan. Prioritize remaining features by dependencies and uncertainty.
This round is limited to static investigation and planning. Do not treat a program without source as directly recompilable, or promise every unlisted interface and feature.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F04

**Verify a finite specification**

```text
Use REA to evaluate how well <implementation> satisfies <explicit specification items>.
Check that existing artifact/function/process or other comparison Evidence corresponds to the targets and specification. Generate missing static comparison Evidence from the supplied original and implementation materials. Then construct a finite specification and evidence bundle according to verify_reconstruction's actual schema. Mark items as unknown when materials are missing or execution would be required.
Report pass, fail, and unknown separately with their corresponding authority sources. Limit this task to static analysis and evidence evaluation; do not run the original or new implementation. A pass covers only the declared requirements.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F05

**One mechanic in an offline game**

```text
Use REA to statically investigate <one of movement/difficulty/scoring/spawning> in <offline game>.
Locate the update loop, constants, randomness or time sources, and explain integer overflow, rounding, and frame-rate assumptions. Preserve candidates when the mechanic is uncertain.
Write a small standalone simulator in <output directory> and validate it against existing samples. Do not modify the original game, reconstruct the entire game, or run undeclared targets.

Use REA for investigation and evidence, and ordinary development tools for implementation and testing. Preserve the original materials in the specified output directory, cite evidence for each rule, and explicitly mark unverified parts.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F06

**Game assets and save-file compatibility**

```text
Use REA to analyze how <offline game> reads <asset or save format>. Use <sample copies> to trace versions, fields, checksums, and failure paths.
Produce a description of the confirmed format scope and a read-only checker, testing truncation and version mismatches on copies.
Do not replace original saves or distribute original game assets. Client save logic does not establish an online game's server-side state rules.

Use REA for investigation and evidence, and ordinary development tools for implementation and testing. Preserve the original materials in the specified output directory, cite evidence for each rule, and explicitly mark unverified parts.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F07

**Data entry points for single-player mods**

```text
Use REA to statically locate whether <one parameter> in <offline single-player game> comes from configuration, scripts, resource tables, or code constants.
Record loading order, defaults, bounds, and dependencies. Prioritize existing configuration or plugin extension points.
Provide locations and a plan for experiments on copies. Do not create online cheating tools or modify process memory; a constant's address is not a stable cross-version interface.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F08

**Assess WASM port feasibility**

```text
Use REA to investigate dependencies of <bounded logic core> in <native game release artifact> on graphics, threads, files, audio, and platform APIs.
Also establish whether <legally available source code> exists. Discuss toolchain compilation only when source is available. With binaries alone, estimate rule reconstruction and a replacement implementation; do not promise direct binary-to-WASM compilation.
Provide a dependency matrix, evidence, performance questions that need measurement, and a minimal browser demo plan. Use development tools for ordinary source-architecture reading rather than forcing it through REA.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F09

**Implement a logic core for the browser**

```text
Using <rule specification and test samples> verified through REA, implement <bounded logic> in <C/Rust/another language> in <new project directory>, and build WASM with the project's toolchain.
Validate numerical precision, random seeds, time steps, and input sequences before adding JS calls and a demo page. If the original state cannot be exported, compare observable outputs instead; do not invent original state hashes.
Run only the new implementation and tests, not the original. List the passing scope, measured performance, and unmeasured costs.

Use REA for investigation and evidence, and ordinary development tools for implementation and testing. Preserve the original materials in the specified output directory, cite evidence for each rule, and explicitly mark unverified parts.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F10

**Choose a version comparison by target type**

```text
Use REA to compare <feature> between <old version path> and <new version path>, first confirming file digests, architectures, build types, and input scope.
Use compare_application_versions for JavaScript application graphs, compare_managed_members for managed members, compare_artifacts for package inventories, and compare_functions for explicit native-function evidence.
Report structural changes, candidate behavior changes, and unmatched items. Do not directly label compiler differences, renaming, or address movement as business behavior changes.
Analyze each version first and produce or reuse full Evidence of the required type, then pass that Evidence or current-session retained references to the comparison tool. Do not pass file paths or summary projections as comparison inputs. Inspect source locations for relevant differences to explain the concrete change; unmatched nodes indicate unresolved identity, not necessarily added or removed functionality.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F11

**Behavioral regression for a command-line program**

```text
Use REA in a supported Linux/macOS environment to run <original command> and <new-version command> separately. The scenario is <explicit arguments, inputs, and interactions>, with <test directory> as the working directory and observation paths.
Use comparable capture_process_scenario scenarios and compare their Evidence. Record terminal behavior, exit, descendant settlement, and selected file results.
Targets execute with the current user's permissions; observation paths are not access restrictions. Run only these specified scenarios. Report timeouts, truncation, and uncontrolled environment differences; matching output does not establish complete equivalence.

Use only the targets and actions specified above; report missing devices, permissions, or capabilities. Cite Evidence IDs, the observation scope, and time, distinguishing actual observations from inferences.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F12

**From crash evidence to candidate root causes**

```text
Use REA to investigate <stack trace/log/dump> for <program and version>. Identify the dump format and target identity first.
Use inspect_recorded_crash only for a supported Linux x86-64 ELF core when dependencies are ready. Keep other dumps as external material; do not claim REA has parsed them.
Relate registers, signals, and threads to static-function evidence. Report candidate root causes and the smallest distinguishing experiment. Historical PIDs do not select current processes. Do not run a reproduction in this task.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## F13

**CTF and self-owned validation-algorithm exercises**

```text
Use REA to statically analyze <validation question> in <my own teaching sample or an explicit CTF file>.
Trace input encoding, transformations, comparisons, and success/failure branches. Verify key instructions before deriving an input that satisfies the challenge.
Provide an address-to-instruction-to-conclusion evidence chain and offline algorithm tests. Do not extend the teaching sample's authorization to other commercial products, modify the sample, or run unknown binaries.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```
