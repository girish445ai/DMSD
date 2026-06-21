# DSMD — Dark Stereo Multi-Exposure Dataset

**DSMD (Dark Stereo Multi-Exposure Dataset)** is a large-scale paired dataset for extreme low-light stereo image restoration and depth estimation. It provides calibrated stereo image pairs captured across multiple exposures under real-world low-light conditions, along with well-lit reference frames for supervised learning.

---

## Overview

Existing low-light image datasets are largely monocular and lack the stereo geometry needed for joint restoration and disparity estimation. DSMD addresses this gap by providing:

- **Calibrated stereo pairs** with a fixed 24 cm outdoor baseline and 6 cm indoor baseline, with daily rectification
- **Multi-exposure captures** spanning extreme low-light to well-lit conditions
- **Paired ground-truth references** (long-exposure well-lit RGB frames) enabling supervised restoration training
- **Both indoor and outdoor** scenes covering diverse real-world lighting conditions

Over **50% of outdoor scenes** qualify as extreme low-light under the EV-based photometric criterion (EV ≤ 1.65, anchored to the SID dataset threshold using EV = log₂(N²/t) per ISO 2720).

### Dataset Sample

![Dataset Sample](https://github.com/girish445ai/DMSD/blob/main/dataset_sample_new_final.jpg?raw=true)

---

## Dataset Structure
DSMD/

├── outdoor/

│   ├── scene_001/

│   │   ├── left/

│   │   │   ├── low_light/      # Low-light input RGB frames

│   │   │   └── well_lit/       # Well-lit ground-truth RGB frames

│   │   └── right/

│   │       ├── low_light/

│   │       └── well_lit/

│   └── ...

└── indoor/

├── scene_001/

│   ├── left/

│   │   ├── low_light/

│   │   └── well_lit/

│   └── right/

│       ├── low_light/

│       └── well_lit/

└── ...


---

## Tasks Supported

| Task | Description |
|------|-------------|
| Low-light image restoration | Paired low-light→well-lit RGB supervision |
| Stereo image enhancement | Joint left-right consistency under dark conditions |
| Stereo depth / disparity estimation | Rectified stereo pairs with fixed baselines |
| Multi-exposure fusion | Multiple exposure levels per scene |

---

## Comparison with Related Datasets

| Dataset | Stereo | Low-light | Multi-exposure | Paired GT | Restoration | Disparity |
|---------|--------|-----------|----------------|-----------|-------------|-----------|
| SID (CVPR 2018) | ✗ | ✓ | ✓ | ✓ | ✓ | ✗ |
| MID (ICCV 2021) | ✓\* | ✓ | ✓ | ✗ | ✗ | ✗ |
| MS2 (2023) | ✓ | ✓ | ✗ | ✗ | ✗ | ✓ |
| LOL | ✗ | ✓ | ✗ | ✓ | ✓ | ✗ |
| **DSMD (Ours)** | **✓** | **✓** | **✓** | **✓** | **✓** | **✓** |

\* MID stereo pairs are captured from arbitrary viewpoints without a fixed baseline or rectified geometry.

---

## Illumination Criterion

Scene darkness in DSMD is quantified using the **Exposure Value (EV)** framework per ISO 2720:
