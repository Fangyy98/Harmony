# 鸿蒙相关文献资料库
这个仓库按“一篇文献一个文件夹”组织。每个文件夹固定包含：
- `url.txt`：论文页、DOI、PDF入口、Google Scholar 等链接。
- `说明.txt`：分类、相关性、收录原因、PDF状态和核验说明。
- `Hxxx.pdf`：如果能公开直接下载，则已放在对应文件夹中。

## 补充材料
- [分类整理文档](docs/harmony_literature.md)：从原始 Word 文档中筛选并粗分类的鸿蒙相关文献表。
- [原始资料压缩包](archives/harmony.zip)：本目录结构的来源压缩包备份。

## 总览
- 文献目录数：29
- 本地 PDF：7 个
- 相关性口径：强相关 = 直接研究 OpenHarmony/HarmonyOS/ArkTS/HAP/ArkUI；平台相关 = 鸿蒙系统服务或 HarmonyOS NEXT 等平台能力；设备生态弱相关 = 通信、离线查找、星闪等设备生态。

## 快速检索
```bash
find 文献 -maxdepth 2 -type f -name "说明.txt" -print
grep -R "ArkTS" 文献
find 文献 -name "*.pdf"
```

## 文献索引
### 代码智能与数据集
- [H006 ArkTS-CodeSearch: A Open-Source ArkTS Dataset for Code Retrieval](文献/H006_ArkTS_CodeSearch_A_Open_Source_ArkTS_Dataset_for_Code_Retrieval/) - 强相关，有PDF
- [H008 ArkTS code generation: A comprehensive evaluation with large language models](文献/H008_ArkTS_code_generation_A_comprehensive_evaluation_with_large_language_m/) - 强相关，有PDF
- [H011 Framework-Aware Code Generation with API Knowledge Graph-Constructed Data: A Study on HarmonyOS](文献/H011_Framework_Aware_Code_Generation_with_API_Knowledge_Graph_Constructed_D/) - 强相关，有PDF

### 安全与静态分析
- [H004 HapFlow: the Taint Analysis Framework for OpenHarmony Apps](文献/H004_HapFlow_the_Taint_Analysis_Framework_for_OpenHarmony_Apps/) - 强相关，无本地PDF
- [H010 ArkAnalyzer: The Static Analysis Framework for OpenHarmony Apps](文献/H010_ArkAnalyzer_The_Static_Analysis_Framework_for_OpenHarmony_Apps/) - 强相关，无本地PDF
- [H013 Context-Sensitive Pointer Analysis for ArkTS](文献/H013_Context_Sensitive_Pointer_Analysis_for_ArkTS/) - 强相关，无本地PDF
- [H014 HarmoBridge: Bridging ArkTS and C/C++ for Cross-Language Static Analysis on HarmonyOS](文献/H014_HarmoBridge_Bridging_ArkTS_and_C_C_for_Cross_Language_Static_Analysis/) - 强相关，无本地PDF
- [H015 HarmonyFlow: 基于方舟Panda IR 的HarmonyOS 应用静态分析框架](文献/H015_HarmonyFlow_Panda_IR_HarmonyOS/) - 强相关，无本地PDF
- [H018 ArkObfux: a multi-layer reinforcement system designed for HarmonyOS terminal applications](文献/H018_ArkObfux_a_multi_layer_reinforcement_system_designed_for_HarmonyOS_ter/) - 强相关，无本地PDF

### 应用测试与动态分析
- [H003 HapTest: The Dynamic Analysis Framework for OpenHarmony](文献/H003_HapTest_The_Dynamic_Analysis_Framework_for_OpenHarmony/) - 强相关，无本地PDF
- [H012 HmTest: Automated Testing of HarmonyOS Apps via Model-Driven Navigation and Reinforcement Learning](文献/H012_HmTest_Automated_Testing_of_HarmonyOS_Apps_via_Model_Driven_Navigation/) - 强相关，无本地PDF
- [H016 HACMony: Automatically Detecting Hopping-related Audio-stream Conflict Issues on HarmonyOS](文献/H016_HACMony_Automatically_Detecting_Hopping_related_Audio_stream_Conflict/) - 强相关，有PDF

### 应用测试与质量
- [H005 An Empirical Study on UI Overlap in OpenHarmony Applications](文献/H005_An_Empirical_Study_on_UI_Overlap_in_OpenHarmony_Applications/) - 强相关，无本地PDF
- [H007 HapRepair: Learn to Repair OpenHarmony Apps](文献/H007_HapRepair_Learn_to_Repair_OpenHarmony_Apps/) - 强相关，无本地PDF
- [H009 Phantom Rendering Detection: Identifying and Analyzing unnecessary UI computations](文献/H009_Phantom_Rendering_Detection_Identifying_and_Analyzing_unnecessary_UI_c/) - 平台相关，有PDF
- [H017 Path-Minimal Objects in ArkTS Symbolic Execution: From Path Constraints to TypeScript Tests](文献/H017_Path_Minimal_Objects_in_ArkTS_Symbolic_Execution_From_Path_Constraints/) - 强相关，无本地PDF
- [H019 HapCheck: DSL-Based Static Bug Detection Framework for OpenHarmony](文献/H019_HapCheck_DSL_Based_Static_Bug_Detection_Framework_for_OpenHarmony/) - 强相关，无本地PDF

### 生态治理与合规
- [H021 LiScopeLens: An Open-Source License Incompatibility Analysis Tool Based on Scope Representation of License Terms](文献/H021_LiScopeLens_An_Open_Source_License_Incompatibility_Analysis_Tool_Based/) - 强相关，无本地PDF
- [H022 Towards a comprehensive framework for verifying open-source software license compatibility](文献/H022_Towards_a_comprehensive_framework_for_verifying_open_source_software_l/) - 强相关，无本地PDF

### 生态移植与兼容
- [H023 CROSS2OH: Enabling Seamless Porting of C/C++ Software Libraries to OpenHarmony](文献/H023_CROSS2OH_Enabling_Seamless_Porting_of_C_C_Software_Libraries_to_OpenHa/) - 强相关，无本地PDF
- [H024 Porting Software Libraries to OpenHarmony: Transitioning from TypeScript or JavaScript to ArkTS](文献/H024_Porting_Software_Libraries_to_OpenHarmony_Transitioning_from_TypeScrip/) - 强相关，无本地PDF

### 系统与运行时优化
- [H001 How to Copy Memory? Coordinated Asynchronous Copy as a First-Class OS Service](文献/H001_How_to_Copy_Memory_Coordinated_Asynchronous_Copy_as_a_First_Class_OS_S/) - 平台相关，无本地PDF
- [H002 OS Rendering Service Made Parallel with Out-of-Order Execution and In-Order Commit](文献/H002_OS_Rendering_Service_Made_Parallel_with_Out_of_Order_Execution_and_In/) - 平台相关，有PDF
- [H025 D-VSync: Decoupled Rendering and Displaying for Smartphone Graphics](文献/H025_D_VSync_Decoupled_Rendering_and_Displaying_for_Smartphone_Graphics/) - 平台相关，无本地PDF

### 综述与路线图
- [H020 Software Engineering for OpenHarmony: A Research Roadmap](文献/H020_Software_Engineering_for_OpenHarmony_A_Research_Roadmap/) - 强相关，无本地PDF

### 通信与设备协同
- [H026 Toward Optimal Broadcast Mode in Offline Finding Network](文献/H026_Toward_Optimal_Broadcast_Mode_in_Offline_Finding_Network/) - 设备生态弱相关，无本地PDF
- [H027 Optimization of BLE Broadcast Mode in Offline Finding Network](文献/H027_Optimization_of_BLE_Broadcast_Mode_in_Offline_Finding_Network/) - 设备生态弱相关，有PDF
- [H028 CPBIS: Achieving Theoretical Minimum Discovery-latency in Offline Finding Network via Certain Proportion Broadcast Intervals Screening Mechanism](文献/H028_CPBIS_Achieving_Theoretical_Minimum_Discovery_latency_in_Offline_Findi/) - 设备生态弱相关，无本地PDF
- [H029 Unveiling SparkLink Low Energy: a Comparative Measurement Study](文献/H029_Unveiling_SparkLink_Low_Energy_a_Comparative_Measurement_Study/) - 设备生态弱相关，无本地PDF
