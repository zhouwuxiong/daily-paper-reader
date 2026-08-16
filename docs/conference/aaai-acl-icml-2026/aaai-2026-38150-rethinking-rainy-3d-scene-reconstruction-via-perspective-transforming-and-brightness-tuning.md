---
title: Rethinking Rainy 3D Scene Reconstruction via Perspective Transforming and Brightness Tuning
title_zh: 通过透视变换与亮度调节重新审视雨天三维场景重建
authors: "Qianfeng Yang, Xiang Chen, Pengpeng Li, Qiyuan Guan, Guiyue Jin, Jiyu Jin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38150/42112"
tags: ["query:d-slam"]
score: 9.0
evidence: 面向雨雾退化多视图图像的三维场景重建与数据集
tldr: 针对雨天多视图图像退化导致三维重建不准确不完整、现有数据集忽略雨线视角依赖和亮度下降的问题，构建OmniRain3D数据集以更真实模拟雨天退化。基于该数据集提出端到端重建框架，通过透视变换与亮度调节增强跨视角一致性。实验表明其在雨天场景重建中有效改善精度与完整性。该工作为退化条件下的三维重建提供了数据与方法支撑。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 雨天多视图图像质量下降，现有数据集未模拟真实雨线的视角依赖与亮度变化，导致重建不准确。
method: 构建OmniRain3D数据集模拟雨线透视变化与亮度动态性，并提出端到端三维重建框架加以恢复。
result: 在雨天场景数据集上重建精度和完整性显著提升，优于现有方法。
conclusion: 真实感退化数据与透视亮度校正能增强雨天三维场景重建的鲁棒性。
---

## Abstract
Rain degrades the visual quality of multi-view images, which are essential for 3D scene reconstruction, resulting in inaccurate and incomplete reconstruction results. Existing datasets often overlook two critical characteristics of real rainy 3D scenes: the viewpoint-dependent variation in the appearance of rain streaks caused by their projection onto 2D images, and the reduction in ambient brightness resulting from cloud coverage during rainfall. To improve data realism, we construct a new dataset named OmniRain3D that incorporates perspective heterogeneity and brightness dynamicity, enabling more faithful simulation of rain degradation in 3D scenes. Based on this dataset, we propose an end-to-end reconstruction framework named REVR-GSNet (Rain Elimination and Visibility Recovery for 3D Gaussian Splatting). Specifically, REVR-GSNet integrates recursive brightness enhancement, Gaussian primitive optimization, and GS-guided rain elimination into a unified architecture through joint alternating optimization, achieving high-fidelity reconstruction of clean 3D scenes from rain-degraded inputs. Extensive experiments show the effectiveness of our dataset and method. Our dataset and method provide a foundation for future research on multi-view image deraining and rainy 3D scene reconstruction.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向雨雾退化多视图图像的三维场景重建与数据集。

### 2. 核心内容
针对雨天多视图图像退化导致三维重建不准确不完整、现有数据集忽略雨线视角依赖和亮度下降的问题，构建OmniRain3D数据集以更真实模拟雨天退化。基于该数据集提出端到端重建框架，通过透视变换与亮度调节增强跨视角一致性。实验表明其在雨天场景重建中有效改善精度与完整性。该工作为退化条件下的三维重建提供了数据与方法支撑。

### 3. 对应检索需求
3D reconstruction from images。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/38150](https://ojs.aaai.org/index.php/AAAI/article/view/38150)
