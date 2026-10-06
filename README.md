# Supplementary tables (ICVGIP rebuttal)

One-at-a-time **hyperparameter sensitivity** sweeps for the classical restoration pipeline (extension of manuscript **Table 4**). **SAM 3 + causal segmentation** is held fixed; metrics are **mIoU** and **mTC** (Section 4.2) on restored dashcam video. **Bold** rows are the manuscript defaults.

---

## Table 6 — Flare threshold τ_flare (Stage 1)

Stage 1 flare suppression only (Section 3.2, Eq. 2); other restoration stages off for this block.

| Restoration stage | Hyperparameters | mIoU (%) | mTC (%) |
|-------------------|-----------------|----------|---------|
| Raw input (no restoration) | — | 65.4 | 77.2 |
| + Stage 1: flare suppression | τ_flare = 220 | 67.3 | 79.5 |
| + Stage 1: flare suppression | **τ_flare = 240** | **68.6** | **81.0** |
| + Stage 1: flare suppression | τ_flare = 260 | 67.9 | 79.4 |

---

## Table 7 — Gaussian scale σ (Stage 2)

Stages 1–2 active; **τ_flare = 240** fixed (Section 3.2, Eq. 3).

| Restoration stage | Hyperparameters | mIoU (%) | mTC (%) |
|-------------------|-----------------|----------|---------|
| Raw input (no restoration) | — | 65.4 | 77.2 |
| + Stage 2: DCP dehazing (guided) | σ = 2.0 | 70.2 | 83.2 |
| + Stage 2: DCP dehazing (guided) | **σ = 3.0** | **71.4** | **84.6** |
| + Stage 2: DCP dehazing (guided) | σ = 4.0 | 70.6 | 83.0 |

---

## Table 8 — Gamma γ (Stage 3)

Stages 1–3 active; **τ_flare = 240**, **σ = 3.0** fixed (Section 3.2, Eq. 10).

| Restoration stage | Hyperparameters | mIoU (%) | mTC (%) |
|-------------------|-----------------|----------|---------|
| Raw input (no restoration) | — | 65.4 | 77.2 |
| + Stage 3: CLAHE & gamma | γ = 0.8 | 71.2 | 85.9 |
| + Stage 3: CLAHE & gamma | **γ = 1.4** | **73.1** | **86.8** |
| + Stage 3: CLAHE & gamma | γ = 2.2 | 71.6 | 86.2 |

**Full tri-stage pipeline (manuscript Table 4, final row):** 74.8% mIoU / 88.4% mTC (all three stages at defaults above).

---

## Downloadable copies

| File | Description |
|------|-------------|
| [appendix_tables.pdf](appendix_tables.pdf) | Same tables, PDF layout |
| [appendix_tables.docx](appendix_tables.docx) | Editable Word (use **Download** on the file page; do not open `.docx` in the GitHub browser tab) |

**Repository:** https://github.com/vishagan12/supplementary_
