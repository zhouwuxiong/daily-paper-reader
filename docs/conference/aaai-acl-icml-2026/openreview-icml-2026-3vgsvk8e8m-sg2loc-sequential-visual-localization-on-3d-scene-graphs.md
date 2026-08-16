---
title: "SG2Loc: Sequential Visual Localization on 3D Scene Graphs"
title_zh: SG2Loc：基于3D场景图的序列视觉定位
authors: "Nicole Damblon, Olga Vysotska, Federico Tombari, Marc Pollefeys, Daniel Barath"
date: 2026-04-30
pdf: "https://openreview.net/pdf/86a5499c8765878ed73e5787cc89f962cfaa2ce2.pdf"
tags: ["query:d-slam"]
score: 7.0
evidence: 面向机器人和AR的序列视觉定位，与视觉SLAM紧密相关
tldr: 针对复杂室内环境中传统视觉定位需要存储大量图像或点云、开销大的问题，提出基于3D场景图的轻量级序列定位方法SG2Loc。该方法以紧凑场景图表示环境，节点为带粗网格的物体、边编码空间关系；在线定位时提取逐块语义特征并预测物体身份，通过粒子滤波估计位姿。实验显示其在降低存储开销的同时保持稳健定位。该工作为机器人和AR提供高效定位方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 传统视觉定位需要保存大量图像或点云，存储开销大，难以支持室内长时序列定位。
method: 用紧凑3D场景图表示环境，结合逐块语义特征与粒子滤波实现轻量级序列视觉定位。
result: 在保持定位精度的同时大幅降低存储需求，适用于机器人及AR场景。
conclusion: 场景图与语义特征相结合的序列定位能显著提升效率，是SLAM定位轻量化的重要方向。
---

## Abstract
Visual localization in complex indoor environments remains a critical challenge for robotics and AR applications. Sequential localization, where pose estimates are refined over time, is important for autonomous agents. However, traditional methods often require storing extensive image databases or point clouds, leading to significant overhead. This paper introduces a novel, lightweight approach to sequential visual localization using 3D scene graphs. Our method represents the environment with a compact scene graph, where nodes represent objects (with coarse meshes) and edges encode spatial relationships. For each image in the localization phase, we extract per-patch semantic features, predicting object identities. Localization is performed within a particle filter framework. Each particle, representing a camera pose, projects the coarse object meshes from the scene graph into the image, assigning object identities to patches based on visibility. The similarity of the per-patch features, in the input image, and object features from the scene graph determines the weight of a particle. Subsequent images are incorporated sequentially, refining the pose estimate. By leveraging a compact scene graph and efficient semantic matching, our method significantly reduces storage while maintaining performance on real-world datasets. The code is available at https://github.com/DmblnNicole/sg2loc.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：复杂室内环境中的视觉定位是机器人和增强现实（AR）应用的关键难题，尤其是需要在时间维度上持续细化位姿的**序列视觉定位**（sequential visual localization）。
- **核心问题**：传统方法通常需要存储大量图像数据库或点云作为地图表示，造成巨大的存储开销，不利于长时运行和轻量化部署。
- **整体含义**：论文提出一种名为 **SG2Loc** 的新方法，利用**3D场景图**作为紧凑环境表示，结合语义特征匹配和粒子滤波，在显著降低存储需求的同时保持定位性能，为机器人/AR提供高效、可扩展的定位方案。

### 2. 方法论

- **环境表示**：使用紧凑的 **3D场景图**，其中：
  - **节点**：代表环境中的物体，附带粗粒度网格（coarse mesh）；
  - **边**：编码物体间的空间关系（如相对位置、朝向等）。
- **在线位姿估计**：
  - 对每一帧输入图像，提取**逐块（per-patch）语义特征**，用于预测物体身份；
  - 采用**粒子滤波**框架，每个粒子表示一个候选相机位姿；
  - 每个粒子将场景图中的粗网格投影到图像平面，根据可见性为图像块**分配物体身份标签**；
  - 将输入图像中逐块特征与场景图中对应物体特征进行**相似度比较**，相似度决定粒子权重；
  - 后续帧按时间顺序依次输入，通过重要性重采样等方式**逐步精化位姿估计**。
- **关键思想**：用轻量级语义级表示替代密集图像/点云存储，用“物体级对应”替代“像素级/关键点级”对应，从而减少存储并保持稳健性。

### 3. 实验设计

- **数据集/场景**：摘要仅提到在 **真实世界数据集**（real-world datasets）上进行评估，并针对复杂室内环境，但未列出具体数据集名称（如 ScanNet、TUM 等）。
- **Benchmark**：未明确说明对比基准；根据元数据，该工作与视觉SLAM领域相关，但摘要未展示标准SLAM/定位基准（如轨迹误差评估）。
- **对比方法**：论文未在摘要中列出对比基线（如经典的基于图像检索的方法、基于点云的特征匹配方法等），因此无法从摘要判断其相对优势的量化结果。

### 4. 资源与算力

- **未明确说明**：提供的文本中未提及 GPU 型号、数量、训练或推理时长、显存占用等算力信息。
- 因此，无法从摘要评估其计算效率（尽管论文主张“轻量级”，但仅有存储开销方面的定性描述，缺乏实测数据支撑）。

### 5. 实验数量与充分性

- **信息有限**：摘要未详列实验组数，也未提及消融实验（例如：
  - 不同场景图粒度的影响；
  - 粒子数对精度和计算时间的影响；
  - 语义特征提取器选择的影响；
  - 与不同存储表示（点云、密集图像）的对比等）。
- **客观性评估**：从摘要看，仅声称“降低存储并保持性能”，但缺乏具体数值，难以判断实验是否充分、公平。需要参考论文全文的图表和对比表才能验证。

### 6. 主要结论与发现

- 3D场景图作为环境表示，可以**大幅降低存储需求**，同时保持可用的定位精度。
- 语义特征匹配与粒子滤波结合，能够实现**序列式、逐步求精的定位**，适合机器人和AR中的长期运行。
- 作者将代码开源（GitHub），有利于复现和后续研究。

### 7. 优点

- **创新性**：将高级语义场景图引入序列视觉定位，区别于传统低层几何表示，思路新颖。
- **存储效率**：用粗网格+关系图代替稠密地图，显著降低内存占用，利于嵌入式/移动设备。
- **可扩展性**：粒子滤波框架天然支持多模态假设，且能随帧序列持续更新，符合在线定位需求。
- **开源复现**：提供代码，便于学界验证和扩展。

### 8. 不足与局限

- **实验细节缺失**：摘要未给出具体数据集、对比方法、误差指标和存储量数值，难以量化其声称的优势。
- **依赖语义质量**：方法依赖物体检测和逐块语义特征的准确性，在光照剧烈变化、动态物体、物体遮挡严重时可能退化。
- **场景图构建成本**：高质量的3D场景图（含物体网格和空间关系）本身需要预先构建，其离线构建代价未在摘要中讨论。
- **评估不充分**：没有显示与其他轻量级定位方法（如基于哈希的图像检索、稀疏特征SLAM）的公平比较，也没有长时间漂移分析。
- **应用限制**：当前面向室内物体级环境，对无结构室外场景或物体类别覆盖不足的场景可能不适用。

（完）
