# Firmware, Hardware Recordings, and Defensive Research

[简体中文](05-firmware-hardware-and-security.md) | **English**

[Back to the main index](../README.en.md)

For authorized samples and lab environments. Firmware scanning, extraction, native-code analysis, and device execution are separate capability layers. Current Binwalk/Unblob, TShark, and sigrok routes have Linux and tool-version prerequisites; do not pretend these adapters are already usable on a Mac.

References: [Firmware](https://github.com/morluto/rea/blob/main/docs/firmware-analysis.md), [Signal recordings](https://github.com/morluto/rea/blob/main/docs/signal-recordings.md), [Packet fields](https://github.com/morluto/rea/blob/main/docs/packet-captures.md).

## On this page

- [E01 · Triage firmware regions](#e01)
- [E02 · Extract firmware and continue analysis](#e02)
- [E03 · Embedded services and startup clues](#e03)
- [E04 · OTA updates and signature verification](#e04)
- [E05 · Can this bare-metal or microcontroller image be analyzed?](#e05)
- [E06 · Decode UART, SPI, or I2C recordings](#e06)
- [E07 · Analyze USB or Bluetooth recordings](#e07)
- [E08 · Static review of drivers and IOCTLs](#e08)
- [E09 · Trust boundaries and vulnerability candidates](#e09)
- [E10 · Patch differences and fix coverage](#e10)
- [E11 · Anti-cheat, DRM, and licensing flows](#e11)
- [E12 · DMA defense samples and platform boundaries](#e12)

## E01

**Triage firmware regions**

```text
Use REA's inspect_firmware_regions to inspect <firmware image>, first verifying Linux, Binwalk, and resource-limiting dependencies.
Report signatures, offsets, engine-reported sizes, and unknown regions. Separate signature candidates from validated formats.
List regions that could be extracted next and missing parsers. Do not call a signature a recovered partition, or flash, mount, or execute the firmware.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E02

**Extract firmware and continue analysis**

```text
Use REA with the configured Unblob to extract <firmware or explicit offset-and-length range> into <absolute directory that does not yet exist, with an existing parent>.
Preserve extracted-file digests, parent-child relationships, failed regions, and missing extractors. Do not overwrite previous output. Original byte ranges and runtime addresses of decompressed children may be unknown.
Continue static analysis of <feature> only with returned, supported children such as ELF files. Extraction completion does not establish complete firmware reconstruction.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E03

**Embedded services and startup clues**

```text
Use REA to inspect startup scripts, configuration, and supported executables related to <service> in <extracted firmware directory>.
Trace service launch arguments, configuration reads, and protocol entry points, preserving architecture, libc, and dependency clues.
Report candidate static startup paths without asserting that the scripts necessarily execute on the device. Keep raw-flash, device-tree, and bootloader semantics unknown where parsing evidence is absent.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E04

**OTA updates and signature verification**

```text
Use REA to statically investigate download, version-checking, signature-verification, and write paths in <extracted updater or supported firmware program>.
Focus on failure branches for <one update format or component> and whether verification happens before writing. Separate the presence of certificate/public-key resources from evidence that verification is actually invoked.
Produce an update state machine and hardening recommendations. Do not contact production update endpoints, flash devices, or attempt to bypass signatures.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E05

**Can this bare-metal or microcontroller image be analyzed?**

```text
Use REA to assess whether <raw firmware file> has a supported loading and analysis route given <known CPU, address map, and byte order>.
Check the current provider's format/architecture support first. Without a matching raw load profile, record only bytes and externally known mappings; do not disguise the file as ELF to open it.
If a route is available, verify one candidate vector table or reset entry. Distinguish vendor documentation, derived addresses, and actual instruction evidence.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E06

**Decode UART, SPI, or I2C recordings**

```text
Use REA to decode <saved logic-analyzer recording>. The sample rate is <value>, the protocol is <protocol>, and the channel mapping and level/clock parameters are <configuration>.
On Linux, first use inspect_signal_decoders to check installed decoders and options, then call decode_signal_recording. Ask for missing settings rather than guessing wiring or baud rate.
Report original annotations, sample ranges, and uncertain interpretations. Page line counts are not sample counts, and decoder text is not independently verified protocol fact. Do not acquire hardware signals in this task.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E07

**Analyze USB or Bluetooth recordings**

```text
Use REA to analyze <device interaction> in <existing USB/Bluetooth pcapng>. In a supported Linux environment, verify TShark encapsulation and dissector support before selecting protocol fields.
Preserve frame numbers, directions, repeated fields, and missing payloads. Organize candidate command/response relationships.
Produce offline protocol notes. Do not connect to devices, replay commands, or infer request/response pairing automatically from nearby timestamps.

Cite Evidence IDs, input identities, and coverage. Distinguish observations, derivations, inferences, and unknowns; missing records are not evidence of absence.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E08

**Static review of drivers and IOCTLs**

```text
Use REA to statically inspect <one device interface> in <.sys or .ko>, first confirming that the current engine supports its format and architecture.
On Windows, focus on dispatch routines, IOCTL buffering methods, and length checks. On Linux, focus on the corresponding ioctl, copy_to_user/copy_from_user, and related paths. Do not mix the two mechanisms.
Report entry points, controllable fields, bounds checks, and risk hypotheses. Preserve coverage gaps when indirect dispatch cannot be resolved. Do not load the driver or claim complete enumeration.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E09

**Trust boundaries and vulnerability candidates**

```text
Use REA to review paths from <one input surface> to <sensitive operation> in <authorized target>.
For each candidate, record the input source, checks, call chain, reachability prerequisites, impact, and counterexamples. Establish existing validation first, rather than merely searching for dangerous function names.
Report at most <number> of the strongest evidence-backed issues, with a minimal controlled validation plan for each. Do not execute attack inputs in this task; static reachability is not a confirmed vulnerability.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E10

**Patch differences and fix coverage**

```text
Use REA to compare <functions related to a known issue> between <old version> and <patched version>, using comparison tools suited to the target type.
Explain new checks, caller coverage, error paths, and similar candidate paths. Address or name changes are not automatically behavior changes.
Report hypotheses about the fix, possible omissions, and required validation. Do not claim a patch is ineffective or exploitable without reproduction.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E11

**Anti-cheat, DRM, and licensing flows**

```text
Use REA to statically inspect <integrity/licensing/telemetry feature> in <protection component I am authorized to study>.
Trace inputs, checks, failure handling, and visible data-collection paths. Distinguish local checks from remote decisions that cannot be observed.
Report the flow, evidence, and hardening recommendations for our product. Do not alter authorization decisions, generate license credentials, or connect to online games. The static presence of a check does not establish protection effectiveness.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## E12

**DMA defense samples and platform boundaries**

```text
Use REA to statically analyze <our DMA defense component or an authorized sample>, investigating only <device identification/access restrictions/audit records>.
List system interfaces called, configuration reads, and visible checks. State which IOMMU and platform-policy facts require firmware, OS configuration, or live evidence to confirm.
Produce a matrix of defensive controls and evidence gaps. Do not derive online-game target offsets, anti-detection steps, or arbitrary-memory-access implementations. A single driver cannot establish the entire hardware security state.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```
