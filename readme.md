# EfficientNet Transfer Learning – Food11 Classification

## Project Overview
This project applies **transfer learning using EfficientNetB0** to classify images from the **Food11 dataset**. Two approaches were evaluated:

1. **Feature Extraction**
2. **Fine-Tuning**

Additionally, **MLflow** was used to track experiments, parameters, metrics, and model artifacts as part of the bonus requirement.

---

# Experiments

## 1. Feature Extraction

### Strategy
- Load **EfficientNetB0 pretrained on ImageNet**
- Freeze the entire backbone
- Train only the classification head

### Test Performance
**Test Accuracy:** 0.9027  
**Test Loss:** 0.2941  

### Classification Report

| Class | Precision | Recall | F1-score | Support |
|------|-----------|--------|---------|--------|
| Bread | 0.85 | 0.86 | 0.86 | 259 |
| Dairy product | 0.94 | 0.82 | 0.88 | 108 |
| Dessert | 0.86 | 0.87 | 0.87 | 375 |
| Egg | 0.86 | 0.87 | 0.87 | 247 |
| Fried food | 0.87 | 0.85 | 0.86 | 219 |
| Meat | 0.90 | 0.93 | 0.92 | 331 |
| Noodles-Pasta | 0.97 | 0.97 | 0.97 | 110 |
| Rice | 0.97 | 0.94 | 0.96 | 71 |
| Seafood | 0.93 | 0.88 | 0.90 | 226 |
| Soup | 0.96 | 0.97 | 0.96 | 375 |
| Vegetable-Fruit | 0.94 | 0.97 | 0.96 | 176 |

**Overall Accuracy:** 0.90  
**Macro Avg F1:** 0.91  
**Weighted Avg F1:** 0.90  

---

## 2. Fine-Tuning

### Strategy
- Initialize EfficientNetB0 with pretrained weights
- Unfreeze the **last 20 layers**
- Train using a **smaller learning rate**

### Test Performance
**Test Accuracy:** 0.9007  
**Test Loss:** 0.3601  

### Classification Report

| Class | Precision | Recall | F1-score | Support |
|------|-----------|--------|---------|--------|
| Bread | 0.86 | 0.85 | 0.85 | 259 |
| Dairy product | 0.95 | 0.84 | 0.89 | 108 |
| Dessert | 0.86 | 0.85 | 0.85 | 375 |
| Egg | 0.85 | 0.87 | 0.86 | 247 |
| Fried food | 0.87 | 0.89 | 0.88 | 219 |
| Meat | 0.92 | 0.92 | 0.92 | 331 |
| Noodles-Pasta | 0.95 | 0.97 | 0.96 | 110 |
| Rice | 0.94 | 0.93 | 0.94 | 71 |
| Seafood | 0.92 | 0.91 | 0.91 | 226 |
| Soup | 0.95 | 0.97 | 0.96 | 375 |
| Vegetable-Fruit | 0.93 | 0.93 | 0.93 | 176 |

**Overall Accuracy:** 0.90  
**Macro Avg F1:** 0.91  
**Weighted Avg F1:** 0.90  

---

# Comparison of Approaches

| Model | Test Accuracy | Test Loss |
|------|---------------|-----------|
| Feature Extraction | **0.9027** | **0.2941** |
| Fine-Tuning | 0.9007 | 0.3601 |

### Observations
- Both approaches achieved **very similar performance (~90% accuracy)**.
- **Feature extraction slightly outperformed fine-tuning** in this experiment.
- Fine-tuning introduced additional trainable parameters, which increased training complexity without significantly improving performance.
- The pretrained EfficientNet features were already highly effective for this dataset.

---

# Generalization and Overfitting

Training used several techniques to improve generalization:

- Data augmentation
- Dropout
- Early stopping
- Learning rate reduction

These techniques helped prevent overfitting and maintain stable validation performance.

---

# Bonus – MLflow Experiment Tracking

MLflow was used to track experiment runs and improve reproducibility.

Each experiment logged:

- model type
- transfer learning approach
- learning rate
- batch size
- number of epochs
- test metrics
- training plots
- saved model artifacts



---

# Conclusion

EfficientNetB0 proved to be a powerful backbone for the Food11 classification task.  
Transfer learning enabled strong performance with limited training time.

- Feature extraction provided an efficient and effective baseline.
- Fine-tuning allowed deeper adaptation but did not significantly outperform feature extraction in this case.
- Experiment tracking with MLflow improved reproducibility and experiment comparison.
