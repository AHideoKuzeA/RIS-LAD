<p align="center">
  <h1 align="center"><b>RIS-LAD</b>: A Benchmark and Model for Referring Low-Altitude Drone Image Segmentation</h1>
  <p align="center">
    <a href="https://arxiv.org/abs/2507.20920"><img src="https://img.shields.io/badge/arXiv-RIS--LAD-red?logo=arxiv" alt="Paper PDF"></a>
    <a href="https://drive.google.com/file/d/1na6DpdBxNbd2juyKGK9QWdqjOrEuER7v/view?usp=sharing"><img src="https://img.shields.io/badge/Dataset-RIS--LAD-yellow?logo=databricks" alt="RIS-LAD Dataset"></a>
    <img src="https://img.shields.io/badge/Code-coming%20soon-blue" alt="Code coming soon">
  </p>
</p>

**😊 TL;DR**

RIS-LAD is the **first fine-grained referring image segmentation (RIS)** benchmark tailored to **low-altitude drone (LAD)** scenarios. It features **13,871** image–text–mask triplets and introduces two LAD-specific challenges: **category drift** and **object drift**. We also propose **SAARN** (Semantic-Aware Adaptive Reasoning Network) with **CDLE** and **ARFM** to address them.

<div align="center">

<table>
  <tr>
    <td align="center" valign="middle">
      <img src="assets/teaser_lad_vs_rs.jpg" width="480"/>
      <br/><sub>RLADIS vs. traditional RS scenes</sub>
    </td>
    <td align="center" valign="middle">
      <img src="assets/drifts.jpg" width="480"/>
      <br/><sub>Category/Object drift in tiny & dense scenes</sub>
    </td>
  </tr>
</table>

</div>

---

## ⭐ Key contributions

- **RIS-LAD dataset**: 13,871 high-quality triplets focusing on **tiny**, **dense**, **multi-view**, and **multi-lighting** LAD scenes.  
- **New challenges**: formalizes **category drift** (tiny objects) and **object drift** (same-class crowding) typical in LAD.  
- **SAARN**: A semantic-aware framework:
  - **CDLE** (Category-Dominated Linguistic Enhancement): early **class-guided** alignment to reduce category drift.  
  - **ARFM** (Adaptive Reasoning Fusion Module): **scale-aware** semantic fusion to mitigate object drift.  
- **Strong results**: SAARN sets a new baseline on RIS-LAD (see benchmark below).

---

## 📥 Download

- 📄 Paper: <https://arxiv.org/abs/2507.20920>  
- 📦 Dataset (Google Drive): <https://drive.google.com/file/d/1na6DpdBxNbd2juyKGK9QWdqjOrEuER7v/view?usp=sharing>

```text
RIS-LAD/
├── images/              # RGB images (cropped/patches for LAD)
├── masks/               # Instance/semantic masks
├── ann/                 # Referring expressions & splits
│   ├── train.json
│   ├── val.json
│   └── test.json
└── README_DATASET.md
⚠️ Code will be released soon. You can already use the dataset for training/evaluation with your RIS pipelines.

🔍 Why LAD is different?
Low altitude (≈30–100 m) → large viewpoint variance, foreshortening.

Tiny & dense objects → ambiguous language grounding; drift becomes common.

Multi-lighting (incl. night) → domain shift vs. standard RS datasets.

🧠 Method overview (SAARN)
CDLE: inject class-level text features early in the encoder; keep description tokens out to avoid misleading activation on semantically similar objects.

ARFM: for multi-scale fusion, dynamically weight global (l), class-level (c), and descriptive (d) cues so the model reasons coarse→fine and picks the correct instance in crowds.

Backbones/text encoders are standard (e.g., Swin + BERT/CLIP text) and easy to plug into existing RIS stacks.

<div align="center"> <img src="assets/saarn_pipeline.png" width="900"/> <br/><sub>SAARN: CDLE (top) + ARFM (bottom) – semantic-aware, scale-aware fusion</sub> </div>
📊 Benchmark (RIS-LAD)
Key metrics reported in the paper:

Method	oIoU (Val)	oIoU (Test)	mIoU (Val)	mIoU (Test)
LAVT (CVPR’22)	44.03	41.97	32.25	30.14
ASDA (MM’24)	38.70	37.53	35.46	33.33
RMSIN (CVPR’24)	50.17	48.82	42.08	39.60
RSRefSeg (IGARSS’25)	50.04	47.71	43.42	41.16
SAARN (ours)	51.54	49.60	44.30	41.67

SAARN also yields large gains at strict localization thresholds (e.g., P@0.9), reflecting better instance disambiguation under density.

🧪 Quick start (dataset only)
Until code release, here’s a minimal example to parse annotations and visualize a sample.

python
复制代码
# examples/quick_vis.py
import json, os
from PIL import Image
import matplotlib.pyplot as plt

root = "RIS-LAD"
with open(os.path.join(root, "ann/val.json"), "r", encoding="utf-8") as f:
    ann = json.load(f)

item = ann[0]
img = Image.open(os.path.join(root, "images", item["image"]))
mask = Image.open(os.path.join(root, "masks", item["mask"]))
expr = item["expression"]

plt.figure(); plt.imshow(img); plt.title(expr); plt.axis("off")
plt.figure(); plt.imshow(mask); plt.title("Mask"); plt.axis("off")
plt.show()
🧱 Characteristics
<div align="center">
Dataset	Source	View	Night	Scale / Density
RefDIOR / NWPU-Refer / RISBench	High-alt RS	Top-down	✗	Large objects
RefSegRS	Helicopter	Fixed	✗	Larger objects
RIS-LAD	Drone (30–100 m)	30°–60° oblique	✓	Tiny & dense

</div>
RIS-LAD includes night scenes, oblique angles, and a semi-automatic MM-LLM + SAM-2 annotation pipeline with human verification.

📦 Planned repo structure (on code release)
text
复制代码
RIS-LAD-code/
├── saarn/                 # model (CDLE/ARFM)
├── data/                  # dataset wrappers
├── configs/               # training configs
├── tools/
│   ├── train.py
│   └── eval.py
├── scripts/               # shell scripts
└── examples/              # quick demos / visualizations
📝 Citation
If you find RIS-LAD or SAARN useful, please cite:

bibtex
复制代码
@misc{ye2025rislad,
  title   = {RIS-LAD: A Benchmark and Model for Referring Low-Altitude Drone Image Segmentation},
  author  = {Kai Ye and Yingshi Luan and Zhudi Chen and Guangyue Meng and Pingyang Dai and Liujuan Cao},
  year    = {2025},
  eprint  = {2507.20920},
  archivePrefix = {arXiv},
  primaryClass = {cs.CV},
  url     = {https://arxiv.org/abs/2507.20920}
}
📬 Contact
Questions / collaboration ideas?
Open an issue or email yekai@stu.xmu.edu.cn.

🔐 License & usage
Dataset: released for research purposes only. Please follow the terms in the dataset’s own README.

Code: license will be specified upon release.
