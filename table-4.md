# Table 4

Component-wise hyperparameter ablation of the tri-stage photometric restoration pipeline evaluated with the SAM 3 causal segmentation engine.

| Restoration pipeline stage (manuscript Table 4) | Hyperparameters | mIoU (%) | mTC (%) |
| --- | --- | --- | --- |
| Raw input (no restoration) | — | 65.4 | 77.2 |
| + Stage 1: flare suppression | τ_flare = 220 | 67.3 | 79.5 |
| + Stage 1: flare suppression | τ_flare = 240 | 68.6 | 81.0 |
| + Stage 1: flare suppression | τ_flare = 260 | 67.9 | 79.4 |
| + Stage 2: DCP dehazing (guided) | σ = 2.0 | 70.2 | 83.2 |
| + Stage 2: DCP dehazing (guided) | σ = 3.0 | 71.4 | 84.6 |
| + Stage 2: DCP dehazing (guided) | σ = 4.0 | 70.6 | 83.0 |
| + Stage 3: CLAHE & gamma | γ = 0.8 | 71.2 | 85.9 |
| + Stage 3: CLAHE & gamma | γ = 1.4 | 73.1 | 86.8 |
| + Stage 3: CLAHE & gamma | γ = 2.2 | 71.6 | 86.2 |
| Tri-stage photometric pipeline | — | 74.8 | 88.4 |
