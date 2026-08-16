---
title: "Rh-3DGS: Robust Open-Vocabulary Scene Understanding via Riemannian Huber Distillation and Manifold-Aware Sampling"
title_zh: Rh-3DGS：基于黎曼Huber蒸馏与流形感知采样的鲁棒开放词汇场景理解
authors: "Xinpeng Zhao, Jiang Jie, Fengyuan Zhang, Lixin Zhan, Dong Wang, Qinyuan Bu, Jiahang Tu, Guangzhen Yao"
date: 2026-04-30
pdf: "https://openreview.net/pdf/8310d4c5a6346eaadb420914138e1711121a0ff8.pdf"
tags: ["query:d-slam"]
score: 4.0
evidence: 对重建的三维高斯场景进行开放词汇语义理解，并非重建本身
tldr: 开放词汇三维场景理解要求对重建场景进行文本查询，但现有方法在欧氏空间平均嵌入易导致特征坍缩，且等权蒸馏各视角会放大遮挡噪声。Rh-3DGS 提出基于黎曼Huber蒸馏和流形感知采样的框架，以可见性校准权重进行可靠性感知蒸馏和流形一致聚合。该方法提升了三维高斯场景语义理解的鲁棒性，但属于场景理解而非三维重建方法。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 三维高斯场景的开放词汇理解面临欧氏平均导致的特征坍缩和视角等权蒸馏的噪声问题。
method: 提出Rh-3DGS，利用可见性校准蒸馏计算逐像素可靠性，并进行流形一致聚合。
result: 在开放词汇三维理解任务上提升鲁棒性，减少遮挡噪声和特征退化。
conclusion: 可靠性感知蒸馏与流形几何建模可有效提升语义三维高斯的表达质量。
---

## Abstract
Open-vocabulary 3D scene understanding answers free-form text queries over reconstructed scenes. However, lifting dense 2D foundation-model embeddings into 3D Gaussian Splatting (3DGS) is still challenging. Existing 3DGS-based methods often average normalized embeddings in Euclidean space. This ignores their hyperspherical geometry and can cause feature collapse. They also distill supervision from all views equally, which amplifies occlusion noise and mixed-depth artifacts. We propose **Rh-3DGS**, a robust semantic 3DGS framework that uses reliability-aware distillation and manifold-consistent aggregation. **Visibility-Calibrated Distillation (VCD)** computes per-pixel reliability weights from rasterization statistics and down-weights ambiguous pixels. **Visibility-Weighted Fréchet Mean (VFM)** aggregates embeddings on the unit hypersphere with a Riemannian Huber objective for robust distillation. **Lightweight Consistency Contrast (LIC)** regularizes the 3D semantic field with neighborhood-based multi-positive contrast to improve local consistency and sharper boundaries. Experiments on three benchmarks show that Rh-3DGS is best on open-vocabulary segmentation, boundary quality, and view-consistent rendering.

---

## 论文详细总结（自动生成）

# Rh-3DGS 论文总结

## 1. 核心问题与整体含义（研究动机和背景）

开放词汇三维场景理解（Open-vocabulary 3D scene understanding）旨在针对已重建的三维场景执行自由形式的文本查询，是实现通用三维语义感知的关键能力。论文指出，将稠密的 2D 基础模型嵌入特征提升（lift）到三维高斯泼溅（3DGS）表示中仍存在两大问题：

- **特征坍缩（Feature Collapse）**：现有方法通常在欧氏空间中对归一化嵌入进行平均，忽略了嵌入本身所在的超球面几何结构，导致语义特征退化、类间区分度下降。
- **遮挡与混合深度噪声被放大**：现有方法对所有视角的监督信号等权蒸馏，导致被遮挡、深度不连续区域的错误特征被过度强调，影响最终三维语义场的质量。

因此，论文的核心研究动机是：如何利用黎曼几何与可靠性感知机制，在三维高斯场景中构建更鲁棒、更一致的开放词汇语义表示。

## 2. 方法论：核心思想、关键技术细节与算法流程

论文提出 **Rh-3DGS**，一个鲁棒的语义 3DGS 框架，核心思想是“可靠性感知的蒸馏”和“流形一致的聚合”。主要包含三个关键技术模块：

- **可见性校准蒸馏（Visibility-Calibrated Distillation, VCD）**
  - 从高斯栅格化统计中计算每个像素的可靠性权重；对遮挡、深度混合等模糊像素赋予较低权重，从而在下游蒸馏中削弱其噪声影响。
  - 实现“可靠性感知蒸馏”，避免等权蒸馏带来的噪声放大。

- **可见性加权 Fréchet 均值（Visibility-Weighted Fréchet Mean, VFM）**
  - 在单位超球面上聚合各视角嵌入，而不是在欧氏空间直接平均；
  - 使用黎曼 Huber 目标函数进行鲁棒聚合，降低异常嵌入对语义均值的影响；
  - 通过可见性权重进一步调整聚合方向，使遮挡像素不主导最终嵌入。

- **轻量一致性对比（Lightweight Consistency Contrast, LIC）**
  - 基于邻域的多正样本对比学习正则化三维语义场；
  - 提高局部特征一致性，并保持更锐利的语义边界；
  - 设计为轻量模块，避免过高计算开销。

整体算法流程可概括为：先训练/重建三维高斯场景，然后利用 VCD 计算逐像素可靠性，接着在超球面上用 VFM 聚合多视角嵌入，最后用 LIC 对语义场进行正则化，从而得到可查询的、具有开放词汇语义能力的三维高斯表示。

## 3. 实验设计

- **数据集/场景**：论文在三个基准（three benchmarks）上评估 Rh-3DGS。
- **评测任务**：主要覆盖三类指标——
  - 开放词汇分割（open-vocabulary segmentation）；
  - 边界质量（boundary quality）；
  - 视图一致性渲染（view-consistent rendering）。
- **对比方法**：摘要未列出具体对比方法名称，但暗示与现有的 3DGS 语义理解方法（尤其是欧氏平均嵌入、等权蒸馏类方法）进行对比，并声称 Rh-3DGS 在以上三个任务上均达到最优。

## 4. 资源与算力

论文摘要与元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力资源。因此，无法从给定内容中判断其计算开销是否可控。不过从方法设计上看，LIC 被描述为“轻量（Lightweight）”模块，暗示其在效率方面有一定考虑，但缺乏具体实验数据支撑。

## 5. 实验数量与充分性

- 摘要提到在“三个基准”上进行了实验，覆盖分割、边界质量、视图一致渲染三类评估，说明实验具有一定广度。
- 但**没有给出详细的消融实验信息**，也未列出具体数值或与基线方法的量化对比表。
- 由于论文完整实验细节在提供的文本中并未展开，无法判断所有消融是否完备。从方法论结构来看，VCD、VFM、LIC 三者理论上应分别做消融验证，但当前摘要无法确认。
- 整体而言，实验设计方向合理、任务覆盖较全面，但给定信息不足以完全评估其客观性与公平性。

## 6. 主要结论与发现

- 在欧氏空间直接平均归一化嵌入会破坏超球面几何，是导致特征坍缩的重要原因；基于黎曼几何的聚合能改善语义表达。
- 等权蒸馏所有视角会放大遮挡和深度混合噪声；通过可见性校准的逐像素可靠性权重，可以显著降低此类干扰。
- 将“黎曼 Huber 鲁棒聚合”与“邻域对比正则化”结合，能够同时提升语义分割精度、边界清晰度和视图一致性渲染质量。
- 总而言之，可靠性感知蒸馏与流形建模是提升语义三维高斯表达质量的有效途径。

## 7. 优点

- **几何建模更合理**：将 CLIP 等模型嵌入视为超球面数据，并采用 Fréchet 均值，符合数据的流形结构，理论动机清晰。
- **鲁棒性设计完整**：从像素级可靠性（VCD）、聚合级鲁棒性（VFM）到局部一致性（LIC），形成“降噪—聚合—正则化”的完整链路。
- **针对实际痛点**：直接解决遮挡、深度不连续导致的语义伪影，有较强实际应用价值。
- **多任务评估**：不仅评估分割精度，还关注边界质量和视图一致性，评估维度较全面。
- **方法命名与描述清楚**：三个模块分工明确，便于复现和扩展。

## 8. 不足与局限

- **算力信息缺失**：未报告训练时间、GPU 配置，难以评估方法的实际部署成本。
- **实验细节不足**：缺少具体数值结果、消融实验表格和与基线方法的统计显著性分析。
- **对比方法不明确**：摘要未列出具体的 baseline，无法判断对比是否充分、公平。
- **场景范围有限**：仅在三个基准上评测，缺乏对大规模室内外场景、开放词汇类别多样性、长尾对象等更复杂条件的验证。
- **依赖 2D 基础模型嵌入质量**：方法的性能上限受限于 CLIP 等基础模型对开放词汇、细粒度语义的判别能力，若下游嵌入本身存在偏差，三维聚合也难以完全消除。
- **存在偏置风险**：可见性权重和邻域对比可能过度平滑细小物体或弱监督区域，需要更多边界案例实验来验证。

（完）
