---
title: Debiased Multiplex Tokenizer for Efficient Map-Free Visual Relocalization
title_zh: 高效地图无关视觉重定位的去偏多路标记器
authors: "Wenshuai Wang, Hong Liu, Shengquan Li, Peifeng Jiang, Runwei Ding"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37982/41944"
tags: ["query:d-slam"]
score: 8.0
evidence: 在无GPS环境下进行机器人位姿估计的视觉重定位
tldr: 视觉重定位在GPS受限环境下对机器人至关重要，但视角和外观变化带来挑战。DeMT 提出基于预训练视觉Mamba编码器与去偏多路标记器的框架，进行相对位姿回归。该方法通过多路交互和去偏机制集成相对位姿预测，实现高效、稳健且轻量的地图无关视觉重定位，适合移动设备部署。实验验证其在位姿精度和效率上的优势，为无地图定位任务提供了新方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 地图无关的视觉重定位面临视角与光照变化，且需兼顾移动端轻量化部署。
method: 提出DeMT，基于预训练视觉Mamba编码器和去偏多路标记器集成相对位姿回归。
result: 在多个基准上实现高效稳健的位姿估计，并保持轻量部署。
conclusion: 视觉Mamba与去偏标记化结合能有效提升地图无关重定位的精度与效率。
---

## Abstract
Image-based feature representation plays a critical role in visual localization, enabling robots to estimate their position and orientation in GPS-denied environments. However, this task is often undermined by significant variations in camera viewpoints and scene appearances. Recently, map-free visual relocalization (MFVR) has emerged as a promising paradigm due to its compatibility with lightweight deployment and privacy isolation on mobile devices. In this paper, we propose the Debiased Multiplex Tokenizer (DeMT) as a novel method for versatile and efficient MFVR. Specifically, DeMT performs relative pose regression through an integrated framework built upon a pretrained vision Mamba encoder, comprising three key modules: First, Multiplex Interactive Tokenization yields robust image tokens with non-local affinities and cross-domain descriptions; Second, Debiased Anchor Registration facilitates anchor token matching through proximity graph retrieval and causal pointer attribution; Third, Geometry-Informed Pose Regression empowers multi-layer perceptrons with a gating mechanism and spectral normalization to support both pair-wise and multi-view modes. Extensive evaluations across nine public datasets demonstrate that DeMT substantially outperforms existing baselines and ablation variants in diverse indoor and outdoor environments.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
在无GPS环境下进行机器人位姿估计的视觉重定位。

### 2. 核心内容
视觉重定位在GPS受限环境下对机器人至关重要，但视角和外观变化带来挑战。DeMT 提出基于预训练视觉Mamba编码器与去偏多路标记器的框架，进行相对位姿回归。该方法通过多路交互和去偏机制集成相对位姿预测，实现高效、稳健且轻量的地图无关视觉重定位，适合移动设备部署。实验验证其在位姿精度和效率上的优势，为无地图定位任务提供了新方案。

### 3. 对应检索需求
visual simultaneous localization and mapping。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/37982](https://ojs.aaai.org/index.php/AAAI/article/view/37982)
