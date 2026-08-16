---
title: "GUSLO: General and Unified Structured Light Optimization"
title_zh: GUSLO：通用统一结构光优化
authors: "Tinglei Wan, Zhongjie Wang, Tonghua Su"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37925/41887"
tags: ["query:d-slam"]
score: 8.0
evidence: 基于图像的结构光三维重建与统一优化
tldr: 针对结构光三维重建依赖场景标定且难以推广到不同条纹模式的问题，提出通用统一结构光优化框架GUSLO。其通过基于二维三角化的插值实现单次标定，将稀疏匹配转换为稠密对应场，并引入顾及伪影的光度自适应，从而提高重建精度与泛化能力。该方法可服务于工业检测和文化遗产数字化等需要高精度三维数据的场景。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有结构光三维重建方法依赖场景特定标定与人工参数调整，且优化框架仅适用于特定条纹模式，泛化性差。
method: 提出GUSLO统一优化框架，结合基于二维三角化插值的单次标定和顾及伪影的光度自适应，实现稀疏到稠密的对应关系估计。
result: 在多种结构光场景下获得高精度三维重建，减少人工标定并提升跨模式泛化能力。
conclusion: 统一的结构光优化显著提高三维重建的通用性与精度，适用于工业检测和文化遗产数字化。
---

## Abstract
Structured light (SL) 3D reconstruction captures the precise surface shape of objects, providing high-accuracy 3D data essential for industrial inspection and cultural heritage digitization. However, existing methods suffer from two key limitations: reliance on scene-specific calibration with manual parameter tuning, and optimization frameworks tailored to specific SL patterns, limiting their generalizability across varied scenarios. We propose General and Unified Structured Light Optimization (GUSLO), a novel framework addressing these issues through two coordinated innovations: (1) single-shot calibration via 2D triangulation-based interpolation that converts sparse matches into dense correspondence fields, and (2) artifact-aware photometric adaptation via explicit transfer functions, balancing generalization and color fidelity. We conduct diverse experiments covering binary, speckle, and color-coded settings. Results show that GUSLO consistently improves accuracy and cross-encoding robustness over conventional methods in challenging industrial and cultural scenarios.

---

## 论文详细总结（自动生成）

# GUSLO 论文总结

## 1. 核心问题与整体含义

- **研究动机**：结构光（Structured Light, SL）三维重建能够获取物体高精度表面形状，对工业检测和文化遗产数字化至关重要。然而，现有方法存在两大关键局限：
  1. **依赖场景特定标定**：需要针对具体场景进行标定并人工调节参数，耗时且繁琐；
  2. **优化框架缺乏通用性**：已有优化方法往往针对特定条纹模式（如相移、散斑等）设计，难以在不同编码模式下泛化。
- **核心问题**：如何构建一个无需场景特定标定、且能跨编码模式统一工作的结构光优化框架？
- **整体意义**：提出统一的结构光优化方法，有望降低人工成本、提升重建精度与泛化能力，从而促进结构光技术在多样实际场景中的落地。

## 2. 方法论

- **核心思想**：提出 GUSLO（通用统一结构光优化）框架，通过两个协调的创新设计解决上述问题。
- **创新点 1：单次标定（Single-shot Calibration）**
  - 采用**基于二维三角化（2D triangulation）的插值**方法；
  - 将稀疏匹配点转换为**稠密对应场**，从而避免逐场景的重复标定与参数调整；
  - 通过一次标定即可适应多个场景，提高效率。
- **创新点 2：伪影感知的光度自适应（Artifact-aware Photometric Adaptation）**
  - 引入**显式传递函数（explicit transfer functions）**；
  - 在颜色保真与泛化能力之间取得平衡；
  - 能够应对光照、反射等引起的伪影，增强鲁棒性。
- **算法流程（基于描述推断）**：
  1. 对结构光图像进行稀疏对应匹配；
  2. 利用二维三角化插值将稀疏对应扩展为稠密对应场；
  3. 通过光度自适应传递函数校正像素强度，抑制伪影；
  4. 基于稠密对应场完成三维重建与优化。
- **说明**：论文摘要未提供具体数学公式或网络结构细节，以上为文字性概括。

## 3. 实验设计

- **覆盖的实验设置**：摘要明确提到实验涵盖三大类编码模式：
  - 二进制（binary）模式；
  - 散斑（speckle）模式；
  - 彩色编码（color-coded）模式。
- **应用场景**：具有挑战性的工业场景和文化遗产数字化场景。
- **Benchmark**：摘要中未给出具体公开数据集名称或基准测试集，也未说明是否与其他统一框架（如有）对比。
- **对比方法**：仅提到“常规方法（conventional methods）”，未列出具体基线方法名称。
- **评估指标**：主要关注重建精度和跨编码鲁棒性，但未给出具体量化数值。

## 4. 资源与算力

- 论文提供的材料（摘要和元数据）**未提及任何算力信息**，包括：
  - GPU 型号与数量；
  - 训练/推理时长；
  - 内存占用或计算复杂度。
- 因此无法评估其计算成本与部署可行性。

## 5. 实验数量与充分性

- **实验数量**：只有定性描述“多组实验”，未给出具体实验次数或表格数量。
- **覆盖广度**：包含三种常见编码模式，在跨模式泛化验证上具有一定代表性。
- **可能存在的不足**：
  - 缺乏消融实验描述（如单独验证两个创新点的贡献）；
  - 缺乏与更多现有方法的定量比较；
  - 未报告具体误差指标（如RMSE、点云精度等）；
  - 未说明实验重复次数和统计显著性。
- **总体评价**：基于现有信息，实验设计思路清晰，但**充分性和客观性难以评判**，因为缺少可复现细节和严谨的对比分析。

## 6. 主要结论与发现

- GUSLO 在二进制、散斑和彩色编码三种结构光场景下均能持续提升重建精度；
- 相比常规方法，GUSLO 具有更好的**跨编码鲁棒性**；
- 统一优化框架能够有效减少对场景特定标定和人工调参的依赖；
- 适用于工业检测和文化遗产数字化等高精度需求场景。

## 7. 优点

- **通用性强**：统一框架覆盖多种编码模式，突破传统方法“一模式一框架”的局限。
- **标定高效**：单次标定配合二维三角化插值，省去重复标定工作，实用价值高。
- **光度自适应设计**：显式传递函数兼顾颜色保真与伪影抑制，是一种新颖的平衡方案。
- **应用前景明确**：针对工业和文化遗产真实需求，落地导向明确。

## 8. 不足与局限

- **信息透明度不足**：未提供具体数据集、定量结果和基线明细，难以独立复现和验证。
- **模式覆盖有限**：虽然测试了三种模式，但未涵盖相移（phase-shifting）、格雷码等常见结构光策略，泛化结论可能过于乐观。
- **标定方法依赖二维插值**：对于复杂拓扑或深度突变场景，基于三角化插值的稠密化可能引入错误对应。
- **未分析计算成本**：统一优化框架可能带来更高计算负担，论文未讨论实时性。
- **缺乏失败案例分析**：未说明在何种情况下性能下降，存在偏差风险。
- **应用限制**：光度自适应可能对极端光照或高反光表面敏感，实际工业环境中的鲁棒性有待进一步验证。

---

**说明**：以上总结基于论文摘要及元数据，部分细节（如公式、数据集、算力）原文未提供，已明确指出。

（完）
