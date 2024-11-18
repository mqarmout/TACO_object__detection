**Trial Number**: Trial 3  
**Date**: 2024-11-13  
**Objective**: Test the impact of oversampling underrepresented classes while maintaining all original categories on model performance.

---

**Adjustments**:
- **Oversampling**: Underrepresented categories such as "Unlabeled litter," "Other plastic," and "Other plastic wrapper" were oversampled to improve their performance and overall model balance.
- **Hyperparameters**: Kept consistent with previous trials to isolate the effect of oversampling.
  - **Model**: YOLOv8 large model (`yolov8l.pt`)
  - **Epochs**: 100
  - **Batch Size**: 16
  - **Patience**: 15 (early stopping if no improvement)
  - **Freeze Layers**: First 10 layers frozen
  - **Augmentation**: Enabled to support diverse backgrounds

---

**Results**:

Model Summary (fused):
- **Layers**: 268  
- **Parameters**: 43,612,776  
- **GFLOPs**: 164.8  

Performance Metrics (Overall):
- **Precision**: 0.406
- **Recall**: 0.373
- **mAP@50**: 0.351
- **mAP@50-95**: 0.271

Class-wise Metrics:

| Class                  | Instances | Precision | Recall | mAP@50 | mAP@50-95 |
|------------------------|-----------|-----------|--------|--------|-----------|
| Plastic film           | 81        | 0.489     | 0.296  | 0.275  | 0.192     |
| Unlabeled litter       | 75        | 0.218     | 0.107  | 0.0735 | 0.0423    |
| Cigarette              | 136       | 0.460     | 0.390  | 0.371  | 0.223     |
| Clear plastic bottle   | 51        | 0.512     | 0.762  | 0.702  | 0.583     |
| Plastic bottle cap     | 40        | 0.517     | 0.475  | 0.511  | 0.399     |
| Other plastic wrapper  | 41        | 0.211     | 0.220  | 0.194  | 0.130     |
| Other plastic          | 34        | 0.450     | 0.588  | 0.528  | 0.464     |
| Drink can              | 47        | 0.394     | 0.149  | 0.153  | 0.136     |

Speed:
- **Preprocessing**: 0.7 ms per image
- **Inference**: 45.0 ms per image
- **Postprocessing**: 1.9 ms per image

Results saved to `runs/detect/train`

---

**Observations**:
- **Impact of Oversampling**: Although the model retained all original categories, oversampling showed a limited positive effect on the performance of underrepresented classes. 
- **Class-Specific Performance**: Some improvements were noted in "Clear plastic bottle" and "Plastic bottle cap" classes, but oversampling had minimal impact on "Unlabeled litter" and "Other plastic wrapper," which continued to exhibit low mAP@50 scores.
- **Overall Metrics**: While there was a slight increase in precision and recall for certain classes, overall model metrics did not match those seen in Trial 2, where underperforming categories were removed.
- **Inference Speed**: With a reduced inference time of 45.0 ms per image, this trial showed an efficiency gain over previous trials.

**Next Steps**:
- **Refine Sampling Strategy**: Re-evaluate the sampling strategy, considering alternative approaches like weighted loss functions instead of pure oversampling for underrepresented classes.
- **Hyperparameter Exploration**: Adjust batch size, learning rates, and augmentation parameters to determine if further improvements can be made.
- **Category Review**: Consider removing or merging consistently underperforming categories in future trials if performance remains low after further optimizations.

This trial demonstrated that oversampling alone may not sufficiently address the challenges posed by underrepresented or poorly defined classes. Future work will focus on more refined strategies to optimize the performance of all categories.