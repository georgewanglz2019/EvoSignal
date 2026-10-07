<p align="center">
  <a href="README.md">English</a> | <a href="README_zh.md">简体中文</a>
</p>

<p align="center">
  <img src="assets/branding/evosignal-logo.png" alt="EvoSignal logo with glowing traffic lights and a code symbol" width="620">
</p>

<p align="center">
  <strong>LLM-Guided Evolutionary Design of Modular Traffic Signal Control Programs</strong>
</p>

EvoSignal uses an LLM **offline** to evolve inspectable traffic signal control programs. The selected program then chooses phases from traffic observations **without online LLM inference**.

> **Paper preview.** This repository currently shares the research overview and figures. The arXiv link will be added when the preprint is public; the source code and reproduction materials are planned for release after paper acceptance.

## Motivation: adaptive rules that remain inspectable

Traffic conditions change across networks and demand patterns, making repeated manual rule tuning laborious. RL learns adaptive policies from traffic experience, while LLM controllers add pretrained knowledge and language reasoning. EvoSignal uses LLM capabilities during program design to revise **explicit traffic-feature computations and control rules** from traffic-performance feedback, then deploys the selected program directly.

| Capability | Conventional TSC | RL-based TSC | LLM-based TSC | EvoSignal |
| :--- | :---: | :---: | :---: | :---: |
| Learns adaptive control policies from experience or feedback | ✗ | ✓ | ✓ | ✓ |
| Uses pretrained LLM knowledge in design or decision making | ✗ | ✗ | ✓ | ✓ |
| Supports online reasoning with natural-language rationales | ✗ | ✗ | ✓ | ✗ |
| Automatically revises explicit traffic-feature computations | ✗ | ✗ | ✗ | ✓ |
| Automatically revises explicit control rules | ✗ | ✗ | ✗ | ✓ |
| Exposes executable decision logic for human inspection and editing | ✓ | ✗ | ✗ | ✓ |
| No online neural-model inference (including LLMs) | ✓ | ✗ | ✗ | ✓ |

*✓ Supported; ✗ not part of the representative formulation. Conventional control denotes predefined rules that can respond to traffic changes without learning a new policy; RL-based control denotes neural policies. LLM-based control includes traffic-trained models such as LightGPT and Traffic-R1.*

*Feature revision changes explicit definitions and computations; inspectable decision logic exposes readable conditions and formulas linking traffic features to decisions. Policy learning occurs during training or program design; “online” refers to phase selection during deployment.*

## How EvoSignal works

![EvoSignal's offline program-evolution framework](assets/figures/evosignal-framework.svg)

*Figure 2 from the paper. Multiple initial strategies (Multi-init) seed a three-module program: traffic features (M1), local phase priorities (M2), and optional network-aware corrections (M3). Simulation performance analysis (SPA) diagnoses traffic behavior, while a Pareto strategy archive (PSA) retains different performance trade-offs to guide later revisions. The selected program runs without an online LLM.*

## What the paper reports

- **Waiting time:** Across five scenarios on two real-world road networks, the selected default program reduces waiting time by **16.8–49.2%** relative to the *lowest waiting time among 20 conventional, RL-based, and LLM-based baselines* in each scenario.
- **Transfer:** A travel-time/queue-length-focused program beats all 20 baselines on travel time, queue length, and waiting time in the J1 search scenario. Reused unchanged in four other scenarios, it ranks in the top three for each metric.

![Paper Table 2: Jinan traffic control results for 20 reference controllers and evolved programs](assets/figures/table-2-jinan.png)

*Paper Table 2, Jinan (J1–J3). TT = travel time, QL = queue length, WT = waiting time; lower is better. Each evolved program's rank is computed separately against the same 20 reference controllers. The blue rows identify EvoSignal programs. For the other two scenarios, see [Table 3: Hangzhou (H1–H2)](assets/figures/table-3-hangzhou.png).*

![Relative improvement over Maxpressure for two EvoSignal programs across five scenarios](assets/figures/control-results.svg)

*Figure 4 from the paper. Relative improvement in travel time, queue length, and waiting time over **Maxpressure**; positive values are better. Both programs were evolved on J1 and reused unchanged. This figure uses Maxpressure as its reference, whereas the 16.8–49.2% result above uses the best waiting-time baseline among 20 methods in each scenario.*

![Search progress and final-score comparison with OpenEvolve and ShinkaEvolve](assets/figures/search-progress.svg)

*Figure 5 from the paper. Search progress and final best scores on J1 under the default objective, over three runs per framework. See the paper for experimental settings, uncertainty, ablations, and full baseline tables.*

The [experimental setup figure](assets/figures/experimental-setup.svg) shows the networks, selectable phases, and demand profiles used in the study.

## Paper and code

**Paper:** *EvoSignal: LLM-Guided Evolutionary Design of Modular Traffic Signal Control Programs*. The arXiv URL and citation will be added after the preprint is posted.

**Code:** The implementation and reproduction guide are being prepared for release after paper acceptance. This preview repository contains no runnable implementation.
