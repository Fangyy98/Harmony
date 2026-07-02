# 鸿蒙（HarmonyOS / OpenHarmony）相关文献资料库

这个仓库收集并整理了围绕鸿蒙生态的学术文献，覆盖系统运行时优化、ArkTS 程序分析、应用测试与质量、代码智能、生态移植与合规、设备协同等方向。目的是给想系统了解鸿蒙软件工程研究的人一个可检索的入口——每篇论文都附了简介、发表信息、论文链接和（如果有的话）开源代码地址，本地也保存了 PDF 方便离线阅读。

## 仓库结构

文献按研究方向分文件夹存放，每个分类目录下再按「一篇文献一个文件夹」组织：

```
文献/
├── 代码智能与数据集/        # ArkTS 代码检索、代码生成评测、框架感知生成
├── 安全与静态分析/          # 污点分析、指针分析、跨语言分析、静态分析框架、应用加固
├── 应用测试与动态分析/      # 动态分析框架、自动化测试、跨设备音频冲突检测
├── 应用测试与质量/          # UI 重叠、缺陷修复、幽灵渲染、符号执行测试、静态缺陷检测
├── 生态治理与合规/          # 开源许可证兼容性分析
├── 生态移植与兼容/          # C/C++ 与 TS/JS 库向 OpenHarmony / ArkTS 移植
├── 系统与运行时优化/        # 内存拷贝、渲染服务并行化、VSync 解耦
├── 综述与路线图/            # OpenHarmony 软件工程研究路线图
└── 通信与设备协同/          # 离线查找网络广播优化、星闪低能耗测量
```

每个文献文件夹固定包含：

- `Hxxx.pdf`：论文 PDF（H019 暂未发现公开 PDF，仅有会议页面信息）。
- `url.txt`：论文页、DOI、PDF 入口、Google Scholar 等链接，部分含开源代码地址。
- `说明.txt`：编号、分类、相关性、收录原因、PDF 状态和核验说明。


## 总览

- 文献目录数：29
- 本地 PDF：28 个（H019 暂未发现公开 PDF）
- 相关性口径：**强相关** = 直接研究 OpenHarmony / HarmonyOS / ArkTS / HAP / ArkUI；**平台相关** = 鸿蒙系统服务或 HarmonyOS NEXT 等平台能力；**设备生态弱相关** = 通信、离线查找、星闪等设备生态。

---

## 文献索引

### 代码智能与数据集

#### H006 ArkTS-CodeSearch：面向代码检索的开源 ArkTS 数据集
- **简介**：针对 ArkTS 代码智能研究缺乏公开数据集和评测基准的问题，从 GitHub 和 Gitee 爬取开源仓库，用 tree-sitter-arkts 抽取「注释—函数」对，构建了首个系统化的 ArkTS 代码检索基准，并在其上微调出一个代码嵌入模型。
- **发表信息**：2026 / arXiv（arXiv:2602.05550）
- **论文**：<https://arxiv.org/abs/2602.05550>
- **开源数据/模型**：<https://huggingface.co/datasets/hreyulog/arkts-code-docstring>、<https://huggingface.co/hreyulog/embedinggemma_arkts>
- **本地 PDF**：[文献/代码智能与数据集/H006_.../H006.pdf](文献/代码智能与数据集/H006_ArkTS_CodeSearch_A_Open_Source_ArkTS_Dataset_for_Code_Retrieval/H006.pdf)

#### H008 ArkTS 代码生成：大语言模型综合评测
- **简介**：首次系统评测 LLM 在 ArkTS 上的代码生成能力。用 300 个分难度的提示测了 21 个模型，考察 Pass@1、编译率和生成时间，并映射编译错误类型。结论是功能正确率普遍偏低，响应式状态与生命周期处理仍是难点；加一个紧凑示例并做一轮编译器引导修复能把 Pass@1 从 23.3% 提到 36.7%。
- **发表信息**：2026 / Empirical Software Engineering（DOI: 10.1007/s10664-026-10844-0）
- **论文**：<https://doi.org/10.1007/s10664-026-10844-0>
- **本地 PDF**：[文献/代码智能与数据集/H008_.../H008.pdf](文献/代码智能与数据集/H008_ArkTS_code_generation_A_comprehensive_evaluation_with_large_language_m/H008.pdf)

#### H011 面向低资源软件开发的知识图谱驱动数据合成（以 HarmonyOS 为例）
- **简介**：针对低资源框架（如 HarmonyOS）下 LLM 因预训练暴露不足而代码生成效果差的问题，提出 APIKG4Syn 框架，利用 API 知识图谱合成「问题—代码」对作为微调数据，结合不确定性估计和 MCTS 构造多 API 数据。以 HarmonyOS 为案例构建代码生成基准，微调 Qwen2.5-Coder-7B 后 pass@1 达 25%，超过未微调的 GPT-4o（17.59%）。
- **发表信息**：2025 / arXiv preprint（arXiv:2512.00380）
- **论文**：<https://arxiv.org/abs/2512.00380>
- **本地 PDF**：[文献/代码智能与数据集/H011_.../H011.pdf](文献/代码智能与数据集/H011_Framework_Aware_Code_Generation_with_API_Knowledge_Graph_Constructed_D/H011.pdf)

### 安全与静态分析

#### H004 HapFlow：面向 OpenHarmony 应用的污点分析框架
- **简介**：针对 OpenHarmony 缺乏可用污点分析框架的现状，提出 HapFlow。它用 LLM 辅助识别和分类源 API，建模 ArkTS 声明式 UI 的生命周期与回调，并扩展 IFDS 污点传播以处理闭包导致的跨函数数据流。在 HapBench 上精确率 96.15%、召回率 94.34%，并在 3000+ 开源项目中检出 73 处敏感数据泄漏。
- **发表信息**：2026 / ACM Transactions on Software Engineering and Methodology（DOI: 10.1145/3793863）
- **论文**：<https://doi.org/10.1145/3793863>
- **本地 PDF**：[文献/安全与静态分析/H004_.../H004.pdf](文献/安全与静态分析/H004_HapFlow_the_Taint_Analysis_Framework_for_OpenHarmony_Apps/H004.pdf)

#### H010 ArkAnalyzer：面向 OpenHarmony 应用的静态分析框架
- **简介**：为 OpenHarmony 社区补上缺失的通用静态分析框架。ArkAnalyzer 已集成控制流图、调用图构造等基础分析能力，开发者可在此基础上实现性能缺陷、隐私泄漏、兼容性等专项检测器。论文声明已开源，并附带了真实 ArkTS 应用数据集。
- **发表信息**：2025 / ICSE 2025 SEIP（DOI: 10.1109/icse-seip66354.2025.00018）
- **论文**：<https://doi.org/10.1109/icse-seip66354.2025.00018>
- **开源**：论文声明开源（仓库地址未在 url.txt 中记录）
- **本地 PDF**：[文献/安全与静态分析/H010_.../H010.pdf](文献/安全与静态分析/H010_ArkAnalyzer_The_Static_Analysis_Framework_for_OpenHarmony_Apps/H010.pdf)

#### H013 面向 ArkTS 的上下文敏感指针分析
- **简介**：针对 ArkTS 调用图生成精度不足、现有 JS/TS 分析工具无法理解 ArkUI 组件树语义的问题，提出首个面向 ArkTS 的上下文敏感指针分析框架 APAK。它设计了 ArkTS 堆对象模型和可扩展插件架构，在 1663 个真实应用上有效边覆盖优于 CHA/RTA，把误报率从 20% 降到 2%，并已合并进官方 ArkAnalyzer。
- **发表信息**：2025 / ASE 2025（DOI: 10.1109/ase63991.2025.00269）
- **论文**：<https://doi.org/10.1109/ase63991.2025.00269>
- **本地 PDF**：[文献/安全与静态分析/H013_.../H013.pdf](文献/安全与静态分析/H013_Context_Sensitive_Pointer_Analysis_for_ArkTS/H013.pdf)

#### H014 HarmoBridge：桥接 ArkTS 与 C/C++ 的跨语言静态分析
- **简介**：HarmonyOS 应用可通过 NDK 集成 C/C++ 模块，但跨语言数据流对单语言分析器不可见。HarmoBridge 提出基于摘要的 SumIR 抽象，从原生代码（支持二进制和源码）抽取数据流摘要并转成 ArkIR 兼容形式，衔接下游分析。配套 CROSSFLOWBENCH 基准，跨语言数据流恢复准确率 81.0%。
- **发表信息**：2025 / ASE 2025（DOI: 10.1109/ase63991.2025.00261）
- **论文**：<https://doi.org/10.1109/ase63991.2025.00261>
- **本地 PDF**：[文献/安全与静态分析/H014_.../H014.pdf](文献/安全与静态分析/H014_HarmoBridge_Bridging_ArkTS_and_C_C_for_Cross_Language_Static_Analysis/H014.pdf)

#### H015 HarmonyFlow：基于方舟 Panda IR 的 HarmonyOS 应用静态分析框架
- **简介**：针对源码难以获取的现实，直接基于方舟中间表示（Panda IR）做鸿蒙应用静态分析。对 318 条指令做语义分类并定制指针流图，设计适应 ArkTS 语法的字段敏感指针分析，新增指向集合传播规则并建模特殊调用。在 9 个开源鸿蒙应用上调用边识别精确率 98.33%、召回率 92.22%，35 个真实应用平均运行 96 秒。
- **发表信息**：2025 / 软件学报（DOI: 10.13328/j.cnki.jos.007477）
- **论文**：<https://www.jos.org.cn/jos/article/abstract/7477>
- **本地 PDF**：[文献/安全与静态分析/H015_.../H015.pdf](文献/安全与静态分析/H015_HarmonyFlow_Panda_IR_HarmonyOS/H015.pdf)

#### H018 ArkObfux：面向 HarmonyOS 终端应用的多层加固系统
- **简介**：针对鸿蒙生态扩张带来的逆向工程、敏感数据泄漏和权限滥用风险，提出 ArkObfux 加固系统，在 ArkTS 源码层集成基于 SM2 的敏感数据加密、虚假控制流、控制流平坦化和布局混淆四种机制，兼容现有 HarmonyOS 开发工具链且无需改动工具链。
- **发表信息**：2026 / SSRN Electronic Journal（DOI: 10.2139/ssrn.6432372）
- **论文**：<https://doi.org/10.2139/ssrn.6432372>
- **本地 PDF**：[文献/安全与静态分析/H018_.../H018.pdf](文献/安全与静态分析/H018_ArkObfux_a_multi_layer_reinforcement_system_designed_for_HarmonyOS_ter/H018.pdf)

### 应用测试与动态分析

#### H003 HapTest：面向 OpenHarmony 的动态分析框架
- **简介**：为 OpenHarmony 应用补上缺失的动态分析框架。HapTest 提供 PTG、DataHub 等基础动态分析能力，可被复用和定制以检测恶意行为或性能问题。在 OpenHarmony 应用市场下载量靠前的 20 款商业应用上测出 26 个此前未报告的崩溃（11 款应用中）。论文声明已开源。
- **发表信息**：2025 / FSE 2025（DOI: 10.1145/3696630.3728565）
- **论文**：<https://doi.org/10.1145/3696630.3728565>
- **开源**：论文声明开源（仓库地址未在 url.txt 中记录）
- **本地 PDF**：[文献/应用测试与动态分析/H003_.../H003.pdf](文献/应用测试与动态分析/H003_HapTest_The_Dynamic_Analysis_Framework_for_OpenHarmony/H003.pdf)

#### H012 HmTest：基于模型驱动导航与强化学习的 HarmonyOS 应用自动化测试
- **简介**：提出 HmTest 自动化测试框架，由两个互补模块组成：白盒的定向探索用静态分析构造页面跳转图（PTG）快速达成高页面覆盖；黑盒的强化学习探索实现细粒度状态覆盖，并用自动机机制在停滞时恢复重启。在 9 款 HarmonyOS NEXT 应用上评测，已开源并提供演示视频。
- **发表信息**：2025 / Journal of Computer Science and Technology（DOI: 10.1007/s11390-025-5142-4）
- **论文**：<https://doi.org/10.1007/s11390-025-5142-4>
- **开源代码**：<https://github.com/sqlab-sustech/hmtest>
- **本地 PDF**：[文献/应用测试与动态分析/H012_.../H012.pdf](文献/应用测试与动态分析/H012_HmTest_Automated_Testing_of_HarmonyOS_Apps_via_Model_Driven_Navigation/H012.pdf)

#### H016 HACMony：自动检测 HarmonyOS 跨设备迁移相关的音频流冲突
- **简介**：HarmonyOS 的应用流转（app-hopping）让应用可跨设备无缝切换，但音频流跨设备迁移时容易触发音频流冲突（HAC）。HACMony 首次形式化了音频流流转的操作语义，设计音频流感知状态转移图（ASTG）建模窗口迁移行为，并基于模型自动检测 HAC 问题。在 20 款真实应用上检出 53 个 HAC 问题，手动确认 18 个，归纳为 MoD 和 MoR 两类。
- **发表信息**：2025 / arXiv（arXiv:2504.07472）
- **论文**：<https://arxiv.org/abs/2504.07472>
- **本地 PDF**：[文献/应用测试与动态分析/H016_.../H016.pdf](文献/应用测试与动态分析/H016_HACMony_Automatically_Detecting_Hopping_related_Audio_stream_Conflict/H016.pdf)

### 应用测试与质量

#### H005 OpenHarmony 应用 UI 重叠的实证研究
- **简介**：首次对 OpenHarmony 生态的 UI 重叠现象做大规模实证研究。分析 100 款热门应用、3300 万+ 重叠实例并提出三层分类法，发现「高代价遮挡」是一类此前难以发现的性能缺陷——被遮挡的高耗资源组件仍在渲染。提出 HCO-Eye 工具，用多模态视觉语言模型自动检测此类问题，在商业应用中识别出 34 例。工具已公开。
- **发表信息**：2025 / ASE 2025（DOI: 10.1109/ase63991.2025.00274）
- **论文**：<https://doi.org/10.1109/ase63991.2025.00274>
- **开源**：论文声明工具已公开（仓库地址未在 url.txt 中记录）
- **本地 PDF**：[文献/应用测试与质量/H005_.../H005.pdf](文献/应用测试与质量/H005_An_Empirical_Study_on_UI_Overlap_in_OpenHarmony_Applications/H005.pdf)

#### H007 HapRepair：学习修复 OpenHarmony 应用
- **简介**：针对 LLM 在 ArkTS 这类新语言上因训练语料不足而缺陷修复效果差的问题，提出 HapRepair。它把 CodeLinter 静态分析集成进迭代修复流程做缺陷检测，用 RAG 配合 ArkAnalyzer 提升修复质量，并设计 Surrounding Context Extractor 和 Context Combination Tool 应对上下文窗口限制。测试集上缺陷修复率约 99%，而直接用 LLM 仅约 37%。
- **发表信息**：2025 / FSE 2025（DOI: 10.1145/3696630.3728556）
- **论文**：<https://doi.org/10.1145/3696630.3728556>
- **本地 PDF**：[文献/应用测试与质量/H007_.../H007.pdf](文献/应用测试与质量/H007_HapRepair_Learn_to_Repair_OpenHarmony_Apps/H007.pdf)

#### H009 幽灵渲染检测：识别并分析不必要的 UI 计算
- **简介**：刻画一类此前被忽视的性能问题——「幽灵渲染」：应用做了不必要的 UI 离屏计算却不在屏幕上渲染（如动画组件停止显示但仍在后台刷新）。提出 HapPRDetection，用细粒度性能剖析器采样 CPU 已退休指令，通过差分分析和层级归因自动检测该问题。在 OpenHarmony 下载量前 22 的应用、193 个测试步骤中，19 个测试步骤、8 款应用存在该问题，单次操作最多浪费 40% CPU 指令。已开源。
- **发表信息**：2026 / FSE 2026
- **论文**：<https://conf.researchr.org/details/fse-2026/fse-2026-research-papers/172/Phantom-Rendering-Detection-Identifying-and-Analyzing-unnecessary-UI-computations>
- **开源代码**：<https://github.com/SMAT-Lab/PhantomRendering>
- **本地 PDF**：[文献/应用测试与质量/H009_.../H009.pdf](文献/应用测试与质量/H009_Phantom_Rendering_Detection_Identifying_and_Analyzing_unnecessary_UI_c/H009.pdf)

#### H017 ArkTS 符号执行中的路径最小对象：从路径约束到 TypeScript 测试
- **简介**：研究在 ArkTS 中间表示（ArkIR）上的符号测试生成，提出「路径最小对象」（PMO）——构造只含满足选定路径所需属性的对象，并生成可运行的 Jest 风格 TypeScript 测试。执行器把类型推理与路径推理分离，精确处理 NaN、-0、异常等运行时值。在代表性 ArkIR 片段上能自动发现并重放覆盖成员缺失、NaN 强制转换、严格/宽松相等、嵌套读取、写后删、不可达分支等路径。
- **发表信息**：2025 / ICCQ 2025（DOI: 10.1109/iccq65694.2025.11314570）
- **论文**：<https://doi.org/10.1109/iccq65694.2025.11314570>
- **本地 PDF**：[文献/应用测试与质量/H017_.../H017.pdf](文献/应用测试与质量/H017_Path_Minimal_Objects_in_ArkTS_Symbolic_Execution_From_Path_Constraints/H017.pdf)

#### H019 HapCheck：面向 OpenHarmony 的基于 DSL 的静态缺陷检测框架 `【暂未发现公开 PDF】`
- **简介**：面向 OpenHarmony 的静态缺陷检测框架，用领域特定语言（DSL）定义检测规则。该论文收录于 ICSE 2026 SEIP，目前暂未发现公开 PDF 和 DOI；待论文公开后会补上本地 PDF。相关链接见作者主页与会议详情页。
- **发表信息**：2026 / ICSE 2026 SEIP
- **会议详情页**：<https://conf.researchr.org/details/icse-2026/icse-2026-software-engineering-in-practice/40/HapCheck-DSL-Based-Static-Bug-Detection-Framework-for-OpenHarmony>
- **作者主页**：<https://zhoumingyi.github.io/>
- **本地 PDF**：暂无（待论文公开后补充）

### 生态治理与合规

#### H021 LiScopeLens：基于许可证条款作用域表示的开源许可证不兼容分析工具
- **简介**：针对许可证不兼容分析难以覆盖多样使用场景、误报率高的问题，从许可证例外入手做大量实证研究，提出更细化的法律术语表示和许可证兼容性推理方法，按不同场景建模兼容性。实现 LiScopeLens 工具，能识别依赖行为并从二进制依赖做起做细粒度兼容性判定，并在 OpenHarmony 5.0 beta 上做了评估。
- **发表信息**：2024 / ISSRE 2024（DOI: 10.1109/issre62328.2024.00013）
- **论文**：<https://doi.org/10.1109/issre62328.2024.00013>
- **本地 PDF**：[文献/生态治理与合规/H021_.../H021.pdf](文献/生态治理与合规/H021_LiScopeLens_An_Open_Source_License_Incompatibility_Analysis_Tool_Based/H021.pdf)

#### H022 面向开源软件许可证兼容性验证的综合框架
- **简介**：针对许可证兼容性分析缺乏统一方法的问题，做大规模实证研究，发现使用场景对兼容性影响广泛——同一语言内不同场景兼容性可能显著不同，不同语言间差异更大。提出聚焦二进制分发中被动许可证传播的统一框架，并实现 LiScopeLens-Plus 工具，可在任意依赖构造图上解析许可证传播并做兼容性分析。在 OpenHarmony 上验证发现大量此前未识别的许可证冲突。
- **发表信息**：2026 / Empirical Software Engineering（DOI: 10.1007/s10664-025-10751-w）
- **论文**：<https://doi.org/10.1007/s10664-025-10751-w>
- **本地 PDF**：[文献/生态治理与合规/H022_.../H022.pdf](文献/生态治理与合规/H022_Towards_a_comprehensive_framework_for_verifying_open_source_software_l/H022.pdf)

### 生态移植与兼容

#### H023 CROSS2OH：让 C/C++ 软件库无缝移植到 OpenHarmony
- **简介**：针对 Linux 到 OpenHarmony 移植 C/C++ 库时因系统库、运行时和构建系统差异导致的跨平台不兼容（CPI）问题，对 92 个成功移植的库做实证研究，归纳出三类差异、八个维度和八种适配策略。据此实现 CROSS2OH，结合适配知识库和静态分析自动检测并修补八类 CPI 问题，召回率 0.94、精确率 0.91，让 40 个关键库成功交叉编译，其中 29 个通过 OpenHarmony 官方评审。
- **发表信息**：2025 / ASE 2025（DOI: 10.1109/ase63991.2025.00146）
- **论文**：<https://doi.org/10.1109/ase63991.2025.00146>
- **本地 PDF**：[文献/生态移植与兼容/H023_.../H023.pdf](文献/生态移植与兼容/H023_CROSS2OH_Enabling_Seamless_Porting_of_C_C_Software_Libraries_to_OpenHa/H023.pdf)

#### H024 软件库移植到 OpenHarmony：从 TypeScript/JavaScript 到 ArkTS
- **简介**：针对把 TS/JS 库迁移到 ArkTS 需要大量手工改动且缺乏自动化工具的问题，提出 ArkAdapter 项目级自动代码适配方法。它建立 ArkTS 语法适配知识库做少样本学习，并用考虑依赖结构和语法失配粒度的适配优先级策略避免不同失配间互相干扰。定位精确率 86.84%、召回率 100%，LLM 推断的适配 80.14% 与开发者实际改动吻合；移植 79 个常用库，70 个通过 ArkCompiler 编译、测试与官方评审。
- **发表信息**：2025 / Proceedings of the ACM on Software Engineering（DOI: 10.1145/3728941）
- **论文**：<https://doi.org/10.1145/3728941>
- **本地 PDF**：[文献/生态移植与兼容/H024_.../H024.pdf](文献/生态移植与兼容/H024_Porting_Software_Libraries_to_OpenHarmony_Transitioning_from_TypeScrip/H024.pdf)

### 系统与运行时优化

#### H001 如何拷贝内存？作为一等 OS 服务的协调异步拷贝
- **简介**：主张把内存拷贝提升为操作系统的一等服务，带来三方面好处：异步拷贝抽象让应用执行与拷贝重叠、能更好利用硬件能力、全局视角支持整体优化。实现 Copier 服务并构建 Copier-Linux，在 Redis、Protobuf、网络栈等场景获得最高 1.8 倍加速，超过 zIO 1.6 倍；并已集成进 HarmonyOS 5.0 用于视频解码优化。
- **发表信息**：2025 / SOSP 2025（DOI: 10.1145/3731569.3764800）
- **论文**：<https://dl.acm.org/doi/10.1145/3731569.3764800>
- **本地 PDF**：[文献/系统与运行时优化/H001_.../H001.pdf](文献/系统与运行时优化/H001_How_to_Copy_Memory_Coordinated_Asynchronous_Copy_as_a_First_Class_OS_S/H001.pdf)

#### H002 让 OS 渲染服务并行化：乱序执行与顺序提交
- **简介**：针对折叠屏、多屏等高扩展显示场景下渲染负载激增、帧率下降的问题，观察到渲染流程中相当一部分可并行化。提出 Spars，借鉴体系结构的乱序执行—顺序提交思想：先顺序准备生成自包含渲染任务，再乱序执行最大化多核并行，最后顺序提交保证绘制顺序。在单屏、双折、三折手机及一芯多屏配置上平均帧率提升 1.76×–1.91×。
- **发表信息**：2025 / OSDI 2025
- **论文**：<https://www.usenix.org/conference/osdi25/presentation/wu-yuanpei>
- **本地 PDF**：[文献/系统与运行时优化/H002_.../H002.pdf](文献/系统与运行时优化/H002_OS_Rendering_Service_Made_Parallel_with_Out_of_Order_Execution_and_In/H002.pdf)

#### H025 D-VSync：面向智能手机图形的渲染与显示解耦
- **简介**：针对大屏高帧率、复杂动效给基于 VSync 的渲染架构带来的压力，提出 D-VSync，把渲染服务的执行与显示解耦，允许帧提前若干个 VSync 周期渲染，让偶发长帧借用短帧省下的算力。在 OpenHarmony（Mate 40 Pro/60 Pro）、Android（Pixel 5）和游戏模拟上，平均掉帧减少 72.7%、可感知卡顿减少 72.3%、渲染延迟降低 31.1%，功耗仅增 0.13%–0.37%。已集成进 HarmonyOS NEXT。
- **发表信息**：2025 / ASPLOS 2025（DOI: 10.1145/3669940.3707235）
- **论文**：<https://doi.org/10.1145/3669940.3707235>
- **本地 PDF**：[文献/系统与运行时优化/H025_.../H025.pdf](文献/系统与运行时优化/H025_D_VSync_Decoupled_Rendering_and_Displaying_for_Smartphone_Graphics/H025.pdf)

### 综述与路线图

#### H020 面向 OpenHarmony 的软件工程：研究路线图
- **简介**：面向移动软件工程社区给出 OpenHarmony 的研究路线图。先做移动软件工程的三级文献综述，理解社区已解决和未解决的问题；再总结 OpenHarmony 现有（有限的）成果，对比 Android/iOS 与 OpenHarmony 的研究差距，由此形成路线图，鼓励研究者投入这个预计将占据中国三分之一市场份额的新平台。
- **发表信息**：2026 / ACM Computing Surveys（DOI: 10.1145/3720538）
- **论文**：<https://doi.org/10.1145/3720538>
- **本地 PDF**：[文献/综述与路线图/H020_.../H020.pdf](文献/综述与路线图/H020_Software_Engineering_for_OpenHarmony_A_Research_Roadmap/H020.pdf)

### 通信与设备协同

> 以下四篇聚焦离线查找网络（OFN）的 BLE 广播优化和星闪低能耗测量，与鸿蒙/华为设备生态相关，但并非直接研究 OpenHarmony 应用，故标记为设备生态弱相关。

#### H026 离线查找网络中广播模式的优化
- **简介**：提出 ElastiCast，一种新的 BLE 广播模式，降低离线查找网络中邻居发现延迟，让丢失设备的广播模式自适应查找设备的扫描模式。提供 Blender 模拟器建模邻居发现行为，通过局部最优估计、共同兴趣提取和区间复用三个组件全局优化广播模式，并有商用产品部署经验。
- **发表信息**：2025 / IEEE Transactions on Mobile Computing（DOI: 10.1109/tmc.2025.3545561）
- **论文**：<https://doi.org/10.1109/tmc.2025.3545561>
- **本地 PDF**：[文献/通信与设备协同/H026_.../H026.pdf](文献/通信与设备协同/H026_Toward_Optimal_Broadcast_Mode_in_Offline_Finding_Network/H026.pdf)

#### H027 离线查找网络中 BLE 广播模式优化
- **简介**：提出 CPBIS 机制——按一定比例筛选广播区间，为离线标签计算最合适的两个广播区间及其比例，降低 BLE 邻居发现过程中的发现延迟、提升发现成功率。是首个针对 BLE 邻居发现中广告者广播区间参数（尤其涉及两个及以上区间）配置的综合方案，在 nRF52832 芯片上验证。与 H028 为同一工作的预印本与正式发表。
- **发表信息**：2025 / arXiv preprint（arXiv:2504.01422）
- **论文**：<https://arxiv.org/abs/2504.01422>
- **本地 PDF**：[文献/通信与设备协同/H027_.../H027.pdf](文献/通信与设备协同/H027_Optimization_of_BLE_Broadcast_Mode_in_Offline_Finding_Network/H027.pdf)

#### H028 CPBIS：通过特定比例广播区间筛选机制在离线查找网络中达到理论最低发现延迟
- **简介**：H027 的正式发表版。证明在多数场景下双区间广播比单区间发现延迟更低，提出 CPBIS 机制由混合分布获取、非递增元素消除、最优区间对计算三模块组成，理论上达到多扫描模式下的最低发现延迟。在 nRF52832 上验证，发现延迟和成功率分别优于基线 31.3% 和 7.3%。
- **发表信息**：2026 / Journal of Network and Computer Applications（DOI: 10.1016/j.jnca.2026.104539）
- **论文**：<https://doi.org/10.1016/j.jnca.2026.104539>
- **本地 PDF**：[文献/通信与设备协同/H028_.../H028.pdf](文献/通信与设备协同/H028_CPBIS_Achieving_Theoretical_Minimum_Discovery_latency_in_Offline_Findi/H028.pdf)

#### H029 揭秘星闪低能耗（SLE）：一项对比测量研究
- **简介**：对星闪低能耗（SLE）这一新型短距无线通信技术做首次全面的实测对比。基准测试显示 SLE 相比传统蓝牙数据率提升 4 倍、延迟降低 3.84 倍、灵敏度改善 10 dB；并在三个实际应用场景下做端到端验证，提出以 QoS 为中心的优化设计。
- **发表信息**：2026 / ACM Transactions on Internet of Things（DOI: 10.1145/3776559）
- **论文**：<https://doi.org/10.1145/3776559>
- **本地 PDF**：[文献/通信与设备协同/H029_.../H029.pdf](文献/通信与设备协同/H029_Unveiling_SparkLink_Low_Energy_a_Comparative_Measurement_Study/H029.pdf)
