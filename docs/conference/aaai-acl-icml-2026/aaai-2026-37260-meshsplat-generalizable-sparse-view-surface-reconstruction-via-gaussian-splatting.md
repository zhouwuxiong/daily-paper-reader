---
title: "MeshSplat: Generalizable Sparse-View Surface Reconstruction via Gaussian Splatting"
title_zh: MeshSplat：通过高斯泼溅实现可泛化的稀疏视角表面重建
authors: "Hanzhi Chang, Ruijie Zhu, Wenjie Chang, Mulin Yu, Yanzhe Liang, Jiahao Lu, Zhuoyuan Li, Tianzhu Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37260/41222"
tags: ["query:d-slam"]
score: 9.0
evidence: 基于高斯泼溅的稀疏视角图像表面重建
tldr: 现有表面重建在输入视角极为稀疏时难以恢复准确几何。MeshSplat借助2DGS连接新视图合成与学习到的几何先验，通过前馈网络预测逐视角像素对齐的2DGS，无需直接3D监督即可将先验迁移到表面重建。实验表明该方法能在稀疏视角下生成可靠的场景几何，为可泛化的表面重建提供有效框架。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 输入视角极端稀疏时，现有表面重建难以恢复准确的场景几何。
method: 以前馈网络预测逐视角像素对齐的2DGS，借助新视图合成迁移几何先验到表面重建。
result: 在稀疏视角设置下恢复出准确可靠的表面几何。
conclusion: 将2DGS作为桥梁可避免直接3D监督，提升稀疏视角重建的泛化性。
---

## Abstract
Surface reconstruction has been widely studied in computer vision and graphics. However, existing surface reconstruction works struggle to recover accurate scene geometry when the input views are extremely sparse. To address this issue, we propose MeshSplat, a generalizable sparse-view surface reconstruction framework via Gaussian Splatting. Our key idea is to leverage 2DGS as a bridge, which connects novel view synthesis to learned geometric priors and then transfers these priors to achieve surface reconstruction. Specifically, we incorporate a feed-forward network to predict per-view pixel-aligned 2DGS, which enables the network to synthesize novel view images and thus eliminates the need for direct 3D ground-truth supervision. To improve the accuracy of 2DGS position and orientation prediction, we propose a Weighted Chamfer Distance Loss to regularize the depth maps, especially in overlapping areas of input views, and also a normal prediction network to align the orientation of 2DGS with normal vectors predicted by a monocular normal estimator. Extensive experiments validate the effectiveness of our proposed improvement, demonstrating that our method achieves state-of-the-art performance in generalizable sparse-view mesh reconstruction tasks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于高斯泼溅的稀疏视角图像表面重建。

### 2. 核心内容
现有表面重建在输入视角极为稀疏时难以恢复准确几何。MeshSplat借助2DGS连接新视图合成与学习到的几何先验，通过前馈网络预测逐视角像素对齐的2DGS，无需直接3D监督即可将先验迁移到表面重建。实验表明该方法能在稀疏视角下生成可靠的场景几何，为可泛化的表面重建提供有效框架。

### 3. 对应检索需求
3D reconstruction from images。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/37260](https://ojs.aaai.org/index.php/AAAI/article/view/37260)
