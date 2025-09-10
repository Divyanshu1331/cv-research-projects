# 🖋 LeNet-5 on MNIST  

## 📌 About LeNet-5  
LeNet-5, introduced by **Yann LeCun in 1998**, is considered the **first successful Convolutional Neural Network (CNN)** architecture.  
- Originally designed for **handwritten digit recognition**, it laid the foundation for modern CNNs like AlexNet, VGG, and ResNet.  
- The key idea: combining **convolutional layers for feature extraction** with **fully connected layers for classification**.  
- Although small by today’s standards, it was revolutionary at the time and demonstrated the power of deep learning for image tasks.  

---

## 🖼 About the Dataset (MNIST)  
I chose the **MNIST dataset** because:  
- It’s the **classic benchmark** for handwritten digit recognition (digits `0–9`).  
- Small and efficient for quick experimentation.  
- Historically aligned with LeNet-5, since the original paper also focused on digit recognition.  

**Dataset Details:**  
- **Training images:** 60,000  
- **Test images:** 10,000  
- **Image size:** 28×28 pixels  
- **Channels:** Grayscale (1 channel)  
- **Labels:** Digits 0–9  

---

## 🔧 Architecture (My Implementation)  

Since MNIST images are 28×28 (instead of 32×32 in the original LeNet-5), I adapted the input layer accordingly.  

```python
# Conv + Pooling
Conv2D(6, kernel_size=(5,5), activation='tanh')  
AveragePooling2D(pool_size=(2,2))  

Conv2D(16, kernel_size=(5,5), activation='tanh')  
AveragePooling2D(pool_size=(2,2))  

# Fully Connected
Flatten()  
Dense(120, activation='tanh')  
Dense(84, activation='tanh')  
Dense(10, activation='softmax')
```
Optimizer: Adam  
Loss: Sparse categorical crossentropy  
Batch size: 32  
Epochs: 10  

## 📊 Results  

The model achieved high accuracy on MNIST, showing the effectiveness of even early CNN architectures:  

| Epoch | Train Accuracy | Val Accuracy |
|-------|----------------|--------------|
| 1     | 89.8%          | 98.2%        |
| 5     | 98.9%          | 98.6%        |
| 10    | 99.4%          | 98.6%        |

**Peak Validation Accuracy:** ~98.9%  

**Observation:** Training accuracy kept improving, but validation accuracy plateaued → indicating a slight overfitting after ~5 epochs. 

---

### 📈 Training Curves  

Training and validation accuracy/loss curves were plotted in the notebook, showing that accuracy plateaued after ~5 epochs, while loss continued to decrease slightly.  

---

### 🖼️ Sample Prediction  

Testing on the first image from the MNIST test set:  

- **True Label:** 7  
- **Model Prediction:** 7 ✅  

This confirmed that the model was able to correctly classify unseen test images. 

---

## 🎯 Key Takeaways  

- LeNet-5 may be a simple model by today’s standards, but it was pioneering in CNN design.  
- Training it on MNIST reinforced my understanding of how convolutional layers extract spatial patterns like edges, curves, and shapes.  
- This project gave me intuition into why depth, pooling, and non-linear activations matter in deep learning.  
  

## 📝 My Blog on This Project  

I’ve written a detailed blog explaining my implementation and learnings:  
👉 [Week 9: CNN Architecture and Backpropagation Made Simple](https://medium.com/@divyanshu1331/week-9-cnn-architecture-and-backpropagation-made-simple-e7e11a667c7d)  
