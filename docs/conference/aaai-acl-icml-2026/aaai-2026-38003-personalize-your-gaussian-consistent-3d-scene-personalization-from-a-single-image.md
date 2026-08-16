---
title: "Personalize Your Gaussian: Consistent 3D Scene Personalization from a Single Image"
title_zh: 个性化你的高斯：从单张图像实现一致的三维场景个性化
authors: "Yuxuan Wang, Xuanyu Yi, Qingshan Xu, Yuan Zhou, Long Chen, Hanwang Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38003/41965"
tags: ["query:d-slam"]
score: 4.0
evidence: 基于单张图像对重建高斯场景进行个性化编辑，并非从图像重建三维
tldr: 从单张参考图个性化三维场景要求同时保持多视角一致性和参考一致性，但单一视角导致视角偏差。CP-GS 提出一种渐进式传播框架，逐步将单视角参考信息扩展到整个三维高斯场景，从而缓解视角偏差，生成跨视角和与参考一致的个性化结果。该工作聚焦三维编辑与生成，而非三维重建或SLAM，但对三维场景一致性建模有一定参考价值。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 单张图像个性化三维场景存在视角偏差，难保多视角一致和参考一致。
method: 提出CP-GS，采用渐进式传播机制从单视角参考信息扩展至全局高斯场景。
result: 在多视角一致性和参考一致性上取得更好结果，缓解视角偏差问题。
conclusion: 渐进传播是解决单图像驱动三维场景个性化的有效策略。
---

## Abstract
Personalizing 3D scenes from a single reference image enables intuitive user-guided editing, which requires achieving both multi-view consistency across perspectives and referential consistency with the input image. However, these goals are particularly challenging due to the viewpoint bias caused by the limited perspective provided in a single image. Lacking the mechanisms to effectively expand reference information beyond the original view, existing methods of image-conditioned 3DGS personalization often suffer from this viewpoint bias and struggle to produce consistent results. Therefore, in this paper, we present Consistent Personalization for 3D Gaussian Splatting (CP-GS), a framework that progressively propagates the single-view reference appearance to novel perspectives. In particular, CP-GS integrates pre-trained image-to-3D generation and iterative LoRA fine-tuning to extract and extend the reference appearance, and finally produces faithful multi-view guidance images and the personalized 3DGS outputs through a view-consistent generation process guided by geometric cues. Extensive experiments on real-world scenes show that our CP-GS effectively mitigates the viewpoint bias, achieving high-quality image-conditioned 3DGS personalization that significantly outperforms existing methods.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于单张图像对重建高斯场景进行个性化编辑，并非从图像重建三维。

### 2. 核心内容
从单张参考图个性化三维场景要求同时保持多视角一致性和参考一致性，但单一视角导致视角偏差。CP-GS 提出一种渐进式传播框架，逐步将单视角参考信息扩展到整个三维高斯场景，从而缓解视角偏差，生成跨视角和与参考一致的个性化结果。该工作聚焦三维编辑与生成，而非三维重建或SLAM，但对三维场景一致性建模有一定参考价值。

### 3. 对应检索需求
Papers central to 查找SLAM和三维重建相关的论文, especially work that connects or combines: 年; visual simultaneous localization and mapping; 3D reconstruction from images; structure from motion for 3D modeling; recent progress in simultaneous localization and mapping with 3D scene reconstruction.

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/38003](https://ojs.aaai.org/index.php/AAAI/article/view/38003)
