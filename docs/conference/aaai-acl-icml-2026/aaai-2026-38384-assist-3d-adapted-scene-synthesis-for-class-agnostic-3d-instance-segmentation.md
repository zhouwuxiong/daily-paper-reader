---
title: "ASSIST-3D: Adapted Scene Synthesis for Class-Agnostic 3D Instance Segmentation"
title_zh: ASSIST-3D：用于类别无关三维实例分割的自适应场景合成
authors: "Shengchao Zhou, Jiehong Lin, Jiahui Liu, Shizhen Zhao, Chirui Chang, Xiaojuan Qi"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38384/42346"
tags: ["query:d-slam"]
score: 4.0
evidence: 为类别无关三维实例分割合成场景数据，与三维重建主题相关性较弱
tldr: 类别无关的三维实例分割因缺少标注数据和嘈杂二值分割而难以泛化。ASSIST-3D 构建一种自适应的三维场景合成流程，同时满足几何多样性、上下文复杂度和布局合理性，为分割模型生成增强数据。实验表明该数据合成方法能够显著提升分割模型对未知类别的泛化能力，但内容聚焦于三维场景理解，而非三维重建或SLAM技术。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 类别无关三维实例分割因标注数据稀缺而泛化性差，现有场景合成难以兼顾几何、上下文和布局。
method: 提出ASSIST-3D，从几何多样性、上下文复杂度和布局合理性三方面合成训练数据。
result: 合成数据增强模型泛化能力，提升类别无关实例分割性能。
conclusion: 针对任务需求自适应的场景合成可显著改善三维实例分割的泛化性。
---

## Abstract
Class-agnostic 3D instance segmentation tackles the challenging task of segmenting all object instances, including previously unseen ones, without semantic class reliance. Current methods struggle with generalization due to the scarce annotated 3D scene data or noisy 2D segmentations. While synthetic data generation offers a promising solution, existing 3D scene synthesis methods fail to simultaneously satisfy geometry diversity, context complexity, and layout reasonability, each essential for this task. To address these needs, we propose an Adapted 3D Scene Synthesis pipeline for class-agnostic 3D Instance SegmenTation, termed as ASSIST-3D, to synthesize proper data for model generalization enhancement. Specifically, ASSIST-3D features three key innovations, including 1) Heterogeneous Object Selection from extensive 3D CAD asset collections, incorporating randomness in object sampling to maximize geometric and contextual diversity; 2) Scene Layout Generation through LLM-guided spatial reasoning combined with depth-first search for reasonable object placements; and 3) Realistic Point Cloud Construction via multi-view RGB-D image rendering and fusion from the synthetic scenes, closely mimicking real-world sensor data acquisition. Experiments on ScanNetV2, ScanNet++, and S3DIS benchmarks demonstrate that models trained with ASSIST-3D-generated data significantly outperform existing methods. Further comparisons underscore the superiority of our purpose-built pipeline over existing 3D scene synthesis approaches.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
为类别无关三维实例分割合成场景数据，与三维重建主题相关性较弱。

### 2. 核心内容
类别无关的三维实例分割因缺少标注数据和嘈杂二值分割而难以泛化。ASSIST-3D 构建一种自适应的三维场景合成流程，同时满足几何多样性、上下文复杂度和布局合理性，为分割模型生成增强数据。实验表明该数据合成方法能够显著提升分割模型对未知类别的泛化能力，但内容聚焦于三维场景理解，而非三维重建或SLAM技术。

### 3. 对应检索需求
Papers central to 查找SLAM和三维重建相关的论文, especially work that connects or combines: 年; visual simultaneous localization and mapping; 3D reconstruction from images; structure from motion for 3D modeling; recent progress in simultaneous localization and mapping with 3D scene reconstruction.

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/38384](https://ojs.aaai.org/index.php/AAAI/article/view/38384)
