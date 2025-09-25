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
  We introduce <b>SAARN</b> (Semantic-Aware Adaptive Reasoning Network) with <b>CDLE</b> and <b>ARFM</b> to tackle LAD-specific <i>category drift</i> and <i>object drift</i>.
</p>

---

## 🔗 Quick Links

- Paper (arXiv): https://arxiv.org/abs/2507.20920  
- Dataset (Google Drive): https://drive.google.com/file/d/1na6DpdBxNbd2juyKGK9QWdqjOrEuER7v/view?usp=sharing  
- Model & Code: _coming soon_

---

## 🧾 Introduction

Low-altitude drones (typically operating below ~200 m) are increasingly deployed in real-world perception systems thanks to their flexibility and cost-effectiveness. However, most existing referring image segmentation (RIS) research focuses on conventional ground-view scenes or high-altitude remote sensing imagery. These settings differ substantially from low-altitude drone (LAD) views, where perspectives are oblique, objects are tiny and densely packed, and illumination varies widely (including night scenes).

To bridge this gap, we present <b>RIS-LAD</b>, a fine-grained benchmark specifically designed for <b>Referring Low-Altitude Drone Image Segmentation (RLADIS)</b>. RIS-LAD offers <b>13,871</b> carefully verified image–text–mask triplets collected from real LAD footage. Beyond providing data, RIS-LAD formalizes two key failure modes frequently observed under LAD settings:
- <b>Category drift</b>: when tiny targets cause models to latch onto larger, semantically similar objects.
- <b>Object drift</b>: when crowds of same-class instances lead to confusion about which instance the expression refers to.

We further propose <b>SAARN</b> (Semantic-Aware Adaptive Reasoning Network) to tackle these challenges. SAARN introduces:
- <b>CDLE</b> (Category-Dominated Linguistic Enhancement): injects <i>class-level</i> linguistic cues early in the encoder to anchor visual features to the correct category and suppress category drift.
- <b>ARFM</b> (Adaptive Reasoning Fusion Module): performs <i>scale-aware</i> fusion of <i>global (l)</i>, <i>class (c)</i>, and <i>descriptive (d)</i> text cues, enabling coarse→fine reasoning and disambiguation among dense same-class instances.

RIS-LAD is built with a semi-automatic pipeline that combines high-quality instance masks (prompted SAM-2) and multimodal LLM–generated initial expressions (given cropped instances and location cues), followed by human refinement. Experiments on RIS-LAD show that <b>SAARN</b> achieves state-of-the-art results on core segmentation metrics and yields pronounced gains at stricter localization thresholds (e.g., P@0.9), demonstrating stronger instance-level discrimination under LAD conditions.

---

## ✨ Highlights (Fig. 1 in paper)

<p align="center">
  <img src="img/first.png" alt="Fig. 1: RLADIS challenges teaser" width="92%"><br>
  <sub><b>Figure 1.</b> RLADIS challenges vs. RRSIS (category/object drift, tiny & dense objects, illumination).</sub>
</p>

- Oblique views (30°–60°), low altitude (≈30–100 m), multi-lighting (incl. night).  
- Tiny & dense targets; LAD-specific <i>category drift</i> and <i>object drift</i>.  

---

## 🏗️ Annotation Pipeline (Fig. 2)

<p align="center">
  <img src="img/annotation_pipeline.png" alt="Fig. 2: Semi-automatic annotation pipeline" width="92%"><br>
  <sub><b>Figure 2.</b> Semi-automatic pipeline: SAM-2 masks + MLLM expressions (with crop & location cues) + human refinement.</sub>
</p>

---

## 🧠 Method Overview – SAARN (Fig. 3)

<p align="center">
  <img src="img/saarn_overview.png" alt="Fig. 3: SAARN overall framework" width="92%"><br>
  <sub><b>Figure 3.</b> SAARN with CDLE and ARFM for semantic-aware, scale-aware reasoning.</sub>
</p>

### CDLE Module (Fig. 4)

<p align="center">
  <img src="img/cdle_block.png" alt="Fig. 4: Category-Dominated Linguistic Enhancement" width="78%"><br>
  <sub><b>Figure 4.</b> CDLE injects class-level cues early; guards against description-induced drift.</sub>
</p>

### ARFM Module (Fig. 5)

<p align="center">
  <img src="img/arfm_block.png" alt="Fig. 5: Adaptive Reasoning Fusion Module" width="78%"><br>
  <sub><b>Figure 5.</b> ARFM dynamically weighs global (l), class (c), and descriptive (d) cues across scales.</sub>
</p>

---

## 📊 Dataset Characteristics (Table/Fig. in paper)

<p align="center">
  <img src="img/dataset_comparison.png" alt="Dataset comparison chart (RIS-LAD vs RRSIS)" width="90%"><br>
  <sub><b>Dataset Comparison.</b> RIS-LAD (drone, oblique, night scenes) vs. existing RRSIS datasets.</sub>
</p>

<p align="center">
  <img src="img/wordcloud.png" alt="Word cloud of referring expressions" width="70%"><br>
  <sub><b>Word Cloud.</b> Linguistic diversity of referring expressions in RIS-LAD.</sub>
</p>

---

## 🖼️ Qualitative Comparisons (Fig. in paper)

<p align="center">
  <img src="img/visual.png" alt="Qualitative comparisons: tiny objects & dense scenes" width="96%"><br>
  <sub><b>Qualitative Results.</b> SAARN vs. prior SOTA on tiny-object and dense same-class cases.</sub>
</p>

---

## 📈 Benchmark Results (Table/Fig. in paper)

<p align="center">
  <img src="img/benchmark_main.png" alt="Main benchmark results (oIoU/mIoU and P@X)" width="90%"><br>
  <sub><b>Benchmark.</b> SAARN achieves SOTA on RIS-LAD with gains at strict thresholds (P@0.9).</sub>
</p>

| Method | oIoU (Val) | oIoU (Test) | mIoU (Val) | mIoU (Test) |
|---|---:|---:|---:|---:|
| LAVT (CVPR’22) | 44.03 | 41.97 | 32.25 | 30.14 |
| ASDA (MM’24) | 38.70 | 37.53 | 35.46 | 33.33 |
| RMSIN (CVPR’24) | 50.17 | 48.82 | 42.08 | 39.60 |
| RSRefSeg (IGARSS’25) | 50.04 | 47.71 | 43.42 | 41.16 |
| **SAARN (ours)** | **51.54** | **49.60** | **44.30** | **41.67** |

---

## 🧭 Roadmap

- [ ] Release training & evaluation code for SAARN  
- [ ] Add dataset loaders for popular toolkits  
- [ ] Provide pretrained weights & full configs  
- [ ] Add extended qualitative gallery and failure cases

---

## 📝 Citation

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

- Issues or questions: **yekai@stu.xmu.edu.cn**  
- Dataset: research use only (see dataset README)  
- Code: license will be provided upon release

