[English](README.md) | [简体中文](README_zh.md)

# EvoSignal

**LLM-Guided Evolutionary Design of Modular Traffic Signal Control Programs**

EvoSignal uses an LLM **offline** to evolve inspectable traffic signal control programs. The selected program then chooses phases from traffic observations **without online LLM inference**.

> **Paper preview.** This repository currently shares the research overview and figures. The arXiv link will be added when the preprint is public; the source code and reproduction materials are planned for release after paper acceptance.

## Motivation: adaptive rules that remain inspectable

Traffic conditions change across networks and demand patterns. Hand-tuning explicit control rules is laborious; neural and LLM controllers can adapt, but their decisions are generally harder to inspect as code and require model inference during operation. EvoSignal uses traffic-performance feedback to revise **both traffic features and phase-priority rules**, then deploys the resulting program directly.

| Capability | Conventional TSC | RL-based TSC | LLM-based TSC | EvoSignal |
| :--- | :---: | :---: | :---: | :---: |
| Improves policies from traffic-performance feedback | ✗ | ✓ | ✓ | ✓ |
| Uses pretrained LLM knowledge | ✗ | ✗ | ✓ | ✓ |
| Online language reasoning and rationales | ✗ | ✗ | ✓ | ✗ |
| Automatically revises explicit traffic-feature code | ✗ | ✗ | ✗ | ✓ |
| Automatically revises explicit phase-priority rules | ✗ | ✗ | ✗ | ✓ |
| Decision rules inspectable as code | ✓ | ✗ | ✗ | ✓ |
| Decision rules editable as code | ✓ | ✗ | ✗ | ✓ |
| No online neural-model inference | ✓ | ✗ | ✗ | ✓ |
| Expected online computation | Low | Model-dependent | Typically higher | Low |

*This is a qualitative comparison of representative formulations, not a measured ranking or a claim about every method in each family. “Conventional” denotes predefined rule-based controllers; “RL-based” denotes neural policies. The LLM-based category includes traffic-trained models. Actual online cost depends on implementation, model size, hardware, batching, and token length.*

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
