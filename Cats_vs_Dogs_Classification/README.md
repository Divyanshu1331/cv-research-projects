# Cats vs Dogs Classification

🖋 **About the Project**  
📌 **Overview**  
This project implements a Convolutional Neural Network (CNN) to classify images of cats and dogs. Using data augmentation, convolutional layers, batch normalization, and dropout regularization, the model achieves robust performance on unseen test images.  

🐱🐶 The classifier can distinguish between cats and dogs in new images with high accuracy.  

---

## 🖼 **About the Dataset**  
I used the **Dogs vs Cats** dataset from Kaggle: [Dataset Link](https://www.kaggle.com/datasets/salader/dogs-vs-cats)  

- Training images: 20,000  
- Testing images: 5,000  
- Image size: 150×150 pixels  
- Channels: RGB (3 channels)  
- Classes: Cats (0), Dogs (1)

---

## 🔧 **Data Augmentation**  
Data augmentation was applied to the training set to improve generalization:  
- Rescaling, rotation, width/height shift, shear, zoom, horizontal flip  
- Batch size: 32  
- Target size: 150×150  

This produced varied image samples to make the model more robust to real-world variations.  

🔧 **CNN Architecture (Summary)**  
| Layer | Output Shape | Parameters |
|-------|--------------|-----------|
| Conv2D(32, 3x3, ReLU) | (None, 148, 148, 32) | 896 |
| BatchNormalization | (None, 148, 148, 32) | 128 |
| MaxPooling2D(2x2) | (None, 74, 74, 32) | 0 |
| Conv2D(32, 3x3, ReLU) | (None, 72, 72, 32) | 9,248 |
| BatchNormalization | (None, 72, 72, 32) | 128 |
| MaxPooling2D(2x2) | (None, 36, 36, 32) | 0 |
| Conv2D(64, 3x3, ReLU) | (None, 34, 34, 64) | 18,496 |
| BatchNormalization | (None, 34, 34, 64) | 256 |
| MaxPooling2D(2x2) | (None, 17, 17, 64) | 0 |
| GlobalAveragePooling2D | (None, 64) | 0 |
| Dense(128, ReLU) | (None, 128) | 8,320 |
| Dropout(0.5) | (None, 128) | 0 |
| Dense(1, Sigmoid) | (None, 1) | 129 |

🧮 **Training Details**  
- Optimizer: Adam  
- Loss function: Binary crossentropy  
- Epochs: 20 (with EarlyStopping, patience=3)  
- Batch size: 32  

---

## 📊 **Results Summary**  

| Metric | Value |
|--------|-------|
| Train Accuracy | ~87.5% |
| Validation Accuracy | ~85.4% |
| Best Validation Loss | 0.3171 |
| Early Stopping Epoch | 15 |
| Peak Performance Epoch | 12 |

Observation: Training and validation accuracy improved steadily initially. Early stopping was triggered after epoch 15, restoring the best model weights at epoch 12.  

---

## 📈 **Training Curves**  
- Accuracy and loss plots were visualized, showing steady improvement and prevention of overfitting.

---  

## 🖼 **Sample Predictions**  

| Image | True Label | Model Prediction | Probability |
|-------|------------|-----------------|-------------|
| Bengal_Cat.jpg | Cat | Cat 🐱 | 0.04 |
| dog.jpg | Dog | Dog 🐶 | 0.97 |

The model correctly predicted unseen images, demonstrating strong generalization.  

---

## 🎯 **Key Takeaways**  
- CNNs can efficiently learn patterns like edges, shapes, and textures to classify images.  
- Data augmentation significantly improves model robustness.  
- Early stopping prevents overfitting, restoring the best weights for generalization.

---


