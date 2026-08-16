---
title: Cross-temporal 3D Gaussian Splatting for Sparse-view Guided Scene Update
title_zh: 跨时间三维高斯泼溅：稀疏视图引导的场景更新
authors: "Zeyuan An, Yanghang Xiao, Zhiying Leng, Frederick W. B. Li, Xiaohui Liang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37217/41179"
tags: ["query:d-slam"]
score: 9.0
evidence: 跨时间相机位姿估计与稀疏视图三维场景更新，结合定位与重建
tldr: 更新跨时间的3D场景常因缺乏密集扫描而困难。Cross-Temporal 3DGS 提出三阶段框架：先进行跨时间相机位姿对齐，再基于干扰的置信度识别变化区域，最后利用历史场景先验与稀疏图像高效更新三维高斯场景。该方法在稀疏观测下实现一致且可扩展的场景更新，适用于城市规划和历史遗迹保护等场景，并为长期三维重建维护提供了有效工具。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 跨时间场景更新需要从稀疏图像重建并保持一致性，现有方法难以处理变化区域。
method: 提出跨时间3DGS，包含跨时间相机对齐、基于干扰的置信度识别和先验引导更新三阶段。
result: 在稀疏视图下实现高质量的场景更新，保持时间一致性。
conclusion: 跨时间位姿对齐与置信度融合可有效支持长期场景维护与更新。
---

## Abstract
Maintaining consistent 3D scene representations over time is a significant challenge in computer vision. 
Updating 3D scenes from sparse-view observations is crucial for various real-world applications, including urban planning, disaster assessment, and historical site preservation, where dense scans are often unavailable or impractical. In this paper, we propose Cross-Temporal 3D Gaussian Splatting (Cross-Temporal 3DGS), a novel framework for efficiently reconstructing and updating 3D scenes across different time periods, using sparse images and previously captured scene priors. 
Our approach comprises three stages: 1) Cross-temporal camera alignment for estimating and aligning camera poses across different timestamps; 2) Interference-based confidence initialization to identify unchanged regions between timestamps, thereby guiding updates; and 3) Progressive cross-temporal optimization, which iteratively integrates historical prior information into the 3D scene to enhance reconstruction quality.
Our method supports non-continuous capture, enabling not only updates using new sparse views to refine existing scenes, but also recovering past scenes from limited data with the help of current captures. Furthermore, we demonstrate the potential of this approach to achieve temporal changes using only sparse images, which can later be reconstructed into detailed 3D representations as needed. Experimental results show significant improvements over baseline methods in reconstruction quality and data efficiency, making this approach a promising solution for scene versioning, cross-temporal digital twins, and long-term spatial documentation.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
跨时间相机位姿估计与稀疏视图三维场景更新，结合定位与重建。

### 2. 核心内容
更新跨时间的3D场景常因缺乏密集扫描而困难。Cross-Temporal 3DGS 提出三阶段框架：先进行跨时间相机位姿对齐，再基于干扰的置信度识别变化区域，最后利用历史场景先验与稀疏图像高效更新三维高斯场景。该方法在稀疏观测下实现一致且可扩展的场景更新，适用于城市规划和历史遗迹保护等场景，并为长期三维重建维护提供了有效工具。

### 3. 对应检索需求
recent progress in simultaneous localization and mapping with 3D scene reconstruction。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/37217](https://ojs.aaai.org/index.php/AAAI/article/view/37217)
