# Notebooks

This folder contains the main Jupyter notebook used in the project.

## Contents

- `face_detectionYOLO.ipynb`  
  The main analysis notebook where all experiments are performed:
  - Confidence threshold sweep  
  - Precision / Recall / F1-score analysis  
  - FPPI & Miss Rate evaluation  
  - NMS IoU optimization  
  - Final baseline vs tuned comparison  

All results, plots, and performance evaluations are generated from this notebook.

## Notes

- The experiments are conducted on the FDDB validation dataset.
- The model used is a pretrained YOLOv8 face detection model.
- No retraining is performed; only inference-time parameters are optimized.
