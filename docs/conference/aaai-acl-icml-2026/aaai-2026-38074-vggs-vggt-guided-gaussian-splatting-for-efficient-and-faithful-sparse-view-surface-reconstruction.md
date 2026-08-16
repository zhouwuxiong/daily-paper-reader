---
title: "VGGS: VGGT-guided Gaussian Splatting for Efficient and Faithful Sparse-View Surface Reconstruction"
title_zh: VGGS：VGGT引导的高斯泼溅高效忠实稀疏视角表面重建
authors: "Peng Xiang, Liang Han, Hui Zhang, Yu-Shen Liu, Zhizhong Han"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38074/42036"
tags: ["query:d-slam"]
score: 9.0
evidence: 利用VGGT多视角几何先验和高斯泼溅进行稀疏视角表面重建
tldr: 从稀疏图像重建忠实几何表面仍具挑战，尤其非重叠区域缺乏多视角线索。VGGS利用VGGT提供的多视角几何先验，提出锚点校准深度估计方案，将深度先验与底层表面对齐。基于高斯泼溅的方法在稀疏视角下实现了高效高保真表面重建。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 稀疏视角图像缺乏多视角几何线索，难以恢复准确的几何表面。
method: 提出锚点校准深度估计，将VGGT深度先验对齐到表面并用于高斯泼溅重建。
result: 在稀疏视角下实现高效高保真的表面重建。
conclusion: 多视角几何先验与锚点对齐可显著提升稀疏视角重建的保真度。
---

## Abstract
Reconstructing a faithful geometric surface from sparse images remains a fundamental challenge in 3D computer vision. While recent methods have achieved remarkable progress, they still struggle to recover reliable geometry due to the lack of multi-view geometric cues, particularly in non-overlapping regions. To address this issue, we introduce VGGS, a Gaussian Splatting (GS) method that exploits multi-view geometric priors from VGGT for efficient and high-fidelity sparse-view surface reconstruction. Our primary contribution is an anchor-calibrated depth estimation scheme, which yields accurate depth maps. The insight is to align the VGGT depth prior to the underlying surface with a sparse set of multi-view consistent anchors, then infer depth for unreliable regions by relative depth estimation. Furthermore, to mitigate misalignment in complex scenes, we propose a relative depth consistency loss that penalizes the rendered depth if its relative depth relationship in local regions is inconsistent to the multi-view prior. Extensive experiments on widely-used benchmarks show that VGGS surpasses state-of-the-art methods in both accuracy and efficiency, delivering 4–7× faster optimization while reducing memory consumption compared to previous GS-based approaches.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
利用VGGT多视角几何先验和高斯泼溅进行稀疏视角表面重建。

### 2. 核心内容
从稀疏图像重建忠实几何表面仍具挑战，尤其非重叠区域缺乏多视角线索。VGGS利用VGGT提供的多视角几何先验，提出锚点校准深度估计方案，将深度先验与底层表面对齐。基于高斯泼溅的方法在稀疏视角下实现了高效高保真表面重建。

### 3. 对应检索需求
3D reconstruction from images。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/38074](https://ojs.aaai.org/index.php/AAAI/article/view/38074)
