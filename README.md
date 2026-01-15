
![](assets/logo.png)

[**InverseBench: Benchmarking Plug-and-Play Diffusion Priors for Inverse Problems in Physical Sciences**](https://openreview.net/pdf?id=U3PBITXNG6) (ICLR 2025 spotlight, this is where i forked from my course design)


# Generative Priors for Medical Image Reconstruction at Test Time

[](https://www.google.com/search?q=https://github.com/musong/TTA-Medical-Reconstruction)
[](https://opensource.org/licenses/MIT)

This repository contains the demo implementation of the framework described in course design, which explores the transition from discriminative modeling to **generative diffusion priors** for solving complex inverse problems in medical imaging. Our work introduces a **Test-Time Adaptation (TTA)** strategy to bridge the distribution gap between synthetic training data and real-world clinical measurements.

## Abstract

While deep learning has revolutionized image restoration, deterministic architectures often fail to generalize to unseen clinical degradations. We systematically evaluate plug-and-play frameworks (DDRM, DPS) across diverse tasks like compressed sensing MRI using the **InverseBench** framework. To ensure biological validity under unknown degradation models, we propose a framework leveraging **Pre-trained Diffusion Models (PDM)** to guide on-the-fly adaptation through **Test-Time Degradation Adaptation (TDA)** and **Adaptive Image Restoration (AIR)**. Our case study on dynamic in-vivo metabolic reconstruction at the **State Key Laboratory for MRSI** demonstrates superior accuracy in tracking water, glucose, and lactate metabolism compared to traditional static models.



## Key Features

  * **Plug-and-Play Diffusion Priors:** Utilizes foundational priors (PDM) to solve inverse problems ($y = Ax + n$) without task-specific retraining.
  * **Test-Time Adaptation (TTA):** Explicitly addresses the "Dilemma of Unknowns" in open-set medical deployments.
  * **Dual-Stage Adaptation:** Includes **TDA** for unknown degradations and **AIR** for result optimization during the denoising process.
  * **Multi-Modal Robustness:** Evaluated on FFHQ (general restoration), Compressed Sensing MRI (2% undersampling), and Black Hole Imaging.



## Methodology Overview

As illustrated in our framework overview (Figure 2), the system performs iterative denoising where each step is conditioned on the measurement $y$ and adapted in real-time:

1.  **PDM Guidance:** Uses a generic pre-trained model for reconstruction.
2.  **TDA:** Adapts to unseen degradations specific to the clinical scanner or subject.
3.  **AIR:** Optimizes the guided image toward a physically grounded, restored clean image.



## Environment Requirements

We recommend using **Linux** with **Python 3.10-3.11** and at least one high-end GPU (e.g., A100) for inference.

### Environment Management (via `uv`)

Consistent with our development workflow, we recommend [uv](https://docs.astral.sh/uv/) for fast environment and dependency management.

```bash
# Sync dependencies and create virtual environment
uv sync

# Activate the environment
source .venv/bin/activate
```



## AI4Science Case Study: Dynamic MRSI

The core of our research was conducted at the **State Key Laboratory for MRSI**. We focus on reconstructing high-fidelity metabolic maps from significantly undersampled in-vivo data.

### Performance Highlights

  * **Temporal Tracking:** Successfully tracks metabolic flux over a **180-minute window**.
  * **Biochemical Validity:** Precisely characterizes the conversion of glucose to lactate in tumor microenvironments, which traditional models like SwinIR often mask.
  * **Robustness:** Maintains high accuracy even when the signal-to-noise ratio fluctuates during longitudinal studies.



## Results

### Qualitative Restoration (FFHQ)

Our **DAPS (Diffusion-based Adaptation for Posterior Sampling)** framework recovers fine-grained features (skin texture, hair) often lost in standard inversion techniques while strictly adhering to measurement constraints.

### Quantitative Comparison

| Task | Traditional Static (SwinIR/Restormer) | Proposed TTA-Enhanced Diffusion |
| :--- | :--- | :--- |
| **2% MRI Undersampling** | High Artifacts / Model Collapse  | Robust Reconstruction  |
| **Dynamic MRSI** | Oversmoothed / Lost Features  | Accurate Flux Characterization  |

