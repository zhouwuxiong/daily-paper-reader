---
title: "Creat3r: Confidence Reaggregation for Exploration-aware Active 3D Reconstruction"
title_zh: Creat3r：面向探索感知主动三维重建的置信度重聚合
authors: "Chih-Jung Tsai, Hwann-Tzong Chen, Tyng-Luh Liu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f275d0cf84eb0f2b3fbdc5da5263aaab65ac93cf.pdf"
tags: ["query:d-slam"]
score: 9.0
evidence: 基于图像的多视角三维重建中的主动下一视角选择
tldr: 稀疏视角下三维重建容易因信息不足而产生伪影，选择哪些视角拍摄是关键。Creat3r 提出迭代式下一最佳视角选择框架，从少量图像位姿对出发，构建中间点云并估计三维置信场，通过高斯投影生成二维置信与探索图，在计算约束下平衡可靠区域的利用和未知区域的探索。该方法能高效提升三维高斯重建的质量，并在多个数据集上展示了比随机或启发式视角选择更优的性能，适用于机器人主动重建。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 稀疏输入下三维重建信息不足，需要主动选择最有信息量的视角以提高重建质量。
method: 提出迭代式下一最佳视角选择框架，利用三维置信场与高斯投影生成置信和探索图，平衡利用与探索。
result: 在有限视角预算下实现高效高质量三维重建，优于随机或启发式视角选择。
conclusion: 主动视角选择与不确定性建模结合能显著提升稀疏视图三维重建效率与质量。
---

## Abstract
We present Creat3r, an iterative next-best-view (NBV) selection framework for efficient, high-quality 3D reconstruction. Starting from a small seed set of image-pose pairs, Creat3r repeatedly selects the most informative next camera pose. After each pose is chosen, the corresponding image is acquired and added to the multi-view set to update a 3DGS reconstruction. To guide selection, Creat3r constructs an intermediate point cloud and estimates reconstruction reliability via a novel 3D confidence field, which is projected to candidate poses through Gaussian projection to produce 2D confidence and exploration maps. These maps balance exploitation of reliable regions and exploration of uncertain or unseen areas under computational constraints. Experiments with standard 3DGS show that Creat3r consistently outperforms baselines in novel view synthesis and surface reconstruction, achieving higher SSIM and F1 scores with fewer views.

---

## 论文详细总结（自动生成）

# 中文总结：Creat3r

## 1. 核心问题与整体含义

- **研究动机**：在基于图像的多视角三维重建中，当输入视角非常稀疏时，模型可用的信息不足，容易产生伪影和几何失真。与其被动接受固定视角集合，不如主动选择“最有信息量”的下一视角，以在有限视角预算下最大化重建质量。
- **整体含义**：论文提出了一种迭代式下一最佳视角（Next-Best-View, NBV）选择框架，将主动视角选择与三维高斯泼溅（3DGS）重建相结合，目标是实现高效、高质量的三维重建，尤其适用于机器人主动重建等需要自主采集图像的场景。

## 2. 方法论

- **核心思想**：构建一个闭环的“重建—评估—选视角—采图—更新”流程，在每一步选择最有利于提升重建质量的相机位姿。
- **关键流程**：
  1. 从一个较小的种子图像-位姿对集合出发；
  2. 基于当前多视图集合更新一个 3DGS 重建；
  3. 构建一个中间点云，并估计一个三维置信场（3D confidence field），用于刻画当前重建在不同空间位置的可靠性；
  4. 通过高斯投影（Gaussian projection）将三维置信场投影到候选相机位姿上，生成二维置信图（confidence map）与探索图（exploration map）；
  5. 利用这两类图在“利用可靠区域”和“探索未知/不确定区域”之间做权衡，在计算约束下选出下一最佳视角；
  6. 获取该视角对应的图像，加入多视图集合，回到步骤 2，迭代进行，直到达到预算或满足停止条件。
- **公式/算法层面**：摘要未给出具体数学表达式，但可理解为优化目标是在候选视角集合上最大化一个融合了置信度与探索收益的评分函数，类似于主动学习中的 acquisition function。

## 3. 实验设计

- **数据集/场景**：摘要和元数据仅提到“在多个数据集上”验证，未列出具体数据集名称（如 DTU、Blender、Tanks and Temples 等）。场景类型应属于多视角三维重建的常见 benchmark 类。
- **基准与指标**：
  - 新视角合成（novel view synthesis）质量：使用 SSIM 等指标；
  - 表面重建（surface reconstruction）质量：使用 F1 分数等指标。
- **对比方法**：摘要未明确列出全部 baselines，但元数据/结论中提到对比了随机视角选择与启发式视角选择方法；实验使用标准 3DGS 作为重建后端，以验证视角选择策略的通用性。

## 4. 资源与算力

- 论文提供的文本中**未明确说明** GPU 型号、数量、训练时长、显存占用等算力信息。
- 也未给出每轮 NBV 选择或重建更新的时间开销，无法直接评估计算效率。

## 5. 实验数量与充分性

- **从可获取信息看**：实验覆盖了新视角合成和表面重建两类任务，使用了多个数据集，并与随机/启发式视角选择进行对比，具备基本的说服力。
- **不充分之处**：
  - 未提供具体数据集名称和规模；
  - 未报告消融实验（如去掉探索项、去掉置信场的影响）；
  - 未说明与更高级的主动重建方法的对比；
  - 未提供与视角数量相关的曲线或阈值敏感性分析。
- **客观性评估**：由于缺少上述细节，无法判断实验是否完全公平（例如是否使用相同的种子视角、相同的候选视角集、相同的 3DGS 超参数等）。信息不完整限制了对其充分性的全面评判。

## 6. 主要结论与发现

- Creat3r 能够在**更少视图**下获得更高的 SSIM 和 F1 分数，显著优于随机视角选择和启发式视角选择。
- 将三维置信场与高斯投影结合，可以在计算约束下有效平衡“利用”与“探索”，从而指导主动重建。
- 该方法不依赖特定重建网络，可与标准 3DGS 配合使用，具有良好的通用性。
- 主动视角选择与不确定性建模结合，能显著提升稀疏视图三维重建的效率与质量。

## 7. 优点

- **问题选择有价值**：稀疏视图下的主动视角选择是三维重建和机器人感知中的实际问题，实用性较强。
- **方法设计巧妙**：通过中间点云和三维置信场表达重建可靠性，再用高斯投影生成二维引导图，既保留了三维几何信息，又直接服务于二维图像采集决策。
- **利用-探索权衡清晰**：同时关注已知可靠区域和未知区域，避免贪心选择导致过度局部优化。
- **后端无关性**：基于标准 3DGS 实验，说明该方法可作为通用视角选择策略嵌入不同重建流程。

## 8. 不足与局限

- **信息不完整**：提供的文本中缺乏关键实现细节（如投影公式、损失函数、候选视角采样方式），难以复现。
- **实验细节缺失**：未给出数据集名称、视角预算范围、具体指标数值、误差条、消融实验等，削弱了论证强度。
- **潜在偏差风险**：中间点云和三维置信场的构建方式可能依赖于当前的 3DGS 质量，若初始重建很差，置信场本身也可能不可靠；文中未见针对这种“自举”问题的讨论。
- **应用限制**：主动重建要求系统能够实际到达并拍摄所选视角，因此受机器人运动约束、遮挡、光照变化等现实因素影响；摘要未提及这些场景下的鲁棒性。
- **算力与实时性**：未报告计算开销，选视角的迭代过程可能较慢，影响在实时或在线场景中的部署。

（完）
