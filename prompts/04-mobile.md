# Android、Flutter 与移动端交付

**简体中文** | [English](04-mobile.en.md)

[返回总目录](../README.md)

APK 静态代码分析依赖完整 JDK 与匹配的 headless JADX；资源解析、ADB 和 JEB 各有独立依赖。Flutter 构建识别与有限 AOT 结构检查不等于 Dart 源码恢复。

参考：[Android](https://github.com/morluto/rea/blob/main/docs/android-analysis.md)、[ADB](https://github.com/morluto/rea/blob/main/docs/adb-device-analysis.md)、[Flutter](https://github.com/morluto/rea/blob/main/docs/flutter-analysis.md)、[Apktool](https://github.com/morluto/rea/blob/main/docs/apktool-resource-analysis.md)。

## 本页目录

- [D01 · APK 权限与组件初筛](#d01)
- [D02 · 移动端功能调用链](#d02)
- [D03 · JNI 边界核对](#d03)
- [D04 · 本地存储与加密使用](#d04)
- [D05 · Deep Link 与外部输入](#d05)
- [D06 · Android 本地化资源](#d06)
- [D07 · 混淆与壳的可见边界](#d07)
- [D08 · Flutter 构建与 ABI 差异](#d08)
- [D09 · 从指定设备取得 APK](#d09)
- [D10 · 移动端故障证据采集](#d10)
- [D11 · 跨平台移动包差异](#d11)
- [D12 · 移动 SDK 升级审查](#d12)

## D01

**APK 权限与组件初筛**

```text
使用 REA 检查 <APK> 的声明权限、组件、intent filter、SDK 线索、域名与存储相关类。
围绕 <业务功能> 选择相关方法，不因类名、域名或 SDK 存在就认定已经收集或发送数据。
区分 manifest 声明、平台版本影响和可证实代码路径；输出风险候选及需要补充的运行证据。

默认只做静态分析，不运行目标。每项结论引用 Evidence ID 和源位置，区分观察、推导、推测与未知，并说明覆盖缺口。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D02

**移动端功能调用链**

```text
使用 REA 在 <APK> 中追踪 <一个功能>，从界面或服务入口到校验、业务处理、存储或请求构造。
标注类、方法与反编译位置，资源引用另行核对；保留反射、动态加载、协程转换及服务端依赖造成的缺口。
给出最短有证据的路径，不承诺恢复原始 Kotlin 或全部 Compose 语义。

默认只做静态分析，不运行目标。每项结论引用 Evidence ID 和源位置，区分观察、推导、推测与未知，并说明覆盖缺口。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D03

**JNI 边界核对**

```text
使用 REA 静态分析 <APK> 的 <功能>，定位 System.loadLibrary、native 声明和 RegisterNatives 线索。
选择包内 <明确 ABI> 的 .so，分别取得 Java 与原生函数证据，核对签名、符号和参数。
无法连接的 JNI 边保留未知，不用相似名字假定端到端绑定，不执行应用或加载库。

默认只做静态分析，不运行目标。每项结论引用 Evidence ID 和源位置，区分观察、推导、推测与未知，并说明覆盖缺口。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D04

**本地存储与加密使用**

```text
使用 REA 调查 <APK> 如何保存 <数据类型>，定位 SharedPreferences、SQLite、文件与 Keystore 使用路径。
区分硬编码材料、算法调用、密钥来源和实际保护效果；说明哪些配置可静态确认，哪些依赖设备状态。
输出数据流和验证计划，不从出现 AES/TLS 字样就认定安全，也不尝试读取设备私有数据。

默认只做静态分析，不运行目标。每项结论引用 Evidence ID 和源位置，区分观察、推导、推测与未知，并说明覆盖缺口。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D05

**Deep Link 与外部输入**

```text
使用 REA 检查 <APK> 的 <URL scheme/导出组件>，跟踪外部参数到页面跳转、WebView、文件或特权操作。
核对 manifest、intent 匹配和代码中的域名、路径、参数校验。
输出输入来源、处理函数、检查和前置条件；只有受控运行验证才能确认实际可利用性，本次不发送 intent。

默认只做静态分析，不运行目标。每项结论引用 Evidence ID 和源位置，区分观察、推导、推测与未知，并说明覆盖缺口。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D06

**Android 本地化资源**

```text
使用 REA 的 decode_android_resources 检查 <APK> 的 <语言或地区>，确认现有 Apktool 启动器及 Java 可用。
比较默认与目标 locale 的资源键、缺失值、格式占位符和应用引用，保留资源来源。
输出本地化回归清单；静态字符串存在不证明该语言在所有界面可达，也不证明布局正确。

默认只做静态分析，不运行目标。每项结论引用 Evidence ID 和源位置，区分观察、推导、推测与未知，并说明覆盖缺口。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D07

**混淆与壳的可见边界**

```text
使用 REA 静态检查 <APK> 的混淆、加载器和保护线索。
列出可解析的 dex/类、native loader、字符串线索及无法解析部分；说明判断来自何种证据。
如果真实代码只在运行时出现，输出缺少的材料和需要另行确认的观察范围，不自动脱壳、注入或改变设备。

默认只做静态分析，不运行目标。每项结论引用 Evidence ID 和源位置，区分观察、推导、推测与未知，并说明覆盖缺口。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D08

**Flutter 构建与 ABI 差异**

```text
使用 REA 的 identify_flutter_build 和可用的 inspect_dart_aot 检查 <APK>，显式选择 <ABI>。
记录 libapp/libflutter 摘要、snapshot hash、build-id、支持范围内的 snapshot 结构和字符串投影。
输出与 <另一 APK 或 ABI> 的构建事实差异。字符串 token 不是已恢复的类；快照 hash 不自动证明 SDK 版本，源代码和业务调用链仍可能未知。

默认只做静态分析，不运行目标。每项结论引用 Evidence ID 和源位置，区分观察、推导、推测与未知，并说明覆盖缺口。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D09

**从指定设备取得 APK**

```text
使用 REA 通过已有 adb 从 <设备序列号> 读取 <包名> 的包信息，将 base 与全部可访问 split APK 保存到 <新的本地输出目录>。
核对包名、版本、设备路径和每个文件摘要；权限不足时保留失败原因，不 root、不安装、不覆盖设备文件。
接着对取得的 APK 做静态分析，说明单个 split 的分析覆盖；首次 adb 查询可能启动本机 adb server。

只执行上述指定目标与动作；缺少设备、权限或能力时报告缺口。引用 Evidence ID、观察范围与时间，区分实际观察和推测。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D10

**移动端故障证据采集**

```text
使用 REA 在 <设备序列号> 上只读收集 <包名> 的版本、指定进程、有限 logcat 和当前窗口信息，时间范围为 <范围>。
我会手动复现 <动作>；按需要保存指定屏幕截图或我明确要求的 bugreport 到 <输出目录>。
输出时间线与静态代码候选位置，不清空日志、不重装应用，也不把日志相邻事件直接视为根因。

只执行上述指定目标与动作；缺少设备、权限或能力时报告缺口。引用 Evidence ID、观察范围与时间，区分实际观察和推测。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D11

**跨平台移动包差异**

```text
使用 REA 盘点 <Android APK> 与 <对应 iOS IPA> 中和 <功能> 有关的资源、脚本、配置及原生组件。
按平台分别采用支持的分析路径；Android 类与 iOS 符号不强行一一匹配。
输出共同行为线索、平台实现差异和无法确认的部分。包清单不能证明功能等价或商店审核状态。

默认只做静态分析，不运行目标。每项结论引用 Evidence ID 和源位置，区分观察、推导、推测与未知，并说明覆盖缺口。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## D12

**移动 SDK 升级审查**

```text
使用 REA 比较 <旧 APK> 与 <新 APK> 中 <SDK或组件> 的声明、资源、native 库和可见调用路径。
先确认 ABI、构建类型和包身份可比，再检查权限、入口和数据处理的变化。
输出发行物中的可观察差异与回归用例；模糊版本特征只作为候选，不把依赖出现当成代码已执行。

默认只做静态分析，不运行目标。每项结论引用 Evidence ID 和源位置，区分观察、推导、推测与未知，并说明覆盖缺口。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```
