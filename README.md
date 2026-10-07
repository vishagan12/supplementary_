# Supplementary materials — ICVGIP 2026, Submission 497

**Causal Video Segmentation of Moving Objects in Dashcam Scenes Under Challenging Visual Conditions**

This repository holds the **OpenReview rebuttal** (by reviewer) and **appendix Tables 6–7** for the manuscript. All rebuttal text is in Markdown so it renders directly on GitHub.

---

## Rebuttal (Action Taken Report)

| Reviewer | Markdown file | # questions |
|----------|---------------|-------------|
| Reviewer 1 | [rebuttal-reviewer-1.md](rebuttal-reviewer-1.md) | 1 |
| Reviewer 2 | [rebuttal-reviewer-2.md](rebuttal-reviewer-2.md) | 12 |
| Reviewer 3 | [rebuttal-reviewer-3.md](rebuttal-reviewer-3.md) | 5 |

Each file includes the submission header and that reviewer’s questions, answers, and any tables cited in those answers.

---

## Appendix Table 6 — Tri-stage restoration ablation and hyperparameter sensitivity

*Manuscript Table 4. SAM 3 + causal segmentation held fixed. **Bold** = manuscript defaults / best in each sweep block.*

| Restoration pipeline stage | Hyperparameters | mIoU (%) | mTC (%) |
|----------------------------|-----------------|----------|---------|
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

## Appendix Table 7 — Comparative benchmark (excerpt)

*Manuscript Table 2. Identical curated multi-scenario dashcam video sequences.*

| Method | mIoU (%) | mTC (%) | FPS |
|--------|----------|---------|-----|
| SAM (per-frame zero-shot) | 62.5 | 64.1 | 12.3 |
| SAM 2 (streaming video) | 71.6 | 85.1 | 22.4 |
| **Restoration + SAM 3 (causal PCS) — ours** | **74.8** | **88.4** | **28.6** |

---

## Other files

| File | Use |
|------|-----|
| [appendix_tables.pdf](appendix_tables.pdf) | Tables 6–7 — preview in browser |
| [appendix_tables.docx](appendix_tables.docx) | Tables 6–7 — Word; use **Download** (do not open `.docx` in the GitHub tab) |

**Repo:** https://github.com/vishagan12/supplementary_
