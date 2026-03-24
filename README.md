<div align="center">
<h2 align="center">
  <b>
    <span>━━━━━━━━━━━━━━━━━━━━━━━━━━━</span>
    <br/>
    <img src="assets/logo.png" height="48" style="display: inline-block; vertical-align: middle; margin: 2px;"> CounterScene
    <br/>
    <span>━━━━━━━━━━━━━━━━━━━━━━━━━━━</span>
    <br/>
  </b>
</h2>
</div>

<p align="center">
  <b>Counterfactual Causal Reasoning in Generative World Models for Safety-Critical Closed-Loop Evaluation</b>
</p>

<p align="center">
  Bowen Jing, Ruiyang Hao, Weitao Zhou, Haibao Yu
</p>

<p align="center">
  <a href="https://arxiv.org/pdf/2603.21104v1">Paper</a> &nbsp;|&nbsp;
  <a href="#overview">Overview</a> &nbsp;|&nbsp;
  <a href="#main-results">Main Results</a> &nbsp;|&nbsp;
  <a href="#citation">Citation</a>
</p>

## Overview

CounterScene studies safety-critical scenario generation through **counterfactual causal reasoning** in generative world models.

Instead of applying arbitrary perturbations, CounterScene identifies the agent whose behavior is causally maintaining safety and performs a **minimal intervention** that transforms a safe scene into a realistic safety-critical interaction while preserving coherent multi-agent dynamics.

<p align="center">
  <img src="assets/intro.jpg" width="900" />
</p>
<p align="center"><em>
  Counterfactual causal reasoning for safety-critical generative BEV world model. Given an observed traffic scene where the adversarial agent waits and the ego vehicle passes safely, CounterScene asks: what if the adversarial agent did not wait? By intervening on the agent trajectory, it constructs a counterfactual world that induces safety-critical interactions while preserving realistic traffic dynamics.
</em></p>

### Key Components

- **Causal adversarial agent selection** identifies the agent whose current behavior suppresses the greatest latent risk.
- **Causal Interaction Graph (CIG)** models conflict-aware dependencies among agents.
- **Counterfactual guidance** perturbs only the selected agent trajectory during diffusion.
- **Closed-loop rollout** allows all other agents to react naturally, preserving realistic multi-agent dynamics.

<p align="center">
  <img src="assets/methodology.jpg" width="900" />
</p>
<p align="center"><em>
  Overview of CounterScene. The framework consists of four modules: (1) causal adversarial agent selection, (2) a Causal Interaction Graph (CIG), (3) a diffusion-based interactive BEV world model with a SceneTransformer denoiser, and (4) counterfactual guidance that perturbs only the adversarial agent trajectory during denoising.
</em></p>

## Main Results

CounterScene achieves stronger realism-effectiveness trade-offs than prior baselines on **nuScenes**, with lower trajectory error and substantially higher collision rates, especially at longer horizons.

| Horizon | Method | ADE | FDE | ORR | HBR | CR |
|:--|:--|--:|--:|--:|--:|--:|
| Short (1-4s) | CCDiff | 0.380 | 0.908 | 0.4% | 1.5% | 1.3% |
| Short (1-4s) | **CounterScene** | **0.288** | **0.703** | 0.5% | 1.6% | **3.3%** |
| Mid (5-7s) | CCDiff | 1.128 | 2.914 | 1.3% | 1.5% | 8.7% |
| Mid (5-7s) | **CounterScene** | **0.982** | **2.639** | 1.3% | 2.0% | **14.7%** |
| Long (8-10s) | CCDiff | 2.092 | 5.898 | 2.3% | 1.5% | 12.3% |
| Long (8-10s) | **CounterScene** | **1.877** | **5.141** | 1.9% | 1.8% | **22.7%** |

**Metric note.** ADE/FDE measure trajectory realism, while ORR, HBR, and CR evaluate off-road rate, hard-brake rate, and collision rate.

For additional qualitative comparisons, ablations, zero-shot transfer, and full per-horizon tables, please refer to the paper.

## Qualitative Results

### Scene 103 — Merging Cut-in

<p align="center">
  <img src="assets/103.png" width="900" />
</p>
<p align="center"><em>
  In the factual scene, the side-road vehicle yields and the ego passes safely. CounterScene identifies that yielding vehicle as the causal variable and compresses its spatiotemporal margin, producing an aggressive cut-in.
</em></p>

### Scene 905 — Rear-End Collision

<p align="center">
  <img src="assets/905.png" width="900" />
</p>
<p align="center"><em>
  The trailing vehicle maintains a safe following margin in the factual scene. CounterScene compresses the margin, causing a realistic rear-end crash without distorting the rest of the scene.
</em></p>

### Scene 913 — Head-On Collision

<p align="center">
  <img src="assets/913.png" width="900" />
</p>
<p align="center"><em>
  CounterScene applies a minimal spatial intervention that redirects the causally critical vehicle into the ego path, culminating in a realistic head-on collision.
</em></p>

## Citation

If you find this work useful, please cite:

```bibtex
@article{jing2026counterscene,
  title={CounterScene: Counterfactual Causal Reasoning in Generative World Models for Safety-Critical Closed-Loop Evaluation},
  author={Jing, Bowen and Hao, Ruiyang and Zhou, Weitao and Yu, Haibao},
  journal={arXiv preprint arXiv:2603.21104},
  year={2026}
}
```
