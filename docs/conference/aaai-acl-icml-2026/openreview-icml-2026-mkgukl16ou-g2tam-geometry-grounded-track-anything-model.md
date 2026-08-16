---
title: "G$^2$TAM: Geometry Grounded Track Anything Model"
title_zh: G2TAM：几何锚定的任意目标跟踪模型
authors: "Chenming Zhu, Peizhou Cao, Jingli Lin, Wenbo Hu, Yunlong Ran, Jiangmiao Pang, Tai Wang, Xihui Liu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a145c4bdeadbedef5312dda0e17186b513b62898.pdf"
tags: ["query:d-slam"]
score: 4.0
evidence: 利用前馈三维重建模型从图像进行几何约束的实例跟踪
tldr: 针对视频分割模型在视角大幅变化和长期遮挡下依赖外观记忆导致跟踪不稳定的问题，提出几何锚定的跟踪模型G2TAM。该方法借助前馈三维重建模型提供的空间一致性，以空间对齐的几何表示为隐式记忆，在无序RGB图像或视频上进行可提示的3D实例跟踪。实验表明其能保持跨帧和跨视角的实例身份与定位稳定性。这项工作展示了三维几何对提升视频理解的重要作用。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视频分割跟踪依赖外观记忆，难以应对大视角变化和长期遮挡。
method: 利用前馈三维重建模型的空间一致性，将几何表示作为隐式记忆进行提示式3D实例跟踪。
result: 在视角变化和遮挡场景下显著提升实例跟踪的跨帧稳定性与定位一致性。
conclusion: 几何锚定的隐式记忆可有效增强多视角实例跟踪鲁棒性，启发重建与跟踪的联合建模。
---

## Abstract
Human spatial understanding arises from jointly perceiving geometry and semantics, enabling consistent object identification and localization across viewpoints and time. Current video segmentation models depend on explicit object appearance memory banks for instance tracking, yet they remain vulnerable to large viewpoint changes and long-term occlusions. Leveraging the spatial consistency afforded by modern feed-forward 3D reconstruction models, we propose the Geometry Grounded Tracking Anything Model (G$^2$TAM), a unified framework for promptable instance tracking in 3D using only unordered RGB images or videos. G$^2$TAM employs spatially aligned geometric representations as implicit memory, ensuring stable instance identity and localization across frames and views. At its core is a cross-modal spatial encoder that integrates visual and textual prompts into a shared geometric space, enabling end-to-end spatial reconstruction and instance-consistent mask prediction. To support training and evaluation, we construct InsTrack, a large-scale dataset with a dedicated validation split for benchmarking. Extensive experiments show that G$^2$TAM delivers strong cross-view consistency, promptable instance spatial tracking, video object segmentation, and spatial reconstruction, establishing a foundation for interactive, geometry-grounded spatial reasoning.

---

## 论文详细总结（自动生成）

# G2TAM：几何锚定的任意目标跟踪模型 —— 中文总结

## 1. 核心问题与整体含义

- **研究动机**：人类的空间理解能力源于对几何与语义的联合感知，从而能够在不同视角和时间上一致地识别和定位物体。现有的视频分割模型在实例跟踪时主要依赖**显式外观记忆库**（appearance memory banks），这使其在**大视角变化**和**长期遮挡**场景下极易丢失目标或产生身份切换，鲁棒性不足。
- **核心问题**：如何利用三维几何信息增强实例跟踪的跨视角、跨时间一致性，突破外观记忆的局限。
- **整体含义**：论文提出将现代前馈三维重建模型提供的**空间一致性**引入视频/图像实例跟踪，构建一个“几何锚定”的跟踪框架，使模型不仅理解“目标长什么样”，还理解“目标在空间中处于什么位置”。这项工作展示了三维几何对提升视频理解任务的重要价值，并为重建与跟踪的联合建模提供了新思路。

## 2. 方法论：核心思想与技术细节

- **核心思想**：用**空间对齐的几何表示**作为**隐式记忆**，替代或补充传统的外观记忆库。几何表示天然具有跨视角的稳定性，因此可在视角变化或遮挡时维持实例身份与位置的一致性。
- **统一框架**：提出 **G²TAM（Geometry Grounded Tracking Anything Model）**，一个**仅使用无序 RGB 图像或视频**即可进行可提示式（promptable）3D 实例跟踪的统一框架。
- **关键组件**：
  - **跨模态空间编码器（cross-modal spatial encoder）**：将**视觉提示**和**文本提示**集成到一个共享的几何空间中，使模型能够端到端地进行空间重建与实例一致的掩码预测。
  - **前馈三维重建模型**：利用现代前馈重建模型提供的空间一致性，为跟踪提供几何锚定。
  - **隐式几何记忆**：通过空间对齐的几何表示存储目标位置与身份信息，避免依赖脆弱的表观特征。
- **输入输出**：输入无序 RGB 图像或视频序列，输出空间重建结果以及实例一致的掩码（即可进行视频目标分割和空间跟踪）。
- **公式/算法流程**（根据摘要描述）大致为：
  1. 输入 RGB 图像/视频帧。
  2. 使用前馈三维重建模型提取几何特征，获得空间一致的三维表示。
  3. 将用户提供的视觉/文本提示通过跨模态空间编码器映射到同一几何空间。
  4. 在几何空间中融合提示与重建特征，隐式存储实例记忆。
  5. 输出跨帧/跨视角一致的实例掩码和空间定位结果。

## 3. 实验设计

- **数据集**：论文构建了 **InsTrack**，一个**大规模数据集**，并专门划分了**验证集**用于基准测试（benchmark）。摘要未说明数据集的详细来源、规模或标注方式。
- **任务/场景**：
  - 跨视图一致性评测（cross-view consistency）
  - 可提示实例空间跟踪（promptable instance spatial tracking）
  - 视频目标分割（video object segmentation）
  - 空间重建（spatial reconstruction）
- **对比方法**：摘要中**未明确列出**对比的具体 baseline 方法，仅从问题背景推断其对比对象可能包括基于外观记忆的视频分割模型（如 SAM 系列扩展模型、视频目标分割方法等），但论文正文细节未提供，无法确认。

## 4. 资源与算力

- 论文提供的内容中（标题、摘要、元数据）**未明确说明**训练所使用的 GPU 型号、数量、训练时长、参数量、显存占用等计算资源信息。
- **需要指出**：由于我们仅获得论文摘要和元数据，无法获知关于算力资源的任何细节。若需完整信息，需查阅论文全文的实验设置部分。

## 5. 实验数量与充分性

- 根据摘要描述，实验覆盖了**四类任务/场景**（跨视图一致性、空间跟踪、视频分割、空间重建），并构建了专属数据集 InsTrack 及验证集。
- 但**未提供**具体的实验数量、消融实验设计、与 baseline 的定量对比数值、不同组件贡献分析等细节。
- **充分性评估**：
  - **优点**：涵盖多任务验证，能较全面展示方法的通用性。
  - **不足**：缺乏可验证的定量结果和消融研究；对比方法不明；数据集构建细节未提供。仅从摘要层面看，实验证据不足以支撑“显著提升”这一结论的强度，客观性和公平性无法在摘要层面确认。

## 6. 主要结论与发现

- G²TAM 通过几何锚定的隐式记忆，在**大视角变化**和**长期遮挡**场景下显著提升实例跟踪的跨帧稳定性和定位一致性。
- 该方法能同时支持**提示式空间跟踪**、**视频目标分割**与**空间重建**，验证了几何信息与语义信息联合建模的有效性。
- 结论强调：**几何锚定的隐式记忆可有效增强多视角实例跟踪鲁棒性**，并启发未来重建与跟踪的**联合建模**方向。

## 7. 优点

- **方法创新性强**：将 3D 重建的空间一致性引入实例跟踪，摆脱对纯外观记忆的依赖，角度新颖。
- **统一框架**：能够处理无序图像或视频，支持视觉/文本多模态提示，具备良好的交互性和通用性。
- **端到端学习**：跨模态空间编码器实现了提示、重建、掩码预测的一体化训练。
- **任务覆盖面广**：同时支持空间重建、视频分割、空间跟踪，可能促进下游 3D 交互应用。
- **数据集贡献**：构建了 InsTrack 大规模数据集，为后续研究提供基准。

## 8. 不足与局限

- **实验信息不透明**：摘要中缺乏定量结果、baseline 细节和消融研究，无法判断方法相较于现有方法的具体优势幅度。
- **数据集细节缺失**：InsTrack 数据的采集方式、规模、类别分布、标注一致性等未说明，可能影响 benchmark 的可信度和通用性。
- **对比公平性存疑**：未说明与哪些方法对比、是否使用相同骨干网络或训练设置，难以评估公平性。
- **应用限制**：依赖前馈三维重建模型，其本身可能受限于输入图像重叠度、相机位姿估计误差、场景尺度等；在纯单目、动态场景或纹理稀疏环境下的表现未知。
- **推理复杂度**：端到端重建与跟踪联合可能带来较高的计算开销，摘要未讨论实时性问题。
- **长期记忆机制**：隐式几何记忆如何应对目标形变、非刚性运动以及场景动态变化，尚未在摘要中说明。
- **论文信息有限**：本总结仅基于提供的摘要和元数据，上述局限中部分为合理推断，具体需以全文为准。

（完）
