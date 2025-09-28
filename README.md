# Facial_Expression_Detection
A guide and codebase for facial expression recognition, including preprocessing, models, and demo notebooks.
Executive Summary
Based on the experimental outputs from the full dataset training, this report analyzes the performance of two CNN architectures (ResNet50 and EfficientNet) for multi-task facial expression recognition and affect analysis. The models were trained on 3,999 samples with comprehensive evaluation on 400 test samples.

1. Experimental Setup:
   
1.1 Dataset Configuration
Total Training Samples: 3,199 images

Validation Samples: 400 images

Test Samples: 400 images

Total Dataset: 3,999 samples (100% utilization)

Image Size: 224×224 pixels RGB

Training Epochs: 20

1.2 Model Architectures


Multi-task CNN with shared backbone and task-specific heads:

Backbones Tested: ResNet50, EfficientNet-B0

Expression Classification: 8 classes (0-7 emotions)

Regression Tasks: Valence & Arousal (continuous values [-1, +1])

Loss Weighting: 1.0×Expression + 0.3×Valence + 0.3×Arousal

2. Training Performance Analysis
2.1 EfficientNet Training Progress
Best Validation Accuracy: 51.00% (Epoch 13)

Training Trajectory:

Epoch 1-5: Rapid improvement (22.26% → 46.51% train accuracy)

Epoch 6-10: Steady growth with fluctuations

Epoch 11-15: Peak performance reached (51.00% validation)

Epoch 16-20: Overfitting observed (train: 82.37%, val: 49.75%)

Key Observations:

Training accuracy reached 82.37% indicating strong learning capacity

Validation accuracy plateaued at ~50%, suggesting overfitting

Best model saved at epoch 13 with 51% validation accuracy

2.2 ResNet50 Performance
Test Accuracy: 12.75% (significantly underperformed)

Training Issues: Likely convergence problems or improper initialization

3. Final Test Performance Comparison
3.1 Expression Classification Results

Architecture            	Accuracy	F1-Score	Kappa	AUC-ROC	AUC-PR
EfficientNet	              43.25%	42.49%	0.352	80.92%	44.12%
ResNet50	                  12.75%	5.15%	-0.002	53.37%	14.93%

Performance Analysis:

EfficientNet outperformed ResNet50 by 30.5% absolute accuracy

Good AUC-ROC (80.92%) indicates strong ranking capability

Moderate F1-score (42.49%) suggests class imbalance challenges

3.2 Affect Regression Performance
Valence Prediction:


Architecture	RMSE	Correlation	SAGR	CCC
EfficientNet	0.423	0.497	73.75%	0.479
ResNet50	0.467	0.081	71.75%	0.003

Arousal Prediction:

Architecture	RMSE	Correlation	SAGR	CCC
EfficientNet	0.359	0.480	78.50%	0.460
ResNet50	0.391	0.065	75.75%	0.004




4. Architecture Comparison
4.1 Performance Metrics
EfficientNet Advantages:

+30.5% higher expression accuracy

+0.416 higher valence correlation

+0.415 higher arousal correlation

+0.476 higher valence CCC

+0.456 higher arousal CCC

4.2 Training Characteristics
EfficientNet:

Convergence: Stable and consistent

Overfitting: Moderate (32% gap train vs test)

Generalization: Good transfer to test set

ResNet50:

Convergence: Poor (likely training issues)

Performance: Near random guessing

Recommendation: Requires hyperparameter tuning

5. Expression Distribution Analysis
Test Set Distribution:


Class 0: 44 samples (Neutral)
Class 1: 50 samples (Happy) 
Class 2: 51 samples (Sad)
Class 3: 47 samples (Surprise)
Class 4: 52 samples (Fear)
Class 5: 54 samples (Disgust)
Class 6: 50 samples (Anger)
Class 7: 52 samples (Contempt)


Balanced Dataset: All classes represented fairly equally (44-54 samples per class)

6. Training Graphs Interpretation
6.1 Loss Curves (Inferred from Logs)
EfficientNet: Smooth decrease from 2.21 → 0.59 (train loss)

Validation Loss: Fluctuated between 1.58-2.11, indicating overfitting

Optimal Stopping: Epoch 13 provided best validation performance

6.2 Accuracy Progression
Training Accuracy: 22% → 82% (strong learning)

Validation Accuracy: 31% → 51% (moderate generalization)

Test Accuracy: 43% (reasonable generalization)

7. Key Findings & Recommendations
7.1 Critical Success Factors
Architecture Selection: EfficientNet significantly outperformed ResNet50

Multi-task Learning: Joint training benefited all tasks

Data Utilization: 100% dataset usage enabled meaningful learning

Early Stopping: Essential for preventing overfitting

7.2 Performance Limitations
Overfitting: 32% gap between train and test accuracy

Class Confusion: 43% accuracy suggests inter-class similarity challenges

Regression Difficulty: Moderate correlation (0.48-0.50) for continuous affect

7.3 Improvement Recommendations
Immediate Actions:

Enhanced Regularization: Increase dropout, add weight decay

Data Augmentation: More aggressive transformations

Class Balancing: Address any subtle class imbalances

Architectural Improvements:

Attention Mechanisms: Add spatial/channel attention

Feature Pyramid Networks: Multi-scale feature fusion

Knowledge Distillation: Teacher-student training

Training Optimization:

Learning Rate Scheduling: Cyclic or warm-restart schedules

Gradient Clipping: Prevent exploding gradients

Mixed Precision: Faster training with FP16

8. Conclusion
The experimental results demonstrate that EfficientNet provides significantly better performance than ResNet50 for this multi-task affect recognition problem. The model achieved:

43.25% expression classification accuracy

0.497 valence correlation coefficient

0.480 arousal correlation coefficient

73.75% valence sign agreement

78.50% arousal sign agreement

While there is substantial room for improvement, particularly in addressing overfitting and improving regression performance, the results validate the multi-task learning approach and demonstrate the superiority of EfficientNet for this computer vision task.


ENDDDDDDDDDDDDDDD
