# Physical AI 论文分类 Summery(2026 年 8 月)
> 8月物理AI方面热门论文阅读小结

---

## 1. JEPA 在智驾和具身领域的优化

**背景说明**：JEPA 是通用世界模型，直接用于智驾和具身需要进行适配，以下论文在这些方面进行了创新。

- **[DA-WAM: Decision-Aligned Future Latents for Driving World Models](https://arxiv.org/html/2608.19085v2)**  
通过「LoRA 适配 V-JEPA 双塔 + 全程持续 JEPA 预测监督」让未来潜变量空间随规划目标协同进化，并为每条轨迹候选生成独立专属的未来潜变量参与打分，从机制上解决「预测得好 ≠ 决策得好」的脱节问题。

- **[WA-JEPA: Rethinking the Video JEPA Paradigm for World-Action Modeling in Autonomous Driving](https://arxiv.org/html/2608.20974v1)**  
对 V-JEPA 进行驾驶范式重塑:重新设计训练阶段的画面掩码策略、引入条件流匹配的隐空间预测形式、对未来场景与自车轨迹进行联合预测，首次证明纯视觉 JEPA 可被改造为强大的因果动作预测器。

- **[Is Forward Prediction Enough? Physical State Grounding for JEPA World Models](https://arxiv.org/html/2608.06799v1)**  
在 JEPA 隐变量上增加两个输出「机器人本体状态」和「状态变化」的辅助 Head，训练时将潜在表征显式锚定到物理状态、推理时去掉 Head，实现零推理开销下显著提升表征的物理可辨识性与策略性能。

---

## 2. Flow Matching 在智驾和具身上的运用

**背景说明**：Flow Matching 是近期相当热门的世界模型技术流派，以下论文在该方向上进行了创新。

- **[SimWAM: A Simple World Action Model for End-to-End Autonomous Driving](https://arxiv.org/abs/2608.07468)**  
采用「视频专家 + 动作专家」双专家架构下的联合流匹配(Joint Flow Matching)，以隔离注意力掩码让视频预测任务在训练时把交通动态先验传递给轻量动作专家，推理时无需生成任何未来帧即可直接输出轨迹。

- **[WA-JEPA: Rethinking the Video JEPA Paradigm for World-Action Modeling in Autonomous Driving](https://arxiv.org/html/2608.20974v1)**  
将条件流匹配(Conditional Flow Matching)引入 JEPA 隐空间，以概率流形式对未来场景和自车轨迹做联合建模，让表征学习更聚焦于驾驶的本质特征。

- **[XCoT-VLA: Executable Chain-of-Thought for Vision-Language-Action Driving](https://arxiv.org/abs/2608.10976)**  
用 2-3 个 Token 的标准化可执行符号链完成推理后，由 Control FFN 以流匹配(Flow Matching)直接并行预测未来 6 秒连续轨迹，兼顾推理效率与轨迹生成质量。

---

## 3. 传统扩散技术方面的持续创新

**背景说明**：传统扩散技术(如 VAE 等)还在持续创新，以Flex-π为代表：

- **[Flex-π: A Multi-Stream World-Action Model with Compute Flexibility](https://arxiv.org/abs/2608.10860)**  
基于 VAE 共享潜在空间，将 RGB、3D 点云图、DINO 语义特征编码为多 token 流送入 MoE Transformer 联合去噪，并通过「流式丢弃 + 跨模态强制」实现单模型从「极速」到「高精度」的灵活推理，几乎零成本注入 3D 几何与语义信息。

---

## 4. VLA 与 WM 融合

**背景说明**：VLA 和 WM 在不断走向融合，以下论文在这方面进行了创新。

- **[World Tokens: Enhancing Embodied Policies with Training-Time World Modeling](https://arxiv.org/html/2608.09730v1)**  
训练时将 VLM 与 WM 联合训练并对齐「未来动作的语言描述」与「未来视频生成」两种能力，推理时去掉 WM 只保留 VLM，使其免费获得物理直觉并提升动作精确度。

- **[BrainWAM: Action-Space Coordination of Semantic Priors and Predictive Dynamics for Autonomous Driving](https://arxiv.org/html/2608.12854v1)**  
仿生「左右脑」设计，让 VLA(语义先验)与 WAM(预测动态)共存于一个模型，并通过类胼胝体的 CAB 桥接模块在动作空间协调两者，实现语义与动态先验的深度融合。

- **[WAM-Diff2: Hierarchical AR-to-Diffusion Distillation for Highly Efficient Autonomous Driving VLA](https://arxiv.org/html/2608.01035v4)**  
通过「渐进式块级适配 → 块级蒸馏 → 模型级跨尺度蒸馏」三阶段分层蒸馏，把 8B 自回归教师的因果语义理解能力注入 2B 扩散模型，以极小参数量兼得 AR 推理与 Diffusion 生成质量。

---

## 5. VLA/VLM 在智驾和具身上的运用

**背景说明**：VLA/VLM 计算量较大、特征表征相对稀疏，在智驾和具身上运用需要持续优化，以下论文在这方面进行了创新。

- **[XCoT-VLA: Executable Chain-of-Thought for Vision-Language-Action Driving](https://arxiv.org/abs/2608.10976)**  
抛弃大段自然语言，把驾驶决策压缩成两三个 Token 的标准化动作符号(如 LEFT_TURN_PREPARE → DECELERATE → RED_LIGHT_HOLD)，以「共享多模态自注意力 + 双 FFN」结构大幅压缩推理算力，并用实车日志自动构建数十万条 XCoT 训练数据。

- **[Multi-View Relational Distillation for Spatial Reasoning with Vision-Language Models](https://arxiv.org/html/2608.10864v1)**  
发现 VLM 无需直接学习多视角图像特征，只需在张量空间中蒸馏不同视角图像间的余弦相似度，即可用极低算力成本自然习得多视角空间几何关系。

- **[TurboVLA: Real-Time Vision-Language-Action Model at 32 Hz on an RTX 4090 with <1 GB VRAM](https://arxiv.org/abs/2607.27205)**  
以精简双向交叉注意力摆脱大语言模型基座依赖，并行解码直接输出动作序列，仅 0.5B 参数、<1 GB 显存即在 RTX 4090 上实现 32 Hz 实时具身推理。

---

## 6. Agent 技术在模型测试评估方面的运用

**背景说明**：Agent 和 Harness 技术大量运用，提升训练和测试工程效率，以下论文在这方面进行了创新。

- **[HarnessEval-W: Agentifying the Evaluation of Visual Worlds](https://arxiv.org/html/2608.16859v1)**  
将世界模型评估 Agent 化:先做场景解析与任务分解，再为每个子问题派生配备专属诊断工具的子智能体分工推理，最终由父智能体汇总为可解释、有完整证据链支撑的「证据树」评判结果。

- **[PlayWorld: Benchmarking World Models with Agent Players over Long-Horizon Objectives](https://arxiv.org/html/2608.13552v1)**  
让多模态 Agent 以「玩游戏」的方式(W/A/S/D、↑/↓/←/→、WAIT)在被测世界模型中长期交互探索，像人类玩家一样品鉴世界模型在长时程目标下的逼真度与质量，突破固定测试用例的局限。

---

## 7. 具身智能综述性优秀论文一篇

- **[Data Pyramid for Embodied Manipulation: A Survey](https://arxiv.org/abs/2607.24744)**  
首次提出「数据金字塔」概念，对高度碎片化的具身操作数据生态进行完整的层级化梳理，并分析不同层级数据如何驱动下一代具身基础模型，是快速定位数据缺口、选择数据集与设计数据策略的纲领性文献。

---

## 总表

<table>
  <thead>
    <tr>
      <th>大类</th>
      <th>论文名称</th>
      <th>链接</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="3">1. JEPA 在智驾和具身领域的优化</td>
      <td>DA-WAM: Decision-Aligned Future Latents for Driving World Models</td>
      <td><a href="https://arxiv.org/html/2608.19085v2">arXiv</a></td>
    </tr>
    <tr>
      <td>WA-JEPA: Rethinking the Video JEPA Paradigm for World-Action Modeling in Autonomous Driving</td>
      <td><a href="https://arxiv.org/html/2608.20974v1">arXiv</a></td>
    </tr>
    <tr>
      <td>Is Forward Prediction Enough? Physical State Grounding for JEPA World Models</td>
      <td><a href="https://arxiv.org/html/2608.06799v1">arXiv</a></td>
    </tr>
    <tr>
      <td rowspan="3">2. Flow Matching 在智驾和具身上的运用</td>
      <td>SimWAM: A Simple World Action Model for End-to-End Autonomous Driving</td>
      <td><a href="https://arxiv.org/abs/2608.07468">arXiv</a></td>
    </tr>
    <tr>
      <td>WA-JEPA: Rethinking the Video JEPA Paradigm for World-Action Modeling in Autonomous Driving</td>
      <td><a href="https://arxiv.org/html/2608.20974v1">arXiv</a></td>
    </tr>
    <tr>
      <td>XCoT-VLA: Executable Chain-of-Thought for Vision-Language-Action Driving</td>
      <td><a href="https://arxiv.org/abs/2608.10976">arXiv</a></td>
    </tr>
    <tr>
      <td>3. 传统扩散技术方面的持续创新</td>
      <td>Flex-π: A Multi-Stream World-Action Model with Compute Flexibility</td>
      <td><a href="https://arxiv.org/abs/2608.10860">arXiv</a></td>
    </tr>
    <tr>
      <td rowspan="3">4. VLA 与 WM 融合</td>
      <td>World Tokens: Enhancing Embodied Policies with Training-Time World Modeling</td>
      <td><a href="https://arxiv.org/html/2608.09730v1">arXiv</a></td>
    </tr>
    <tr>
      <td>BrainWAM: Action-Space Coordination of Semantic Priors and Predictive Dynamics for Autonomous Driving</td>
      <td><a href="https://arxiv.org/html/2608.12854v1">arXiv</a></td>
    </tr>
    <tr>
      <td>WAM-Diff2: Hierarchical AR-to-Diffusion Distillation for Highly Efficient Autonomous Driving VLA</td>
      <td><a href="https://arxiv.org/html/2608.01035v4">arXiv</a></td>
    </tr>
    <tr>
      <td rowspan="3">5. VLA/VLM 在智驾和具身上的运用</td>
      <td>XCoT-VLA: Executable Chain-of-Thought for Vision-Language-Action Driving</td>
      <td><a href="https://arxiv.org/abs/2608.10976">arXiv</a></td>
    </tr>
    <tr>
      <td>Multi-View Relational Distillation for Spatial Reasoning with Vision-Language Models</td>
      <td><a href="https://arxiv.org/html/2608.10864v1">arXiv</a></td>
    </tr>
    <tr>
      <td>TurboVLA: Real-Time Vision-Language-Action Model at 32 Hz on an RTX 4090 with &lt;1 GB VRAM</td>
      <td><a href="https://arxiv.org/abs/2607.27205">arXiv</a></td>
    </tr>
    <tr>
      <td rowspan="2">6. Agent 技术在模型测试评估方面的运用</td>
      <td>HarnessEval-W: Agentifying the Evaluation of Visual Worlds</td>
      <td><a href="https://arxiv.org/html/2608.16859v1">arXiv</a></td>
    </tr>
    <tr>
      <td>PlayWorld: Benchmarking World Models with Agent Players over Long-Horizon Objectives</td>
      <td><a href="https://arxiv.org/html/2608.13552v1">arXiv</a></td>
    </tr>
    <tr>
      <td>7. 具身智能系统性综述(压轴)</td>
      <td>Data Pyramid for Embodied Manipulation: A Survey</td>
      <td><a href="https://arxiv.org/abs/2607.24744">arXiv</a></td>
    </tr>
  </tbody>
</table>

> 注:WA-JEPA 和 XCoT-VLA 各横跨两个类别(分别体现了 JEPA 与 Flow Matching、Flow Matching 与 VLA 优化的交叉创新)。
