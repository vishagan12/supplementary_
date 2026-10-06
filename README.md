# Supplementary tables

Appendix **Tables 6 and 7** for dashcam causal video segmentation. **Bold** rows highlight our proposed configuration or the best metric in each sweep block.

---

## Table 6 — Tri-stage restoration ablation and hyperparameter sensitivity

*Component-wise ablation and one-at-a-time hyperparameter sweeps for the photometric restoration pipeline, evaluated with SAM 3 + causal segmentation fixed (manuscript Table 4).*

| Restoration pipeline stage (Table 6) | Hyperparameters | mIoU (%) | mTC (%) |
|--------------------------------------|-----------------|----------|---------|
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

## Table 7 — Comparative benchmark (excerpt)

*State-of-the-art comparison on identical curated multi-scenario dashcam video sequences (manuscript Table 2).*

| Method (Table 7) | mIoU (%) | mTC (%) | FPS |
|------------------|----------|---------|-----|
| SAM (per-frame zero-shot) | 62.5 | 64.1 | 12.3 |
| SAM 2 (streaming video) | 71.6 | 85.1 | 22.4 |
| **Restoration + SAM 3 (causal PCS) — ours** | **74.8** | **88.4** | **28.6** |

---

## Downloadable copies

| File | Description |
|------|-------------|
| [appendix_tables.pdf](appendix_tables.pdf) | Tables 6 and 7 in PDF layout |
| [appendix_tables.docx](appendix_tables.docx) | Editable Word — use **Download** on the file page (do not open `.docx` in the GitHub browser tab) |

**Repository:** https://github.com/vishagan12/supplementary_
