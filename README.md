<p align="center">
  <img src="img/cover_rislad.jpg" alt="RIS-LAD Teaser" width="88%">
</p>

<h1 align="center">RIS-LAD: Referring Low-Altitude Drone Image Segmentation</h1>

<p align="center">
  <a href="https://arxiv.org/abs/2507.20920">
    <img src="https://img.shields.io/badge/arXiv-2507.20920-B31B1B?logo=arxiv&logoColor=white" alt="arXiv">
  </a>
  <a href="https://drive.google.com/file/d/1na6DpdBxNbd2juyKGK9QWdqjOrEuER7v/view?usp=sharing">
    <img src="https://img.shields.io/badge/Dataset-Google%20Drive-ffb300?logo=googledrive&logoColor=white" alt="Dataset">
  </a>
  <img src="https://img.shields.io/badge/Code-Coming%20Soon-4C9A2A" alt="Code coming soon">
</p>

<p align="center">
  <b>RIS-LAD</b> is the first fine-grained Referring Image Segmentation benchmark for <b>low-altitude drone (LAD)</b> scenes, featuring <b>13,871</b> image–text–mask triplets.<br>
  We also introduce <b>SAARN</b> (Semantic-Aware Adaptive Reasoning Network) with <b>CDLE</b> and <b>ARFM</b> to tackle LAD-specific <i>category drift</i> and <i>object drift</i>.
</p>

---

## 🔗 Quick Links

- Paper (arXiv): https://arxiv.org/abs/2507.20920  
- Dataset (Google Drive): https://drive.google.com/file/d/1na6DpdBxNbd2juyKGK9QWdqjOrEuER7v/view?usp=sharing  
- Model & Code: _coming soon_

---

## ✨ Highlights

<p align="center">
  <img src="img/lad_vs_rs.jpg" alt="LAD vs conventional RS scenes" width="90%"><br>
  <sub>Oblique views, low altitude, night scenes, tiny & dense targets.</sub>
</p>

- **New LAD Benchmark** — Oblique views (30°–60°), low altitude (≈30–100 m), multi-lighting (incl. night), **tiny & dense** targets.  
- **13,871 Triplets** — Image, referring expression, and segmentation mask with human-verified quality.  
- **SAARN Framework** —  
  - **CDLE**: early **class-guided** alignment to suppress _category drift_.  
  - **ARFM**: scale-aware fusion of **global (l)**, **class (c)**, and **descriptive (d)** cues to mitigate _object drift_.  
- **Strong Baseline** — SOTA on RIS-LAD with clear gains under strict thresholds (e.g., P@0.9).

---

## 🗂️ Dataset Layout (suggested)

```
RIS-LAD/
├─ images/                 # RGB images (LAD patches)
├─ masks/                  # Segmentation masks
├─ ann/                    # Referring expressions & splits
│  ├─ train.json
│  ├─ val.json
│  └─ test.json
└─ README_DATASET.md
```

---

## 🧠 Method (SAARN) at a Glance

<p align="center">
  <img src="img/saarn_overview.png" alt="SAARN overall framework" width="92%"><br>
  <sub>CDLE injects early class-level cues; ARFM performs scale-aware reasoning with global (l), class (c), and descriptive (d) features.</sub>
</p>

### CDLE: Category-Dominated Linguistic Enhancement
<p align="center">
  <img src="img/cdle_block.png" alt="CDLE module" width="78%">
</p>

### ARFM: Adaptive Reasoning Fusion Module
<p align="center">
  <img src="img/arfm_block.png" alt="ARFM module" width="78%">
</p>

---

## 📊 Benchmark on RIS-LAD

<p align="center">
  <img src="img/benchmark_bars.png" alt="oIoU/mIoU bar chart" width="88%">
</p>

| Method | oIoU (Val) | oIoU (Test) | mIoU (Val) | mIoU (Test) |
|---|---:|---:|---:|---:|
| LAVT (CVPR’22) | 44.03 | 41.97 | 32.25 | 30.14 |
| ASDA (MM’24) | 38.70 | 37.53 | 35.46 | 33.33 |
| RMSIN (CVPR’24) | 50.17 | 48.82 | 42.08 | 39.60 |
| RSRefSeg (IGARSS’25) | 50.04 | 47.71 | 43.42 | 41.16 |
| **SAARN (ours)** | **51.54** | **49.60** | **44.30** | **41.67** |

> SAARN excels at strict thresholds (e.g., **P@0.9**), indicating better instance disambiguation in dense scenes.

---

## 🔎 Why LAD is Different

<p align="center">
  <img src="img/dataset_comparison.png" alt="Dataset comparison table figure" width="90%">
</p>

| Factor | Conventional RS | **RIS-LAD (ours)** |
|---|---|---|
| Viewpoint | Top-down, fixed | **Oblique (30°–60°), varied** |
| Altitude | High | **Low (≈30–100 m)** |
| Illumination | Day | **Day & Night** |
| Scale/Density | Larger, sparser | **Tiny & dense** |

---

## 🎨 Qualitative Examples

<table align="center">
  <tr>
    <td align="center" valign="middle">
      <img src="img/qual_tiny_1.jpg" alt="Tiny-object case A" width="95%"><br>
      <sub>Tiny-object case A</sub>
    </td>
    <td align="center" valign="middle">
      <img src="img/qual_tiny_2.jpg" alt="Tiny-object case B" width="95%"><br>
      <sub>Tiny-object case B</sub>
    </td>
  </tr>
  <tr>
    <td align="center" valign="middle">
      <img src="img/qual_dense_1.jpg" alt="Dense same-class case A" width="95%"><br>
      <sub>Dense same-class case A</sub>
    </td>
    <td align="center" valign="middle">
      <img src="img/qual_dense_2.jpg" alt="Dense same-class case B" width="95%"><br>
      <sub>Dense same-class case B</sub>
    </td>
  </tr>
</table>

---

## 🧭 Roadmap

- [ ] Release training & evaluation code for SAARN  
- [ ] Add dataset loaders for popular toolkits  
- [ ] Provide pretrained weights & full configs  
- [ ] Add extended qualitative gallery and failure cases

---

## 📝 Citation

If you find RIS-LAD or SAARN helpful, please cite:

```bibtex
@misc{ye2025risladbenchmarkmodelreferring, 
  title        = {RIS-LAD: A Benchmark and Model for Referring Low-Altitude Drone Image Segmentation}, 
  author       = {Kai Ye and YingShi Luan and Zhudi Chen and Guangyue Meng and Pingyang Dai and Liujuan Cao},
  year         = {2025},
  eprint       = {2507.20920},
  archivePrefix= {arXiv},
  primaryClass = {cs.CV},
  url          = {https://arxiv.org/abs/2507.20920}
}
```

---

## 📫 Contact & License

- Questions? Open an issue or email **yekai@stu.xmu.edu.cn**  
- **Dataset**: research use only (see dataset README for terms)  
- **Code**: license will be provided upon release

