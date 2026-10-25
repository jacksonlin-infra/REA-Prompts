# Android, Flutter, and Mobile Delivery

[简体中文](04-mobile.md) | **English**

[Back to the main index](../README.en.md)

Static APK code analysis depends on a full JDK and a matching headless JADX. Resource decoding, ADB, and JEB have their own dependencies. Flutter build identification and limited AOT structure inspection do not recover Dart source code.

References: [Android](https://github.com/morluto/rea/blob/main/docs/android-analysis.md), [ADB](https://github.com/morluto/rea/blob/main/docs/adb-device-analysis.md), [Flutter](https://github.com/morluto/rea/blob/main/docs/flutter-analysis.md), [Apktool](https://github.com/morluto/rea/blob/main/docs/apktool-resource-analysis.md).

## On this page

- [D01 · Triage APK permissions and components](#d01)
- [D02 · Trace a mobile feature](#d02)
- [D03 · Verify JNI boundaries](#d03)
- [D04 · Local storage and cryptography usage](#d04)
- [D05 · Deep links and external input](#d05)
- [D06 · Android localization resources](#d06)
- [D07 · Visibility limits for obfuscation and packers](#d07)
- [D08 · Flutter build and ABI differences](#d08)
- [D09 · Acquire an APK from a specified device](#d09)
- [D10 · Collect evidence for a mobile failure](#d10)
- [D11 · Compare mobile packages across platforms](#d11)
- [D12 · Review a mobile SDK upgrade](#d12)

## D01

**Triage APK permissions and components**

```text
Use REA to inspect declared permissions, components, intent filters, SDK clues, domains, and storage-related classes in <APK>.
Select methods relevant to <business feature>. Do not conclude that data was collected or sent merely because a class name, domain, or SDK is present.
Distinguish manifest declarations, platform-version effects, and code paths supported by evidence. Report candidate risks and the additional runtime evidence needed.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D02

**Trace a mobile feature**

```text
Use REA to trace <one feature> in <APK>, from its UI or service entry point through validation, business logic, storage, or request construction.
Identify classes, methods, and decompiled locations; verify resource references separately. Preserve gaps caused by reflection, dynamic loading, coroutine transformations, and server dependencies.
Give the shortest evidence-backed path. Do not promise recovery of original Kotlin or complete Compose semantics.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D03

**Verify JNI boundaries**

```text
Use REA to statically analyze <feature> in <APK>, locating System.loadLibrary, native declarations, and RegisterNatives clues.
Select the .so for <explicit ABI> in the package. Obtain Java and native-function evidence separately, then check signatures, symbols, and arguments.
Keep unconnected JNI edges unknown. Do not assume end-to-end bindings from similar names, execute the application, or load the library.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D04

**Local storage and cryptography usage**

```text
Use REA to investigate how <APK> stores <data type>, locating paths that use SharedPreferences, SQLite, files, and Keystore.
Distinguish hardcoded material, algorithm calls, key sources, and actual protection. Explain which settings can be established statically and which depend on device state.
Provide data flow and a validation plan. Do not conclude that storage or transport is secure merely because AES/TLS appears, or attempt to read private device data.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D05

**Deep links and external input**

```text
Use REA to inspect <URL scheme/exported component> in <APK>, tracing external parameters to navigation, WebView, file, or privileged operations.
Check the manifest, intent matching, and domain, path, and parameter validation in code.
Report input sources, handlers, checks, and prerequisites. Actual exploitability requires controlled runtime validation; do not send intents in this task.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D06

**Android localization resources**

```text
Use REA's decode_android_resources to inspect <language or region> in <APK>, confirming that an existing Apktool launcher and Java are available.
Compare resource keys, missing values, format placeholders, and application references between the default and target locale, preserving resource provenance.
Produce a localization regression checklist. Static string presence does not prove that the language is reachable in every view or that the layout is correct.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D07

**Visibility limits for obfuscation and packers**

```text
Use REA to statically inspect <APK> for obfuscation, loader, and protection clues.
List parseable dex/classes, native loaders, string clues, and unparseable portions. State the evidence behind each judgment.
If the real code appears only at runtime, identify missing materials and the observation scope that requires separate confirmation. Do not automatically unpack protected code, inject code, or change the device.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D08

**Flutter build and ABI differences**

```text
Use REA's identify_flutter_build and, when available, inspect_dart_aot to inspect <APK>, explicitly selecting <ABI>.
Record libapp/libflutter digests, snapshot hash, build-id, supported snapshot structures, and string projections.
Report differences in build facts against <another APK or ABI>. String tokens are not recovered classes; a snapshot hash does not automatically establish the SDK version, and source code and business call chains may remain unknown.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D09

**Acquire an APK from a specified device**

```text
Use REA through an existing adb to read package information for <package name> on <device serial>, saving the base APK and every accessible split APK to <new local output directory>.
Verify the package name, version, device paths, and each file's digest. Preserve failure reasons when permissions are insufficient; do not root, install, or overwrite device files.
Then statically analyze the acquired APKs, explaining the coverage of an individual split. The first adb query may start the local adb server.

Use only the targets and actions specified above; report missing devices, permissions, or capabilities. Cite Evidence IDs, the observation scope, and time, distinguishing actual observations from inferences.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D10

**Collect evidence for a mobile failure**

```text
Use REA on <device serial> to collect read-only evidence for <package name>: its version, selected process, bounded logcat output, and current window information, within <time range>.
I will manually reproduce <action>. Save specified screenshots as needed, or a bugreport I explicitly request, to <output directory>.
Produce a timeline and candidate static-code locations. Do not clear logs, reinstall the app, or directly treat adjacent log events as the root cause.

Use only the targets and actions specified above; report missing devices, permissions, or capabilities. Cite Evidence IDs, the observation scope, and time, distinguishing actual observations from inferences.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D11

**Compare mobile packages across platforms**

```text
Use REA to inventory resources, scripts, configuration, and native components related to <feature> in <Android APK> and <corresponding iOS IPA>.
Use a supported analysis route for each platform. Do not force one-to-one matches between Android classes and iOS symbols.
Report clues to shared behavior, platform-specific differences, and unconfirmed areas. Package inventories do not establish feature equivalence or app-store review status.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```

## D12

**Review a mobile SDK upgrade**

```text
Use REA to compare declarations, resources, native libraries, and visible call paths for <SDK or component> in <old APK> and <new APK>.
First confirm that ABI, build type, and package identity are comparable, then inspect changes to permissions, entry points, and data handling.
Report observable release-artifact differences and regression cases. Treat weak version signatures as candidates only; dependency presence does not mean its code executed.

Default to static analysis only; do not run the target. Cite Evidence IDs and source locations for each conclusion, distinguish observations, derivations, inferences, and unknowns, and state coverage gaps.

Reuse available REA tools. If no entry point is available, use npx -y rea-agents@latest --help to find supported commands. Present a plan and obtain approval only when configuration changes are needed; identify specific blockers for anything you cannot complete.
```
