---
title: "FoundationSLAM: Unleashing the Power of Depth Foundation Models for End-to-End Dense Visual SLAM"
title_zh: FoundationSLAM：利用深度基础模型实现端到端稠密视觉SLAM
authors: "Yuchen Wu, Jiahe Li, Fabio Tosi, Matteo Poggi, Jin Zheng, Xiao Bai"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38061/42023"
tags: ["query:d-slam"]
score: 10.0
evidence: 基于学习的单目稠密视觉SLAM，实现鲁棒跟踪与建图
tldr: 基于光流的稠密SLAM常缺少几何一致性。FoundationSLAM引入深度基础模型引导混合光流网络，生成几何感知的对应关系并联合估计深度与位姿；通过双一致束调整层与可靠性感知细化机制增强多视角全局一致性。在单目稠密跟踪与建图任务上展现出准确鲁棒的结果，为端到端稠密视觉SLAM提供了新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有基于光流的稠密SLAM缺乏几何一致性，跟踪和建图不够准确鲁棒。
method: 提出混合光流网络与双一致束调整层，结合深度基础模型引导实现位姿深度联合优化。
result: 在单目稠密SLAM基准上实现了准确鲁棒的跟踪与建图，验证了几何一致性提升。
conclusion: 利用基础深度模型先验桥接光流与几何推理，提升稠密SLAM的全局一致性。
---

## Abstract
We present FoundationSLAM, a learning-based monocular dense SLAM system that addresses the absence of geometric consistency in previous flow-based approaches for accurate and robust tracking and mapping.
Our core idea is to bridge flow estimation with geometric reasoning by leveraging the guidance from foundation depth models. 
To this end, we first develop a Hybrid Flow Network that produces geometry-aware correspondences, enabling consistent depth and pose inference across diverse keyframes. 
To enforce global consistency, we propose a Bi-Consistent Bundle Adjustment Layer that jointly optimizes keyframe pose and depth under multi-view constraints. Furthermore, we introduce a Reliability-Aware Refinement mechanism that dynamically adapts the flow update process by distinguishing between reliable and uncertain regions, forming a closed feedback loop between matching and optimization.
Extensive experiments demonstrate that FoundationSLAM achieves superior trajectory accuracy and dense reconstruction quality across multiple challenging datasets, while running in real-time at 18 FPS, demonstrating strong generalization to various scenarios and practical applicability of our method.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于学习的单目稠密视觉SLAM，实现鲁棒跟踪与建图。

### 2. 核心内容
基于光流的稠密SLAM常缺少几何一致性。FoundationSLAM引入深度基础模型引导混合光流网络，生成几何感知的对应关系并联合估计深度与位姿；通过双一致束调整层与可靠性感知细化机制增强多视角全局一致性。在单目稠密跟踪与建图任务上展现出准确鲁棒的结果，为端到端稠密视觉SLAM提供了新思路。

### 3. 对应检索需求
visual simultaneous localization and mapping。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/38061](https://ojs.aaai.org/index.php/AAAI/article/view/38061)
