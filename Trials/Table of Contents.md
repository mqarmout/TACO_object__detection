# Table of Contents

This document provides an overview of each trial conducted in the `Trials` folder, detailing the adjustments and objectives for each model iteration. Refer to the respective `Trial # details.txt` files for comprehensive results, observations, and next steps.

---

## Trial #1 
- **Trial Number**: Trial 1
- **Date**: 2024-11-12
- **Objective**: Establish a baseline performance with a large YOLO model to detect small objects in complex environments.
- **Adjustments**:
  - **Model Architecture**: YOLOv8 large model (`yolov8l.pt`) selected for handling small objects and complex backgrounds.
  - **Image Resolution**: High resolution (1536x1536) used to improve small object detection.
  - **Dataset Modification**: Reduced categories to only those with a large number of objects, enhancing focus on relevant data.
  - **Hyperparameters**:
    - Epochs: 100
    - Batch Size: 16
    - Patience: 15
    - Freeze Layers: First 10 layers
    - Augmentation: Enabled

---

## Trial #2 details.txt
- **Trial Number**: Trial 2
- **Date**: 2024-11-12
- **Objective**: Assess the impact of removing underperforming categories (Unlabeled litter, Other plastic, Other plastic wrapper) on model performance.
- **Adjustments**:
  - **Category Removal**: Excluded categories with poor detection performance based on Trial 1 results.
  - **Hyperparameters**: Maintained consistency with Trial 1 to isolate the effect of category removal.
    - Model: YOLOv8 large model (`yolov8l.pt`)
    - Epochs: 100
    - Batch Size: 16
    - Patience: 15
    - Freeze Layers: First 10 layers
    - Augmentation: Enabled

---

## Trial Number: Trial 3
- **Trial Number**: Trial 3
- **Date**: 2024-11-13
- **Objective**: Test the impact of removing implementing data augmentation, then down sampling and removing categories that couldn't allow balancing
 **Adjustments**:
- Model Architecture: YOLOv8 large model (`yolov8l.pt`) selected to better handle small objects and complex backgrounds.
- Image Resolution: High resolution (1536x1536) was used to capture detail, crucial for detecting small objects within the dataset.
- Dataset Modification: Categories reduced to include only classes with a significant number of objects, increasing focus on relevant data and reducing noise.
- **Category Removal**: we kept 6 Categories:  [Clear plastic bottle, Plastic bottle cap, Plastic film, Cigarette, Drink can, 
                       Other plastic wrapper]
- Data Augmentation then down sampling for balancing and generalization
 - **Hyperparameters**:
  - Epochs: 100
  - Batch Size: 16
  - Patience: 15 (early stopping if no improvement)
  - Freeze Layers: First 10 layers frozen to leverage pretrained weights for low-level feature extraction
 



This is the initial structure for tracking trials in the `Trials` folder. As additional trials are conducted, more entries will be added to this Table of Contents to document the evolving improvements and adjustments.