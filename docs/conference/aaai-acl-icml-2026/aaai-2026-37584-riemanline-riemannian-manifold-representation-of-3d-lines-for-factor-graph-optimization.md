---
title: "RiemanLine: Riemannian Manifold Representation of 3D Lines for Factor Graph Optimization"
title_zh: RiemanLine：用于因子图优化的3D直线黎曼流形表示
authors: "Yan Li, Ze Yang, Keisuke Tateno, Federico Tombari, Liang Zhao, Gim Hee Lee"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37584/41546"
tags: ["query:d-slam"]
score: 8.0
evidence: 通过紧凑3D直线表示支持相机定位与结构建图，适用于SLAM式因子图优化
tldr: 现有3D直线表示大多独立处理直线，忽略环境中大量存在的平行线结构。RiemanLine提出一种基于黎曼流形的统一最小表示，将直线地标分解为共享消隐方向和正交子空间上的缩放法向量，可同时表达单条直线与平行线组。该方法为因子图优化提供紧凑参数化，可提升相机定位与结构建图的效率。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有3D直线参数化未利用平行线等结构规律，导致定位与建图的表达不够紧凑。
method: 提出基于黎曼流形的最小3D直线表示，将直线解耦为全局消隐方向与局部缩放法向量。
result: 在相机定位与结构建图相关优化中实现了更紧凑有效的直线参数化。
conclusion: 统一表达单条直线与平行线组，提升因子图优化的鲁棒性与表达效率。
---

## Abstract
Minimal parametrization of 3D lines plays a critical role in camera localization and structural mapping. Existing representations in robotics and computer vision predominantly handle independent lines, overlooking structural regularities such as sets of parallel lines that are pervasive in man-made environments. This paper introduces RiemanLine, a unified minimal representation for 3D lines formulated on Riemannian manifolds that jointly accommodates both individual lines and parallel-line groups. 
Our key idea is to decouple each line landmark into global and local components: a shared vanishing direction optimized on the unit sphere, and scaled normal vectors constrained on orthogonal subspaces, enabling compact encoding of structural regularities. For n parallel lines, the proposed representation reduces the parameter space from 4n (orthonormal form) to 2n+2, naturally embedding parallelism without explicit constraints. We further integrate this parameterization into a factor graph framework, allowing global direction alignment and local reprojection optimization within a unified manifold-based bundle adjustment. Extensive experiments on ICL-NUIM, TartanAir, and synthetic benchmarks demonstrate that our method achieves significantly more accurate pose estimation and line reconstruction, while reducing parameter dimensionality and improving convergence stability.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过紧凑3D直线表示支持相机定位与结构建图，适用于SLAM式因子图优化。

### 2. 核心内容
现有3D直线表示大多独立处理直线，忽略环境中大量存在的平行线结构。RiemanLine提出一种基于黎曼流形的统一最小表示，将直线地标分解为共享消隐方向和正交子空间上的缩放法向量，可同时表达单条直线与平行线组。该方法为因子图优化提供紧凑参数化，可提升相机定位与结构建图的效率。

### 3. 对应检索需求
visual simultaneous localization and mapping。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/37584](https://ojs.aaai.org/index.php/AAAI/article/view/37584)
