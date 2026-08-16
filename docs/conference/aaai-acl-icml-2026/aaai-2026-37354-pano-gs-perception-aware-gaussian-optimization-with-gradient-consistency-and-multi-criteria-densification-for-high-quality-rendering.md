---
title: "Pano-GS: Perception-Aware Gaussian Optimization with Gradient Consistency and Multi-Criteria Densification for High-Quality Rendering"
title_zh: Pano-GS：面向高质量渲染的感知感知高斯优化（梯度一致性与多准则致密化）
authors: "Yang Deng, Zhanke Wang, Jiahao Wu, Jie Liang, Jingui Ma, Yang Hu, Ronggang Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37354/41316"
tags: ["query:d-slam"]
score: 8.0
evidence: 基于感知感知的高斯优化从多视图图像进行三维场景重建与渲染
tldr: 针对3D高斯泼溅重建中像素级L1损失与人类感知不一致、以及仅基于位置梯度的致密化导致高频细节缺失和伪影的问题，提出Pano-GS。该方法引入梯度一致性约束损失对齐感知，并设计多准则致密化策略补充高斯原语，从而提升多视图图像三维重建的渲染质量。实验验证其生成更丰富细节并减少伪影，改善高保真3D场景重建。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 多视图三维重建中现有3D高斯泼溅依赖像素级L1损失，与人类感知不一致，且致密化不充分导致高频细节缺失。
method: 提出感知感知的高斯优化框架，引入梯度一致性约束损失和多准则致密化策略。
result: 相比基线方法，重建渲染质量更高、伪影更少、高频细节更丰富。
conclusion: 感知感知优化显著提升3D高斯泼溅重建质量，适用于高保真场景渲染。
---

## Abstract
Reconstructing 3D scenes from multi-view image sequences remains a significant challenge in practical applications. While recent advances in 3D Gaussian Splatting have enabled high-quality rendering, existing methods rely heavily on pixel-level L1 loss, which misaligns with human perception, leading to a lack of high-frequency details and the emergence of artifacts. Additionally, the position gradient-based densification strategy often results in under-densified Gaussian primitives, thereby degrading rendering quality. To address these challenges, we propose Pano-GS, a perception-aware Gaussian optimization framework. Specifically, we introduce a gradient consistency-constrained loss to capture high-frequency details, mitigating the inherent shortcomings of traditional L1 loss and enhancing reconstruction fidelity. In addition, we use a multi-criteria densification strategy to reduce the sole reliance on average position gradients. Extensive experiments demonstrate that Pano-GS achieves state-of-the-art performance, confirming its effectiveness and robust generalization across diverse real-world scenes.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于感知感知的高斯优化从多视图图像进行三维场景重建与渲染。

### 2. 核心内容
针对3D高斯泼溅重建中像素级L1损失与人类感知不一致、以及仅基于位置梯度的致密化导致高频细节缺失和伪影的问题，提出Pano-GS。该方法引入梯度一致性约束损失对齐感知，并设计多准则致密化策略补充高斯原语，从而提升多视图图像三维重建的渲染质量。实验验证其生成更丰富细节并减少伪影，改善高保真3D场景重建。

### 3. 对应检索需求
3D reconstruction from images。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/37354](https://ojs.aaai.org/index.php/AAAI/article/view/37354)
