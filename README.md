# Center-DETR: Center-Aware Detection with Swin-based Co-DETR Framework for Cervical Cytology

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.10%2B-orange)](https://pytorch.org/)

**1st Place Winner in Track B, 2nd Place in Track A - RIVA Cervical Cytology Challenge 2026**

Curious about **boosting your mAP**—especially when your bounding boxes are at a **fixed size**? The little trick in this work might just be the spark you've been waiting for! 💡✨

This repository contains the official implementation of our winning solution for the RIVA Cervical Cytology Challenge. We present a center-aware detection framework with geometric box optimization, achieving superior performance on cervical cell detection and classification.

## 📖 Overview

Our approach leverages a powerful Co-DINO framework with Swin-Large backbone, integrating:
- **Center-Preserving Data Augmentation**: Ensures morphological integrity of cell nuclei
- **Analytical Geometric Box Optimization**: Post-processes predictions to 101.5×101.5 for optimal mAP
- **Track-Specific Loss Tuning**: Adapts optimization focus for detection vs. detection+classification tasks

For more details, please refer to our paper:
> **Center-Aware Detection with Swin-Based Co-DETR Framework for Cervical Cytology**  
> Yan Kong, Yuan Yin, Yuqi Fang*, Caifeng Shan*  
> ISBI Challenge 2026

[[Paper Link]](link-to-paper) | [[Challenge Link]](https://www.kaggle.com/competitions/riva-cervical-cytology-challenge-track-a-isbi-final-evaluation/overview)

---

## 🚀 Quick Start

### Installation

1. **Clone Co-DETR repository**
```bash
# Clone the official Co-DETR repository
git clone https://github.com/Sense-X/Co-DETR.git
cd Co-DETR
```
2. **Install dependencies and packages**
Follow the official [Co-DETR installation guide](https://github.com/open-mmlab/mmcv/tree/v1.5.0#installation) for environment setup. For reference, our exact environment configuration is provided in [environment.yml](https://github.com/YanKong0408/Center-DETR/blob/main/environment.yml)

### Data Preparation
1. **Download the dataset**
Register and download from the [RIVA Challenge page](https://www.kaggle.com/competitions/riva-cervical-cytology-challenge-track-a-isbi-final-evaluation/overview)
Process to [Co-DETR/data/]() directory

2. **Directory structure**
```bash
Co-DETR
└── riva
    ├── coco
        ├── annotations
        │      ├── instances_train2017.json
        │      └── instances_val2017.json
        ├── train2017
        └── val2017
```

### 🔧 Configuration
1. **Replace Transform Modules**
Copy our custom [transform](https://github.com/YanKong0408/Center-DETR/blob/main/transforms.py) modules to replace the Co-DETR repository file at [Co-DETR/mmdet/datasets/pipelines/transforms.py]()

Key modifications: Implements center-preserving random cropping

2. **Copy Config Files**
get our config.py for [Track A](https://github.com/YanKong0408/Center-DETR/blob/main/co_dino_5scale_swin_large_16e_o365tococo_yankong_a.py) and [Track B](https://github.com/YanKong0408/Center-DETR/blob/main/co_dino_5scale_swin_large_16e_o365tococo_yankong_b.py)
Key modifications: Implements track-specific loss tuning

3. **Training**
```bash
python tools/train.py configs/co_dino_5scale_swin_large_16e_o365tococo_yankong_b.py \
    --work-dir work_dirs/riva_track_b
```

4. **Inference**
See [inference_demo.ipynb](https://github.com/YanKong0408/Center-DETR/blob/main/inference_demo.ipynb)
Remember to place our [inference_demo.ipynb]() in [\Co-DETR\demo](), then run it.

### Our models
Download our models from HuggingFace:
| Model  | Track | mAP (Testset) | Download |
| ------ | -------- | ------ | ------- | 
| Co-Dino Swin-L | A | 0.18038 | [model](https://huggingface.co/yankon0408/ISBI-2026-RIVA-track-A/tree/main) |
| Co-Dino Swin-L | B | 0.60705 | [model](https://huggingface.co/yankon0408/ISBI-2026-RIVA-track-B/tree/main) |

### 📝 Citation
If you find our work useful, please consider citing:
```bibtex
coming soon
```
