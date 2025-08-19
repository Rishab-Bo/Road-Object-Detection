\# Pruning on Deformable DETR



\*\*Authors:\*\* Shashank Shashidhar, Rishab Bohra, Ebin Royce, Suhas Ungarala, Muhammed Shahbas V S  



---



\## Introduction

State-of-the-art object detectors such as \*\*Deformable DETR\*\* achieve high accuracy but are computationally expensive and memory-heavy. This limits deployment on \*\*edge devices\*\* and \*\*real-time systems\*\*.  



This project explores \*\*pruning techniques\*\* (structured filter pruning, unstructured weight pruning, and structured layer pruning) to compress Deformable DETR while analyzing the trade-off between \*\*accuracy\*\*, \*\*speed\*\*, and \*\*model size\*\*.



---



\##  Background



\### Deformable DETR

\- Faster convergence vs. DETR  

\- Better handling of small objects  

\- Key innovation: \*\*Multi-Scale Deformable Attention\*\*  

\- Architecture: ResNet-50 + FPN backbone, Transformer Encoder/Decoder, prediction heads  



\### Pruning Approaches

1\. \*\*Structured Filter Pruning\*\* – removes filters based on L1-norm  

2\. \*\*Unstructured Weight Pruning\*\* – removes individual low-magnitude weights  

3\. \*\*Structured Layer Pruning\*\* – removes entire encoder/decoder layers  



---



\## Methodology

\- \*\*Dataset\*\*: KITTI Object Detection (Cars, Pedestrians, Cyclists)  

\- \*\*Preprocessing\*\*: Converted KITTI `.txt` annotations → COCO JSON format  

\- \*\*Baseline Model\*\*: Deformable DETR (ResNet-50 backbone) trained in MMDetection  

\- \*\*Pruning Experiments\*\*:  

&nbsp; - Filter pruning (10–50%)  

&nbsp; - Weight pruning (10–90%)  

&nbsp; - Layer pruning (1–3 encoder/decoder pairs)  



---



\## Evaluation Metrics

\- \*\*Accuracy\*\*: mAP, mAP50, per-class AP  

\- \*\*Efficiency\*\*: Inference latency (CPU/GPU), FLOPs  

\- \*\*Model Size\*\*: Parameters, checkpoint size, compression ratio  



---

=

\## Key Results



\### Baseline

\- mAP ≈ 0.117  

\- Latency ~205 ms  

\- ~205 GFLOPs  



\### Structured Filter Pruning

\- Severe accuracy collapse (>20%)  

\- ~24% FLOP reduction at 50% pruning  

\- Minor runtime gain  



\### Unstructured Weight Pruning

\- Better robustness at 30–40% sparsity  

\- Sharp collapse beyond 50–70%  

\- Reduced storage but \*\*no speedup\*\*  



\### Structured Layer Pruning

\- Only method with \*\*meaningful latency reduction\*\*  

\- ~17% faster with 1 layer pair pruned (205 → 170 ms)  

\- Accuracy dropped ~16% (still viable)  

\- Pruning >1 pair caused severe accuracy loss  



---



\## Comparative Analysis

\- \*\*Filter Pruning\*\* → Least robust, fast accuracy collapse  

\- \*\*Weight Pruning\*\* → Good storage reduction, no latency gain  

\- \*\*Layer Pruning\*\* → Best trade-off, practical speedup with acceptable accuracy drop  



---



\##  Conclusion

Pruning Deformable DETR is challenging due to its sensitivity.  



\- \*\*Structured Filter Pruning\*\* → Poor trade-off  

\- \*\*Unstructured Weight Pruning\*\* → Storage benefit only  

\- \*\*Structured Layer Pruning\*\* → Most promising, with ~17% latency gain for ~16% accuracy drop  



&nbsp;Overall: \*\*Layer pruning (removing 1 encoder/decoder pair)\*\* is the most practical compression strategy found in this study.



---



\## Repository Contents

\- `torch\_filter\_pruning\_final.ipynb` → Structured Filter Pruning experiments  

\- `training+unstructured\_weight\_pruning.ipynb` → Unstructured Weight Pruning experiments  

\- `README.md` → Project summary (this file)  



