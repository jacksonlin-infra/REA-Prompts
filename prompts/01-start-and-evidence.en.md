# Getting Started, Scope, and Evidence Management

[简体中文](01-start-and-evidence.md) | **English**

[Back to the main index](../README.en.md)

For a first investigation, resuming work, or preparing results for handoff. Each code block can be copied independently and focuses on a specific question and a verifiable deliverable.

On this page, “current project” and “output directory” mean your investigation workspace, not the REA source repository. If you have no existing project, choose a new directory. “Save” means writing to that directory; in-session Evidence IDs are not guaranteed to remain readable across processes.

## On this page

- [A01 · Interactive onboarding across clients](#a01)
- [A02 · A minimal overview of an unfamiliar application](#a02)
- [A03 · First exercise: trace an export](#a03)
- [A04 · From a user action to its result](#a04)
- [A05 · Trace a feature from an error message](#a05)
- [A06 · Analyze only one subsystem](#a06)
- [A07 · Turn findings into a verifiable report](#a07)
- [A08 · Resume a long-running investigation](#a08)
- [A09 · Review unresolved questions](#a09)
- [A10 · Export evidence and hand off an investigation](#a10)
- [A11 · Resolve conflicting evidence](#a11)
- [A12 · Continue after truncation or an unavailable tool](#a12)

## A01

**Interactive onboarding across clients**

```text
Act as my REA investigation assistant and explain in English. First read REA-TASK.md in the current project, if it exists, and verify that its target path, version, and digest still match this task.
Determine from the existing conversation what the target is, where it is, which feature to explain, and whether the desired output is an explanation, a specification, or a minimal implementation. Ask only for missing information that blocks progress; do not choose a sample application yourself or scan the entire disk.
Check the current client's REA connection and target-related capabilities. Start when the required capabilities are available; show a setup plan before repairing configuration. Do not block independent routes such as JavaScript because an unrelated native engine is missing.
Record the question, target identity, allowed actions, evidence locations, and next step in REA-TASK.md. Trace one feature first and provide an explanation backed by evidence. Write an implementation in the specified new directory only if I chose that outcome.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A02

**A minimal overview of an unfamiliar application**

```text
Use REA to inspect <absolute target path>, identify its main components, and determine where to begin investigating <business question>.
First return the format, architecture or runtime, key resources, and up to three evidence-backed candidate entry points; do not pad the list. Explore only one entry point relevant to the question, rather than dumping every string or function.
Provide a component table, the reason for choosing an entry point, and the most useful next query. Filenames and dependency names are clues, not direct proof of functionality.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A03

**First exercise: trace an export**

```text
Use REA to inspect <practice application directory or ASAR I provide> and investigate the “Export notes” feature.
Trace from the button or command handler through data selection, CSV encoding, and file writing. Determine how field order, escaping, encoding, and the destination path are chosen.
Provide a short call chain and a sample CSV derived from the code. Without an actual execution record, do not say the original application generated that file.
Use the application graph or search to locate entry points, then inspect relevant functions and source locations to answer each question; do not stop at a module inventory. Mark unproven window/preload loading, dynamic directories, and input origins separately as unknown. State the exact sample input and expected byte representation, including line endings and quotes.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A04

**From a user action to its result**

```text
Use REA to investigate <one specific action> in <target>. Locate its entry point and follow parameters, validation, state changes, and final output.
Separate established connections from missing connections. Leave gaps caused by dynamic dispatch, reflection, IPC, or missing server code as unknowns.
Show “entry → processing → output” with key locations. Do not invent a complete call chain when the evidence is insufficient.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A05

**Trace a feature from an error message**

```text
Use REA to locate references to <exact error text or error code> in <target>, then trace the conditions that produce it and the path that displays it to the user.
Distinguish translated resources, unused strings, and reachable handling logic. Determine which inputs or states could trigger it.
Provide candidate root causes and a minimal test plan that distinguishes them; do not execute the tests in this task.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A06

**Analyze only one subsystem**

```text
Use REA to answer <specific question> about <subsystem> in <target>. The analysis budget is <time or number of calls>, and the scope is limited to <modules/directories/functions/samples>.
Read summaries and existing evidence first, then page through relevant items. Do not reparse the same input merely to get shorter output.
Within the budget, give the most reliable conclusion, the unexamined scope, and whether further analysis could change the conclusion.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A07

**Turn findings into a verifiable report**

```text
Use REA's saved <evidence bundle path or current-session evidence> to prepare a report on <investigation question>.
For each finding, record the conclusion, evidence type, target digest, source location, supporting and opposing evidence, applicable scope, and remaining unknowns. List source-derived reasoning separately from actual runtime observations.
Write the report to <output directory>/REPORT.md and list the minimum additional evidence needed. Do not run the target in this task.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A08

**Resume a long-running investigation**

```text
Use REA to continue the task in <investigation directory>. Read REA-TASK.md and exported evidence bundles, then verify target file digests, tool versions, and unresolved questions.
If the session has ended, do not directly reuse its old in-session IDs. Restore references through exported files or an import method explicitly supported by the current tools.
Repeat only observations whose inputs changed or whose freshness matters. Update the known facts, unknowns, and next steps in INVESTIGATION.md.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A09

**Review unresolved questions**

```text
Use REA to review unresolved questions within <investigation scope>. If the client supports the audit_residual_unknowns prompt workflow, use that prompt. Otherwise, perform the corresponding steps with available tools such as list_unknowns and verify_unknown_resolution; do not call a nonexistent tool with the prompt's name.
Prioritize by “impact on the conclusion × verifiability.” Mark a question resolved only when the evidence meets its requirements. Being out of scope or abandoning an investigation does not establish an answer.
Report each question, its current status, the evidence required, and the smallest next probe.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A10

**Export evidence and hand off an investigation**

```text
Use REA to export complete evidence for <current investigation> to <output directory>, and produce handoff notes.
Include target paths and digests, actual tool and engine versions, operation scope, unresolved questions, and an index linking the report to evidence. Preserve original selections and limitations, not just chat summaries.
Check that the corresponding reader can parse the exported bundle. Explain which live state cannot be restored from an offline bundle. Handle transport credentials and values I explicitly mark sensitive according to the tool's rules.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A11

**Resolve conflicting evidence**

```text
Use REA to examine differing conclusions about <the same question> in <two sets of evidence or reports>.
Compare target digests, platforms, configurations, inputs, sampling times, and coverage before comparing individual fields. Do not automatically replace a result for a different target because another result is newer.
Separate genuine contradictions, different observation conditions, and different interpretations. Propose the smallest plan for collecting additional evidence.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## A12

**Continue after truncation or an unavailable tool**

```text
Use REA to continue <current question>. Read the failure reason or coverage notes first, and determine whether the cause is an output transport limit, an analysis budget, an unconfigured tool, an unsupported host, or an unsupported target.
When retained Evidence exists, use inspect_analysis_view with the returned parent_evidence_id to obtain relevant summaries or pages. Do not repeat the same failed call.
If the required capability is unavailable, finish independent work that is possible and list the remaining prerequisites. Never treat a truncated preview as complete JSON or a complete search result.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```
