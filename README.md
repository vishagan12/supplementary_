# Supplementary tables

Quantitative results from the dashcam causal segmentation manuscript. **Bold** rows highlight our proposed configuration (or the best metric in each sweep block, as in Table 4).

---

## Table 2 — Comparative benchmark (excerpt)

| Method (manuscript Table 2) | mIoU (%) | mTC (%) | FPS |
|-----------------------------|----------|---------|-----|
| SAM (per-frame zero-shot) | 62.5 | 64.1 | 12.3 |
| SAM 2 (streaming video) | 71.6 | 85.1 | 22.4 |
| **Restoration + SAM 3 (causal PCS) — ours** | **74.8** | **88.4** | **28.6** |

---

## Table 4 — Restoration pipeline (component-wise and hyperparameter sweeps)

| Restoration pipeline stage (manuscript Table 4) | Hyperparameters | mIoU (%) | mTC (%) |
|-------------------------------------------------|-----------------|----------|---------|
| Raw input (no restoration) | — | **65.4** | 77.2 |
| + Stage 1: flare suppression | τ_flare = 220 | 67.3 | 79.5 |
| + Stage 1: flare suppression | τ_flare = 240 | **68.6** | **81.0** |
| + Stage 1: flare suppression | τ_flare = 260 | 67.9 | 79.4 |
| + Stage 2: DCP dehazing (guided) | σ = 2.0 | 70.2 | 83.2 |
| + Stage 2: DCP dehazing (guided) | σ = 3.0 | **71.4** | **84.6** |
| + Stage 2: DCP dehazing (guided) | σ = 4.0 | 70.6 | 83.0 |
| + Stage 3: CLAHE & gamma | γ = 0.8 | 71.2 | 85.9 |
| + Stage 3: CLAHE & gamma | γ = 1.4 | **73.1** | **86.8** |
| + Stage 3: CLAHE & gamma | γ = 2.2 | 71.6 | 86.2 |
| Tri-stage photometric pipeline | — | **74.8** | **88.4** |

---

## Table 5 — Embedded efficiency (Jetson AGX Orin, FP16)

| Framework (Jetson AGX Orin, FP16 — manuscript Table 5) | Restoration (ms) | Seg. (ms) | FPS | Peak VRAM (MB) |
|----------------------------------------------------------|------------------|-----------|-----|----------------|
| YOLOv11s + SAM | 5.8 | 92.4 | 10.2 | 6480 |
| Grounding DINO + SAM | 5.8 | 128.2 | 7.8 | 7920 |
| **Proposed causal pipeline** | **5.8** | **29.1** | **28.6** | **4005** |

---

## Downloadable copies

| File | Description |
|------|-------------|
| [appendix_tables.pdf](appendix_tables.pdf) | Same tables in PDF layout |
| [appendix_tables.docx](appendix_tables.docx) | Editable Word — use **Download** on the file page (do not open `.docx` in the GitHub browser tab) |

**Repository:** https://github.com/vishagan12/supplementary_
