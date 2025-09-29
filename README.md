# Awesome Physics + Generative AI

Papers about incorporating physics into generative models.

## Contents
### 
- **A.1 Physics in Generative Models**
  - A.1.1 Physics in Robotic World Models
    - A.1.1.1 [RoboScape: Physics-informed Embodied World Model](#a111-roboscape-physics-informed-embodied-world-model)
  - A.1.2 Physics in General World Simulators
    - A.1.2.1 [NewtonGen: Physics-Consistent and Controllable Text-to-Video Generation via Neural Newtonian Dynamics](#a121-newtongen-physics-consistent-and-controllable-text-to-video-generation-via-neural-newtonian-dynamics)
  - A.1.3 Human Preference Alignment
    - A.1.3.1 [BranchGRPO: Stable and Efficient GRPO with Structured Branching in Diffusion Models](#a131-branchgrpo-stable-and-efficient-grpo-with-structured-branching-in-diffusion-models)
- **B (3dgs based)**
---


## A.1 Physics in Generative Models

### A.1.1 Physics in Robotic World Models

#### A.1.1.1 [RoboScape: Physics-informed Embodied World Model](https://arxiv.org/abs/2506.23135) Tsinghua University; Manifold AI.
<details><summary>Abstract</summary>
World models have become indispensable tools for embodied intelligence, serving as powerful simulators capable of generating realistic robotic videos while addressing critical data scarcity challenges. However, current embodied world models exhibit limited physical awareness, particularly in modeling 3D geometry and motion dynamics, resulting in unrealistic video generation for contact-rich robotic scenarios. In this paper, we present RoboScape, a unified physics-informed world model that jointly learns RGB video generation and physics knowledge within an integrated framework. We introduce two key physics-informed joint training tasks: temporal depth prediction that enhances 3D geometric consistency in video rendering, and keypoint dynamics learning that implicitly encodes physical properties (e.g., object shape and material characteristics) while improving complex motion modeling. Extensive experiments demonstrate that RoboScape generates videos with superior visual fidelity and physical plausibility across diverse robotic scenarios. We further validate its practical utility through downstream applications including robotic policy training with generated data and policy evaluation. Our work provides new insights for building efficient physics-informed world models to advance embodied intelligence research. The code is available at: https://github.com/tsinghua-fib-lab/RoboScape.
</details>
<details><summary>Comment</summary>
Introduce two physics-informed tasks: 1)temporal depth prediction and 2) keypoint dynamic learning in the training of an embodied world model to predict visual observation given past observations and robotic actions using dual-branch co-autoregressive Transformer(DCT).
</details>

### A.1.2 Physics in General World Simulators
#### A.1.2.1 [NewtonGen: Physics-Consistent and Controllable Text-to-Video Generation via Neural Newtonian Dynamics](https://arxiv.org/abs/2509.21309) Purdue University; Samsung Research America
<details><summary>Abstract</summary>
A primary bottleneck in large-scale text-to-video generation today is physical consistency and controllability. Despite recent advances, state-of-the-art models often produce unrealistic motions, such as objects falling upward, or abrupt changes in velocity and direction. Moreover, these models lack precise parameter control, struggling to generate physically consistent dynamics under different initial conditions. We argue that this fundamental limitation stems from current models learning motion distributions solely from appearance, while lacking an understanding of the underlying dynamics. In this work, we propose NewtonGen, a framework that integrates data-driven synthesis with learnable physical principles. At its core lies trainable Neural Newtonian Dynamics (NND), which can model and predict a variety of Newtonian motions, thereby injecting latent dynamical constraints into the video generation process. By jointly leveraging data priors and dynamical guidance, NewtonGen enables physically consistent video synthesis with precise parameter control.
</details>

<details><summary>Comment</summary>
Propose Neural Newtonian Dynamics (NND) to model physical dynamics in video generation, which models and predicts a variaty of Newtonian motions, thereby injecting dynamical constraints into video generation. Experiments conducted on " physics-clean" data geberated python-based physics data simulator. Compare "Go-with-the-Flow"(CogVideoX) model with existing Sora, Veo3, CogVideoX-5B, Wan2.2 etc. SOTA generative models, resulting SOTA performance.
</details>

### A.1.3 Human Preference Alignment
#### A.1.3.1 [BranchGRPO: Stable and Efficient GRPO with Structured Branching in Diffusion Models](https://arxiv.org/abs/2509.06040) Peking University; Beijing Normal University; ByteDance
<details><summary>Abstract</summary>
Recent progress in aligning image and video generative models with Group Relative Policy Optimization (GRPO) has improved human preference alignment, yet existing approaches still suffer from high computational cost due to sequential rollouts and large numbers of SDE sampling steps, as well as training instability caused by sparse rewards. In this paper, we present BranchGRPO, a method that restructures the rollout process into a branching tree, where shared prefixes amortize computation and pruning removes low-value paths and redundant depths. BranchGRPO introduces three contributions: (1) a branch sampling scheme that reduces rollout cost by reusing common segments; (2) a tree-based advantage estimator that converts sparse terminal rewards into dense, step-level signals; and (3) pruning strategies that accelerate convergence while preserving exploration. On HPDv2.1 image alignment, BranchGRPO improves alignment scores by up to 16% over strong baselines, while reducing per-iteration training time by nearly 55%. On WanX-1.3B video generation, it further achieves higher Video-Align scores with sharper and temporally consistent frames compared to DanceGRPO.
</details>

<details><summary>Comment</summary>
Propose BranchGRPO, a method that restructures the rollout process into a branching tree, where shared prefixes amortize computation and pruning removes low-value paths and redundant depths. Depth-wise normalization are applied to balance contribution of different denoising steps. Experiments conducted on HPDv2.1 image alignment compared with DanceGRPO and MixGROP shows better performance and smaller iteration time. 
</details>