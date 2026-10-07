# Action Taken Report

## ICVGIP 2026 — Submission 497

### Causal Video Segmentation of Moving Objects in Dashcam Scenes Under Challenging Visual Conditions

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
