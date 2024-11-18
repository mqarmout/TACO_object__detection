# Trials Folder Structure and Documentation Format

This `Trials` folder system is designed to track and document model training progress through sequential trials. Each trial will be stored in its own sub-folder, named sequentially in the order they are completed (e.g., `Trial 1`, `Trial 2`, etc.), regardless of date, to allow for multiple trials on the same day. This structure supports organized, clear documentation and improvement tracking across all team members.

### Folder Structure
- **Trials** folder will contain a sub-folder for each trial (e.g., `Trial 1`, `Trial 2`).
- Each trial sub-folder will include:
  - **Python Notebook(s)**: The Jupyter notebook(s) used for model training, improvements, or parameter changes for that specific trial.
  - **Text File**: A `.txt` file that provides a detailed summary of the trial.

### Text File Format (`Trial # details.txt`)
Each trial's `.txt` file will document the trial’s specifics, providing a clear record of the reasoning, changes, and observations for that trial. The text file should follow this structure:

1. **Trial Number**: Specify the trial number (consistent with the folder name).
2. **Date**: Include the date when the trial was completed.
3. **Objective**: Briefly state the goal of the trial (e.g., “Optimize learning rate”, “Increase dataset size”).
4. **Adjustments**: List any changes made from the previous trial (e.g., hyperparameters, model architecture, data preprocessing steps).
5. **Reasoning**: Explain the rationale behind the changes made in this trial, detailing why these adjustments were expected to improve performance.
6. **Results**: Summarize the key outcomes of the trial, including model performance metrics.
7. **Observations**: Document any significant insights, such as unexpected behaviors or challenges encountered.
8. **Next Steps**: Outline any proposed adjustments for future trials based on the results of this trial.

### Example Text File Format
```
Trial Number: Trial 1
Date: 2024-11-12
Objective: Establish a baseline performance with a large YOLO model to detect small objects in complex environments.

---

Adjustments:
- Model Architecture: YOLOv8 large model (`yolov8l.pt`) selected to better handle small objects and complex backgrounds.
- Image Resolution: High resolution (1536x1536) was used to capture detail, crucial for detecting small objects within the dataset.
- Dataset Modification: Categories reduced to include only classes with a significant number of objects, increasing focus on relevant data and reducing noise.
- Hyperparameters:
  - Epochs: 100
  - Batch Size: 16
  - Patience: 15 (early stopping if no improvement)
  - Freeze Layers: First 10 layers frozen to leverage pretrained weights for low-level feature extraction
  - Augmentation: Enabled to help with model generalization on diverse backgrounds

---

Results:
Model Summary:
- Layers: 268
- Parameters: 43,612,776
- GFLOPs: 164.8

Performance Metrics:
- Overall:
  - Precision: 0.405
  - Recall: 0.363
  - mAP@50: 0.320
  - mAP@50-95: 0.235

Class-wise Metrics:
| Class                  | Instances | Precision | Recall | mAP@50 | mAP@50-95 |
|------------------------|-----------|-----------|--------|--------|------------|
| Plastic film           | 100       | 0.309     | 0.450  | 0.300  | 0.219      |
| Unlabeled litter       | 107       | 0.186     | 0.215  | 0.0841 | 0.0458     |
| Cigarette              | 112       | 0.626     | 0.411  | 0.443  | 0.252      |
| Clear plastic bottle   | 61        | 0.683     | 0.494  | 0.574  | 0.466      |
| Plastic bottle cap     | 39        | 0.385     | 0.513  | 0.458  | 0.352      |
| Other plastic wrapper  | 85        | 0.351     | 0.129  | 0.202  | 0.121      |
| Other plastic          | 59        | 0.392     | 0.153  | 0.150  | 0.132      |
| Drink can              | 35        | 0.306     | 0.543  | 0.345  | 0.289      |

Speed:
- Preprocessing: 0.7ms per image
- Inference: 100.4ms per image
- Postprocess: 0.9ms per image

---

Observations:
- The model architecture and high resolution have resulted in relatively strong performance on classes like Cigarette and Clear plastic bottle, likely due to the model’s ability to capture finer details at higher resolutions.
- Unlabeled litter, Other plastic wrapper, and Other plastic categories show low precision and recall, indicating difficulties in recognizing these classes in complex backgrounds.
- Average precision (mAP@50) across classes suggests that model adjustments are needed to improve detection, particularly in the challenging background settings.

Next Steps:
- Refine Classes: Consider removing low-performing categories (e.g., Unlabeled litter, Other plastic wrapper, Other plastic) to focus on classes with better detection potential.
- Augmentation Review: Investigate additional or targeted augmentation strategies that might better address the complex backgrounds in the dataset.
- Experiment with Hyperparameters: Consider reducing the batch size or adjusting learning rate to improve model convergence.

This baseline provides a foundation for further tuning and optimizations in subsequent trials.
```

### Python Notebook Naming Convention
Each trial’s notebook should be named with the trial number and date (e.g., `Trial_1_2024-11-12.ipynb`). This naming will help anyone reviewing the folder easily identify the notebook associated with each trial.

### Notes for Team Members
- Only meaningful improvements should be documented; avoid redundant or minor changes.
- Each trial builds upon the last, with explanations in each text file detailing why changes were made and what improvements are anticipated.
- Follow this standardized format to maintain clarity and consistency across all trials.

This documentation format will ensure that the process is transparent, collaborative, and easy to follow.