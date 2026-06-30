# 鸿蒙相关文献筛选与分类

整理日期：2026-06-30

来源文档：`/home/fang/文档/xwechat_files/wxid_4fxhjv0agumy22_019a/temp/RWTemp/2026-06/3fc6267a1a16424020ab50596cc8f418/文献分析.docx`

## 筛选标准

纳入标准：

- 标题或内容明确包含 `HarmonyOS`、`OpenHarmony`、`ArkTS`、`ArkUI`、`鸿蒙` 等关键词。
- 研究对象、实验平台或工具链明确面向鸿蒙 / OpenHarmony / ArkTS 生态。
- 少数论文虽不是鸿蒙专属研究，但在文档中明确说明已集成、部署或评估于 HarmonyOS / OpenHarmony，列为“弱相关参考”。

未纳入标准：

- 仅属于普通移动系统、Android、边缘计算、LLM 推理、通用 UI 代码生成等方向，且没有明确鸿蒙生态对象的文献。
- 仅因所在俱乐部名称包含“开源鸿蒙”而出现，但论文内容本身与鸿蒙无直接关系的文献。

说明：Google Scholar 链接采用标题精确检索入口；部分“刚录用/未发表”或内部整理中的新论文，Google Scholar 可能暂时没有正式条目。

## 分类总览

| 类别 | 主题范围 | 代表文献 |
| --- | --- | --- |
| 应用分析、测试与质量保障 | OpenHarmony/HarmonyOS 应用动态分析、污点分析、GUI 测试、UI 缺陷检测、迁移场景测试 | HapTest、HapFlow、HmTest、HACMony |
| 静态分析、跨语言与安全加固 | ArkTS 静态分析、指针分析、字节码分析、ArkTS 与 C/C++ 跨语言分析、混淆加固 | ArkAnalyzer、HarmoBridge、HarmonyFlow、ArkObfux |
| ArkTS 代码智能、数据集与移植 | ArkTS 代码生成评估、代码检索数据集、API 知识图谱数据合成、第三方库迁移 | ArkTS-CodeSearch、APIKG4SYN、CROSS2OH、ArkAdapter |
| 生态治理与研究路线图 | OpenHarmony 软件工程研究方向、开源许可证兼容性治理 | Software Engineering for OpenHarmony、LiScopeLens |
| 系统服务、图形性能与通信 | HarmonyOS/OpenHarmony 上的图形显示、渲染服务、内存拷贝优化、离线查找网络广播优化 | D-VSync、Spars、Copier、ElastiCast |

## 文献列表

### 应用分析、测试与质量保障

| 文献 | 来源 | 关联强度 | 简要说明 | Google Scholar |
| --- | --- | --- | --- | --- |
| HapTest: The Dynamic Analysis Framework for OpenHarmony | 主条目 | 直接相关 | 面向 OpenHarmony 应用的动态分析框架，覆盖代码插桩、UI/系统事件执行、页面转换图和可插拔探索策略。 | [检索](https://scholar.google.com/scholar?q=%22HapTest%3A+The+Dynamic+Analysis+Framework+for+OpenHarmony%22) |
| HapFlow: The Taint Analysis Framework for OpenHarmony Apps | 引用/主条目复现 | 直接相关 | 面向 OpenHarmony 原生应用的静态污点分析框架，处理生命周期回调、闭包、敏感 API 和数据泄漏路径。 | [检索](https://scholar.google.com/scholar?q=%22HapFlow%3A+The+Taint+Analysis+Framework+for+OpenHarmony+Apps%22) |
| An Empirical Study on UI Overlap in OpenHarmony Applications | 引用/主条目复现 | 直接相关 | 对 OpenHarmony 应用中的 UI 重叠现象进行大规模实证研究，并提出高代价遮挡缺陷检测思路。 | [检索](https://scholar.google.com/scholar?q=%22An+Empirical+Study+on+UI+Overlap+in+OpenHarmony+Applications%22) |
| HmTest: Automated Testing of HarmonyOS Apps via Model-Driven Navigation and Reinforcement Learning | 引用条目 | 直接相关 | 面向鸿蒙应用的自动化 GUI 测试框架，结合 ArkAnalyzer 构建页面转换图和强化学习探索。 | [检索](https://scholar.google.com/scholar?q=%22HmTest%3A+Automated+Testing+of+HarmonyOS+Apps+via+Model-Driven+Navigation+and+Reinforcement+Learning%22) |
| HACMony: Automatically Detecting Hopping-related Audio-stream Conflict Issues on HarmonyOS | 引用条目 | 直接相关 | 检测 HarmonyOS 跨设备迁移场景中的音频流冲突问题，关注多设备应用迁移语义。 | [检索](https://scholar.google.com/scholar?q=%22HACMony%3A+Automatically+Detecting+Hopping-related+Audio-stream+Conflict+Issues+on+HarmonyOS%22) |
| HapRepair: Learn to Repair OpenHarmony Apps | 主条目 | 直接相关 | 针对 OpenHarmony 应用 ArkTS 缺陷的自动修复框架，结合 CodeLinter、RAG 和 LLM 生成补丁。 | [检索](https://scholar.google.com/scholar?q=%22HapRepair%3A+Learn+to+Repair+OpenHarmony+Apps%22) |
| HapCheck: DSL-Based Static Bug Detection Framework for OpenHarmony | 主条目 | 直接相关 | 面向 OpenHarmony 的 DSL 静态缺陷检测框架；文档中标注为刚录用、尚未发表，信息较少。 | [检索](https://scholar.google.com/scholar?q=%22HapCheck%3A+DSL-Based+Static+Bug+Detection+Framework+for+OpenHarmony%22) |

### 静态分析、跨语言与安全加固

| 文献 | 来源 | 关联强度 | 简要说明 | Google Scholar |
| --- | --- | --- | --- | --- |
| ArkAnalyzer: The Static Analysis Framework for OpenHarmony Apps | 主条目 | 直接相关 | 面向 OpenHarmony/ArkTS 的静态分析框架，提供 ArkTS 中间表示、调用图、类型推断和分析能力。 | [检索](https://scholar.google.com/scholar?q=%22ArkAnalyzer%3A+The+Static+Analysis+Framework+for+OpenHarmony+Apps%22) |
| Context-Sensitive Pointer Analysis for ArkTS | 引用/主条目复现 | 直接相关 | 面向 ArkTS 的上下文敏感指针分析，补足 OpenHarmony 应用静态分析精度。 | [检索](https://scholar.google.com/scholar?q=%22Context-Sensitive+Pointer+Analysis+for+ArkTS%22) |
| HarmoBridge: Bridging ArkTS and C/C++ for Cross-Language Static Analysis on HarmonyOS | 主/引用条目 | 直接相关 | 面向 HarmonyOS 应用的 ArkTS 与 C/C++ 跨语言静态分析框架，建模 Node-API 数据流。 | [检索](https://scholar.google.com/scholar?q=%22HarmoBridge%3A+Bridging+ArkTS+and+C%2FC%2B%2B+for+Cross-Language+Static+Analysis+on+HarmonyOS%22) |
| HarmonyFlow: 基于方舟Panda IR 的HarmonyOS 应用静态分析框架 | 引用条目 | 直接相关 | 基于方舟 Panda IR 分析 HarmonyOS 应用字节码，解决 ArkAnalyzer 依赖源代码的局限。 | [检索](https://scholar.google.com/scholar?q=%22HarmonyFlow+Panda+IR+HarmonyOS+static+analysis+framework%22) |
| Path-Minimal Objects in ArkTS Symbolic Execution: From Path Constraints to TypeScript Tests | 引用条目 | 直接相关 | 面向 ArkTS/TypeScript/JavaScript 的符号测试生成方法，依托 ArkAnalyzer/ArkIR 场景。 | [检索](https://scholar.google.com/scholar?q=%22Path-Minimal+Objects+in+ArkTS+Symbolic+Execution%3A+From+Path+Constraints+to+TypeScript+Tests%22) |
| ArkObfux: a multi-layer reinforcement system designed for HarmonyOS terminal applications | 引用条目 | 直接相关 | 面向鸿蒙终端应用的源码级多层混淆与安全加固系统。 | [检索](https://scholar.google.com/scholar?q=%22ArkObfux+a+multi-layer+reinforcement+system+designed+for+HarmonyOS+terminal+applications%22) |

### ArkTS 代码智能、数据集与移植

| 文献 | 来源 | 关联强度 | 简要说明 | Google Scholar |
| --- | --- | --- | --- | --- |
| ArkTS-CodeSearch: A Open-Source ArkTS Dataset for Code Retrieval | 引用条目 | 直接相关 | 首个面向 ArkTS 语言的大规模代码检索数据集和评估基准，服务 OpenHarmony 代码智能研究。 | [检索](https://scholar.google.com/scholar?q=%22ArkTS-CodeSearch%3A+A+Open-Source+ArkTS+Dataset+for+Code+Retrieval%22) |
| ArkTS code generation: A comprehensive evaluation with large language models | 引用条目 | 直接相关 | 系统评估 LLM 在鸿蒙专用语言 ArkTS 上的代码生成能力，覆盖 API 使用和 UI 设计任务。 | [检索](https://scholar.google.com/scholar?q=%22ArkTS+code+generation%3A+A+comprehensive+evaluation+with+large+language+models%22) |
| Framework-Aware Code Generation with API Knowledge Graph-Constructed Data: A Study on HarmonyOS | 引用条目 | 直接相关 | 以 HarmonyOS 为案例，使用 API 知识图谱构建数据并微调模型，提升低资源框架代码生成。 | [检索](https://scholar.google.com/scholar?q=%22Framework-Aware+Code+Generation+with+API+Knowledge+Graph-Constructed+Data%3A+A+Study+on+HarmonyOS%22) |
| CROSS2OH: Enabling Seamless Porting of C/C++ Software Libraries to OpenHarmony | 主条目 | 直接相关 | 自动将 Linux C/C++ 软件库迁移到 OpenHarmony，识别并修复跨平台不兼容问题。 | [检索](https://scholar.google.com/scholar?q=%22CROSS2OH%3A+Enabling+Seamless+Porting+of+C%2FC%2B%2B+Software+Libraries+to+OpenHarmony%22) |
| Porting Software Libraries to OpenHarmony: Transitioning from TypeScript or JavaScript to ArkTS | 主条目 | 直接相关 | 研究 TypeScript/JavaScript 库迁移到 ArkTS 的语法差异和自动适配工具 ArkAdapter。 | [检索](https://scholar.google.com/scholar?q=%22Porting+Software+Libraries+to+OpenHarmony%3A+Transitioning+from+TypeScript+or+JavaScript+to+ArkTS%22) |

### 生态治理与研究路线图

| 文献 | 来源 | 关联强度 | 简要说明 | Google Scholar |
| --- | --- | --- | --- | --- |
| LiScopeLens: An Open-Source License Incompatibility Analysis Tool Based on Scope Representation of License Terms | 主条目 | 中等相关 | 通用开源许可证兼容性工具，但文档中明确在 OpenHarmony 5.0 beta 上评估并发现许可证冲突风险。 | [检索](https://scholar.google.com/scholar?q=%22LiScopeLens%3A+An+Open-Source+License+Incompatibility+Analysis+Tool+Based+on+Scope+Representation+of+License+Terms%22) |
| Software Engineering for OpenHarmony: A Research Roadmap | 主条目复现 | 直接相关 | 面向 OpenHarmony 软件工程研究的路线图，适合作为领域综述和研究方向入口。 | [检索](https://scholar.google.com/scholar?q=%22Software+Engineering+for+OpenHarmony%3A+A+Research+Roadmap%22) |

### 系统服务、图形性能与通信

| 文献 | 来源 | 关联强度 | 简要说明 | Google Scholar |
| --- | --- | --- | --- | --- |
| D-VSync: Decoupled Rendering and Displaying for Smartphone Graphics | 主条目 | 直接相关 | 在 OpenHarmony 和 Android 上评估，文档中说明已集成到 HarmonyOS NEXT，属于鸿蒙图形流畅性方向。 | [检索](https://scholar.google.com/scholar?q=%22D-VSync%3A+Decoupled+Rendering+and+Displaying+for+Smartphone+Graphics%22) |
| OS Rendering Service Made Parallel with Out-of-Order Execution and In-Order Commit | 主/引用条目 | 弱相关参考 | 提出 Spars 并行化操作系统渲染服务，在华为 Mate 设备和多屏场景上评估；标题不直接限定鸿蒙。 | [检索](https://scholar.google.com/scholar?q=%22OS+Rendering+Service+Made+Parallel+with+Out-of-Order+Execution+and+In-Order+Commit%22) |
| How to Copy Memory? Coordinated Asynchronous Copy as a First-Class OS Service | 主条目 | 弱相关参考 | Copier 是通用 OS 内存拷贝服务；文档中明确提到集成到鸿蒙 5.0 并优化视频解码。 | [检索](https://scholar.google.com/scholar?q=%22How+to+Copy+Memory%3F+Coordinated+Asynchronous+Copy+as+a+First-Class+OS+Service%22) |
| Toward Optimal Broadcast Mode in Offline Finding Network | 主条目 | 弱相关参考 | 离线查找网络与 BLE 广播优化；文档中涉及 HarmonyOS 扫描模式和华为 Tag 部署。 | [检索](https://scholar.google.com/scholar?q=%22Toward+Optimal+Broadcast+Mode+in+Offline+Finding+Network%22) |

## 可优先阅读的核心文献

如果只选少量鸿蒙核心文献，建议优先看以下几类：

1. `ArkAnalyzer`：OpenHarmony/ArkTS 后续静态分析、测试、修复工具的重要基础。
2. `HapTest`、`HapFlow`、`HmTest`：分别代表动态分析、污点分析和自动化 GUI 测试。
3. `CROSS2OH` 与 `Porting Software Libraries to OpenHarmony`：对应 OpenHarmony 生态迁移和第三方库补足问题。
4. `D-VSync`：代表 HarmonyOS/OpenHarmony 系统图形与流畅性优化方向。
5. `Software Engineering for OpenHarmony`：适合作为研究路线图入口。
