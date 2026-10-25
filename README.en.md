# REA Investigation Prompt Collection

[简体中文](README.md) | **English**

A general-purpose English collection of REA prompts for coding agents such as Claude Code, Codex, and Cursor. Start with software release artifacts, client applications, and saved recordings to explain a feature, develop an evidence-backed specification, and implement and validate it when needed.

**114 copyable prompts: 3 general entry points and 111 topic-specific scenarios, including 32 organized by industry.** Replace everything `<inside angle brackets>`, then copy the code block. REA provides analysis capabilities and Evidence; the agent organizes the investigation and explanation, while ordinary development tools handle implementation, compilation, and project tests.

## How to use this collection

1. Choose a scenario, fill in the target path, specific question, and available samples, then send the complete code block to a coding agent that can access those materials.
2. Each prompt defines the investigation, scope, and deliverable first. Start analysis through an available REA entry point; if none exists, follow the conditional instruction at the end of the block.
3. Check whether the result answers the question, cites verifiable locations, and identifies unresolved parts. A component inventory, successful tool call, or completed installation does not replace the requested deliverable.

“Project directory” and “output directory” refer to the workspace for this investigation. Target materials, tool permissions, and platform dependencies must actually be available. If a required input is missing, the agent should identify the blocker and complete the unaffected work.

## Choose an entry point

| What you want to do | Start here |
|---|---|
| Start your first investigation or resume previous work | [Interactive onboarding A01](prompts/01-start-and-evidence.en.md#a01) · [Resume an investigation A08](prompts/01-start-and-evidence.en.md#a08) |
| Understand a button, command, or error | [From action to result A04](prompts/01-start-and-evidence.en.md#a04) · [Trace from an error A05](prompts/01-start-and-evidence.en.md#a05) |
| Analyze native programs, .NET, Go/Rust, or data files | [Desktop and data topics](prompts/02-native-desktop-and-data.en.md) |
| Analyze Electron, websites, WASM, or captures | [Web and network topics](prompts/03-web-electron-and-network.en.md) |
| Analyze APKs, Flutter, mobile logs, and resources | [Mobile topics](prompts/04-mobile.en.md) |
| Analyze firmware, drivers, hardware recordings, or security questions | [Firmware and defensive research](prompts/05-firmware-hardware-and-security.en.md) |
| Reconstruct features, study games, compare versions, or investigate crashes | [Reconstruction and regression](prompts/06-reconstruction-games-and-regression.en.md) |
| Find a business scenario by industry | [Industry scenarios](prompts/07-industry-scenarios.en.md) |

## Installation and verification

Use the following prompt for initial setup. Do not repeatedly configure a working connection. The base runtime requirement is Node.js 22.x ≥22.19, 24.x ≥24.11, or 26+; capabilities such as SQLite have higher requirements. The installer does not install or upgrade unrelated dependencies such as Node.js, Java, Ghidra, or JADX for you.

```text
Configure and verify REA for the current coding agent (https://github.com/morluto/rea; npm package: rea-agents). Completion requires a tool entry point that can actually be called.

1. Identify the current system, terminal permissions, and client. If REA MCP is already available, verify the capabilities needed for the task. If only the CLI is available, use it first rather than repeatedly installing tools for the investigation. Configure only the current client when installing or repairing a connection.

2. If no working entry point exists, check Node.js/npm. If they are missing or their versions are incompatible, use the official installation guide at https://rea.tools/ and the current version's requirements to provide steps for this system. Obtain my approval before installing additional software. Once ready, run npx -y rea-agents@latest --help.

3. After identifying and verifying the current client ID, run npx -y rea-agents@latest setup --client <verified client ID> --dry-run --json. Identify this ID yourself; do not require me to know it in advance. If reusing an installed CLI, use its actual entry point and equivalent commands supported by its help. Show configuration paths, backups, workflows, and optional engine changes, then apply the same plan only after approval. Using -y to download the package does not mean I approved configuration changes.

4. After configuration, use the same entry point to run doctor --client <verified client ID> --json, and check the REA tools actually discovered by the client. If a restart is needed, save the task and explain how to resume; successful registration does not mean the current session is connected. If MCP is temporarily unavailable, follow --help to continue suitable tasks through the npx CLI. If setup does not support this client, use the official documentation's manual-registration or CLI route instead of guessing a client ID.

5. Check only the engines and runtime conditions needed for this task, for example doctor --provider ghidra --json. If no task target has been specified, verify only the tool entry point. Explain missing dependencies and work that remains possible; do not install every engine. Record the actual version and determine availability from current capabilities / binary_session results and tool schemas.

Finally, report the available entry points, what was verified, remaining prerequisites, and how to start or resume the investigation. Do not report installations or checks that were not executed as completed.
```

Common client IDs include `claude_code`, `codex`, and `cursor`. For other clients, consult the installed version's help and the [installation guide](https://github.com/morluto/rea/blob/main/docs/installation.md). A successfully installed native engine does not necessarily support every file format, CPU, or runtime observation operation.

## General investigation template

Use this for a specific question without a matching scenario. Fill in the inputs, allowed scope, and deliverable; the template works independently.

```text
Use REA to investigate <one specific feature or question> in <absolute target path/explicit page/recording file>.

Known inputs: <version, platform, relevant samples or logs>.
Allowed scope: <static analysis by default; if execution is needed, specify targets, actions, accounts/test data, and output directory>.
Desired deliverable: <evidence-backed explanation/behavioral specification/read-only parser/minimal implementation/comparison report>.

First confirm target identity, format, and currently available capabilities, recording the version, digest, and selected engine. Use the most relevant workflow directly. If no applicable capability exists, explain the gap without inventing tools or replacing the target.

Start with summaries and a specific entry point, exploring only relevant modules/functions/records. Prefer summary and retained-evidence views when supported; follow up with parent_evidence_id queries to avoid repeated analysis and whole-bundle output. Do not pass parameters that the current schema does not expose.

Cite Evidence IDs and files/functions/addresses/record ordinals for each key conclusion, identifying the target version or digest. Distinguish observations, deterministic derivations, inferences, and unknowns. Static presence does not establish actual execution; matching finite samples does not establish complete equivalence.

Report the conclusion, key evidence chain, coverage and limitations, unresolved questions, and the smallest next validation step. Execute targets only within the already authorized runtime scope; present a concrete plan before expanding it. Do not repeatedly ask for information already provided.

Answer the question directly and deliver the requested result; an overview or tool log is not a substitute. If evidence is insufficient, inspect the most relevant materials within the authorized scope. Mark anything still unresolved as unknown and identify the missing evidence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## If you are unsure which prompt to choose

```text
I want to understand <business question> about <target>, and I have <files/versions/samples/existing records>.
Using REA's actual current capabilities, choose the most suitable investigation route, explain what it can answer and what is missing, and directly complete the static work that does not require additional information.
Do not require me to learn reverse-engineering terminology first. Do not present ordinary source reading, compilation, or testing as REA-specific capabilities. Support each conclusion in the report with evidence and preserve unknowns.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## Topic index

| Topic | IDs and count | Main contents |
|---|---|---|
| [Getting started, scope, and evidence management](prompts/01-start-and-evidence.en.md) | A01–A12 · 12 | Onboarding, error location, analysis budgets, reports, resumption, export, unknowns, and truncation |
| [Native programs, desktop applications, and local data](prompts/02-native-desktop-and-data.en.md) | B01–B14 · 14 | Native functions, formats, protocols, .NET, Go/Rust, Apple packages, PE resources, SQLite, plugins, and native windows |
| [Websites, Electron, WASM, and network recordings](prompts/03-web-electron-and-network.en.md) | C01–C16 · 16 | IPC, source maps, browser actions, HAR/SAZ/mitmproxy, PCAP, qlog, streaming messages, and WASM |
| [Android, Flutter, and mobile delivery](prompts/04-mobile.en.md) | D01–D12 · 12 | APKs, JNI, storage, deep links, resources, Flutter, ADB, cross-platform comparison, and SDK upgrades |
| [Firmware, hardware recordings, and defensive research](prompts/05-firmware-hardware-and-security.en.md) | E01–E12 · 12 | Extraction, startup, OTA, bare-metal analyzability, signals, USB/Bluetooth, drivers, patches, and protection mechanisms |
| [Feature reconstruction, games, versions, and regression](prompts/06-reconstruction-games-and-regression.en.md) | F01–F13 · 13 | Specifications, implementation, finite verification, game mechanics, saves, WASM planning, versions, CLI behavior, crashes, and CTFs |
| [Industry and business scenarios](prompts/07-industry-scenarios.en.md) | G01–G32 · 32 | Industry-specific inputs, business questions, deliverables, and boundaries |

## Find prompts by industry

| Field | Scenarios |
|---|---|
| Enterprise IT and system migration | [Legacy replacement G01](prompts/07-industry-scenarios.en.md#g01) · [Single sign-on G02](prompts/07-industry-scenarios.en.md#g02) |
| E-commerce and retail | [Discount rules G03](prompts/07-industry-scenarios.en.md#g03) · [POS receipts G04](prompts/07-industry-scenarios.en.md#g04) |
| Logistics and warehousing | [Labels and barcodes G05](prompts/07-industry-scenarios.en.md#g05) · [Offline scan synchronization G06](prompts/07-industry-scenarios.en.md#g06) |
| Finance and accounting software | [Monetary precision G07](prompts/07-industry-scenarios.en.md#g07) · [Transaction files G08](prompts/07-industry-scenarios.en.md#g08) |
| Healthcare and device companion software | [Data interoperability G09](prompts/07-industry-scenarios.en.md#g09) · [Measurement conversion G10](prompts/07-industry-scenarios.en.md#g10) |
| Manufacturing, energy, and buildings | [Engineering files G11](prompts/07-industry-scenarios.en.md#g11) · [Telemetry fields G12](prompts/07-industry-scenarios.en.md#g12) |
| Automotive, mobility, and IoT | [Bus recordings G13](prompts/07-industry-scenarios.en.md#g13) · [Provisioning and synchronization G14](prompts/07-industry-scenarios.en.md#g14) |
| Audio, video, and music software | [Encoder presets G15](prompts/07-industry-scenarios.en.md#g15) · [Audio plugins G16](prompts/07-industry-scenarios.en.md#g16) |
| Design and office software | [CAD coordinates G17](prompts/07-industry-scenarios.en.md#g17) · [Clipboard G18](prompts/07-industry-scenarios.en.md#g18) |
| Education and research | [Learning progress G19](prompts/07-industry-scenarios.en.md#g19) · [Instrument files G20](prompts/07-industry-scenarios.en.md#g20) |
| AI products | [Model requests G21](prompts/07-industry-scenarios.en.md#g21) · [Tool approvals G22](prompts/07-industry-scenarios.en.md#g22) |
| Supply chain and release acceptance | [Dependency evidence G23](prompts/07-industry-scenarios.en.md#g23) · [Upgrade acceptance G24](prompts/07-industry-scenarios.en.md#g24) |
| Privacy and incident response | [Data destinations G25](prompts/07-industry-scenarios.en.md#g25) · [Suspicious samples G26](prompts/07-industry-scenarios.en.md#g26) |
| Operations and customer support | [CLI replacement G27](prompts/07-industry-scenarios.en.md#g27) · [Error attribution G28](prompts/07-industry-scenarios.en.md#g28) |
| Web3 | [Offline interface candidates G29](prompts/07-industry-scenarios.en.md#g29) · [Bytecode upgrades G30](prompts/07-industry-scenarios.en.md#g30) |
| Product evaluation and digital preservation | [Feature substitution G31](prompts/07-industry-scenarios.en.md#g31) · [Historical behavior archives G32](prompts/07-industry-scenarios.en.md#g32) |

## Capabilities and prerequisites at a glance

“Available” requires all of the following: the current version provides the tool, dependencies are ready, the host and target format are supported, and the requested scope is permitted. A tool appearing in a list does not mean it can analyze this target. The routes below reflect the source baseline; consult the linked guides for detailed versions and verification scope.

| Target | Common route | Conditions and limitations to preserve |
|---|---|---|
| Native EXE/ELF/Mach-O | `open_binary` → relevant function tools | [Check engine, CPU, and host separately](https://github.com/morluto/rea/blob/main/docs/native-investigation.md); Windows Ghidra has a separate P0 boundary; IDA does not provide `binary_overview` |
| JS/Electron release artifact | `analyze_javascript_application` | [Static analysis](https://github.com/morluto/rea/blob/main/docs/javascript-application-workflows.md) requires no native engine; dynamic loading and native addons may leave gaps |
| Browser | `list_browser_targets`, `capture_browser_scenario` | [Chrome-family debugging connection and separate profile](https://github.com/morluto/rea/blob/main/docs/browser-observation.md); actions may submit data, and unavailable backend implementations cannot be observed |
| Native macOS window | `observe_native_ui`, `capture_native_ui_scenario` | [The current window route](https://github.com/morluto/rea/blob/main/docs/native-investigation.md) requires macOS 14+, an explicit target, and appropriate system permissions |
| .NET / Unity Mono | `inspect_managed_artifact`, member tools | [Static metadata and CIL inspection](https://github.com/morluto/rea/blob/main/docs/managed-code-analysis.md); not automatic C# recovery; use separate routes for IL2CPP/NativeAOT |
| Go / Rust | `inspect_go_binary` / `inspect_rust_binary` | [Go](https://github.com/morluto/rea/blob/main/docs/go-binaries.md) build information; [Rust](https://github.com/morluto/rea/blob/main/docs/rust-binaries.md) dependencies rely on cargo-auditable metadata; absence does not mean no dependencies |
| APK code | `inspect_android_package` and related tools | [Full JDK 17+ and matching headless JADX](https://github.com/morluto/rea/blob/main/docs/android-analysis.md); Windows x64 also requires matching packaged native components |
| Android resources / devices | `decode_android_resources` / ADB family | Configure [Apktool](https://github.com/morluto/rea/blob/main/docs/apktool-resource-analysis.md) and [ADB](https://github.com/morluto/rea/blob/main/docs/adb-device-analysis.md) independently; device writes and installation are not read-only operations |
| Flutter APK | `identify_flutter_build`, `inspect_dart_aot` | [Build facts, limited structure, and string projections](https://github.com/morluto/rea/blob/main/docs/flutter-analysis.md); not complete Dart decompilation |
| Firmware image | `inspect_firmware_regions`, `extract_firmware` | [Linux, Binwalk 3.1.x / Unblob 26.6.x, prlimit](https://github.com/morluto/rea/blob/main/docs/firmware-analysis.md); format-specific extractors may be required; extraction is not arbitrary bare-metal decompilation |
| HAR/SAZ/mitmproxy/qlog | `inspect_web_network_capture` | [Read-only historical records and supported profiles](https://github.com/morluto/rea/blob/main/docs/web-network-captures.md); native mitmproxy decoding requires Linux; qlog does not guarantee body recovery or conclusions about network loss |
| PCAP fields | `inspect_packet_fields`, `inspect_packet_capture` | [Linux, TShark 4.x, prlimit](https://github.com/morluto/rea/blob/main/docs/packet-captures.md); field/frame queries, not live acquisition |
| PCAP overview | `inspect_pcap_capture` | [tshark + capinfos](https://github.com/morluto/rea/blob/main/docs/pcap-analysis.md); current resource-control routes support Linux/Windows, with real verification based on Linux; Mac inspection has a capability gap |
| Saved logic signals | `inspect_signal_decoders`, `decode_signal_recording` | [Linux, sigrok-cli 0.7.2, prlimit](https://github.com/morluto/rea/blob/main/docs/signal-recordings.md); explicit channel/protocol settings, no hardware sampling connection |
| Local WASM | `inspect_wasm_artifact` | [Caller-supplied WABT 1.0.42](https://github.com/morluto/rea/blob/main/docs/wasm-artifacts.md); no target execution or automatic downloads; WAT is not original source |
| Local EVM bytecode | `inspect_evm_interface` | [Linux x64, prlimit, raw/hex](https://github.com/morluto/rea/blob/main/docs/evm-bytecode.md); inferred interface candidates, no chain queries, and no current EOF-container support |
| SQLite snapshot | `inspect_sqlite_database` | [Node.js 24.x ≥24.15 or 26+](https://github.com/morluto/rea/blob/main/docs/sqlite-databases.md); a consistent database/WAL snapshot and selected tables/columns; no arbitrary SQL execution |
| Linux core | `inspect_recorded_crash` | [Linux x86-64 ELF core and pwntools](https://github.com/morluto/rea/blob/main/docs/recorded-crashes.md), optional GDB/pwndbg; not a universal system-dump parser |
| Packages, resources, and components | `inspect_artifact`, `inspect_pe_resources`, and others | [Archives and resources](https://github.com/morluto/rea/blob/main/docs/javascript-artifact-reconstruction.md), [Apple package graphs](https://github.com/morluto/rea/blob/main/docs/apple-application-analysis.md); inventories do not establish runtime loading or signature validity |
| Command execution and comparison | `capture_process_scenario`, `compare_process_captures` | [Linux/macOS with a native PTY](https://github.com/morluto/rea/blob/main/docs/process-capture.md); runs with user permissions, not in an isolation environment; native Windows capture is unavailable |

“Host” means the environment where REA and its associated tools actually run. If a Linux route is unavailable on a Mac, report the gap or use a separately configured Linux environment that can access the materials. Do not pass local paths unchanged merely because tools exist remotely.

## License

The prompts in this repository retain the original draft's MIT license declaration. REA and referenced materials remain subject to their respective upstream licenses; see [REA LICENSE](https://github.com/morluto/rea/blob/main/LICENSE).

## Star History

GitHub stars over time for this repository. Click the chart to open the interactive view.

<a href="https://www.star-history.com/?repos=jacksonlin-infra%2FREA-Prompts&amp;type=date">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=jacksonlin-infra/REA-Prompts&amp;type=Date&amp;theme=dark" />
    <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=jacksonlin-infra/REA-Prompts&amp;type=Date" />
    <img alt="REA-Prompts Star History" src="https://api.star-history.com/svg?repos=jacksonlin-infra/REA-Prompts&amp;type=Date" width="800" />
  </picture>
</a>
