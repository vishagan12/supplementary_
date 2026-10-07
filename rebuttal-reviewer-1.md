# Action Taken Report

## ICVGIP 2026 — Submission 497

### Causal Video Segmentation of Moving Objects in Dashcam Scenes Under Challenging Visual Conditions

## Reviewer 1

### Reviewer 1 — Q1

**Question: **The fixed hyperparameters are empirically set with no analysis reported. A single study on parameters which control flare suppression or tone expansion would strengthen the paper.

**Answer: **The restoration parameters are explicitly reported in Section 3.2, including τ_flare = 240, σ = 3.0, β = 0.45, ω = 0.95 and γ = 1.40. Their effect is indirectly studied through the restoration ablation in Table 4, where the SAM 3 causal engine is kept fixed. Adding the restoration stages progressively improves mIoU from 65.4% to 68.6%, 71.4%, 73.1%, and finally 74.8%, while mTC improves from 77.2% to 88.4%. Thus, the reported results show that the selected restoration settings contribute consistently to the final segmentation performance. **Table 4: Component-wise hyperparameter ablation of the tri-stage photometric restoration pipeline evaluated with the SAM3 causal segmentation engine. **

| **Restoration pipeline stage **<br>**(manuscript Table 4)** | **Hyperparameters ** | **mIoU (%)** | **mTC (%)** |
| --- | --- | --- | --- |
| **Raw input (no restoration)** | **—** | **65.4** | **77.2** |
| + Stage 1: flare suppression | τ_flare=220 | 67.3 | 79.5 |
| **+ Stage 1: flare suppression** | **τ_flare=240** | **68.6** | **81.0** |
| + Stage 1: flare suppression | τ_flare=260 | 67.9 | 79.4 |
| + Stage 2: DCP dehazing (guided) | σ = 2.0 | 70.2 | 83.2 |
| **+ Stage 2: DCP dehazing (guided)** | **σ = 3.0** | **71.4** | **84.6** |
| + Stage 2: DCP dehazing (guided) | σ = 4.0 | 70.6 | 83.0 |
| + Stage 3: CLAHE & gamma | γ = 0.8 | 71.2 | 85.9 |
| **+ Stage 3: CLAHE & gamma** | **γ = 1.4** | **73.1** | **86.8** |
| + Stage 3: CLAHE & gamma | γ = 2.2 | 71.6 | 86.2 |
| **Tri-stage photometric pipeline** | **—-** | **74.8** | **88.4** |
