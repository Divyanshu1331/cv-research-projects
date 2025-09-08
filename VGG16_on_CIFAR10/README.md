# VGG16 on CIFAR-10  

## 📌 About VGG16  
VGG16 is a **deep convolutional neural network** introduced by **Karen Simonyan and Andrew Zisserman (2014)** in their paper *"Very Deep Convolutional Networks for Large-Scale Image Recognition"*.  
- It was submitted to the **ILSVRC (ImageNet Large Scale Visual Recognition Challenge) 2014**, where it ranked among the top performers.  
- The architecture is notable for its simplicity: stacking **3×3 convolution filters** with stride 1 and max-pooling layers, demonstrating that network **depth plays a crucial role in achieving higher accuracy**.  

---

## 🛠 What I Built in This Project  

I implemented the **VGG16 architecture from scratch** and trained it on the **CIFAR-10 dataset**.  

### 🖼 About the Dataset  
- **CIFAR-10** consists of **60,000 32×32 color images** across **10 classes** (such as airplanes, automobiles, birds, cats, etc.).  
- Each class has 6,000 images, with 50,000 for training and 10,000 for testing.  
- I chose CIFAR-10 because it provides **diversity across object categories** while being computationally manageable, and it resembles a **scaled-down version of ImageNet** — making it a perfect playground for experimenting with deep architectures like VGG16.  

### 🔧 Modifications Introduced  
Since CIFAR-10 images are smaller (32×32) compared to ImageNet (224×224), I adapted the architecture as follows:  

- **Dropout layers** added after pooling and fully connected layers to reduce overfitting.  
- **Fully connected layers reduced** from 4096 units (in original VGG16) to 512 units, since CIFAR-10 does not require as much capacity.  
- **Output layer adjusted** to 10 neurons (softmax), matching CIFAR-10 classes instead of ImageNet’s 1000 classes.  
- **Adam optimizer** with a learning rate of `1e-4` for smoother convergence.  
- **Early stopping** to prevent unnecessary training once validation loss plateaued.  

### Architecture (Summary of Implementation)  
```python
# Block 1
Conv2D(64) → Conv2D(64) → MaxPooling2D → Dropout(0.25)

# Block 2
Conv2D(128) → Conv2D(128) → MaxPooling2D → Dropout(0.25)

# Block 3
Conv2D(256) → Conv2D(256) → Conv2D(256) → MaxPooling2D → Dropout(0.3)

# Block 4
Conv2D(512) → Conv2D(512) → Conv2D(512) → MaxPooling2D → Dropout(0.3)

# Block 5
Conv2D(512) → Conv2D(512) → Conv2D(512) → MaxPooling2D → Dropout(0.4)

# Fully Connected
Flatten → Dense(512, relu) → Dropout(0.5) → Dense(512, relu) → Dropout(0.5) → Dense(10, softmax)
```
---

## Results

- Training improved steadily from ~12% accuracy in the first epoch to **~81% validation accuracy by epoch 19**.  
- Early stopping was applied to prevent overfitting, restoring the best-performing weights.  
- The adapted VGG16 architecture demonstrated strong generalization capability on the chosen dataset.

### Training Snapshot
- **Epoch 1**: Accuracy = 12.8% | Validation Accuracy = 17.6%  
- **Epoch 10**: Accuracy = 73.1% | Validation Accuracy = 72.5%  
- **Epoch 19**: Accuracy = 87.6% | Validation Accuracy = 81.1%  

---

## 💡 Intuition Developed

Working with CIFAR-10 (32×32 images) gave me important insights into the challenges of using deep CNNs on small, low-resolution datasets:

- **Blurriness and human-level difficulty:** Many CIFAR-10 images are so low-resolution that even humans may struggle to recognize them, for e.g., automobile image I showed in the beggning os the notebook, its blurred and lack sharp edges. Training a model on such data made me realize that the network has to extract patterns from very limited information.  

- **Interesting misclassification (Deer vs. Airplane):**  
  At the end, I tested my trained model with 5 real-world images (outside the dataset). While it classified most correctly, I noticed a fascinating error:
  - **Chital Stag (large antlers):** Misclassified as an **airplane**. I believe the network mistook the long antlers for airplane wings.  
  - **Fallow Deer (no antlers):** Correctly classified as **deer**.  

  This highlighted an intuition: **when images are blurred or too small, convolutional filters may fail to capture fine edges, leading the network to focus on exaggerated shapes (like antlers → wings) rather than true class-specific features.**

- **Takeaway:** Small datasets like CIFAR-10 are excellent for testing architectures but may lead to unexpected feature associations. It taught me to always validate models on external, clearer data to check for such biases.

---
## 📚 References

- Simonyan, K., & Zisserman, A. (2014). *Very Deep Convolutional Networks for Large-Scale Image Recognition*. [arXiv:1409.1556](https://arxiv.org/abs/1409.1556)  
- Dataset: [CIFAR-10 (Kaggle)](https://www.kaggle.com/c/cifar-10) | [CIFAR-10 (Google Drive Copy)](https://drive.google.com/drive/folders/1LAeIEqBSsloVt463H0bcgQXnz90xht5w?usp=sharing)

---

## 📝 My Related Work

I wrote a detailed blog post on this project, where I dive deeper into the **theory, architecture, and experiments with VGG16**.  
👉 [My Blog on VGG16](https://medium.com/@divyanshu1331/week-10-building-cnns-vgg16-from-scratch-cat-vs-dog-classifier-b88a23845428)

