# Awesome Physics + Generative AI

[🇨🇳 中文版](README.zh-CN.md)

A curated map of work at the intersection of generative models, physical reasoning,
world simulation, and embodied AI.

**Frontier thesis, as of 2026-06-04.** Video generation is moving from
photorealistic open-loop synthesis toward interactive, evaluable world models for
Physical AI. The sober caveat: current frontier video models show partial
physical intuitions, but benchmark evidence still does not support treating them
as reliable physics engines.

## Contents

- [Quick Map](#quick-map)
- [What Counts Here](#what-counts-here)
- [Curated Works](#curated-works)
  - [Surveys and Positioning](#surveys-and-positioning)
  - [Video and World Simulators](#video-and-world-simulators)
  - [Embodied AI and Robotics](#embodied-ai-and-robotics)
  - [Physics-Aware Training and Alignment](#physics-aware-training-and-alignment)
  - [Benchmarks and Diagnostics](#benchmarks-and-diagnostics)
- [Reading Roadmap](#reading-roadmap)
- [Contributing](#contributing)

## Quick Map

| Track | Core question | Representative work |
| --- | --- | --- |
| Video to world simulator | Can a video model maintain state, object persistence, and plausible dynamics? | Sora, Sora 2, Genie 3, Cosmos 3 |
| Interactive simulation | Can generated worlds respond to actions or promptable events in a closed loop? | Genie 3, Cosmos-Predict2.5 |
| Latent dynamics | Can models predict state transitions without rendering every pixel? | V-JEPA 2 |
| Robotics use | Are video/world models useful for planning, data generation, or policy evaluation? | Veo-Act, RoboScape, Cosmos-Predict2.5 |
| Physics post-training | Can preference data and continuation training improve physical faithfulness? | PhyWorld, NewtonGen |
| Physics evaluation | Does visual realism actually imply physical understanding? | Physics-IQ, Morpheus, PhyGround |

## What Counts Here

This list prioritizes work where physics is central to the claim, method, or
evaluation:

- **State and dynamics:** object permanence, contact, material change, motion,
  conservation, causality, and long-horizon consistency.
- **Action-conditioned rollout:** generated futures that respond to user,
  robot, vehicle, or agent actions.
- **Physical AI deployment:** robotics, autonomous driving, synthetic data,
  policy evaluation, closed-loop simulation, or failure-case generation.
- **Law-specific evaluation:** benchmarks that test physical principles rather
  than only aesthetic quality or temporal smoothness.

## Curated Works

### Surveys and Positioning

| Work | Type | Why it matters |
| --- | --- | --- |
| [A Mechanistic View on Video Generation as World Models: State and Dynamics](https://arxiv.org/abs/2601.17067) | Survey / taxonomy | Frames the field around **state construction** and **dynamics modeling**, and argues that evaluation should move from visual fidelity to physical persistence and causal reasoning. |
| [Video generation models as world simulators](https://openai.com/index/video-generation-models-as-world-simulators/) | Technical report / position | Popularized the thesis that large video diffusion transformers can become general-purpose simulators of the physical world. It also explicitly documents failure modes in basic physics, object state changes, and long-horizon coherence. |

### Video and World Simulators

| Work | Organization | Physics / world-model signal | Notes |
| --- | --- | --- | --- |
| [Sora 2](https://openai.com/index/sora-2/) | OpenAI | Emphasizes more physically accurate and controllable video generation, synchronized audio, and the ability to model failure instead of satisfying prompts by implausible shortcuts. | Product page states that the Sora product is no longer available as of 2026-04-26, but the model remains an important route marker. |
| [Genie 3: A new frontier for world models](https://deepmind.google/blog/genie-3-a-new-frontier-for-world-models/) | Google DeepMind | Text-to-interactive-world generation at 24 fps and 720p, with a few minutes of consistency, navigation inputs, and promptable world events. | A key shift from video clip generation to an interaction loop; limitations include constrained action space, multi-agent interaction, real-world geographic precision, and interaction duration. |
| [Cosmos 3: Omnimodal World Models for Physical AI](https://arxiv.org/abs/2606.02800) | NVIDIA | Unified language, image, video, audio, and action-sequence modeling for Physical AI. | Treats VLMs, video generators, world simulators, and world-action models as one omnimodal framework; releases code, checkpoints, data, and benchmarks. |
| [World Simulation with Video Foundation Models for Physical AI](https://arxiv.org/abs/2511.00062) | NVIDIA | Cosmos-Predict2.5 unifies Text2World, Image2World, and Video2World generation, with physical semantic grounding via Cosmos-Reason1. | Targets synthetic data generation, policy evaluation, and closed-loop simulation for robotics and autonomous systems. |

### Embodied AI and Robotics

| Work | Type | Physics / robotics angle | Notes |
| --- | --- | --- | --- |
| [Introducing the V-JEPA 2 world model and new benchmarks for physical reasoning](https://ai.meta.com/blog/v-jepa-2-world-model-benchmarks/) | Latent world model | Predicts in embedding space rather than pixel space, learning state representations and dynamics for understanding, prediction, and planning. | Especially relevant for robot planning because it avoids the cost of full pixel generation; Meta reports zero-shot planning/control with limited robot data. |
| [Veo-Act: How Far Can Frontier Video Models Advance Generalizable Robot Manipulation?](https://arxiv.org/abs/2604.04502) | Robot manipulation study | Uses Veo-3 to imagine future robot image sequences and an inverse dynamics model to recover actions. | Shows a useful boundary: frontier video models can produce task-level trajectories, but low-level contact-rich control remains unreliable, so hierarchical planning plus a robot policy is more practical. |
| [RoboScape: Physics-informed Embodied World Model](https://arxiv.org/abs/2506.23135) | Embodied world model | Adds temporal depth prediction and keypoint dynamics learning to improve 3D consistency and motion modeling in generated robot videos. | Demonstrates downstream use for robotic policy training with generated data and policy evaluation. |

### Physics-Aware Training and Alignment

| Work | Method | Physics signal | Notes |
| --- | --- | --- | --- |
| [PhyWorld: Physics-Faithful World Model for Video Generation](https://arxiv.org/abs/2605.19242) | Two-stage post-training | Flow matching fine-tuning improves video continuation; DPO over physics preference pairs aligns generated dynamics with physical plausibility. | A strong example of the emerging recipe: scale plus physical preference data plus per-law evaluation. |
| [NewtonGen: Physics-Consistent and Controllable Text-to-Video Generation via Neural Newtonian Dynamics](https://arxiv.org/abs/2509.21309) | Neural dynamics guidance | Injects trainable Neural Newtonian Dynamics into video generation to improve controllable Newtonian motion. | A more explicit dynamics route than purely scaling video data. |
| [BranchGRPO: Stable and Efficient GRPO with Structured Branching in Diffusion Models](https://arxiv.org/abs/2509.06040) | Related preference optimization | Not physics-specific, but relevant as an efficient diffusion-model alignment method that could support physics preference optimization. | Keep separate from core physics methods unless used with physical rewards or physics-specific preference data. |

### Benchmarks and Diagnostics

| Work | Evaluation focus | Main takeaway |
| --- | --- | --- |
| [Do generative video models understand physical principles?](https://arxiv.org/abs/2501.09038) | Physics-IQ: fluids, optics, solids, magnetism, thermodynamics | Visual realism is not strongly correlated with physical understanding; current models remain severely limited, though some cases are solvable. |
| [Morpheus: Benchmarking Physical Reasoning of Video Generative Models with Real Physical Experiments](https://arxiv.org/abs/2504.02918) | Real physical experiments and conservation-law metrics | Even with advanced prompting and video conditioning, current models struggle to encode stable physical principles. |
| [PhyGround: Benchmarking Physical Reasoning in Generative World Models](https://arxiv.org/abs/2605.10806) | Criteria-grounded benchmark with 13 physical-law categories | Moves evaluation from "looks good" to "which physical rule failed", using fine-grained human labels and a physics-specialized VLM judge. |

## Reading Roadmap

1. Start with the framing: [A Mechanistic View](https://arxiv.org/abs/2601.17067)
   and OpenAI's [Sora world-simulator report](https://openai.com/index/video-generation-models-as-world-simulators/).
2. Follow the simulator line: Sora 2 -> Genie 3 -> Cosmos 3 / Cosmos-Predict2.5.
3. Compare the latent-dynamics line with [V-JEPA 2](https://ai.meta.com/blog/v-jepa-2-world-model-benchmarks/).
4. For robotics, read [Veo-Act](https://arxiv.org/abs/2604.04502) and
   [RoboScape](https://arxiv.org/abs/2506.23135) together: the useful pattern is
   high-level imagination or rollout plus separate low-level control.
5. For evaluation, read Physics-IQ, Morpheus, and PhyGround before claiming that
   a model "understands physics".
6. For improving models, read [PhyWorld](https://arxiv.org/abs/2605.19242) and
   [NewtonGen](https://arxiv.org/abs/2509.21309): they represent preference
   alignment and explicit dynamics injection, respectively.

## Contributing

Pull requests are welcome. Please include:

- A direct paper, project, or technical-report link.
- A short note explaining the physics signal: dynamics, state, action, material,
  conservation law, robot rollout, simulator use, or physics benchmark.
- A clear category suggestion from the sections above.

Avoid adding papers that are only visually realistic video/image generation unless
they make a concrete physics, world-model, robotics, or evaluation contribution.
