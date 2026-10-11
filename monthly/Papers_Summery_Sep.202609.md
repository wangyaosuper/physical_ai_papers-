# Physical AI 论文分类 Summery(2026 年 9 月)
> 9月物理AI方面热门论文阅读小结

---

## 1. 世界模型对几何表征的理解

**背景说明**: 传统世界模型多基于像素或潜空间推理,缺乏显式的三维几何结构信息,导致长程一致性差、物理幻觉严重。以下论文从不同路径强化世界模型对几何表征的理解。

- **[GeoWorldAD: Geometry World Action Model for Autonomous Driving](https://arxiv.org/html/2607.17521v2)** 🔥热度:24  
  基于自车对齐(Ego-aligned)的4D时空几何表示,通过几何世界模型预测潜在未来几何Token,并采用迭代轨迹细化机制渐进式融合多尺度当前几何与未来几何,使自动驾驶规划建立在显式3D几何可解释性之上。

- **[HyWorldVLA: A Vision-Language-Action Model with Hybrid World Modeling for Autonomous Driving](https://arxiv.org/html/2607.20988v1)** 🔥热度:27  
  提出混合世界模型架构,预训练阶段通过"双向锚定"同时预测潜在特征并重建像素画面,让潜空间被像素级几何约束锚定,微调阶段再瘦身专注潜在特征预测,兼顾几何物理约束与抗噪声鲁棒性。
  
- **[Code World Model: Coding Agent as World Brain](https://arxiv.org/html/2608.25927v1)** 🔥热度:115  
  通过LLM Coding Agent生成可执行代码维护持久世界状态,以Proxy Interface将代码状态转化为帧级时空约束(实体边界框、动作轨迹、相机视角),从符号逻辑层面为世界模型注入显式几何表征,彻底摆脱纯像素推理的几何幻觉。

**整体对比**: 三者分别从"显式4D几何空间"、"像素+潜空间混合几何”、"代码逻辑几何"三条不同路径强化世界模型的几何表征理解,共同推动世界模型从"像素黑盒"走向"几何可解释"。

---

## 2. 世界模型和高斯泼溅的结合

**背景说明**: 3D高斯泼溅(3DGS)为世界模型提供了显式的几何载体,以下论文探索世界模型与高斯泼溅结合的不同范式。

- **[4DGS-WAM: Bridging Past and Future with an Object-Centric World Action Model based on 4D Gaussian Splatting](https://arxiv.org/pdf/2608.25956)** 🔥热度:20  
  将世界拆分为静态背景与动态物体,用持久化4D高斯进行高精表征,策略网络预测动态物体SE(3)刚体动作、世界模型预测高斯基元非刚体微调,实现具有完整三维几何信息的世界动作预测。

- **[GaussianDWM++: Language-Grounded 3D Gaussian Driving World Model for Unified Scene Understanding, Editing, and Multi-Modal Generation](https://arxiv.org/html/2608.16234v1)** 🔥热度:17  
  首次将基础多模态特征直接嵌入显式3D高斯基元,通过基础特征高斯分词器构建开放词汇高斯语义场,实现"图像观察-语言语义-3D空间几何"三者紧密对齐,支持统一场景理解、编辑与多模态生成。

**整体对比**: 4DGS-WAM侧重"动静态解耦+刚体动作预测",GaussianDWM++侧重"语言语义嵌入高斯+场景理解编辑",前者以3D高斯为载体分别从"动作预测"和"语义理解"两个维度拓展世界模型能力。

---

## 3. 强化学习在自动驾驶和具身智能方面的运用

**背景说明**: 强化学习为自动驾驶和具身智能提供了超越模仿学习上限的潜力,以下论文在RL与世界模型结合、闭环训练等方面进行创新。

- **[DriveZero: End-to-End Driving Beyond Human Demonstrations](https://arxiv.org/html/2609.06055v1)** 🔥热度:23  
  完全摆脱人类驾驶轨迹依赖,通过特权Teacher策略在混合Agent交互世界中进行PPO闭环强化学习,再蒸馏为纯视觉端到端Planner,实现超越人类示范的自动驾驶能力。

- **[Q-Learning With World Models](https://arxiv.org/html/2608.17163v1)** 🔥热度:104  
  将世界模型从训练循环中剥离,仅作为Q-learning推理时的短视野树搜索工具,策略和价值函数仅在真实环境转移上训练,从根本上避免模型偏差复合累积。

- **[Motus2: A Self-Evolving General World Model for Dexterous Manipulation](https://arxiv.org/pdf/2608.30237)** 🔥热度:113  
  将"策略→模拟→评估器"三个角色统一到一个共享参数集的通用世界模型中,通过特殊因果掩码和接口设计让其同时胜任三角色,形成"提出动作→预测后果→评估选择"的完整闭环,实现无需真实交互的Model-Based RL。

**整体对比**: DriveZero面向自动驾驶侧重"超越人类示范的闭环RL+蒸馏",QWM侧重"世界模型作为推理时搜索插件避免偏差复合",Motus2侧重"三位一体通用世界模型Model-Based的闭环自进化",三者分别从"数据来源"、"模型用法"、"架构统一"三个维度创新RL在自动驾驶和具身智能中的运用。

---

## 4. 用视觉预测来指导动作规划 vs 用动作规划来指导视觉预测

**背景说明**: 视觉预测与规划动作之间存在双向牵引关系,以下论文从"视觉预测指导动作"和"动作牵引视觉预测"两个方向展开探索。

- **[Hydra-0: Action Flow for Generalist World Modeling and Control](https://arxiv.org/html/2608.18077v1)** 🔥热度:120  
  将机器人物理动作统一转化为像素空间的"动作流(Action Flow)",以动作流预测周围环境动态变化来指导规划,同时涌现出逆向世界动作模型能力——输入期望物体运动轨迹反向预测机器人动作。

- **[Motus2: A Self-Evolving General World Model for Dexterous Manipulation](https://arxiv.org/pdf/2608.30237)** 🔥热度:113  
  三位一体架构中策略角色提出动作、模拟角色预测视觉后果、评估器角色评估选择,形成"动作牵引视觉预测→视觉预测反馈动作选择"的闭环,实现规划动作与视觉预测互为牵引。

**整体对比**: Hydra-0代表"视觉预测(动作流)指导规划动作"的正向路径,Motus2代表"规划动作牵引视觉预测再反馈动作"的闭环路径,两者从不同方向探索视觉预测与规划动作的相互牵引关系。

---

## 5. 把语言融入到世界模型中

**背景说明**: 语言为世界模型提供了逻辑推理和语义理解能力,以下论文探索语言融入世界模型的不同方式。

- **[Code World Model: Coding Agent as World Brain](https://arxiv.org/html/2608.25927v1)** 🔥热度:115  
  以LLM Coding Agent作为"世界大脑"负责推理逻辑、理解规则并生成可执行代码维护持久世界状态,将自然语言指令通过代码转化为结构化时空约束,实现语言对世界运行的深度融入。

- **[Plug-and-Play Traffic Element Awareness for End-to-End Autonomous Driving](https://arxiv.org/html/2608.18035v1)** 🔥热度:19  
  通过语言风格嵌入(Language-style embeddings)编码车道与信号灯的拓扑映射关系,将交通元素的语义规则直接引导轨迹解码,实现物理感知与规则约束的融合。

**整体对比**: Code World Model将语言作为"世界运行逻辑"深度融入世界模型运行机制,Plug-and-Play将语言作为"拓扑规则约束"融入自动驾驶感知增强,前者从架构层面、后者从特征层面实现语言对世界模型的融入。

---

## 6. 时序记忆方面的优化

**背景说明**: 时序记忆是端到端自动驾驶模型处理长时序场景的关键,以下论文在记忆的有效性和时效性方面进行优化。

- **[MomADv2: Reliable Temporal Memory for End-to-End Autonomous Driving](https://arxiv.org/html/2608.23405v1)** 🔥热度:18  
  采取选择性状态空间规划记忆查询技术,基于"时序连续性"和"指令一致性"对历史规划查询进行过滤,只检索与当前驾驶指令匹配的历史信息,并通过流匹配轨迹残差优化器进行细粒度轨迹微调。

**整体对比**: MomADv2通过"选择性记忆查询+残差优化"双机制解决历史记忆与当前意图冲突问题,在保证记忆有效性的同时抑制失效记忆干扰。

---

## 7. 真实城市环境下Agent空间理解能力的实测

**背景说明**: 多模态大模型在真实城市物理环境中的空间代理能力缺乏标准化评估,以下论文构建了真实城市沙盒进行实测。

- **[UrbanGround: From Local Perception to Spatial Agency in a Real-Scale City](https://arxiv.org/html/2608.27456v1)** 🔥热度:30  
  基于真实香港三维地理数据构建城市智能体沙盒,系统性评估多模态大语言模型在长程导航、方向保持及动态环境交互等空间代理核心维度的能力,揭示当前模型在真实城市空间理解上的结构性缺陷。

**整体对比**: UrbanGround填补了真实城市物理环境下Agent空间代理能力评估的空白,为多模态大模型的空间理解能力提供了标准化实测基准。

---

## 小结

<style>
.paper-table {
  border-collapse: collapse;
  width: 100%;
}
.paper-table th,
.paper-table td {
  border: 1px solid #999;
  padding: 6px 12px;
}
</style>

<table class="paper-table">
  <thead>
    <tr>
      <th>大类</th>
      <th>论文名称</th>
      <th>链接</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="3">1. 加强世界模型对几何表征的理解</td>
      <td>Code World Model: Coding Agent as World Brain</td>
      <td><a href="https://arxiv.org/html/2608.25927v1">arXiv</a></td>
    </tr>
    <tr>
      <td>GeoWorldAD: Geometry World Action Model for Autonomous Driving</td>
      <td><a href="https://arxiv.org/html/2607.17521v2">arXiv</a></td>
    </tr>
    <tr>
      <td>HyWorldVLA: A Vision-Language-Action Model with Hybrid World Modeling for Autonomous Driving</td>
      <td><a href="https://arxiv.org/html/2607.20988v1">arXiv</a></td>
    </tr>
    <tr>
      <td rowspan="2">2. 世界模型和高斯泼溅的结合</td>
      <td>4DGS-WAM: Bridging Past and Future with an Object-Centric World Action Model based on 4D Gaussian Splatting</td>
      <td><a href="https://arxiv.org/pdf/2608.25956">arXiv</a></td>
    </tr>
    <tr>
      <td>GaussianDWM++: Language-Grounded 3D Gaussian Driving World Model for Unified Scene Understanding, Editing, and Multi-Modal Generation</td>
      <td><a href="https://arxiv.org/html/2608.16234v1">arXiv</a></td>
    </tr>
    <tr>
      <td rowspan="3">3. 强化学习在自动驾驶和具身智能方面的运用</td>
      <td>DriveZero: End-to-End Driving Beyond Human Demonstrations</td>
      <td><a href="https://arxiv.org/html/2609.06055v1">arXiv</a></td>
    </tr>
    <tr>
      <td>Q-Learning With World Models</td>
      <td><a href="https://arxiv.org/html/2608.17163v1">arXiv</a></td>
    </tr>
    <tr>
      <td>Motus2: A Self-Evolving General World Model for Dexterous Manipulation</td>
      <td><a href="https://arxiv.org/pdf/2608.30237">arXiv</a></td>
    </tr>
    <tr>
      <td rowspan="2">4. 用视觉预测来指导规划动作 vs 用规划动作来牵引视觉预测</td>
      <td>Hydra-0: Action Flow for Generalist World Modeling and Control</td>
      <td><a href="https://arxiv.org/html/2608.18077v1">arXiv</a></td>
    </tr>
    <tr>
      <td>Motus2: A Self-Evolving General World Model for Dexterous Manipulation</td>
      <td><a href="https://arxiv.org/pdf/2608.30237">arXiv</a></td>
    </tr>
    <tr>
      <td rowspan="2">5. 把语言融入到世界模型中</td>
      <td>Code World Model: Coding Agent as World Brain</td>
      <td><a href="https://arxiv.org/html/2608.25927v1">arXiv</a></td>
    </tr>
    <tr>
      <td>Plug-and-Play Traffic Element Awareness for End-to-End Autonomous Driving</td>
      <td><a href="https://arxiv.org/html/2608.18035v1">arXiv</a></td>
    </tr>
    <tr>
      <td>6. 时序记忆方面的优化</td>
      <td>MomADv2: Reliable Temporal Memory for End-to-End Autonomous Driving</td>
      <td><a href="https://arxiv.org/html/2608.23405v1">arXiv</a></td>
    </tr>
    <tr>
      <td>7. 真实城市环境下Agent空间理解能力的实测</td>
      <td>UrbanGround: From Local Perception to Spatial Agency in a Real-Scale City</td>
      <td><a href="https://arxiv.org/html/2608.27456v1">arXiv</a></td>
    </tr>
  </tbody>
</table>

