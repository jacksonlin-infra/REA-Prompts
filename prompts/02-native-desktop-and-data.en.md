# Native Programs, Desktop Applications, and Local Data

[简体中文](02-native-desktop-and-data.md) | **English**

[Back to the main index](../README.en.md)

Deep native analysis requires a working engine such as Hopper, Ghidra, or IDA. Verify format, CPU, and host support individually. Go/Rust metadata, PE resources, and managed assemblies have independent static routes; do not always start by opening a native engine.

References: [Native investigation](https://github.com/morluto/rea/blob/main/docs/native-investigation.md), [Managed code](https://github.com/morluto/rea/blob/main/docs/managed-code-analysis.md), [SQLite](https://github.com/morluto/rea/blob/main/docs/sqlite-databases.md).

## On this page

- [B01 · Binary triage](#b01)
- [B02 · A function and its context](#b02)
- [B03 · A file format and a minimal reader](#b03)
- [B04 · Serialization and communication protocols](#b04)
- [B05 · .NET business logic](#b05)
- [B06 · The boundary between .NET and native libraries](#b06)
- [B07 · Go release artifacts and dependencies](#b07)
- [B08 · Rust release artifacts and dependencies](#b08)
- [B09 · macOS and iOS package structure](#b09)
- [B10 · Windows resources and localization](#b10)
- [B11 · The SQLite storage model](#b11)
- [B12 · Checks before migrating local data](#b12)
- [B13 · Plugin and dynamic-library loading](#b13)
- [B14 · Observe a native macOS window](#b14)

## B01

**Binary triage**

```text
Use REA to analyze <executable or library>, identifying its format, architecture, entry points, sections or segments, imports, exports, and relevant strings.
Select the functions most worth investigating for <target feature>. High entropy, unusual imports, or few strings are only clues to compression, packing, or obfuscation, not conclusive evidence by themselves.
Produce a one-page triage report naming the selected engine and the analysis dimensions it cannot support.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B02

**A function and its context**

```text
Use REA to analyze <exact function name or address> in <binary path>. Obtain available pseudocode, assembly, direct call relationships, cross-references, and related constants.
Explain inputs, outputs, branches, and possible data structures. Decompiled types and automatic names are recovered interpretations; verify against instructions when necessary.
Do not claim that indirect call targets or global-variable inventories are complete. Label addresses with their module, architecture, and address kind.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B03

**A file format and a minimal reader**

```text
Use REA with <program> and <a set of sample files> to investigate the parsing logic for <file type>.
Record field offsets, lengths, byte order, versions, checksums, and unknown regions. Test field interpretations against different samples.
Write a minimal read-only parser in <output directory>, with explicit errors for truncation, invalid lengths, and unknown versions. Parse only the samples; do not run the target program or generalize one sample's interpretation into a complete format.

Use REA for investigation and evidence, and ordinary development tools for implementation and testing. Preserve the original materials in the specified output directory, cite evidence for each rule, and explicitly mark unverified parts.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B04

**Serialization and communication protocols**

```text
Use REA to statically analyze the encoding and decoding paths for <specific message> in <program>, using <existing message samples> to recover fields.
Distinguish length prefixes, byte order, encoding, message types, checksums, and compression. Preserve raw bytes and candidate interpretations for uncertain fields.
Produce a protocol draft and offline parsing/construction examples. Do not connect to or send messages to real endpoints. Choose a concrete representation such as struct or protobuf only when supported by evidence.

Use REA for investigation and evidence, and ordinary development tools for implementation and testing. Preserve the original materials in the specified output directory, cite evidence for each rule, and explicitly mark unverified parts.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B05

**.NET business logic**

```text
Use REA to statically inspect <type or business feature> in <PE/CLI assembly>. Confirm that the file contains parseable managed metadata before selecting members.
Trace CIL, method calls, field reads and writes, and exception paths. Explain the rules in business-oriented language.
Do not promise automatic recovery of the original C#. Mark missing method bodies, obfuscation, or dynamically generated logic as unknown. Unity Mono can use this route; do not treat IL2CPP as an ordinary managed assembly.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B06

**The boundary between .NET and native libraries**

```text
Use REA to inspect P/Invoke or other native dependency declarations from <assembly> to <native library>.
List method signatures, library names, entry points, calling conventions, and marshaling clues. Check candidate bindings against export and function evidence from <corresponding native library> that I provide.
Report matches, conflicts, and unknowns. A matching declaration and export name does not prove that the library was loaded at runtime or that marshaling semantics are identical.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B07

**Go release artifacts and dependencies**

```text
Use REA's inspect_go_binary to inspect <Go binary>, recording compiler markers, modules, replacement dependencies, and build settings.
Focus on <dependency or build option>, preserving local replacement paths, development versions, and unparsed records.
Produce a dependency evidence table for the release artifact. Missing metadata does not prove it is not Go; an embedded version is not authenticated build provenance.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B08

**Rust release artifacts and dependencies**

```text
Use REA's inspect_rust_binary to inspect cargo-auditable metadata in <Rust binary>.
List crates, versions, sources, dependency indices, and relationships for <dependency of interest>. Preserve missing fields, unknown format versions, and unusual cycles.
If .dep-v0 is absent, report that this route cannot recover the inventory; do not invent a complete SBOM. Label a commit hash found through a /rustc/ path as an inference only.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B09

**macOS and iOS package structure**

```text
Use REA to inventory the main executable, extensions, Frameworks, XPC services, helpers, and scripts in <.app/IPA/ZIP/DMG>.
Identify the components most likely relevant to <feature>, then select a supported Mach-O for deeper analysis. DMG children depend on host mounting support; record this limitation.
Path names only suggest component roles or runtimes. A resource inventory does not establish valid signatures, granted permissions, or actual code loading. Do not decrypt protected packages.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B10

**Windows resources and localization**

```text
Use REA's inspect_pe_resources to inspect resource types, names, languages, and icon-group references in <EXE/DLL>.
For <version information/missing language/resource change>, record source ranges and digests, distinguishing decodable content from opaque payloads.
Produce a list of resource issues. Product names and versions in resources are declarations inside the file, not proof of publisher identity.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B11

**The SQLite storage model**

```text
Use REA's inspect_sqlite_database to inspect <consistent database snapshot path>. First confirm that Node.js 24.x >=24.15 or 26+ and the required SQLite capability are available.
Read the schema inventory first, then select one ordinary table and the necessary columns for <business object>. Explicitly request database scope when the full schema is needed; do not treat the default inventory as a complete schema.
Describe relationships among tables, indexes, triggers, and application write paths. Preserve the identities of the database and any existing WAL; do not infer stable ordering or database-wide statistics from sampled rows.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B12

**Checks before migrating local data**

```text
Use REA to compare <old database snapshot>, <new database snapshot>, and <migration code in the application>, investigating the migration of <specified table or object>.
Check column changes, defaults, uniqueness, foreign keys, and transaction-failure paths. Snapshots must come from a stopped writer or the application's backup workflow.
Provide field mappings, data-loss risks, and validation steps for copies. Do not run the migration, modify the database, or claim support for decrypting encrypted SQLite in this task.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B13

**Plugin and dynamic-library loading**

```text
Use REA to investigate how <desktop application> discovers and loads <plugin or dynamic library>.
Trace search paths, architecture filtering, version/interface checks, and failure messages. Separate static declarations, candidate resolution, and actual runtime loading.
Produce a compatibility checklist and identify the runtime observation needed to confirm the final library identity. Do not automatically install or load plugins.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## B14

**Observe a native macOS window**

```text
Use REA to observe the existing <PID/window ID> I select, recording the state and screenshots of <one control> before and after <explicit action list>.
First verify the macOS version, unique window identity, Accessibility and Screen Recording permissions, and tool availability. Perform actions only on the declared test data; do not expand to other windows.
Report actions, UI changes, failures, and incomplete captures. Visible UI changes do not directly prove the underlying call chain. If action permissions are missing, perform only available read-only observations.

Use only the targets and actions specified above; report missing devices, permissions, or capabilities. Cite Evidence IDs, the observation scope, and time, distinguishing actual observations from inferences.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```
