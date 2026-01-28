# Face Detection Optimization with YOLOv8

This project analyzes and optimizes the inference performance of a YOLOv8-based face detection model on the FDDB dataset.  
The main goal is to improve detection quality by tuning inference-time parameters without retraining the model.

---

##  Project Overview

In this study, we perform a detailed analysis of:

- Confidence threshold sweep  
- Precision / Recall / F1-score trade-offs  
- FPPI (False Positives Per Image) & Miss Rate analysis  
- NMS IoU threshold optimization  
- Final baseline vs tuned model comparison  

All experiments are conducted on the validation split of the FDDB dataset using a pretrained YOLOv8 model.

---

##  Methodology

### 1. Baseline Model
- Model: YOLOv8 (Ultralytics)
- Default inference parameters:
  - Confidence = 0.25  
  - NMS IoU = 0.50  

Baseline performance is evaluated using custom FP / FN / TP analysis.

---

### 2. Confidence Threshold Sweep

We evaluate multiple confidence thresholds:

[0.10, 0.15, 0.20, 0.25, 0.30, 0.35, 0.40, 0.50]


Metrics computed for each threshold:

- Precision  
- Recall  
- F1-score  
- FPPI  
- Miss Rate  

This allows us to identify the best operating point that balances false positives and missed detections.

---

### 3. NMS IoU Optimization

We analyze the effect of different NMS IoU thresholds:

[0.30, 0.40, 0.50, 0.60, 0.70]


Observations:

- Recall remains almost constant → model already detects most faces  
- Precision decreases for higher IoU thresholds due to excessive suppression  
- Best trade-off observed around **IoU = 0.30**

---

### 4. Final Tuned Configuration

Best performing configuration:

- Confidence = **0.40**  
- NMS IoU = **0.30**

This setting improves overall F1-score and reduces false positives compared to the baseline.

---

## Final Results

| Setting | Precision | Recall | F1-score |
|--------|-----------|--------|----------|
| Baseline (conf=0.25, iou=0.50) | ~0.94 | ~0.96 | ~0.95 |
| Tuned (conf=0.40, iou=0.30) | ~0.96 | ~0.96 | ~0.96 |

The tuned configuration achieves a better balance between precision and recall and increases the final F1-score.

---

## Key Takeaways

- Inference-time optimization can significantly improve model performance without retraining  
- Confidence threshold tuning provides the largest gain  
- NMS IoU should be carefully selected to avoid over-suppression  
- The final tuned model achieves a more stable and balanced detection behavior  

---

## Technologies Used

- Python  
- Ultralytics YOLOv8  
- NumPy, Pandas  
- Matplotlib  
- FDDB Face Detection Dataset  

---


## Author

Sude Soylemez  
Face Detection Optimization Project – 2026

---

## Results & Analysis

This section presents the quantitative results of inference-time optimization
performed on the YOLOv8 face detection model.

### Confidence Threshold Optimization
![Confidence Threshold Sweep](figures/conf_effect.png)

This figure shows the trade-off between Precision, Recall, and F1-score as the
confidence threshold is varied. The selected operating point achieves a balanced
precision–recall trade-off.

---

### NMS IoU Optimization
![NMS IoU Effect](figures/nms_iou_effect.png)

The effect of the Non-Maximum Suppression (NMS) IoU threshold on detection
performance is illustrated above. Lower IoU thresholds lead to better suppression
of duplicate detections.

---

### FPPI & Miss Rate vs Confidence
![FPPI vs Miss Rate](figures/conf_fppi_missrate.png)

As the confidence threshold increases, the False Positives Per Image (FPPI)
decreases steadily, while the miss rate increases slightly. This behavior
motivates the chosen operating point.

---

### Baseline vs Optimized (FPPI & Miss Rate)
![Baseline vs Optimized FPPI MissRate](figures/baseline_vs_optimized_fppi_missrate.png)

This comparison highlights the reduction in false positives and missed detections
after inference-time optimization, without retraining the model.

---

### Relative Performance Improvement
![Relative Improvement](figures/relative_improvement_metrics.png)

The relative improvement (%) of Precision, Recall, and F1-score demonstrates that
the proposed optimization strategy yields consistent gains across all key metrics.
