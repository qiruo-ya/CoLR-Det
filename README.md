# CoLR-Det

# CoLR-Det: Collaborative Latent Restoration for Small Object Detection in Low-Resolution Remote Sensing Images

<div align="center">

[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-green.svg)](https://www.python.org/)
[![PyTorch 1.10+](https://img.shields.io/badge/PyTorch-1.10+-orange.svg)](https://pytorch.org/)
[![MMDetection](https://img.shields.io/badge/MMDetection-3.0+-red.svg)](https://github.com/open-mmlab/mmdetection)
[![License](https://img.shields.io/badge/License-Apache%202.0-yellow.svg)](LICENSE)

**[Ruo Qi](mailto:qiruo2023@email.szu.edu.cn), [Linhui Dai*](mailto:dailinhui@szu.edu.cn), Yusong Qin, Chaolei Yang, Yanshan Li**


</div>

---

## 📋 Overview

CoLR-Det is a Collaborative Latent-Restoration Assisted Small Object Detection framework for remote sensing images. Different from explicit SR-before-detection pipelines, CoLR-Det does not use super-resolution as an image-level preprocessing step.

### Key Features

- 🔗 **Implicit Feature Sharing Paradigm**: Enables semantically consistent collaboration between SR and detection tasks
- 🎯 **Saliency-Driven Query Token Selection**: Dynamically focuses on small object regions and suppresses feature pollution
- ⚡ **Gradient Routing Strategy**: Alleviates optimization conflicts between reconstruction and detection
- 🚀 **Competitive Efficiency**: Achieves 5× FLOPs reduction compared to serial baselines while improving accuracy

---

## 🏗️ Architecture

<!-- 
TODO: Add your network architecture figure here
Recommended: Save as 'assets/architecture.png' or 'figures/framework.png'
-->

<div align="center">
<img src="backbone.png" alt="CoLR-Det Architecture" width="90%">
<p><em>Figure 1: Given an LR image, a parameter-shared multiscale encoder extracts latent features for both detection and training-time restoration supervision. The restoration branch injects auxiliary reconstruction cues during training and is removed during inference. The detection branch predicts saliency responses and performs object-preserving token routing before DINO-style decoding. CoLR-Det is optimized with a detection-prioritized two-stage strategy, where object-level semantics are first stabilized and restoration supervision is later incorporated under a decoupled learning-rate schedule.</em></p>
</div>

---



## 🔧 Installation

### Requirements

- Python >= 3.8
- PyTorch >= 1.10
- CUDA >= 11.1
- MMDetection >= 3.0

### Step-by-Step Installation

```bash
# Clone the repository
git clone https://github.com/qiruo-ya/CoLR-Det.git
cd CoLR-Det

# Create conda environment
conda create -n CoLR-Det python=3.8 -y
conda activate CoLR-Det

# Install PyTorch (adjust CUDA version as needed)
pip install torch==1.12.1+cu113 torchvision==0.13.1+cu113 --extra-index-url https://download.pytorch.org/whl/cu113

# Install MMDetection dependencies
pip install -U openmim
mim install mmengine
mim install "mmcv>=2.0.0"

# Install MMDetection
pip install mmdet

# Install other dependencies
pip install -r requirements.txt

# Install CoLR-Det
pip install -e .
```

---

## 📁 Dataset Preparation

### Dataset Structure

```
data/
├── NWPU_VHR10_Split/
│   ├── train/
│   │   ├── images/
│   │   └── annotations/
│   └── test/
│       ├── images/
│       └── annotations/
├── DOTAv1.5_Split/
│   ├── train/
│   │   ├── images/
│   │   └── annotations/
│   └── test/
│       ├── images/
│       └── annotations/
└── HRSSD_Split/
    ├── train/
    │   ├── images/
    │   └── annotations/
    └── test/
        ├── images/
        └── annotations/
```

### Dataset Download

| Dataset | Images | Categories | Download |
|:-------:|:------:|:----------:|:--------:|
| NWPU VHR-10 | 3,631 | 10 | [Link](https://github.com/chaozhong2010/VHR-10_dataset_coco) |
| DOTAv1.5 | 15,883 | 16 | [Link](https://captain-whu.github.io/DOTA/) |
| HRSSD | 53,056 | 13 | [Link](https://github.com/TongkunGuan/SRSSD) |

---

## 🚀 Training

### Single GPU Training

```bash
# Train on NWPU VHR-10-Split
python tools/train.py

```



## 📈 Evaluation

### Test Single Model

```bash
# Evaluate on NWPU VHR-10-Split
python tools/test.py
```


## 🔬 Visualization

### Detection Results

<!-- 
TODO: Add your visualization results here
Recommended: Save as 'assets/visualization.png'
-->

<div align="center">
<img src="DetectionResults.png" alt="Detection Results" width="90%">
<p><em>Figure 2: Qualitative detection results comparing CoLR-Det with state-of-the-art methods.</em></p>
</div>

### Feature Map Visualization

<!-- 
TODO: Add your feature visualization here
Recommended: Save as 'assets/feature_maps.png'
-->

<div align="center">
<img src="heatmap.png" alt="Feature Maps" width="80%">
<p><em>Figure 3: Visualization of intermediate feature maps showing the effect of SR branch on representation quality.</em></p>
</div>

---

## 📖 Citation

If you find this work useful in your research, please consider citing:

```bibtex
@article{qi2026,
  title={CoLR-Det: Collaborative Latent Restoration for Small Object Detection in Low-Resolution Remote Sensing Images},
  author={Qi, Ruo and Dai, Linhui and Qin, Yusong and Yang, Chaolei and Li, Yanshan},
  year={2026},
}
```

---

## 🙏 Acknowledgements

This project is built upon the following open-source projects:

- [MMDetection](https://github.com/open-mmlab/mmdetection)
- [DINO](https://github.com/IDEA-Research/DINO)
- [Swin Transformer](https://github.com/microsoft/Swin-Transformer)

We thank the authors for their excellent work.

---

## 📧 Contact

For any questions, please contact:

- **Ruo Qi**: qiruo2023@email.szu.edu.cn

---

## 📄 License

This project is released under the [Apache 2.0 License](LICENSE).

---

<div align="center">

**If you find SDCoNet useful, please give us a ⭐!**

</div>
