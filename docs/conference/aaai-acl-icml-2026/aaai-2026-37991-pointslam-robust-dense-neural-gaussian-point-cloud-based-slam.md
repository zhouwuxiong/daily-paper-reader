---
title: "PointSLAM++: Robust Dense Neural Gaussian Point Cloud-based SLAM"
title_zh: PointSLAM++：基于神经高斯点云的鲁棒稠密SLAM
authors: "Xu Wang, Boyao Han, Xiaojun Chen, Ying Liu, Ruihui Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37991/41953"
tags: ["query:d-slam"]
score: 10.0
evidence: 基于RGB-D的视觉SLAM，神经高斯点云稠密重建与稳健位姿估计
tldr: 现有SLAM在深度噪声下难以保持结构一致性与位姿鲁棒性。为此提出PointSLAM++，一种RGB-D SLAM系统，采用分层约束的神经高斯表示生成场景地图，并通过渐进式位姿优化抑制深度传感器噪声，显著提升定位精度。进一步利用动态神经表示图根据局部几何复杂度调整高斯节点分布，实现更一致的稠密三维重建。实时稠密重建对机器人和增强现实应用具有重要价值。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 实时SLAM在深度噪声下难以同时保证场景结构一致和位姿估计鲁棒，影响机器人及AR应用。
method: 提出PointSLAM++，用分层约束神经高斯点云表达场景，结合渐进式位姿优化和基于几何复杂度的动态神经表示图。
result: 在RGB-D数据集上显著提升定位精度和稠密重建结构一致性，优于现有SLAM方法。
conclusion: 通过结构感知的神经高斯表示和鲁棒位姿优化，实现高质量实时稠密重建SLAM。
---

## Abstract
Real-time 3D reconstruction is crucial for robotics and augmented reality, yet current simultaneous localization and mapping(SLAM) approaches often struggle to maintain structural consistency and robust pose estimation in the presence of depth noise. This work introduces PointSLAM++, a novel RGB-D SLAM system that leverages a hierarchically constrained neural Gaussian representation to preserve structural relationships while generating Gaussian primitives for scene mapping. It also employs progressive pose optimization to mitigate depth sensor noise, significantly enhancing localization accuracy. Furthermore, it utilizes a dynamic neural representation graph that adjusts the distribution of Gaussian nodes based on local geometric complexity, enabling the map to adapt to intricate scene details in real time. This combination yields high-precision 3D mapping and photorealistic scene rendering. Experimental results show PointSLAM++ outperforms existing 3DGS-based SLAM methods in reconstruction accuracy and rendering quality, demonstrating its advantages for large-scale AR and robotics.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于RGB-D的视觉SLAM，神经高斯点云稠密重建与稳健位姿估计。

### 2. 核心内容
现有SLAM在深度噪声下难以保持结构一致性与位姿鲁棒性。为此提出PointSLAM++，一种RGB-D SLAM系统，采用分层约束的神经高斯表示生成场景地图，并通过渐进式位姿优化抑制深度传感器噪声，显著提升定位精度。进一步利用动态神经表示图根据局部几何复杂度调整高斯节点分布，实现更一致的稠密三维重建。实时稠密重建对机器人和增强现实应用具有重要价值。

### 3. 对应检索需求
visual simultaneous localization and mapping。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/37991](https://ojs.aaai.org/index.php/AAAI/article/view/37991)
