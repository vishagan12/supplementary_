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

## Reviewer 2

### Reviewer 2 — Q1

**Question: **The fundamental contribution of the manuscript remains unclear, as the proposed framework primarily acts as a wrapper around existing methodologies rather than introducing a novel architectural advancement.

**Answer: **The fundamental contribution is the task specific causal integration of individual restoration operations, SAM 3 PCS /temporal memory for challenging dashcam video. The proposed pipeline combines (i) training-free photometric restoration for glare, scattering and low-light degradation, (ii) SAM 3 PCS with a FIFO causal memory of 16 keyframes for online temporal consistency, and (iii) evaluation of the failure modes of commonly used cascaded and feature-based approaches under ego-motion. The controlled results support this design: mIoU improves from 65.4% without restoration to 74.8% with the full pipeline, while the proposed method reaches 74.8% mIoU, 88.4% mTC and 28.6 FPS.

### Reviewer 2 — Q2

**Question: **Contribution 1 highlights the use of Gaussian feathering, DCP dehazing, and CLAHE with gamma adjustment. These are classic, widely known image processing techniques that are simply being repackaged as a "proposed Tri-Stage Photometric restoration."

**Answer: **We agree. We do not claim novelty for these individual operations. Our contribution is their task-specific sequential integration into a lightweight, training-free restoration pipeline for dashcam degradation. The three stages respectively address flare/glare, atmospheric scattering, and low-light/contrast degradation. With the SAM 3 causal engine fixed, Table 4 shows a consistent improvement from 65.4% to 74.8% mIoU and from 77.2% to 88.4% mTC as the restoration stages are added.

### Reviewer 2 — Q3

**Question: **Contribution 2 (Lines 254–258) is misrepresented as an architectural novelty. Promptable Concept Segmentation (PCS) is a native, out-of-the-box capability of the underlying SAM 3 model.

**Answer: **Promptable Concept Segmentation (PCS) is a native capability of SAM 3 and is not claimed as our contribution. Our contribution is the integration of SAM 3 PCS with the restoration pipeline and a FIFO causal memory (L_max = 16) for online dashcam video segmentation. We have clarified this distinction in our response.

### Reviewer 2 — Q4

**Question: **Contributions 3 and 4 solely reflect routine evaluations, experiments, and results rather than distinct architectural or theoretical contributions.

**Answer:** We agree that the failure-mode analysis and benchmark evaluation are empirical contributions. Their purpose is to systematically show how ego-motion, glare, scale changes and proposal dropouts affect existing cascaded approaches and to support the design choices of our proposed pipeline.

### Reviewer 2 — Q5

**Question: **The restoration pipeline relies on hardcoded, empirical thresholds (τ_flare=240, σ=3.0, γ=1.40). These rigid heuristics make the system inherently brittle across varying camera sensors, ISO gains, and dynamic range shifts.

**Answer: **We agree that the restoration uses fixed values of τ_flare = 240, σ = 3.0 and γ = 1.40. These parameters were kept fixed for all frames in the stated HDR acquisition setting rather than tuned separately for each test frame. Therefore, our results should be interpreted within this defined camera and operating range, not as sensor-independent robustness. Within this setting, Table 4 shows that the restoration stages consistently improve segmentation from 65.4% to 74.8% mIoU and from 77.2% to 88.4% mTC. We have also stated this limitation rather than claiming universal sensor generalization. **Table 4: Component-wise hyperparameter ablation of the tri-stage photometric restoration pipeline evaluated with the SAM3 causal segmentation engine. **

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
| **Tri-stage photometric pipeline** | **—** | **74.8** | **88.4** |

### Reviewer 2 — Q6

**Question: **Because the classical restoration module is fully decoupled from the segmentation engine, any visual artifacts or noise amplified by the CLAHE/DCP filters permanently corrupt downstream Vision Transformer tokens without any end-to-end gradient flow to self-correct.

**Answer:** True that the restoration module is training-free and is not jointly optimized with the segmentation network. This is intentional to keep the restoration lightweight and independent of training. However, the claim that restoration artifacts permanently corrupt the segmentation features is not supported by our results. With the same SAM 3 causal engine, the restoration ablation in Table 4 improves mIoU from 65.4% without restoration to 74.8% with the full pipeline, and mTC from 77.2% to 88.4%. Thus, within our evaluated dashcam conditions, the restoration provides a net improvement rather than a measured degradation.

### Reviewer 2 — Q7

**Question: **Table 2 compares a SAM 2 baseline against the SAM 3-based pipeline to claim superior segmentation accuracy (Line 266). However, the manuscript fails to apply the proposed tri-stage photometric restoration module across all baseline architectures to properly isolate the mIoU, mTC, and VRAM improvements attributable to the restoration versus the SAM 3 backbone upgrade.

**Answer:** Table 4 provides this controlled ablation by keeping the SAM 3 causal engine fixed. With raw input, the same engine gives 65.4% mIoU and 77.2% mTC. Adding the complete restoration pipeline increases these values to 74.8% mIoU and 88.4% mTC, giving +9.4 percentage points in mIoU and +11.2 percentage points in mTC. Therefore, the improvement is not attributed only to the SAM 3 backbone.

### Reviewer 2 — Q8

**Question: **The manuscript entirely lacks cross-dataset performance evaluation to prove out-of-domain generalization.

**Answer: **We agree that this is not a cross-dataset evaluation. Our evaluation is multi-domain within the acquired dataset, covering four conditions: urban arterials, suburban shadow transitions, high-speed expressways, and adverse rain/fog. As shown in Table 3, the proposed method gives the best mIoU in all four domains: 76.4%, 73.2%, 75.8%, and 73.9%, with 74.8% overall. These results show consistent performance under different dashcam conditions. We do not claim independent cross-dataset generalization.

### Reviewer 2 — Q9

**Question: **Section 4.1 presents a major ambiguity regarding whether the data was originally acquired or simply curated. The section title mentions "acquisition", Line 488 states it was "curated", and Line 489 states it was "acquired." If original acquisition, exact dataset details, camera hardware, and capture conditions must be provided. If curated from existing public datasets, the sources must be cited.

**Answer: **Yes. the terms “acquired” and “curated” were unclear. The video was acquired using a windshield-mounted HDR optical sensor at 2560×1440 resolution and 20 FPS, with more than 120 dB dynamic range. The footage was then organized into four domains, and 4,500 continuous frames were densely annotated for five classes. Here, “curated” only means the domain organization and annotation process. The data were not taken from any public dataset.

### Reviewer 2 — Q10

**Question: **Lines 629–630: The phrase "our causal memory framework" is ambiguous and should explicitly specify which framework configuration is being referenced.

**Answer:** The phrase “our causal memory framework” was ambiguous. We refer specifically to the proposed SAM 3 PCS configuration with the FIFO causal memory of L_max = 16 described in Section 3.3.2.

### Reviewer 2 — Q11

**Question: **Figure 3 Sub-caption: The acronym "CA" is undefined.

**Answer: **As per the suggestion given by the reviewer, the acronym is now defined at first use in the caption.

### Reviewer 2 — Q12

**Question: **Margin Errors: Text is overflowing the document margins on Lines 291 and 385.

**Answer: **As per the reviewer comments, the margin errors have been corrected in the revised manuscript.

## Reviewer 3

### Reviewer 3 — Q1

**Question: **SAM 2 already introduced streaming video segmentation with memory, and the paper itself cites temporal-memory and SAM-based tracking approaches. The main architectural contribution appears to be applying/customizing causal memory around SAM 3 PCS plus classical restoration. The paper needs to clearly explain what is fundamentally new in the proposed causal attention compared with SAM 2/SAM-Track/other causal VOS architectures. The central novelty is insufficiently distinguished from existing video-memory approaches.

**Answer: **Our contribution is the causal integration of restoration-conditioned dashcam frames, SAM 3 PCS, and a FIFO memory (L_max = 16) for online segmentation under ego-motion and severe visual degradation. On the same benchmark, our method achieves 74.8% mIoU, 88.4% mTC, and 28.6 FPS, compared with 71.6% mIoU, 85.1% mTC, and 22.4 FPS for SAM 2 streaming as shown in Table 7. We present this as a task-specific system contribution, not as a new general-purpose memory architecture. **Table 7: Performance Comparison of Proposed Causal Attention vs SAM2/SAM2-Track**

| **Method (manuscript Table 2)** | **mIoU (%)** | **mTC (%)** | **FPS** |
| --- | --- | --- | --- |
| SAM2 (per-frame zero-shot) | 62.5 | 64.1 | 12.3 |
| SAM2-Track (streaming video) | 71.6 | 85.1 | 22.4 |
| **Restoration + SAM 3**<br>** (causal PCS) — Proposed** | **74.8** | **88.4** | **28.6** |

### Reviewer 3 — Q2

**Question: **The restoration is explicitly training-free, while the paper introduces learned projections, relative positional bias, memory encoding, and mask decoding. However, there is no clear description of which parameters are trained, on what data, with what loss, optimizer, schedule, or number of iterations. This is a major reproducibility issue.

**Answer: **Our pipeline is entirely training-free: all learned modules are SAM 3's pretrained weights, used frozen, and the only change is inference-time decoder cross-attention to a causal FIFO memory of 16 keyframes, so no loss, optimizer, schedule, or training data applies. We have clarified this in the manuscript and will release code and configs to reproduce the reported results (74.8% mIoU, 88.4% mTC, 28.6 FPS).

### Reviewer 3 — Q3

**Question: **The paper states that 4,500 continuous frames were densely annotated across four domains, but the experimental section does not clearly establish a train/validation/test split, number of independent video sequences, geographic diversity, or whether frames from the same continuous sequence occur across splits. A frame-level random split from continuous video could produce substantial temporal leakage and artificially inflate results.

**Answer:** To address this, we performed a chronological hold-out evaluation on the continuous video. The first 70% of the frames were used for parameter setting, while the last 30% were kept completely unseen for final evaluation. Thus, adjacent frames from the same temporal segment were not mixed between development and test portions. The causal memory was also initialized empty at the start of the held-out test segment. On this strict temporal test, the proposed method obtained 72.6% mIoU, 85.9 % mTC, and 5.3 ID switches/1k frames, which is consistent with the reported results. This confirms that the performance is not simply due to random frame-level splitting or the use of future-frame information.

### Reviewer 3 — Q4

**Question: **Only 4,500 frames are densely annotated, while the conclusions characterize the system as a robust solution for challenging automotive perception generally. Evaluation on established benchmarks such as BDD100K, Cityscapes/KITTI video subsets, or another independent dashcam dataset would make the claims considerably stronger.

**Answer: **We agree that 4,500 frames from one acquired corpus cannot establish broad out-of-domain generalization. Therefore, our results demonstrate performance under the four evaluated dashcam conditions, not universal automotive perception. Under these conditions, the proposed method achieves 74.8% mIoU and 88.4% mTC, compared with 64.2% and 67.5% for YOLO-SAM, and 71.6% and 85.1% for SAM 2 streaming depicted in Table 7. We have limited our conclusion to the evaluated conditions and stated broader evaluation as a limitation.

### Reviewer 3 — Q5

**Question: **The 28.6 FPS real-time claim needs more careful interpretation. The source video is recorded at 20 FPS, while the system reports 28.6 FPS. The latency calculation should clarify whether preprocessing, memory operations, prompt encoding, data transfer, TensorRT initialization, and output post-processing are all included. The comparison also needs identical optimization settings for all baselines.

**Answer:** The 28.6 FPS was measured on the NVIDIA Jetson AGX Orin 64 GB using FP16 TensorRT. The per-frame time was 5.8 ms for restoration and 29.1 ms for segmentation, giving about 34.9 ms per frame and 28.6 FPS. The comparison methods were also tested on the same board and with the same optimization setting. For example, YOLOv11s + SAM gives 10.2 FPS with 6480 MB peak VRAM. We agree that initialization and data transfer are separate from steady-state processing. Therefore, 28.6 FPS in Table 5 refers to the measured steady-state throughput, not the end-to-end startup latency.
