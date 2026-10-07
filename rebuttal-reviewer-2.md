# Action Taken Report

## ICVGIP 2026 — Submission 497

### Causal Video Segmentation of Moving Objects in Dashcam Scenes Under Challenging Visual Conditions

## Reviewer 2

### Reviewer 2 — Q1

Question: The fundamental contribution of the manuscript remains unclear, as the proposed framework primarily acts as a wrapper around existing methodologies rather than introducing a novel architectural advancement.

Answer: The fundamental contribution is the task specific causal integration of individual restoration operations, SAM 3 PCS /temporal memory for challenging dashcam video. The proposed pipeline combines (i) training-free photometric restoration for glare, scattering and low-light degradation, (ii) SAM 3 PCS with a FIFO causal memory of 16 keyframes for online temporal consistency, and (iii) evaluation of the failure modes of commonly used cascaded and feature-based approaches under ego-motion. The controlled results support this design: mIoU improves from 65.4% without restoration to 74.8% with the full pipeline, while the proposed method reaches 74.8% mIoU, 88.4% mTC and 28.6 FPS.

### Reviewer 2 — Q2

Question: Contribution 1 highlights the use of Gaussian feathering, DCP dehazing, and CLAHE with gamma adjustment. These are classic, widely known image processing techniques that are simply being repackaged as a "proposed Tri-Stage Photometric restoration."

Answer: We agree. We do not claim novelty for these individual operations. Our contribution is their task-specific sequential integration into a lightweight, training-free restoration pipeline for dashcam degradation. The three stages respectively address flare/glare, atmospheric scattering, and low-light/contrast degradation. With the SAM 3 causal engine fixed, Table 4 shows a consistent improvement from 65.4% to 74.8% mIoU and from 77.2% to 88.4% mTC as the restoration stages are added.

### Reviewer 2 — Q3

Question: Contribution 2 (Lines 254–258) is misrepresented as an architectural novelty. Promptable Concept Segmentation (PCS) is a native, out-of-the-box capability of the underlying SAM 3 model.

Answer: Promptable Concept Segmentation (PCS) is a native capability of SAM 3 and is not claimed as our contribution. Our contribution is the integration of SAM 3 PCS with the restoration pipeline and a FIFO causal memory (L_max = 16) for online dashcam video segmentation. We have clarified this distinction in our response.

### Reviewer 2 — Q4

Question: Contributions 3 and 4 solely reflect routine evaluations, experiments, and results rather than distinct architectural or theoretical contributions.

Answer: We agree that the failure-mode analysis and benchmark evaluation are empirical contributions. Their purpose is to systematically show how ego-motion, glare, scale changes and proposal dropouts affect existing cascaded approaches and to support the design choices of our proposed pipeline.

### Reviewer 2 — Q5

Question: The restoration pipeline relies on hardcoded, empirical thresholds (τ_flare=240, σ=3.0, γ=1.40). These rigid heuristics make the system inherently brittle across varying camera sensors, ISO gains, and dynamic range shifts.

Answer: We agree that the restoration uses fixed values of τ_flare = 240, σ = 3.0 and γ = 1.40. These parameters were kept fixed for all frames in the stated HDR acquisition setting rather than tuned separately for each test frame. Therefore, our results should be interpreted within this defined camera and operating range, not as sensor-independent robustness. Within this setting, Table 4 shows that the restoration stages consistently improve segmentation from 65.4% to 74.8% mIoU and from 77.2% to 88.4% mTC. We have also stated this limitation rather than claiming universal sensor generalization.

Table 4: Component-wise hyperparameter ablation of the tri-stage photometric restoration pipeline evaluated with the SAM3 causal segmentation engine.

| Restoration pipeline stage<br>(manuscript Table 4) | Hyperparameters | mIoU (%) | mTC (%) |
| --- | --- | --- | --- |
| Raw input (no restoration) | — | 65.4 | 77.2 |
| + Stage 1: flare suppression | τ_flare=220 | 67.3 | 79.5 |
| + Stage 1: flare suppression | τ_flare=240 | 68.6 | 81.0 |
| + Stage 1: flare suppression | τ_flare=260 | 67.9 | 79.4 |
| + Stage 2: DCP dehazing (guided) | σ = 2.0 | 70.2 | 83.2 |
| + Stage 2: DCP dehazing (guided) | σ = 3.0 | 71.4 | 84.6 |
| + Stage 2: DCP dehazing (guided) | σ = 4.0 | 70.6 | 83.0 |
| + Stage 3: CLAHE & gamma | γ = 0.8 | 71.2 | 85.9 |
| + Stage 3: CLAHE & gamma | γ = 1.4 | 73.1 | 86.8 |
| + Stage 3: CLAHE & gamma | γ = 2.2 | 71.6 | 86.2 |
| Tri-stage photometric pipeline | — | 74.8 | 88.4 |

### Reviewer 2 — Q6

Question: Because the classical restoration module is fully decoupled from the segmentation engine, any visual artifacts or noise amplified by the CLAHE/DCP filters permanently corrupt downstream Vision Transformer tokens without any end-to-end gradient flow to self-correct.

Answer: True that the restoration module is training-free and is not jointly optimized with the segmentation network. This is intentional to keep the restoration lightweight and independent of training. However, the claim that restoration artifacts permanently corrupt the segmentation features is not supported by our results. With the same SAM 3 causal engine, the restoration ablation in Table 4 improves mIoU from 65.4% without restoration to 74.8% with the full pipeline, and mTC from 77.2% to 88.4%. Thus, within our evaluated dashcam conditions, the restoration provides a net improvement rather than a measured degradation.

### Reviewer 2 — Q7

Question: Table 2 compares a SAM 2 baseline against the SAM 3-based pipeline to claim superior segmentation accuracy (Line 266). However, the manuscript fails to apply the proposed tri-stage photometric restoration module across all baseline architectures to properly isolate the mIoU, mTC, and VRAM improvements attributable to the restoration versus the SAM 3 backbone upgrade.

Answer: Table 4 provides this controlled ablation by keeping the SAM 3 causal engine fixed. With raw input, the same engine gives 65.4% mIoU and 77.2% mTC. Adding the complete restoration pipeline increases these values to 74.8% mIoU and 88.4% mTC, giving +9.4 percentage points in mIoU and +11.2 percentage points in mTC. Therefore, the improvement is not attributed only to the SAM 3 backbone.

### Reviewer 2 — Q8

Question: The manuscript entirely lacks cross-dataset performance evaluation to prove out-of-domain generalization.

Answer: We agree that this is not a cross-dataset evaluation. Our evaluation is multi-domain within the acquired dataset, covering four conditions: urban arterials, suburban shadow transitions, high-speed expressways, and adverse rain/fog. As shown in Table 3, the proposed method gives the best mIoU in all four domains: 76.4%, 73.2%, 75.8%, and 73.9%, with 74.8% overall. These results show consistent performance under different dashcam conditions. We do not claim independent cross-dataset generalization.

### Reviewer 2 — Q9

Question: Section 4.1 presents a major ambiguity regarding whether the data was originally acquired or simply curated. The section title mentions "acquisition", Line 488 states it was "curated", and Line 489 states it was "acquired." If original acquisition, exact dataset details, camera hardware, and capture conditions must be provided. If curated from existing public datasets, the sources must be cited.

Answer: Yes. the terms “acquired” and “curated” were unclear. The video was acquired using a windshield-mounted HDR optical sensor at 2560×1440 resolution and 20 FPS, with more than 120 dB dynamic range. The footage was then organized into four domains, and 4,500 continuous frames were densely annotated for five classes. Here, “curated” only means the domain organization and annotation process. The data were not taken from any public dataset.

### Reviewer 2 — Q10

Question: Lines 629–630: The phrase "our causal memory framework" is ambiguous and should explicitly specify which framework configuration is being referenced.

Answer: The phrase “our causal memory framework” was ambiguous. We refer specifically to the proposed SAM 3 PCS configuration with the FIFO causal memory of L_max = 16 described in Section 3.3.2.

### Reviewer 2 — Q11

Question: Figure 3 Sub-caption: The acronym "CA" is undefined.

Answer: As per the suggestion given by the reviewer, the acronym is now defined at first use in the caption.

### Reviewer 2 — Q12

Question: Margin Errors: Text is overflowing the document margins on Lines 291 and 385.

Answer: As per the reviewer comments, the margin errors have been corrected in the revised manuscript.
