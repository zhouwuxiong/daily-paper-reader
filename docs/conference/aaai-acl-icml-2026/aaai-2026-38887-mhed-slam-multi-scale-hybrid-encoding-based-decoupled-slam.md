---
title: "MHED-SLAM: Multi-Scale Hybrid Encoding-Based Decoupled SLAM"
title_zh: MHED-SLAM：基于多尺度混合编码的解耦SLAM
authors: "Dengfang Feng, Wenyang Qin, Zhongchen Shi, Wei Chen, Yanhui Duan, Liang Xie, Erwei Yin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38887/42849"
tags: ["query:d-slam"]
score: 9.0
evidence: 基于NeRF的视觉SLAM，多尺度混合编码提升几何建模与跟踪精度
tldr: 针对NeRF类视觉SLAM中哈希编码碰撞导致伪影以及室内多视角颜色不一致引发形状-辐射模糊的问题，提出MHED-SLAM。该方法采用多尺度混合编码减少可学习参数并抑制伪影，同时将几何与跟踪优化解耦，提升场景几何建模质量和相机跟踪精度。实验表明其在室内场景重建与定位上优于现有方法，为视觉SLAM提供更稳健的神经表示方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: NeRF视觉SLAM常受哈希碰撞伪影和室内多视颜色不一致造成的形状-辐射模糊影响，几何质量与跟踪精度下降。
method: 提出多尺度混合编码的MHED-SLAM，通过混合编码降低参数、缓解哈希碰撞，并采用解耦优化提升几何与跟踪。
result: 在室内场景重建与跟踪任务上获得更优几何质量和定位精度，优于已有神经SLAM方法。
conclusion: 多尺度混合编码与解耦策略有效增强视觉SLAM的稳健性和重建精度。
---

## Abstract
Neural Radiance Fields (NeRF)-based Visual Simultaneous Localization and Mapping (SLAM) achieve superior scene geometric modeling and robust camera tracking by leveraging neural representations. 
Existing methods typically relied on multi-resolution hash encoding with truncated signed distance fields (TSDF) to achieve high frame rates. However, unavoidable hash collisions can lead to artifacts, and multi-view color inconsistencies in indoor scenes can result in shape-radiance ambiguity,  adversely affecting geometric quality and tracking accuracy.
To address these issues, we propose a novel Multi-scale Hybrid Encoding-based Decoupled SLAM (MHED-SLAM). 
First, to mitigate the adverse effects of hash collisions and reduce the number of learnable parameters, we innovatively fuse a coarse-scale hash tri-plane with a fine-scale hash grid within a single latent volume. 
Second, to enable precise geometric reconstruction and camera tracking, we decouple the reconstruction and rendering processes, independently learning a TSDF field for reconstruction and a density field for rendering.
Third, we devise a Symmetric Kullback-Leibler (SKL) strategy based on ray termination distributions to align the probability distributions derived from the TSDF and density fields for their synchronous convergence. 
Extensive experimental evaluations demonstrate that our approach surpasses the state-of-the-art (SOTA) methods by utilizing a faster frame rate of 20 Hz and fewer parameters, while achieving higher tracking and reconstruction accuracy.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于NeRF的视觉SLAM，多尺度混合编码提升几何建模与跟踪精度。

### 2. 核心内容
针对NeRF类视觉SLAM中哈希编码碰撞导致伪影以及室内多视角颜色不一致引发形状-辐射模糊的问题，提出MHED-SLAM。该方法采用多尺度混合编码减少可学习参数并抑制伪影，同时将几何与跟踪优化解耦，提升场景几何建模质量和相机跟踪精度。实验表明其在室内场景重建与定位上优于现有方法，为视觉SLAM提供更稳健的神经表示方案。

### 3. 对应检索需求
visual simultaneous localization and mapping。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/38887](https://ojs.aaai.org/index.php/AAAI/article/view/38887)
