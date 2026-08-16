---
title: Parallelizable Riemannian Alternating Direction Method of Multipliers for Non-convex Pose Graph Optimization
title_zh: 用于非凸位姿图优化的可并行黎曼交替方向乘子法
authors: "Xin Chen, Chunfeng Cui, Deren Han, Liqun Qi"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/41007/44968"
tags: ["query:d-slam"]
score: 8.0
evidence: 位姿图优化求解器，是SLAM的数学核心
tldr: 针对位姿图优化（PGO）作为SLAM后端在规模增大时计算复杂度呈多项式增长、难以实时部署的问题，提出可并行化的黎曼交替方向乘子法PRADMM。通过复制变量并引入等式约束重构问题，使求解过程可在图上并行计算。相比现有方法，PRADMM在保证精度的同时显著降低大规模SLAM后端求解时间，促进实时应用。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 位姿图优化复杂度随图规模增长，制约大规模SLAM实时求解。
method: 通过变量复制与等式约束重构位姿图优化，提出可并行化黎曼ADMM求解器。
result: 相比现有方法，显著减少大规模SLAM后端求解时间并支持并行计算。
conclusion: 并行化PGO求解器可有效提升SLAM系统的实时性与可扩展性。
---

## Abstract
Pose graph optimization (PGO) is fundamental to robot perception and navigation systems, serving as the mathematical backbone for solving simultaneous localization and mapping (SLAM). Existing solvers suffer from polynomial growth in computational complexity with graph size, hindering real-time deployment in large-scale scenarios. In this paper, by duplicating variables and introducing equality constraints, we reformulate the problem and propose a Parallelizable Riemannian Alternating Direction Method of Multipliers (PRADMM) to solve it efficiently. Compared with the state-of-the-art methods that usually exhibit polynomial time complexity growth with graph size,  PRADMM  enables efficient parallel computation across vertices regardless of graph size. Crucially, all subproblems admit closed-form solutions, ensuring  PRADMM maintains exceptionally stable performance. Furthermore, by carefully exploiting the structures of the coefficient matrices in the constraints, we establish the global convergence of PRADMM under mild conditions, enabling larger relaxation step sizes within the interval (0,2). Extensive empirical validation on two synthetic datasets and multiple real-world 3D SLAM benchmarks confirms the superior computational performance of PRADMM.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
位姿图优化求解器，是SLAM的数学核心。

### 2. 核心内容
针对位姿图优化（PGO）作为SLAM后端在规模增大时计算复杂度呈多项式增长、难以实时部署的问题，提出可并行化的黎曼交替方向乘子法PRADMM。通过复制变量并引入等式约束重构问题，使求解过程可在图上并行计算。相比现有方法，PRADMM在保证精度的同时显著降低大规模SLAM后端求解时间，促进实时应用。

### 3. 对应检索需求
visual simultaneous localization and mapping。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/41007](https://ojs.aaai.org/index.php/AAAI/article/view/41007)
