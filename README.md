# REA 提示词集

**简体中文** | [English](README.en.md)

面向 Claude Code、Codex、Cursor 等编程智能体的通用 REA 中文提示词库：从软件发行物、客户端与已保存记录出发，解释一个功能，形成有证据的规格，再按需要实现与验证。

**共 114 条可复制提示词：3 条通用入口 + 111 条专题场景，其中 32 条按行业组织。** 替换 `<尖括号中的内容>` 后复制代码块即可。REA 负责提供分析能力和 Evidence；智能体负责组织调查与解释，普通开发工具负责实现、编译和项目测试。

## 如何使用

1. 选择场景，填写目标路径、具体问题和已有样本，复制完整代码块交给能够访问这些材料的编程智能体。
2. 提示词直接定义调查任务、范围和成果。已有 REA 入口就开始分析；缺少入口时，按代码块末尾的条件处理。
3. 检查结果是否回答了具体问题、引用了可核验位置，并说明未解决部分。组件清单、工具调用成功或安装完成，都不能替代任务成果。

“项目目录”和“输出目录”是本次调查的工作目录。目标材料、所需工具权限和平台依赖必须实际可用；缺少关键输入时，智能体应说明阻塞并继续完成不受影响的部分。

## 先选一个入口

| 你现在想做什么 | 从这里开始 |
|---|---|
| 第一次使用或恢复上次调查 | [交互式向导 A01](prompts/01-start-and-evidence.md#a01) · [恢复调查 A08](prompts/01-start-and-evidence.md#a08) |
| 看懂一个按钮、命令或错误 | [动作到结果 A04](prompts/01-start-and-evidence.md#a04) · [错误反查 A05](prompts/01-start-and-evidence.md#a05) |
| 分析原生程序、.NET、Go/Rust 或数据文件 | [桌面与数据专题](prompts/02-native-desktop-and-data.md) |
| 分析 Electron、网页、WASM 或抓包 | [Web 与网络专题](prompts/03-web-electron-and-network.md) |
| 分析 APK、Flutter、移动端日志与资源 | [移动端专题](prompts/04-mobile.md) |
| 分析固件、驱动、硬件记录或安全问题 | [固件与防御专题](prompts/05-firmware-hardware-and-security.md) |
| 复现功能、研究游戏、比较版本、定位崩溃 | [复现与回归专题](prompts/06-reconstruction-games-and-regression.md) |
| 按行业找业务场景 | [行业专题](prompts/07-industry-scenarios.md) |

## 安装与验证

首次安装使用下面的提示词。已经可用的连接无需反复配置。基础运行时要求是 Node.js 22.x ≥22.19、24.x ≥24.11 或 26+；SQLite 等能力有更高要求。安装器不替你安装或升级 Node.js、Java、Ghidra、JADX 等无关依赖。

```text
为当前编程智能体配置并验证 REA（https://github.com/morluto/rea，npm 包 rea-agents），以实际可调用的工具入口作为完成条件。

1. 先识别当前系统、终端权限和客户端。已有可用的 REA MCP 时验证任务所需能力；只有 CLI 时可先通过 CLI 工作，无需为调查反复安装。安装或修复连接时只配置当前客户端。

2. 如果没有可用入口，检查 Node.js/npm。缺少或版本不符时，依据官方安装指南 https://rea.tools/ 和当前版本要求给出适合本系统的安装步骤；安装额外软件须经我批准。就绪后运行 npx -y rea-agents@latest --help。

3. 确定并核对当前客户端 ID 后，执行 npx -y rea-agents@latest setup --client <已确认的客户端ID> --dry-run --json。这个 ID 由你识别，不要求我先知道。若复用已安装的 CLI，则使用其实际入口及帮助支持的同等命令。展示配置路径、备份、工作流和可选引擎变更，获批后才应用同一计划；不要因下载包时使用了 -y 就视为我已批准配置变更。

4. 配置后使用相同入口运行 doctor --client <已确认的客户端ID> --json，并检查客户端实际发现的 REA 工具。需要重启时保存任务并说明恢复方式；注册成功不等于当前会话已连接。MCP 暂不可用时，可按 --help 用 npx CLI 继续适用的任务。客户端不在 setup 支持列表时使用官方文档的手动注册或 CLI 路线，不猜客户端 ID。

5. 只检查本次任务需要的引擎和运行条件，例如 doctor --provider ghidra --json；没有任务目标时仅验证工具入口。缺少引擎时说明依赖与可完成的部分，不把所有引擎都装一遍。记录实际版本，按当前 capabilities / binary_session 和工具 schema 判断可用性。

最后告诉我：已可用的入口、已验证内容、仍缺的条件，以及如何开始或恢复调查。未执行的安装或验证不得报告为已完成。
```

常用客户端 ID 包括 `claude_code`、`codex`、`cursor`；其他客户端以所用版本的帮助和 [安装指南](https://github.com/morluto/rea/blob/main/docs/installation.md) 为准。原生分析引擎安装成功也不代表它支持每一种文件、CPU 和运行观察操作。

## 通用调查模板

用于没有对应专题的具体问题。填写输入、允许范围和成果要求后，可独立使用。

```text
使用 REA 调查 <目标绝对路径/明确页面/记录文件> 中的 <一个具体功能或问题>。

已知输入：<版本、平台、相关样本或日志>。
允许范围：<默认只静态分析；如需运行，写明目标、动作、账号/测试数据和输出目录>。
期望成果：<有证据的解释/行为规格/只读解析器/最小实现/比较报告>。

先确认目标身份、格式和当前可用能力，记录版本、摘要与选择的引擎。直接使用最相关的工作流；没有适用能力时说明缺口，不编造工具或更换目标。

从摘要和具体入口开始，只深入相关模块/函数/记录。在支持 summary 与保留证据视图时优先使用；后续按 parent_evidence_id 查询，避免重复分析和整包输出。当前 schema 未提供的参数不要传入。

每个关键结论引用 Evidence ID 及文件/函数/地址/记录序号，注明目标版本或摘要。区分观察、确定性推导、推测与未知；静态存在不等于实际执行，有限样本相同不等于完整等价。

先直接回答问题并交付约定成果，不以概览或工具日志代替答案。证据不足时，继续检查授权范围内最相关的材料；仍不能确认的结论标记未知并说明缺少什么。
输出：结论、关键证据链、覆盖与限制、仍未解决的问题、下一步最小验证。只在已经授权的运行范围内执行目标；需要扩大范围时先给出具体计划。不要反复询问已明确的信息。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## 不确定选哪条时

```text
我想了解 <目标> 的 <业务问题>，手头材料有 <文件/版本/样本/已有记录>。
请结合当前 REA 的实际能力，选出最合适的一条调查路线，说明它能回答什么、还缺什么，并直接完成无需额外信息的静态部分。
不要要求我先掌握逆向术语；不要把一般源代码阅读、编译或测试包装成 REA 专用能力。报告中的每项结论应有证据，并保留未知。

优先使用现有 REA 工具；没有入口时用 npx -y rea-agents@latest --help 确认可用命令。仅在任务确需配置变更时展示计划并获批；无法继续的部分说明具体阻塞。
```

## 专题目录

| 专题 | 编号与数量 | 主要内容 |
|---|---|---|
| [入门、范围与证据管理](prompts/01-start-and-evidence.md) | A01–A12 · 12 | 交互向导、错误定位、分析预算、报告、恢复、导出、未知与截断处理 |
| [原生程序、桌面应用与本地数据](prompts/02-native-desktop-and-data.md) | B01–B14 · 14 | 原生函数、格式、协议、.NET、Go/Rust、Apple 包、PE 资源、SQLite、插件、原生窗口 |
| [网站、Electron、WASM 与网络记录](prompts/03-web-electron-and-network.md) | C01–C16 · 16 | IPC、source map、浏览器操作、HAR/SAZ/mitmproxy、PCAP、qlog、流式消息、WASM |
| [Android、Flutter 与移动端交付](prompts/04-mobile.md) | D01–D12 · 12 | APK、JNI、存储、Deep Link、资源、Flutter、ADB、跨平台和 SDK 升级 |
| [固件、硬件记录与防御研究](prompts/05-firmware-hardware-and-security.md) | E01–E12 · 12 | 提取、启动、OTA、裸机可分析性、信号、USB/蓝牙、驱动、补丁和保护机制 |
| [功能复现、游戏、版本与回归](prompts/06-reconstruction-games-and-regression.md) | F01–F13 · 13 | 规格、实现、有限验证、游戏机制、存档、WASM 计划、版本、CLI、崩溃、CTF |
| [行业与业务场景](prompts/07-industry-scenarios.md) | G01–G32 · 32 | 行业输入、业务问题、交付成果和边界 |

## 按行业快速查找

| 领域 | 场景 |
|---|---|
| 企业 IT 与系统迁移 | [旧系统替换 G01](prompts/07-industry-scenarios.md#g01) · [单点登录 G02](prompts/07-industry-scenarios.md#g02) |
| 电商与零售 | [优惠规则 G03](prompts/07-industry-scenarios.md#g03) · [POS 小票 G04](prompts/07-industry-scenarios.md#g04) |
| 物流与仓储 | [面单条码 G05](prompts/07-industry-scenarios.md#g05) · [离线扫码同步 G06](prompts/07-industry-scenarios.md#g06) |
| 金融与会计软件 | [金额精度 G07](prompts/07-industry-scenarios.md#g07) · [交易文件 G08](prompts/07-industry-scenarios.md#g08) |
| 医疗与设备配套软件 | [数据互操作 G09](prompts/07-industry-scenarios.md#g09) · [测量转换 G10](prompts/07-industry-scenarios.md#g10) |
| 制造、能源与楼宇 | [工程文件 G11](prompts/07-industry-scenarios.md#g11) · [遥测字段 G12](prompts/07-industry-scenarios.md#g12) |
| 汽车、出行与 IoT | [总线记录 G13](prompts/07-industry-scenarios.md#g13) · [配网与同步 G14](prompts/07-industry-scenarios.md#g14) |
| 音视频与音乐软件 | [编码预设 G15](prompts/07-industry-scenarios.md#g15) · [音频插件 G16](prompts/07-industry-scenarios.md#g16) |
| 设计与办公 | [CAD 坐标 G17](prompts/07-industry-scenarios.md#g17) · [剪贴板 G18](prompts/07-industry-scenarios.md#g18) |
| 教育与科研 | [学习进度 G19](prompts/07-industry-scenarios.md#g19) · [仪器文件 G20](prompts/07-industry-scenarios.md#g20) |
| AI 产品 | [模型请求 G21](prompts/07-industry-scenarios.md#g21) · [工具审批 G22](prompts/07-industry-scenarios.md#g22) |
| 供应链与发行验收 | [依赖证据 G23](prompts/07-industry-scenarios.md#g23) · [升级验收 G24](prompts/07-industry-scenarios.md#g24) |
| 隐私与事件响应 | [数据去向 G25](prompts/07-industry-scenarios.md#g25) · [可疑样本 G26](prompts/07-industry-scenarios.md#g26) |
| 运维与客户支持 | [CLI 替换 G27](prompts/07-industry-scenarios.md#g27) · [错误归因 G28](prompts/07-industry-scenarios.md#g28) |
| Web3 | [离线接口候选 G29](prompts/07-industry-scenarios.md#g29) · [字节码升级 G30](prompts/07-industry-scenarios.md#g30) |
| 产品评估与数字保存 | [功能可替代性 G31](prompts/07-industry-scenarios.md#g31) · [历史行为档案 G32](prompts/07-industry-scenarios.md#g32) |

## 能力与前提速查

“可用”须同时满足：当前版本提供工具、依赖就绪、宿主支持、目标格式支持、请求范围允许。工具出现在列表里不等于本次目标可分析。下面是源码基线中的路线，详细版本和验证范围以链接指南为准。

| 对象 | 常用路线 | 必须保留的条件与限制 |
|---|---|---|
| 原生 EXE/ELF/Mach-O | `open_binary` → 相关函数工具 | [引擎、CPU、宿主分别检查](https://github.com/morluto/rea/blob/main/docs/native-investigation.md)；Windows Ghidra 有独立 P0 边界；IDA 不提供 `binary_overview` |
| JS/Electron 发行物 | `analyze_javascript_application` | [静态分析](https://github.com/morluto/rea/blob/main/docs/javascript-application-workflows.md)不需要原生引擎；动态加载及 native addon 可留下缺口 |
| 浏览器 | `list_browser_targets`、`capture_browser_scenario` | [Chrome 系调试连接与独立配置](https://github.com/morluto/rea/blob/main/docs/browser-observation.md)；动作可能提交数据，不能观察未提供的后端实现 |
| 原生 macOS 窗口 | `observe_native_ui`、`capture_native_ui_scenario` | [当前窗口路线](https://github.com/morluto/rea/blob/main/docs/native-investigation.md)要求 macOS 14+、明确目标和相应系统权限 |
| .NET / Unity Mono | `inspect_managed_artifact`、成员工具 | [元数据与 CIL 静态检查](https://github.com/morluto/rea/blob/main/docs/managed-code-analysis.md)；不等于自动恢复 C#，IL2CPP/NativeAOT 另选路线 |
| Go / Rust | `inspect_go_binary` / `inspect_rust_binary` | [Go](https://github.com/morluto/rea/blob/main/docs/go-binaries.md) 构建信息；[Rust](https://github.com/morluto/rea/blob/main/docs/rust-binaries.md) 依赖依靠 cargo-auditable 元数据；缺失不等于无依赖 |
| APK 代码 | `inspect_android_package` 及相关工具 | [完整 JDK 17+、匹配 headless JADX](https://github.com/morluto/rea/blob/main/docs/android-analysis.md)；Windows x64 另有打包原生组件条件 |
| Android 资源 / 设备 | `decode_android_resources` / ADB 家族 | [Apktool](https://github.com/morluto/rea/blob/main/docs/apktool-resource-analysis.md) 与 [ADB](https://github.com/morluto/rea/blob/main/docs/adb-device-analysis.md) 独立配置；写设备与安装不是只读操作 |
| Flutter APK | `identify_flutter_build`、`inspect_dart_aot` | [构建、有限结构与字符串投影](https://github.com/morluto/rea/blob/main/docs/flutter-analysis.md)；不是完整 Dart 反编译 |
| 固件镜像 | `inspect_firmware_regions`、`extract_firmware` | [Linux，Binwalk 3.1.x / Unblob 26.6.x、prlimit](https://github.com/morluto/rea/blob/main/docs/firmware-analysis.md)；依格式需 extractor；提取不等于任意裸机反编译 |
| HAR/SAZ/mitmproxy/qlog | `inspect_web_network_capture` | [只读历史记录与受支持 profile](https://github.com/morluto/rea/blob/main/docs/web-network-captures.md)；mitmproxy 原生解码需 Linux，qlog 不保证正文或网络丢包结论 |
| PCAP 字段 | `inspect_packet_fields`、`inspect_packet_capture` | [Linux、TShark 4.x、prlimit](https://github.com/morluto/rea/blob/main/docs/packet-captures.md)；按字段和帧查询，不实时采集 |
| PCAP 概览 | `inspect_pcap_capture` | [tshark + capinfos](https://github.com/morluto/rea/blob/main/docs/pcap-analysis.md)；当前支持 Linux/Windows 资源控制路线，真实验证以 Linux 为准，Mac 检查有能力缺口 |
| 已保存逻辑信号 | `inspect_signal_decoders`、`decode_signal_recording` | [Linux、sigrok-cli 0.7.2、prlimit](https://github.com/morluto/rea/blob/main/docs/signal-recordings.md)；需要通道和协议参数，不连接硬件采样 |
| 本地 WASM | `inspect_wasm_artifact` | [调用方提供 WABT 1.0.42](https://github.com/morluto/rea/blob/main/docs/wasm-artifacts.md)，无目标执行或自动下载；WAT 不是原始源码 |
| 本地 EVM 字节码 | `inspect_evm_interface` | [Linux x64、prlimit、raw/hex](https://github.com/morluto/rea/blob/main/docs/evm-bytecode.md)；推导接口候选，无链查询，当前不支持 EOF 容器 |
| SQLite 快照 | `inspect_sqlite_database` | [Node.js 24.x ≥24.15 或 26+](https://github.com/morluto/rea/blob/main/docs/sqlite-databases.md)；一致的数据库/WAL 快照、选表选列；不任意执行 SQL |
| Linux core | `inspect_recorded_crash` | [Linux x86-64 ELF core 与 pwntools](https://github.com/morluto/rea/blob/main/docs/recorded-crashes.md)，可选 GDB/pwndbg；不通用于所有系统转储 |
| 包、资源与组件 | `inspect_artifact`、`inspect_pe_resources` 等 | [归档与资源](https://github.com/morluto/rea/blob/main/docs/javascript-artifact-reconstruction.md)、[Apple 包图](https://github.com/morluto/rea/blob/main/docs/apple-application-analysis.md)；清单不证明运行加载或签名有效 |
| 命令运行与比较 | `capture_process_scenario`、`compare_process_captures` | [Linux/macOS 与原生 PTY](https://github.com/morluto/rea/blob/main/docs/process-capture.md)；以用户权限运行，不是隔离环境，Windows 原生捕获未提供 |

宿主指 REA 与对应工具实际运行的位置。Mac 上缺少 Linux 路线时，明确缺口或使用另行配置、可访问材料的 Linux 环境；不能因为远端有工具就把本机路径原样传过去。

## 许可证

本仓库中的提示词沿用原稿的 MIT 许可声明。REA 及引用材料的许可分别以其上游声明为准，参见 [REA LICENSE](https://github.com/morluto/rea/blob/main/LICENSE)。
