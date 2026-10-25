# Websites, Electron, WASM, and Network Recordings

[简体中文](03-web-electron-and-network.md) | **English**

[Back to the main index](../README.en.md)

Static JavaScript investigation and browser runtime observation are separate routes. REA cannot recover server-side implementations that were not supplied from frontend code. Historical HAR/SAZ/PCAP files are saved records, not the website's current state.

References: [JavaScript](https://github.com/morluto/rea/blob/main/docs/javascript-application-workflows.md), [Browser observation](https://github.com/morluto/rea/blob/main/docs/browser-observation.md), [Historical network captures](https://github.com/morluto/rea/blob/main/docs/web-network-captures.md), [WASM](https://github.com/morluto/rea/blob/main/docs/wasm-artifacts.md).

## On this page

- [C01 · Trace an Electron feature](#c01)
- [C02 · Review Electron IPC security](#c02)
- [C03 · Minified code and source maps](#c03)
- [C04 · A business workflow in the browser](#c04)
- [C05 · Client-side routes and state transitions](#c05)
- [C06 · Separate frontend and server responsibilities](#c06)
- [C07 · An offline API inventory from HAR](#c07)
- [C08 · Fiddler SAZ or mitmproxy recordings](#c08)
- [C09 · An overview of communication endpoints in PCAP](#c09)
- [C10 · Exact protocol fields from PCAP](#c10)
- [C11 · Investigate QUIC/qlog recordings](#c11)
- [C12 · WebSocket and streaming interfaces](#c12)
- [C13 · WASM interfaces and glue code](#c13)
- [C14 · WASM upgrade compatibility](#c14)
- [C15 · Prepare to observe Electron at runtime](#c15)
- [C16 · Differences between source and release bundles](#c16)

## C01

**Trace an Electron feature**

```text
Use REA to analyze <feature> in <ASAR or extracted application directory>, selecting relevant modules from the summary.
Trace connections among renderer, preload, contextBridge, IPC, and main, then follow file or network operations. List native addon boundaries separately.
Report evidence-backed connections and gaps. Do not infer a call relationship from matching channel names alone or scan directories unrelated to this application.
Trace from an observed channel, API, or node. Inspect relevant code for function internals not covered by the application graph. Explain how inputs become results, distinguishing static connections, inferences, and runtime observations at each step; graph reachability does not establish execution.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C02

**Review Electron IPC security**

```text
Use REA to statically review IPC and preload-exposed interfaces related to <feature> in <application>.
Check parameter sources, sender/origin validation, path constraints, shell.openExternal, child_process, and file operations.
Separate “a sensitive operation exists,” “a reachable input path exists,” and “exploitability has been verified.” Provide only evidence, impact prerequisites, and a controlled validation plan in this task; do not execute attack inputs.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C03

**Minified code and source maps**

```text
Use REA to trace <feature or visible string> in <bundle/ASAR>.
Locate code using source maps that actually exist and match the current release artifact, along with module structure. Label names you invent for functions as “analysis aliases” and preserve original locations.
Report relevant modules and data flow. Do not treat beautified code as original source or claim complete deobfuscation.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C04

**A business workflow in the browser**

```text
Use REA to observe <site and page> that I have already opened. The target operations are <explicit action list>, using <test account and test-data scope>.
Select one unambiguous browser target first. Record the page, scripts, requests, and state before and after actions. If I need to act manually, state the start and end boundaries of the observation.
Report the workflow, request fields, and response facts that the client can establish. Leave server internals, databases, and other users' behavior unknown.

Use only the targets and actions specified above; report missing devices, permissions, or capabilities. Cite Evidence IDs, the observation scope, and time, distinguishing actual observations from inferences.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C05

**Client-side routes and state transitions**

```text
Use REA to statically analyze <a set of related routes> in <frontend build directory>, locating route matching, page loading, state storage, and error branches.
Distinguish routes present in the build, conditional loading branches, and pages reachable at runtime. Produce a state diagram or table.
List missing inputs for branches controlled by remote configuration or login state; do not guess current production feature flags.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C06

**Separate frontend and server responsibilities**

```text
Use REA to analyze <frontend files> and <existing HAR/browser evidence>, investigating <validation, sorting, or calculation feature>.
List frontend steps, requests actually sent, fields already calculated in responses, and server-side steps that cannot be confirmed.
Produce a responsibility table and a draft replacement interface. Do not infer a unique backend algorithm from response results. Do not replay recorded requests.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C07

**An offline API inventory from HAR**

```text
Use REA's inspect_web_network_capture to read <HAR path>, focusing only on <domain/path/operation>.
From retained evidence, produce an inventory of request methods, path templates, query-parameter names, response shapes, and original record ordinals. Label templates and field types as sample-derived.
Preserve limitations from unrecorded response bodies, authentication exclusions, and truncation. Do not present observed interfaces as the complete server API or visit recorded URLs.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C08

**Fiddler SAZ or mitmproxy recordings**

```text
Use REA to inspect the requests and responses for <one operation> in <SAZ or native mitmproxy file>.
Explicitly select the actual format and confirm the upstream version and host supported by the parser. The native mitmproxy route requires a matching Linux decoding environment.
Preserve original record identities, raw payloads, and decoding limitations. Do not assume SAZ bodies are decompressed or dechunked, connect to a live proxy, or replay traffic.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C09

**An overview of communication endpoints in PCAP**

```text
Use REA's inspect_pcap_capture to inspect <pcap/pcapng>, summarizing endpoints, DNS, TLS SNI, protocol distribution, and visible HTTP requests.
Verify tshark, capinfos, and host resource controls first, then answer <question> using summaries and relevant pages.
Report observable communication relationships. IP addresses, SNI, and packet times alone do not establish a specific process, service identity, or request causality. Do not capture live traffic.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C10

**Exact protocol fields from PCAP**

```text
Use REA on Linux to analyze <protocol question> in <pcap/pcapng>. First discover available fields with inspect_packet_fields, then choose the smallest useful field set, filters, and any necessary decode-as rules.
Use inspect_packet_capture to preserve original frame numbers and repeated fields. State both the input-packet scope and matching-output page scope; check the file digest across pages.
Provide field-level evidence and undecodable portions. Without decryption material, do not claim to see TLS plaintext. An empty filtered result does not establish that the original capture has no traffic.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C11

**Investigate QUIC/qlog recordings**

```text
Use REA to inspect records for <selected trace/stream/direction> in <aioquic 1.5.0 JSON 0.3 qlog file>.
Verify the supported format first, then move from the summary into trace, stream, and contribution ranges, preserving upstream loss or coverage declarations.
Report event relationships supported by the recording and its gaps. Do not directly interpret missing qlog events as network packet loss, claim recovery of unrecorded bodies, or claim automatic correlation with PCAP.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C12

**WebSocket and streaming interfaces**

```text
Use REA to inspect <frontend build> and <captured streaming-interaction evidence>, explaining message parsing, incremental updates, reconnection, and completion conditions for <one streaming feature>.
Map client handling code to frames or events actually recorded. Preserve gaps when the capture did not retain messages.
Produce a message state machine and offline replay test vectors. Do not initiate a real session or assume HAR automatically contains complete WebSocket frames.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C13

**WASM interfaces and glue code**

```text
Use REA's inspect_wasm_artifact to inspect <local WASM>, explicitly supplying <JavaScript glue path> as well.
Verify WABT 1.0.42 and target limits, then extract imports, exports, memory/table information, exact WAT signatures, and instructions relevant to <feature>.
Distinguish file byte offsets, function indices, and memory addresses. WAT is not the original C/Rust. Do not automatically download candidate modules referenced by URLs or execute WASM.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C14

**WASM upgrade compatibility**

```text
Use REA to inspect <old WASM>, <new WASM>, and their respective glue files. Compare import/export names, types, memory/table constraints, and calling-convention clues for <specified interface>.
Report definite structural differences and potentially affected JS call sites. Matching function signatures establishes only that structural dimension, not equivalent memory layout, numerical behavior, or side effects.
Prepare a differential test plan. Do not execute modules in this task or assume a dedicated WASM comparison tool exists.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C15

**Prepare to observe Electron at runtime**

```text
Use REA to check whether <Electron application> has the runtime observation entry points needed for <feature>. Inspect packaged fuses first, then verify the already running target I selected.
If EnableNodeCliInspectArguments is disabled, explain that --inspect may be ignored; do not repeatedly try the same launch argument.
Only report available entry points and a supported follow-up observation plan in this task. Do not restart the application, change fuses, or inject code.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## C16

**Differences between source and release bundles**

```text
Use REA to compare <source snapshot I provide> with <corresponding JavaScript release bundle>, investigating whether <feature> actually made it into the build.
Generate or reuse the required source-graph and application-graph Evidence from the supplied source and release bundle, then use compare_source_to_bundle. Identify specific gaps when materials are missing or unsupported; do not force matches based on filenames.
Distinguish splits, merges, removals, modifications, and weak matches. Produce an evidence mapping from source to release artifacts, including unknowns.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```
