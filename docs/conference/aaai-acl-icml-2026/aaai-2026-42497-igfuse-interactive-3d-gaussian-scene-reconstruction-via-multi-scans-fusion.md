---
title: "IGFuse: Interactive 3D Gaussian Scene Reconstruction via Multi-Scans Fusion"
title_zh: IGFuse：基于多扫描融合的交互式三维高斯场景重建
authors: "Wenhao Hu, Zesheng Li, Haonan Zhou, Liu Liu, Xuexiang Wen, Zhizhong Su, Xi Li, Gaoang Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/42497/46458"
tags: ["query:d-slam"]
score: 8.0
evidence: 融合多次扫描观测重建交互式三维场景以处理遮挡
tldr: 单次多视角扫描难以恢复被遮挡的完整三维结构，现有方法依赖分割、背景补全等多阶段流程且易错。IGFuse 提出融合多次扫描的交互式高斯场景重建框架，利用两次捕获之间物体自然移动暴露被遮挡区域，以分割引导的方式融合观测。该方法可生成更完整、可交互的三维场景，减少了多阶段流水线的误差，为复杂场景重建提供了高效方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 单次扫描存在遮挡和覆盖不足，需融合多次扫描以重建完整交互式三维场景。
method: 提出IGFuse，利用物体在多次捕获间的自然重新排列暴露被遮挡区域，构建分割感知高斯融合表示。
result: 在复杂场景中生成更完整的交互式三维重建，避免多阶段流程的误差积累。
conclusion: 多扫描自然重排有效提升三维重建完整性，为交互场景重建提供新思路。
---

## Abstract
Reconstructing complete and interactive 3D scenes remains a fundamental challenge in computer vision and robotics, particularly due to persistent object occlusions and limited sensor coverage. Even multi-view observations from a single scene scan often fail to capture the full structural details. Existing approaches typically rely on multi-stage pipelines—such as segmentation, background completion, and inpainting—or require per-object dense scanning, both of which are error-prone, and not easily scalable. We propose IGFuse, a novel framework that reconstructs interactive Gaussian scene by fusing observations from multiple scans, where natural object rearrangement between captures reveal previously occluded regions. Our method constructs segmentation-aware Gaussian fields and enforces bi-directional photometric and semantic consistency across scans. To handle spatial misalignments, we introduce a pseudo-intermediate scene state for symmetric alignment, alongside collaborative co-pruning strategies to refine geometry. IGFuse enables high-fidelity rendering and object-level scene manipulation without dense observations or complex pipelines. Extensive experiments validate the framework’s strong generalization to novel  scene configurations, demonstrating its effectiveness for real-world 3D reconstruction and real-to-simulation transfer.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
融合多次扫描观测重建交互式三维场景以处理遮挡。

### 2. 核心内容
单次多视角扫描难以恢复被遮挡的完整三维结构，现有方法依赖分割、背景补全等多阶段流程且易错。IGFuse 提出融合多次扫描的交互式高斯场景重建框架，利用两次捕获之间物体自然移动暴露被遮挡区域，以分割引导的方式融合观测。该方法可生成更完整、可交互的三维场景，减少了多阶段流水线的误差，为复杂场景重建提供了高效方案。

### 3. 对应检索需求
3D reconstruction from images。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/42497](https://ojs.aaai.org/index.php/AAAI/article/view/42497)
