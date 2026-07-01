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
- **本地 PDF**：[文献/安全与静态分析/H013_.../H013.pdf](文献/安全与静态分析/H013_Context_Sensitive_Pointer_Analysis_for_ArkTS/H013.pdf)

#### H014 HarmoBridge：桥接 ArkTS 与 C/C++ 的跨语言静态分析
- **本地 PDF**：[文献/安全与静态分析/H014_.../H014.pdf](文献/安全与静态分析/H014_HarmoBridge_Bridging_ArkTS_and_C_C_for_Cross_Language_Static_Analysis/H014.pdf)

#### H015 HarmonyFlow：基于方舟 Panda IR 的 HarmonyOS 应用静态分析框架
- **本地 PDF**：[文献/安全与静态分析/H015_.../H015.pdf](文献/安全与静态分析/H015_HarmonyFlow_Panda_IR_HarmonyOS/H015.pdf)

#### H018 ArkObfux：面向 HarmonyOS 终端应用的多层加固系统
- **本地 PDF**：[文献/安全与静态分析/H018_.../H018.pdf](文献/安全与静态分析/H018_ArkObfux_a_multi_layer_reinforcement_system_designed_for_HarmonyOS_ter/H018.pdf)

### 应用测试与动态分析

#### H003 HapTest：面向 OpenHarmony 的动态分析框架
- **本地 PDF**：[文献/应用测试与动态分析/H003_.../H003.pdf](文献/应用测试与动态分析/H003_HapTest_The_Dynamic_Analysis_Framework_for_OpenHarmony/H003.pdf)

#### H012 HmTest：基于模型驱动导航与强化学习的 HarmonyOS 应用自动化测试
- **本地 PDF**：[文献/应用测试与动态分析/H012_.../H012.pdf](文献/应用测试与动态分析/H012_HmTest_Automated_Testing_of_HarmonyOS_Apps_via_Model_Driven_Navigation/H012.pdf)

#### H016 HACMony：自动检测 HarmonyOS 跨设备迁移相关的音频流冲突
- **本地 PDF**：[文献/应用测试与动态分析/H016_.../H016.pdf](文献/应用测试与动态分析/H016_HACMony_Automatically_Detecting_Hopping_related_Audio_stream_Conflict/H016.pdf)

### 应用测试与质量

#### H005 OpenHarmony 应用 UI 重叠的实证研究
- **本地 PDF**：[文献/应用测试与质量/H005_.../H005.pdf](文献/应用测试与质量/H005_An_Empirical_Study_on_UI_Overlap_in_OpenHarmony_Applications/H005.pdf)

#### H007 HapRepair：学习修复 OpenHarmony 应用
- **本地 PDF**：[文献/应用测试与质量/H007_.../H007.pdf](文献/应用测试与质量/H007_HapRepair_Learn_to_Repair_OpenHarmony_Apps/H007.pdf)

#### H009 幽灵渲染检测：识别并分析不必要的 UI 计算
- **本地 PDF**：[文献/应用测试与质量/H009_.../H009.pdf](文献/应用测试与质量/H009_Phantom_Rendering_Detection_Identifying_and_Analyzing_unnecessary_UI_c/H009.pdf)

#### H017 ArkTS 符号执行中的路径最小对象：从路径约束到 TypeScript 测试
- **本地 PDF**：[文献/应用测试与质量/H017_.../H017.pdf](文献/应用测试与质量/H017_Path_Minimal_Objects_in_ArkTS_Symbolic_Execution_From_Path_Constraints/H017.pdf)

#### H019 HapCheck：面向 OpenHarmony 的基于 DSL 的静态缺陷检测框架 `【暂未发现公开 PDF】`
- **本地 PDF**：暂无（待论文公开后补充）

### 生态治理与合规

#### H021 LiScopeLens：基于许可证条款作用域表示的开源许可证不兼容分析工具
- **本地 PDF**：[文献/生态治理与合规/H021_.../H021.pdf](文献/生态治理与合规/H021_LiScopeLens_An_Open_Source_License_Incompatibility_Analysis_Tool_Based/H021.pdf)

#### H022 面向开源软件许可证兼容性验证的综合框架
- **本地 PDF**：[文献/生态治理与合规/H022_.../H022.pdf](文献/生态治理与合规/H022_Towards_a_comprehensive_framework_for_verifying_open_source_software_l/H022.pdf)

### 生态移植与兼容

#### H023 CROSS2OH：让 C/C++ 软件库无缝移植到 OpenHarmony
- **本地 PDF**：[文献/生态移植与兼容/H023_.../H023.pdf](文献/生态移植与兼容/H023_CROSS2OH_Enabling_Seamless_Porting_of_C_C_Software_Libraries_to_OpenHa/H023.pdf)

#### H024 软件库移植到 OpenHarmony：从 TypeScript/JavaScript 到 ArkTS
- **本地 PDF**：[文献/生态移植与兼容/H024_.../H024.pdf](文献/生态移植与兼容/H024_Porting_Software_Libraries_to_OpenHarmony_Transitioning_from_TypeScrip/H024.pdf)

### 系统与运行时优化

#### H001 如何拷贝内存？作为一等 OS 服务的协调异步拷贝
- **本地 PDF**：[文献/系统与运行时优化/H001_.../H001.pdf](文献/系统与运行时优化/H001_How_to_Copy_Memory_Coordinated_Asynchronous_Copy_as_a_First_Class_OS_S/H001.pdf)

#### H002 让 OS 渲染服务并行化：乱序执行与顺序提交
- **本地 PDF**：[文献/系统与运行时优化/H002_.../H002.pdf](文献/系统与运行时优化/H002_OS_Rendering_Service_Made_Parallel_with_Out_of_Order_Execution_and_In/H002.pdf)

#### H025 D-VSync：面向智能手机图形的渲染与显示解耦
- **本地 PDF**：[文献/系统与运行时优化/H025_.../H025.pdf](文献/系统与运行时优化/H025_D_VSync_Decoupled_Rendering_and_Displaying_for_Smartphone_Graphics/H025.pdf)

### 综述与路线图

#### H020 面向 OpenHarmony 的软件工程：研究路线图
- **本地 PDF**：[文献/综述与路线图/H020_.../H020.pdf](文献/综述与路线图/H020_Software_Engineering_for_OpenHarmony_A_Research_Roadmap/H020.pdf)

### 通信与设备协同

#### H026 离线查找网络中广播模式的优化
- **本地 PDF**：[文献/通信与设备协同/H026_.../H026.pdf](文献/通信与设备协同/H026_Toward_Optimal_Broadcast_Mode_in_Offline_Finding_Network/H026.pdf)

#### H027 离线查找网络中 BLE 广播模式优化
- **本地 PDF**：[文献/通信与设备协同/H027_.../H027.pdf](文献/通信与设备协同/H027_Optimization_of_BLE_Broadcast_Mode_in_Offline_Finding_Network/H027.pdf)

#### H028 CPBIS：通过特定比例广播区间筛选机制在离线查找网络中达到理论最低发现延迟
- **本地 PDF**：[文献/通信与设备协同/H028_.../H028.pdf](文献/通信与设备协同/H028_CPBIS_Achieving_Theoretical_Minimum_Discovery_latency_in_Offline_Findi/H028.pdf)

#### H029 揭秘星闪低能耗（SLE）：一项对比测量研究
- **本地 PDF**：[文献/通信与设备协同/H029_.../H029.pdf](文献/通信与设备协同/H029_Unveiling_SparkLink_Low_Energy_a_Comparative_Measurement_Study/H029.pdf)
