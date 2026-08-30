# Forensic Evaluation of Explainable AI for Deepfake Detection 

## Repository Structure 

├── code/
│ ├── Dissertationcode # Jupyter notebook 
├── model_results/ # XceptionNet model perfromance 
├── results/
│ ├── SHAP/ # SHAP per-image and category-level results (CSV, figures)
│ └── LIME/ # LIME per-image and category-level results (CSV, figures)
│ └── SHAP_vs_LIME/ #misclassified images and figure  
│ └── Framework/ #localisation, fidelity and consistency 
└── README.md

## Overview 
This project :
1. Trains an XceptionNet deepfake detection model on FaceForensics++ and Celeb-DF v2, using an identity-safe train/validation split
2. Generates SHAP and LIME for 35 sampled images (5 per category, 7 categories)
3. Evaluates both methods against the five forensic criteria: transparency, consistency, localisation, reproducibility, and fidelity.

## Model 

- **Architecture:** XceptionNet was fine-tuned from ImageNet weights with 80% of parameters frozen.
- **Training data:** 9,000 frames (1,800 real, 7,200 fake) across 60 identity clusters.
- **Validation data:** 3,150 frames (900 real, 2,250 fake) across 16 identity clusters.
- **Result:** AUC = 0.6975.
- The trained model checkpoint (`xceptionnet_video_v5_identitysafe.pth`) is not included in this repository due to file size. 

## Datasets 
- **FaceForensics++** (Rössler et al., 2019): 150 videos per category (Real, Deepfakes, Face2Face, FaceSwap, NeuralTextures), c23 compression, obtained through the official request process.
- **Celeb-DF v2** (Li et al., 2019): 30 real and 30 fake videos.

## Explainability Analysis 

- SHAP and LIME were applied to [the same 35 images](https://github.com/aditidisswork/DissertationCode_DeepfakeDetection_with_XAI/blob/main/results/SHAP/selected_images_35.json).
- Consistency was assessed on a subset of 14 images (2 per category)  — `results/SHAP/shap_metrics_final.csv` and `results/LIME/lime_metrics_final.csv`, where `consistency` is `NaN` for images outside this subset.
- Localisation IoU was computed against ground-truth manipulation masks, available for four FaceForensics++ manipulation categories (Deepfakes, Face2Face, FaceSwap, NeuralTextures); masks were not available for Celeb-DF v2.
## References 
- Li, Y. et al. (2019) “Celeb-DF: A Large-scale Challenging Dataset for DeepFake Forensics.” arXiv. Available at: https://doi.org/10.48550/ARXIV.1909.12962.

- Rössler, A. et al. (2019) “FaceForensics++: Learning to Detect Manipulated Facial Images.” arXiv. Available at: https://doi.org/10.48550/ARXIV.1901.08971.

