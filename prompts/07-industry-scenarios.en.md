# Industry and Business Scenarios

[简体中文](07-industry-scenarios.md) | **English**

[Back to the main index](../README.en.md)

These templates apply REA's existing analysis capabilities to concrete business questions. They do not imply built-in industry-specific decoders or certification capabilities. Each requires a client application, release artifact, samples, or existing recordings. When only a cloud service is available without observable materials, its server-side implementation remains unknown.

Industry deliverables should be grounded in software evidence. Results for healthcare, finance, and industrial scenarios do not automatically establish clinical validity, financial compliance, or device safety certification.

## On this page

- [G01 · Enterprise IT: inventory before replacing a legacy system](#g01)
- [G02 · Enterprise IT: hand off a single sign-on client integration](#g02)
- [G03 · E-commerce: discount and price-display rules](#g03)
- [G04 · Retail: POS and receipt formats](#g04)
- [G05 · Logistics: shipping labels and barcode fields](#g05)
- [G06 · Warehousing: offline scans and synchronization queues](#g06)
- [G07 · Financial software: migrating monetary precision](#g07)
- [G08 · Financial software: transaction-file interoperability](#g08)
- [G09 · Healthcare software: data-export interoperability](#g09)
- [G10 · Medical-device companion software: measurement conversion](#g10)
- [G11 · Manufacturing: engineering-project file compatibility](#g11)
- [G12 · Energy and buildings: interpret telemetry fields](#g12)
- [G13 · Automotive and mobility: offline decoding of recorded data](#g13)
- [G14 · IoT: provisioning and state synchronization](#g14)
- [G15 · Audio and video: export presets and encoder parameters](#g15)
- [G16 · Music software: migrate plugin presets](#g16)
- [G17 · Design and CAD: project units and coordinates](#g17)
- [G18 · Office software: clipboard interoperability](#g18)
- [G19 · Education: progress and grade files](#g19)
- [G20 · Research: make legacy instrument data readable](#g20)
- [G21 · AI applications: how model requests are built](#g21)
- [G22 · AI applications: tool permissions and approvals](#g22)
- [G23 · Software supply chain: release dependency inventory](#g23)
- [G24 · Software supply chain: upgrade acceptance](#g24)
- [G25 · Privacy engineering: where one data field goes](#g25)
- [G26 · Incident response: static triage of a suspicious sample](#g26)
- [G27 · Operations: plan CLI replacement compatibility](#g27)
- [G28 · Customer support: attribute an error](#g28)
- [G29 · Web3: local contract-interface candidates](#g29)
- [G30 · Web3: compare local bytecode upgrades](#g30)
- [G31 · Commercial evaluation: can one feature replace another?](#g31)
- [G32 · Digital preservation: archive historical software behavior](#g32)

## G01

**Enterprise IT: inventory before replacing a legacy system**

```text
Use REA to inspect <one critical business workflow> in <legacy desktop application>, mapping input files, local calculations, outputs, and external interfaces.
Use <sample files and existing logs> to separate business rules, platform dependencies, and operator conventions.
Produce a minimal compatibility specification for the replacement, with evidence and unknowns. Prioritize formats or interfaces that block migration.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G02

**Enterprise IT: hand off a single sign-on client integration**

```text
Use REA to statically analyze <SSO login flow> in <client application or frontend bundle>. Use <existing redacted records> to locate redirects, callbacks, token use, and logout paths.
Distinguish client validation, identity-provider responses, and unseen server policies.
Produce an integration contract and error branches. Do not acquire real credentials, initiate login, or change account settings.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G03

**E-commerce: discount and price-display rules**

```text
Use REA to investigate <one discount combination> in <store frontend or client>, using <products, quantities, discounts, and displayed amounts> as input samples.
Trace client rounding, discount order, display fields, and parameters submitted to the backend. Record server-returned final prices separately.
Report local rules that can be established, pricing logic that cannot be confirmed, and offline test vectors. Do not create real orders.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G04

**Retail: POS and receipt formats**

```text
Use REA to inspect <POS application> and <receipt/print-data samples>, explaining how <amount field or print command> is generated.
Check encoding, display order for tax and discounts, line width, and control bytes. Adopt a protocol such as ESC/POS only after finding matching evidence.
Produce a format description and offline rendered samples. Do not connect to payment terminals or send print or payment commands.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G05

**Logistics: shipping labels and barcode fields**

```text
Use REA to inspect <label generation> in <logistics client>, using <fictional orders and sample labels> to trace templates, character encoding, barcode payloads, and check digits.
Distinguish program-generated fields from server-assigned tracking numbers. Record conditions for different print sizes.
Produce an offline label compatibility specification and test samples. Do not place orders with real carriers.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G06

**Warehousing: offline scans and synchronization queues**

```text
Use REA to inspect <offline stock receipt after scanning> in <warehouse client or APK>. Use <consistent local database snapshot> to trace deduplication keys, queue states, retries, and conflict handling.
Distinguish local acknowledgments from final server confirmation. Preserve unknowns around disconnection, repeated scans, and partial failures.
Produce a state table and offline replay cases. Do not change inventory or connect to production systems.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G07

**Financial software: migrating monetary precision**

```text
Use REA to inspect <one monetary calculation> in <finance or accounting client>, using <input/output samples unrelated to real accounts>.
Locate fixed-point/floating-point representation, rounding stages, negative-number handling, and currency decimal-place rules. Distinguish local display from server-side accounting.
Produce an implementation compatibility specification and boundary tests. Do not trade or alter ledgers, and do not present the analysis as an accounting compliance conclusion.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G08

**Financial software: transaction-file interoperability**

```text
Use REA to inspect import and export of <file type> in <reporting or transaction-file client>, using <synthetic samples>.
Trace headers, encoding, dates, time zones, precision, checksums, and rejection conditions, marking proprietary extensions.
Produce a read-only format description and migration checklist. Do not submit transaction files to a real trading system.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G09

**Healthcare software: data-export interoperability**

```text
Use REA to inspect how <healthcare software client> generates <one object in DICOM/HL7/FHIR or a proprietary format>, using <synthetic or de-identified samples>.
Trace identifiers, units, time zones, encoding, and field mappings. Check interpretations of standard fields separately against the relevant standard; names alone do not establish conformance.
Produce interface mappings, data-loss risks, and an offline validation plan. Do not perform real clinical operations or draw conclusions about clinical accuracy.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G10

**Medical-device companion software: measurement conversion**

```text
Use REA to statically analyze <one measurement-record conversion> in <device companion client or extracted program>, using <synthetic raw data and displayed values>.
Locate scaling, unit conversion, truncation, outlier handling, and version branches. State limitations when original sensor evidence is unavailable.
Produce software-level conversion formulas and candidate tests. Do not send device commands or describe software consistency as measurement-accuracy certification.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G11

**Manufacturing: engineering-project file compatibility**

```text
Use REA to inspect how <engineering configuration software> reads and writes <project file type>, using <normal/missing-field/old-version copies>.
Identify field versions, units, checksums, defaults, and import-failure paths. Do not infer the runtime logic of a PLC that was not provided.
Produce a read-only checker design and compatibility matrix. Do not connect to controllers, download projects to them, or write registers.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G12

**Energy and buildings: interpret telemetry fields**

```text
Use REA to inspect <gateway program> and <existing protocol or signal recordings>, explaining only <one measurement or alarm field>.
Map registers/message fields, byte order, scaling, units, and alarm thresholds. Record field matches separately from actual device configuration.
Produce an evidence mapping and offline calculation examples. Do not send control commands or use inferred thresholds for live control.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G13

**Automotive and mobility: offline decoding of recorded data**

```text
Use REA to inspect <one status field> in <saved bus recordings and the corresponding host application>.
First confirm the recording format, encapsulation, and available dissectors. Do not falsely claim native REA parsing of unsupported BLF, MDF, or proprietary formats. Record any external conversion tool and provenance separately.
Produce candidate mappings from frames to fields to displayed values. Do not connect to vehicles, inject messages, or guarantee the runtime behavior of safety functions.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G14

**IoT: provisioning and state synchronization**

```text
Use REA to statically analyze <provisioning or state-synchronization flow> in <IoT APK/client> and <existing capture>.
Trace device identifiers, local-network/cloud branches, retries, and error messages. Distinguish client logic from device-side unknowns.
Produce a state machine and interoperability gaps. Do not automatically scan the LAN, send device configuration, or extract other people's credentials.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G15

**Audio and video: export presets and encoder parameters**

```text
Use REA to inspect <one export preset> in <editing or transcoding application>, using <existing export logs and samples>.
Trace resolution, frame rate, bitrate, audio parameters, and external encoder calls. Distinguish UI values, values passed to the encoder, and actual output-file properties.
Produce parameter mappings and an offline comparison plan. Do not claim that command arguments alone establish final image quality.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G16

**Music software: migrate plugin presets**

```text
Use REA to inspect <preset format> in <host or audio plugin>, using <preset samples I own>.
Locate parameter identifiers, normalized ranges, defaults, version migration, and unknown binary blocks. Treat DSP algorithms separately from the preset container.
Produce a read-only parsing specification and parameter mappings. Do not copy commercial sounds or protection logic.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G17

**Design and CAD: project units and coordinates**

```text
Use REA to inspect <unit or coordinate conversion> when <design software> imports <sample project format>.
Trace axes, scale, origin, angles, precision, and transformation order, checking against <known geometry samples>.
Produce conversion rules, candidate error sources, and boundary cases. Without geometry-kernel evidence, do not promise complete file compatibility.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G18

**Office software: clipboard interoperability**

```text
Use REA to inspect <copying/pasting one content type> in <office or note-taking client>, using <clipboard samples I own>.
Trace generation, precedence, and fallback paths for plain text, HTML, RTF, or proprietary formats, along with Electron/native boundaries.
Produce a format matrix and compatibility examples. Do not read current clipboard contents that were not explicitly selected.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G19

**Education: progress and grade files**

```text
Use REA to inspect <saving progress or exporting a course> in <learning client>, using <synthetic student data>.
Trace local records, synchronization queues, timestamps, completion state, and duplicate submission handling. Leave server-side grading logic unknown if it is unavailable.
Produce migration fields and test cases. Do not change real grades, accounts, or server records.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G20

**Research: make legacy instrument data readable**

```text
Use REA to inspect how <instrument companion software> reads <historical data files>, using <known calibration samples>.
Locate headers, sampling frequency, channels, units, scaling, and checksums. Separate software-calculated values from external calibration facts.
Produce a read-only parsing description and reproducible examples. Do not fill missing experimental data with unsupported interpolation.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G21

**AI applications: how model requests are built**

```text
Use REA to statically analyze the implementation of <sending one chat message> in <AI client or Electron package>.
Trace message assembly, visible templates, attachment processing, model parameters, request construction, and streaming-response parsing. Distinguish local templates from content appended by the server.
Produce an evidence-backed client data flow. Do not claim to recover model weights, prompts never sent to the client, or complete server orchestration, and do not initiate paid calls.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G22

**AI applications: tool permissions and approvals**

```text
Use REA to inspect the request, approval display, parameter transformation, and execution entry point for <one tool call> in <agent client>.
Check rejection, timeout, duplicate execution, and result-return behavior against <existing test-session records>. A UI label saying “approval required” does not directly establish an underlying permission restriction.
Report permission boundaries and gaps. Do not execute undeclared tools or attempt to bypass approval.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G23

**Software supply chain: release dependency inventory**

```text
Use REA to inventory actual files, Go/Rust metadata, managed references, and JavaScript package clues related to <component of interest> in <vendor release package>.
Distinguish verifiable versions, weak signatures, and unknowns, preserving sample digests and locations. Missing metadata does not establish the absence of dependencies.
Produce a vendor-verification checklist. Do not turn a string match directly into a confirmed vulnerability or a complete SBOM.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G24

**Software supply chain: upgrade acceptance**

```text
Use REA to compare <one promised fix or feature> between <old vendor package> and <new package>.
Compare packaged files first, then inspect relevant functions, managed members, or JavaScript graphs, checking permission and dependency changes.
Report observed changes, reasoning about whether they match the promise, and validation materials the vendor still needs to provide. Do not run installers in this task.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G25

**Privacy engineering: where one data field goes**

```text
Use REA to investigate <specific data field> in <client>, tracing collection and transformation through local storage and request construction, using <authorized historical records>.
List capabilities present in code separately from transmissions actually seen in the records. State trigger conditions and unknown scope.
Produce data flow and minimization recommendations. Do not treat a static domain list as proof of actual data transmission or as a legal compliance conclusion.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G26

**Incident response: static triage of a suspicious sample**

```text
Use REA to inspect <copy of a suspicious sample> read-only for clues to <one of persistence/communication/file access>.
Record its digest, format, relevant imports, strings, and reachable paths. Distinguish candidate IOCs in resources from established behavior.
Produce hypotheses and evidence for later isolated experiments. Do not run, load, or inject the sample, or visit domains found in it.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G27

**Operations: plan CLI replacement compatibility**

```text
Use REA to statically investigate <one subcommand> in <legacy command-line tool>, using <historical invocations and output samples>.
Record argument parsing, standard output/error, exit codes, configuration precedence, and filesystem side effects.
Produce the contract a replacement must preserve and regression scenarios still to run. A successful exit code is not a substitute for correct results.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G28

**Customer support: attribute an error**

```text
Use REA to inspect <specific error> using <customer-provided release artifact, version, and redacted logs>.
Verify that the binary and logs correspond to the same build before locating error conditions and environmental dependencies.
Produce an explanation for support staff, the minimum additional information needed, and next checks that will not modify customer data. Do not invent an on-site reproduction.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G29

**Web3: local contract-interface candidates**

```text
Use REA's inspect_evm_interface to inspect <local runtime bytecode file>, explicitly selecting raw or hex encoding. Verify Linux x64 and the required dependencies first.
Record selectors, byte offsets, inferred arguments, and mutability. Preserve separate digests for the carrier and decoded bytes.
Report interface candidates and unknowns. Do not automatically query a chain, send transactions, or call the result a complete ABI. Do not mislabel a hash as an Ethereum Keccak code hash; explicitly report unsupported EOF containers.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G30

**Web3: compare local bytecode upgrades**

```text
Use REA to inspect <old runtime bytecode> and <new runtime bytecode> separately, focusing on <selector or interface change>.
Compare inferred interfaces, offsets, and original-byte evidence. These results alone cannot determine selector collisions, proxy delegation targets, or on-chain storage state.
Report established byte changes and candidate interface-compatibility findings. Do not connect to a chain in this task or claim a complete smart-contract security audit.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G31

**Commercial evaluation: can one feature replace another?**

```text
Use REA to make a bounded comparison of <the same feature> in <two lawfully obtained clients>, using <identical local samples or existing observations>.
Extract inputs, outputs, limits, errors, and platform dependencies for each. Compare dimensions supported by evidence of comparable strength.
List what is replaceable, requires adaptation, or remains unknown. Do not infer the other product's cloud architecture from frontend appearances or claim coverage of unexamined features.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## G32

**Digital preservation: archive historical software behavior**

```text
Use REA to statically document <one feature to preserve> in <historical software release artifact>, using <samples I own and existing operation records>.
Preserve original digests, dependencies, formats, key algorithms, environment assumptions, and unreproducible portions in a behavioral record that others can inspect again later.
Produce a specification and evidence index. Do not call automatically decompiled output the original source, or distribute resources outside my authorization.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```
