# Awesome Physics + Generative AI

[🇺🇸 English](README.md)

一个面向生成式模型、物理推理、世界模拟和具身智能交叉方向的精选路线图。

**前沿判断，截至 2026-06-04。** 视频生成正在从“视觉上像真的开环合成”，转向“可交互、可评测、可用于 Physical AI 的世界模型”。但结论需要冷静：目前 benchmark 证据仍不足以说明前沿视频模型已经可靠学会物理定律；它们更像具备部分物理直觉的高维预测器，而不是可信物理引擎。

## 目录

- [速览](#速览)
- [筛选标准](#筛选标准)
- [精选工作](#精选工作)
  - [综述与定位](#综述与定位)
  - [视频与世界模拟器](#视频与世界模拟器)
  - [具身智能与机器人](#具身智能与机器人)
  - [物理感知训练与对齐](#物理感知训练与对齐)
  - [评测与诊断](#评测与诊断)
- [阅读路线](#阅读路线)
- [贡献方式](#贡献方式)

## 速览

| 方向 | 核心问题 | 代表工作 |
| --- | --- | --- |
| 视频到世界模拟器 | 视频模型能否维持状态、物体持久性和可信动力学？ | Sora, Sora 2, Genie 3, Cosmos 3 |
| 交互式模拟 | 生成世界能否在闭环中响应动作或 promptable events？ | Genie 3, Cosmos-Predict2.5 |
| 潜空间动力学 | 能否不生成每个像素，而是预测状态转移？ | V-JEPA 2 |
| 机器人应用 | 视频 / 世界模型能否用于规划、数据生成或策略评估？ | Veo-Act, RoboScape, Cosmos-Predict2.5 |
| 物理后训练 | 偏好数据和 continuation training 能否提升物理一致性？ | PhyWorld, NewtonGen |
| 物理评测 | 视觉真实是否等于物理理解？ | Physics-IQ, Morpheus, PhyGround |

## 筛选标准

本列表优先收录 physics 是核心 claim、方法或评测对象的工作：

- **状态与动力学：** 物体持久性、接触、材料变化、运动、守恒、因果关系和长时一致性。
- **动作条件 rollout：** 生成未来会响应用户、机器人、车辆或 agent 的动作。
- **Physical AI 落地：** 机器人、自动驾驶、合成数据、策略评估、闭环仿真或 failure-case generation。
- **面向物理定律的评测：** 不只评估美观度或时序平滑度，而是测试具体物理原则。

## 精选工作

### 综述与定位

| 工作 | 类型 | 为什么重要 |
| --- | --- | --- |
| [A Mechanistic View on Video Generation as World Models: State and Dynamics](https://arxiv.org/abs/2601.17067) | 综述 / taxonomy | 把领域归纳为 **state construction** 与 **dynamics modeling** 两个核心问题，并主张评测从视觉保真度转向物理持久性和因果推理。 |
| [Video generation models as world simulators](https://openai.com/index/video-generation-models-as-world-simulators/) | 技术报告 / 定位文章 | 将大型视频 diffusion transformer 作为通用物理世界模拟器的早期路线推到台前；同时明确记录了基础物理、物体状态变化和长时一致性上的失败模式。 |

### 视频与世界模拟器

| 工作 | 机构 | Physics / world-model 信号 | 备注 |
| --- | --- | --- | --- |
| [Sora 2](https://openai.com/index/sora-2/) | OpenAI | 强调更物理准确、更可控的视频生成、同步声音，以及能模拟失败，而不是通过不合理捷径满足 prompt。 | 产品页面显示 Sora 产品截至 2026-04-26 已不再可用，但该模型仍是重要路线节点。 |
| [Genie 3: A new frontier for world models](https://deepmind.google/blog/genie-3-a-new-frontier-for-world-models/) | Google DeepMind | 文本生成可交互动态世界，24 fps、720p，可在几分钟尺度保持一致性，并支持导航输入和 promptable world events。 | 关键意义是从视频片段生成转向 interaction loop；限制包括动作空间、多智能体交互、精确地理位置和连续交互时长。 |
| [Cosmos 3: Omnimodal World Models for Physical AI](https://arxiv.org/abs/2606.02800) | NVIDIA | 统一语言、图像、视频、音频和动作序列建模，服务于 Physical AI。 | 将 VLM、视频生成器、world simulator 和 world-action model 放进统一 omnimodal 框架，并开放代码、权重、数据和 benchmark。 |
| [World Simulation with Video Foundation Models for Physical AI](https://arxiv.org/abs/2511.00062) | NVIDIA | Cosmos-Predict2.5 统一 Text2World、Image2World 和 Video2World，并用 Cosmos-Reason1 做物理语义 grounding。 | 面向机器人和自动驾驶中的合成数据生成、策略评估和闭环仿真。 |

### 具身智能与机器人

| 工作 | 类型 | 物理 / 机器人角度 | 备注 |
| --- | --- | --- | --- |
| [Introducing the V-JEPA 2 world model and new benchmarks for physical reasoning](https://ai.meta.com/blog/v-jepa-2-world-model-benchmarks/) | 潜空间世界模型 | 不在像素空间生成视频，而是在 embedding space 预测，学习用于理解、预测和规划的状态表示与动力学。 | 对机器人规划尤其重要，因为它避开了完整像素生成的成本；Meta 报告其可用少量机器人数据进行 zero-shot planning/control。 |
| [Veo-Act: How Far Can Frontier Video Models Advance Generalizable Robot Manipulation?](https://arxiv.org/abs/2604.04502) | 机器人操作研究 | 用 Veo-3 想象机器人未来图像序列，再用 inverse dynamics model 反推出动作。 | 给出一个现实边界：前沿视频模型可产生任务级轨迹，但低层接触控制仍不可靠，因此更适合作为高层 planner，与机器人策略分工。 |
| [RoboScape: Physics-informed Embodied World Model](https://arxiv.org/abs/2506.23135) | 具身世界模型 | 通过 temporal depth prediction 和 keypoint dynamics learning 提升机器人视频生成中的 3D 一致性和运动建模。 | 展示了生成数据用于机器人策略训练和策略评估的下游价值。 |

### 物理感知训练与对齐

| 工作 | 方法 | 物理信号 | 备注 |
| --- | --- | --- | --- |
| [PhyWorld: Physics-Faithful World Model for Video Generation](https://arxiv.org/abs/2605.19242) | 两阶段 post-training | Flow matching fine-tuning 改善视频 continuation；基于 physics preference pairs 的 DPO 将生成动态对齐到更高物理 plausibility。 | 代表一种新配方：scale + physical preference data + per-law evaluation。 |
| [NewtonGen: Physics-Consistent and Controllable Text-to-Video Generation via Neural Newtonian Dynamics](https://arxiv.org/abs/2509.21309) | 神经动力学引导 | 将可训练 Neural Newtonian Dynamics 注入视频生成，提升可控牛顿运动的一致性。 | 相比纯靠视频数据 scale，这是一条更显式的 dynamics route。 |
| [BranchGRPO: Stable and Efficient GRPO with Structured Branching in Diffusion Models](https://arxiv.org/abs/2509.06040) | 相关偏好优化方法 | 本身不是 physics-specific，但作为高效 diffusion-model alignment 方法，可能服务于物理偏好优化。 | 除非结合物理奖励或 physics preference data，否则应与核心物理方法区分。 |

### 评测与诊断

| 工作 | 评测重点 | 核心结论 |
| --- | --- | --- |
| [Do generative video models understand physical principles?](https://arxiv.org/abs/2501.09038) | Physics-IQ：流体、光学、固体、磁学、热力学 | 视觉真实度与物理理解不强相关；当前模型整体仍很有限，虽然部分场景可被解决。 |
| [Morpheus: Benchmarking Physical Reasoning of Video Generative Models with Real Physical Experiments](https://arxiv.org/abs/2504.02918) | 真实物理实验和守恒律指标 | 即便使用高级 prompt 和视频条件，当前模型仍难以稳定编码物理原则。 |
| [PhyGround: Benchmarking Physical Reasoning in Generative World Models](https://arxiv.org/abs/2605.10806) | 覆盖 13 类物理定律的 criteria-grounded benchmark | 将评测从“看起来好不好”推进到“具体哪条物理规律错了”，并结合细粒度人工标注和物理专用 VLM judge。 |

## 阅读路线

1. 先读定位：[A Mechanistic View](https://arxiv.org/abs/2601.17067) 和 OpenAI 的 [Sora world-simulator report](https://openai.com/index/video-generation-models-as-world-simulators/)。
2. 再顺着 simulator 主线读：Sora 2 -> Genie 3 -> Cosmos 3 / Cosmos-Predict2.5。
3. 用 [V-JEPA 2](https://ai.meta.com/blog/v-jepa-2-world-model-benchmarks/) 对比 latent-dynamics 路线。
4. 如果关注机器人，把 [Veo-Act](https://arxiv.org/abs/2604.04502) 和 [RoboScape](https://arxiv.org/abs/2506.23135) 放在一起看：更实际的架构是高层 imagination / rollout 加独立低层控制。
5. 声称模型“懂物理”之前，先读 Physics-IQ、Morpheus 和 PhyGround。
6. 如果关注改进方法，读 [PhyWorld](https://arxiv.org/abs/2605.19242) 和 [NewtonGen](https://arxiv.org/abs/2509.21309)：前者代表偏好对齐路线，后者代表显式动力学注入路线。

## 贡献方式

欢迎提交 PR。请尽量包含：

- 论文、项目或技术报告的直接链接。
- 一句简短说明：该工作涉及 dynamics、state、action、material、conservation law、robot rollout、simulator use 或 physics benchmark 中的哪类物理信号。
- 建议放入上方哪个类别。

请避免添加只强调视觉真实的视频 / 图像生成工作；除非它对 physics、world model、robotics 或 evaluation 有明确贡献。
