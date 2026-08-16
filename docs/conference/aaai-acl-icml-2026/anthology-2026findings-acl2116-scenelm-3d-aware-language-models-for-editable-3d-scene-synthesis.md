---
title: "SceneLM: 3D-Aware Language Models for Editable 3D Scene Synthesis"
title_zh: SceneLM：面向可编辑3D场景合成的3D感知语言模型
authors: "Xingbo Yao, Xiaoyu Chen, Doudou Zhang, Mingzhi Sheng, Boyuan Cao, Ying-Cong Chen, Hui Xiong"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2116.pdf"
tags: ["query:d-slam"]
score: 7.0
evidence: 从单张RGB图像恢复可执行度量3D布局，用于可编辑3D场景合成
tldr: 从单张RGB图像合成可编辑3D场景对内容创作和AR/VR很重要，但现有几何管线难以交互编辑，LLM方法又缺少精确度量理解。SceneLM利用语言模型从图像直接恢复可执行的度量3D布局，将3D场景合成锚定在视觉证据上。该方法兼顾高保真重建与便捷交互编辑，为图像驱动的可编辑场景生成提供统一框架。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2116/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1635, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2116/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1652, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2116/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1629, \"height\": 906, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2116/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1663, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2116/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1664, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2116/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 835, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2116/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 181, \"label\": \"Table\"}]"
motivation: 现有3D场景合成管线要么难以编辑，要么缺乏来自图像的精确度量理解。
method: 用语言模型从单张RGB图像恢复可执行度量3D布局，实现视觉锚定的场景合成。
result: 同时实现高保真重建与便捷交互编辑的3D场景生成。
conclusion: 将3D布局恢复与语言模型结合，使场景合成更具可编辑性和视觉一致性。
---

## Abstract
Synthesizing an editable 3D scene from a single RGB image is central to content creation, embodied-agent data generation, and AR/VR, yet remains challenging to achieve both high-fidelity reconstruction and convenient interactive editing. Existing geometry-based pipelines produce high-quality 3D results but are typically hard to refine without rerunning the full process, while LLM-driven procedural systems enable interactive tool use but are mostly text-driven and lack precise metric 3D understanding from images. We present SceneLM, a language-model-based framework that grounds 3D scene synthesis in visual evidence by recovering an executable metric 3D layout directly from a single image. Given an RGB image (and camera intrinsics when available), SceneLM outputs a JSON-form layout specifying each object’s category, 3D center, size, and discretized yaw, and then deterministically executes this layout with a tool suite to instantiate, place, and edit objects for iterative refinement. To train metric layout recovery at scale, we curate five datasets covering diverse indoor, outdoor, and tabletop scenes and convert heterogeneous 3D annotations into a unified instruction-tuning format. To improve numerical stability and metric accuracy while preserving the text interface, we augment autoregressive JSON generation with a lightweight geometry prediction branch and dual supervision. Experiments show that SceneLM substantially improves single-image 3D layout estimation over strong open and proprietary MLLM baselines, and yields higher-quality end-to-end scene generation in geometric consistency, physical plausibility, semantic alignment, and realism.

---

## 论文详细总结（自动生成）

## 论文详细总结

### 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：如何从**单张RGB图像**出发，合成**高保真且可交互编辑**的3D场景。
- **现有方法的困境**：
  - **基于几何的方法**（如布局引导生成、场景图控制、3D高斯泼溅等）：能产出高质量3D结果，但**难以编辑**，任何修正都需要重跑整个流程。
  - **LLM/VLM驱动的程序化方法**：支持语言交互和工具调用，但**主要基于文本驱动**，语言固有的歧义性使其难以指定唯一的、精确的度量布局，且普遍缺乏从图像中恢复**度量级3D几何**的能力。
- **关键差距**：当前VLM虽能进行对话式3D定位（如“左侧”“附近”等相对关系），但**不足以支撑可执行的场景构建**——这需要精确的物体中心、尺寸和朝向。
- **本文目标**：通过语言模型直接**从图像恢复可执行的度量3D布局**，将3D场景合成锚定在视觉证据上，从而兼顾高保真重建与便捷交互编辑。

### 2. 方法论

**核心思想**：SceneLM 是一个基于语言模型的框架，将单图像3D场景合成解耦为**两个阶段**：①度量3D布局估计（图像→JSON布局）；②工具化场景合成与编辑（JSON布局→可编辑3D场景）。

**关键技术细节**：

- **任务形式化**：给定RGB图像 I 和相机内参 K，模型输出一个JSON格式的3D布局 L，其中每个物体包含：
  - `class`：语义类别
  - `center ∈ R³`：3D框中心（毫米）
  - `size ∈ R³`：3D框尺寸（毫米）
  - `yaw_bin`：离散化的偏航角（15°/bin，共24类）
  - 布局 L 随后通过工具套件 T 确定性执行，生成可编辑的3D场景 S = T(L)。
- **模型架构**（如图2b所示）：
  - **视觉编码器**：SigLIP-2 ViT 将图像编码为patch特征，经轻量投影器压缩为视觉token；
  - **LLM解码**：视觉token与文本提示拼接，由 Qwen-2B 语言模型自回归解码为JSON布局；
  - **几何头（GeomHead）**：在LLM最后一层隐藏状态上附加一个轻量MLP，对每个物体直接回归 center/size（Huber损失）并对 yaw_bin 进行分类（交叉熵损失）；
  - **双重监督**：总损失 L = L_CE + λ·L_geom，其中 L_CE 是标准自回归交叉熵，用于保证JSON语法有效；L_geom 是几何损失，用于强化度量精度。λ = 0.5。
- **数据结构与训练格式**：
  - 所有3D标注统一为“图像 + 相机内参 + 每物体度量3D框”；
  - 序列化为 LLaMAFactory 消息格式，度量值编码为整数毫米（避免浮点数伪影）；
  - yaw 离散化为24个bin（15°/bin），避免连续角度回归在自回归解码中的不稳定性。
- **工具化场景合成管线**（如图2d–e所示）：
  - 将资产创建与场景组装**解耦**；
  - 对每个物体，先用外部生成器（如Hunyuan3D）生成规范化3D资产，再根据布局施加度量变换（中心、尺寸、朝向）；
  - 提供 `add_object`、`set_transform`、`remove_object`、`replace_object`、`query_scene`、`export_scene` 等工具，支持**显式的迭代式编辑**，无需重跑整个生成流程。

### 3. 实验设计

- **数据集**：整合了五个异构数据集，涵盖室内、室外和桌面场景：
  - **Omni3D**（室内外通用3D检测）
  - **SUN RGB-D**（室内RGB-D场景理解）
  - **ARKitScenes**（移动RGB-D室内场景）
  - **Hypersim**（室内合成场景）——原PDF中未将Hypersim单列，可能为笔误？但正文明确列出Hypersim，故保留
  - **KITTI**（室外驾驶场景）
  - **Objectron**（多物体桌面场景）
  - 全部转换为统一的指令微调格式。

  > 注：五个数据集在原文表述为 indoor (Omni3D, SUN RGB-D, ARKitScenes, Hypersim)、outdoor (KITTI)、tabletop (Objectron)，其中描述为五个数据集但列出了六个名称，原文可能存在笔误。

- **Benchmark 1：单图像3D布局估计**
  - 评估指标：F1@IoU_3D=0.25 和 F1@IoU_3D=0.5（采用与 SpatialLM 一致的3D IoU 定义和一一匹配策略）；
  - 测试集：从五个基准数据集的测试集统一采样1000张图像；
  - 对比方法：Qwen3-VL-Instruct（2B/8B/30B-A3B三种规模，提示词输出相同JSON格式）、GPT-5.2（100张子集）、Gemini 3 Pro（100张子集）。
- **Benchmark 2：单图像3D场景生成（端到端）**
  - 评估指标：Volumetric IoU（几何一致性↑）、Collided Pairs（物理合理性↓）、CLIP Score（语义对齐↑）、FID（真实感↓）；
  - 对比方法：SceneGen（前馈式单图像3D场景生成模型）、Qwen3-VL-30B-A3B-Instruct + 相同工具链执行。
- **消融实验**：
  - 移除 GeomHead + 双重监督；
  - 禁用 yaw_bin（24分类）；
  - 对比纯 Qwen3-VL-2B + JSON CE（仅语言监督）；
  - 对比 LoRA 微调与全参数微调。

### 4. 资源与算力

- **GPU**：4× NVIDIA A800（80GB）
- **精度**：BF16
- **训练轮数**：20 epochs
- **最大序列长度**：2048
- **微批大小**：1，梯度累积步数16
- **总batch size**：隐含为 4×16 = 64（以micro-batch 1计）
- **模型规模**：以 Qwen3-VL-2B-Instruct 为基座，参数量约2B
- **训练框架**：基于 LLaMAFactory 数据格式构建指令微调样本
- **说明**：论文未披露具体训练时长（小时数）、总FLOPs或数据量（样本总数），也未报告推理延迟。

### 5. 实验数量与充分性

- **实验组数**：约5组核心实验，包含——
  1. 单图像3D布局估计（对比5个基线，含开源和闭源模型）；
  2. 端到端单图像3D场景生成（对比2个基线，4项指标）；
  3. 消融实验（GeomHead/双重监督、yaw_bin离散化）；
  4. 全参数微调 vs LoRA 对比；
  5. 定性可视化比较（室内/室外/桌面场景）。
- **充分性与客观性评估**：
  - **优点**：消融设计紧扣核心组件，验证了每个设计决策的必要性；对比基线涵盖不同规模开源模型和闭源商业模型，具有代表性；端到端评价指标覆盖面广（几何、物理、语义、真实感四个维度）。
  - **不足**：
    - 闭源模型（GPT-5.2、Gemini 3 Pro）仅用100张图像评估，数据量偏小，且未报告方差/置信区间；
    - 仅报告平均指标，未按场景类型（室内/室外/桌面）分类报告，无法判断方法在不同领域的鲁棒性；
    - 未报告与最新几何重建方法（如WonderWorld、ScenePainter等）的直接定量对比；
    - 消融实验仅在单一测试集上报告聚合结果，缺少分数据集或分阈值下的细粒度分析。

### 6. 主要结论与发现

- SceneLM **以2B参数量超越了30B级开源MLLM和专有闭源MLLM**，在F1@IoU_3D=0.25上达58.5（相比Qwen3-VL-30B的41.5提升17个百分点；相比GPT-5.2的47.3提升11个百分点），在F1@IoU_3D=0.5上达36.1（相比GPT-5.2的29.2与Gemini的22.3均有显著优势）；
- **仅扩大模型规模并不能解决精确3D度量恢复**：Qwen3-VL从2B扩到30B，F1@0.25只从18.2提升到41.5，而F1@0.5提升有限（12.4→23.6）；表明纯自回归JSON监督无法可靠地约束精确几何；
- **几何头与双重监督带来显著增益**：移除GeomHead后F1@0.25从58.5降至47.6，F1@0.5从36.1降至28.4，说明该组件对高精度度量定位至关重要；
- **yaw离散化是必要的**：禁用yaw_bin后F1@0.5降至25.1，表明朝向是纯自回归JSON学习下的主要失败模式，24向分类提供了更稳定的监督信号；
- **端到端场景生成质量全面领先**：SceneLM将Volumetric IoU从SceneGen的0.35/Qwen30B+工具的0.39提升至0.53，CLIP Score达0.85，FID仅20.8，优于所有基线；
- **完整场景重建vs低碰撞率的权衡**：SceneGen碰撞率最低（0.23）但原因在于它漏检了较多小物体、场景稀疏；SceneLM在重建更完整场景的情况下仍保持低碰撞率（0.37），物理合理性更强；
- **全参数微调优于LoRA**：全微调在F1@0.25（58.5 vs 51.3）和F1@0.5（36.1 vs 32.7）上均更优，说明精确度量3D布局预测受益于全模型容量更新。

### 7. 优点

- **问题定位精准**：准确识别了“几何管线不可编辑”与“LLM管线缺乏度量3D理解”这一核心矛盾，并提出统一框架解决；
- **视觉锚定设计**：以图像为输入直接恢复度量布局，有效缓解文本驱动方法中语言歧义带来的布局不确定性；
- **可编辑性为第一公民**：通过工具套件将布局与执行解耦，支持细粒度、显式的迭代编辑和局部修正，不须重跑完整流程；
- **几何头+双重监督的设计精巧**：在不改变文本推理接口的前提下，显式约束数值稳定性与度量精度，兼顾了语言模型的通用性与3D任务的特殊性；
- **数据统一化策略**：将六个异构数据集（涵盖室内/室外/桌面）统一到指令微调格式，具备良好的可扩展性，为后续研究降低了数据门槛；
- **框架模块化**：资产生成、场景组装、布局预测、工具执行各环节解耦，便于替换升级单个组件；
- **实验设计相对规范**：消融实验逐一验证了各设计选择；与不同规模基线对比，结论具有说服力。

### 8. 不足与局限

- **对相机内参的依赖**：SceneLM依赖相机内参恢复度量布局；当内参不可用而使用默认参数时，可能引入绝对尺度和物体尺寸的偏差；
- **外部资产质量瓶颈**：最终场景质量受限于外部资产生成器（如Hunyuan3D）的资产保真度、尺度对齐和碰撞处理能力，模型本身无法控制这些外部因素；
- **复杂场景下输出可能不完整**：在复杂场景中，模型仍可能输出无效或不完整的JSON，影响下游执行；
- **闭源基线评估规模有限**：GPT-5.2和Gemini 3 Pro仅在100张图像上评估，且无方差报告，统计显著性存疑；
- **未报告按场景类型的分解结果**：无法判断模型在室内、室外、桌面三类场景上的各自表现差异和潜在短板；
- **缺少用户研究或交互式编辑评估**：论文声称支持交互编辑，但未对编辑体验（如操作延迟、用户满意度）进行定量或定性的用户研究；
- **与图像仅单视角相关性的固有限制**：单视图恢复3D布局本质上存在深度歧义，虽然在多个数据集上表现良好，但极端情况下（如遮挡严重、罕见视角）的鲁棒性未充分测试；
- **训练细节披露有限**：未报告数据量、训练时长、收敛曲线等关键信息，复现成本较高。

---

（完）
