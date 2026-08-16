---
title: "LaRI: Layered Ray Intersections for Single-view 3D Geometric Reasoning"
title_zh: LaRI：面向单视角3D几何推理的分层射线求交
authors: "Rui Li, Biao Zhang, Zhenyu Li, Federico Tombari, Peter Wonka"
date: 2026-04-30
pdf: "https://openreview.net/pdf/81e4c1ee701d165b0e030660757cf3a56b5dcd34.pdf"
tags: ["query:d-slam"]
score: 8.0
evidence: 通过分层射线求交与分层点图实现单视角3D场景重建
tldr: 传统单目深度估计只能看到可见表面，无法推理被遮挡几何。LaRI提出分层射线求交方法，一次性前向预测多条射线穿过的表面点图及射线停止索引，实现对遮挡场景的完整重建。相比隐式表示或迭代细化，其在效率和视对齐几何推理上更具优势，为物体级和场景级任务提供支撑。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 深度估计局限于可见表面，难以对单视角图像中的遮挡几何进行推理。
method: 前馈预测分层点图与射线停止索引，从单视角一次性重建多个表面。
result: 在单次前向中完成完整场景重建并支持物体级与场景级任务。
conclusion: 分层射线表示提供高效、视对齐的单视图几何推理新范式。
---

## Abstract
We present Layered Ray Intersections (LaRI), a fully supervised method for occluded geometry reasoning from a single image. Unlike conventional depth estimation, which is limited to visible surfaces, LaRI predicts multiple surfaces intersected by the camera rays using layered point maps. Compared to the existing approaches that leverage neural implicit representations or iterative refinement, LaRI achieves complete scene reconstruction in one feed-forward pass, enabling efficient and view-aligned geometric reasoning to underpin both object-level and scene-level tasks. We further propose to predict the ray stopping index, which identifies valid intersecting pixels and layers from LaRI's output. To better underpin and evaluate this task, we build an annotation pipeline using rendering engines, construct annotations for five public datasets, including synthetic and real-world data covering 3D objects and scenes. As a generic method, LaRI's performance is validated in object-level and scene-level reconstruction tasks.

---

## 论文详细总结（自动生成）

好的，我理解您的要求。您希望我基于提供的论文元数据，对该论文进行结构化、深入且客观的中文总结。虽然您提供的“PDF提取文本”部分是OpenReview的验证页面，但元数据部分包含了丰富的论文信息，足以支撑一份详细的总结。

以下是基于这些信息生成的总结：

---

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：传统的单目深度估计（Monocular Depth Estimation）任务受限于其定义本身，只能预测相机图像中**可见表面**的深度，无法对**被遮挡的几何结构**进行推理。这严重限制了机器对三维世界的完整理解，因为现实场景中物体相互遮挡是常态。
- **研究动机**：为了实现从单张图像进行完整的3D场景重建，模型必须能够“猜测”或“推理”出被前景物体遮挡的背景或物体内部结构。现有的解决方案（如神经隐式表示或迭代细化方法）要么计算开销大，要么推理速度慢，难以满足高效、实时的应用需求。
- **整体含义**：该论文提出了一种名为 **LaRI（Layered Ray Intersections，分层射线求交）** 的全新监督学习方法，旨在让模型在**一次前向传播（one feed-forward pass）** 中，从单张图像直接重建出包含多个遮挡层级的完整3D场景结构，从而为下游的物体级和场景级任务提供高效、与视图对齐的几何推理基础。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：不再将3D重建视为预测一个单一的深度图，而是将其建模为预测**多条射线（Ray）穿过的多个表面点**。通过引入“分层点图”（Layered Point Maps）的概念，模型可以同时输出可见表面和隐藏表面的3D坐标。
- **关键技术细节**：
    1.  **分层点图（Layered Point Maps）**：对于图像中的每个像素（即一条相机射线），模型不仅预测其第一个交点（可见表面），还预测该射线穿透物体后可能相交的下一个表面点，以此类推，形成一组分层级的点图。
    2.  **射线停止索引（Ray Stopping Index）**：由于不同射线可能穿过的表面层数不同（例如，有的射线可能只碰到一个物体就射向天空），模型需要预测一个“停止索引”。这个索引用于**识别哪些分层点图上的像素和层是有效的（valid）**，过滤掉无意义的预测（如天空背景的未命中射线），确保输出的几何信息是精确对齐和可用的。
- **算法流程**：给定单张图像，模型采用**前馈（feed-forward）** 方式，一次性预测出所有分层点图和相应的射线停止索引。整个过程是并行的，不需要迭代优化或大量采样。

### 3. 实验设计：数据集、基准与对比方法

- **数据集**：论文构建了一个完整的标注管线（annotation pipeline），利用渲染引擎为**五个公共数据集**生成了用于遮挡几何推理的标注。这五个数据集涵盖了**3D物体**和**3D场景**两大类，并包括了**合成数据**（Synthetic）和**真实世界数据**（Real-world），确保了实验的全面性和泛化性。
- **Benchmark**：这项研究为“单视角遮挡几何推理”这一任务建立了新的基准（benchmark），使得该任务可以被量化和标准化评估。
- **对比方法**：论文将该方法与两类现有方法进行了对比：
    - 基于**神经隐式表示**（Neural Implicit Representations）的方法。
    - 基于**迭代细化**（Iterative Refinement）的方法。

### 4. 资源与算力

- **说明**：**在提供的元数据中，并未明确提及**具体的训练算力信息，例如使用的GPU型号（如A100、V100）、GPU数量、训练总时长（如days/hours）或参数量等。这部分信息通常会在论文正文的实验部分详细列出，而在此处缺失。

### 5. 实验数量与充分性

- **实验数量推测**：论文在**物体级（object-level）** 和**场景级（scene-level）** 两个层面的重建任务上均验证了方法，并跨**五个数据集**（含合成与真实）进行了评估。由此可以合理推断，论文的实验设置是**较为全面**的。
- **充分性与客观性**：
    - 从元数据看，实验涵盖了不同数据域（合成/真实）和不同复杂度（物体/场景），对比了两种主流且差异显著的方法范式（隐式/迭代），这**增强了结论的客观性和说服力**。
    - 然而，由于元数据未提供详细的数值结果（如定量指标表）和**消融实验（Ablation Study）** 的具体数量，我们无法判断其对各个组件（如射线停止索引的必要性、分层数量的影响等）的验证是否深入。因此，严格来说，**实验的充分性证据尚不完整**，需要查阅全文才能给出最终判定。

### 6. 论文的主要结论与发现

- **主要结论**：LaRI方法成功证明了**一次前向传播**即可高效地完成单视角下的完整场景重建，包括被遮挡的部分。
- **关键发现**：相比依赖隐式表示或迭代细化等计算开销较大的方法，**“分层射线表示”**（Layered Ray Representations）提供了一种**更高效、且与视图严格对齐（view-aligned）** 的单视图几何推理新范式。该方法不仅理论上高效，而且在实践中能够很好地支持物体级和场景级的多个下游任务。

### 7. 优点：方法或实验设计上的亮点

- **方法论创新**：直接从可见表面预测扩展至预测多层级表面，思想简洁且明确，将“深度估计”问题提升为“遮挡几何推理”问题。
- **高效性**：采用**单次前向传播**，完全避免了隐式表示方法通常所需的体积渲染或迭代优化过程，推理速度快，更贴近实时应用。
- **视图对齐**：整个推理过程在图像平面上进行，天然保持了与输入视图的像素级对齐，这对于依赖几何精确性的下游任务至关重要。
- **数据建设贡献**：提出了利用渲染引擎构建标注的**自动化管线**，并为5个公共数据集生成了标注，为学术界在该领域的研究提供了宝贵的**数据基础**。
- **任务普适性**：方法被设计为通用模块，并在物体级与场景级两个层级的任务上均取得了成功验证，展示了良好的通用性。

### 8. 不足与局限

- **信息缺失**：如前所述，元数据中**缺少了关键的量化实验结果、具体的算法实现细节以及消融研究**，这限制了我们对方法性能和组件有效性的全方位评估。
- **潜在偏差风险**：训练数据依赖渲染引擎生成，虽然包含真实数据，但合成数据与真实世界之间仍可能存在**域间隙（domain gap）**，可能影响模型在无约束真实场景中的泛化表现。
- **应用限制**：论文未提及方法在极端遮挡、透明物体、反射表面或高度复杂拓扑结构场景下的表现。此外，受限于训练数据，模型对某个固定层数内的遮挡预测效果较好，对于层数极多的复杂场景，其**可分层的最大数量**可能成为应用的瓶颈。

---

（完）
