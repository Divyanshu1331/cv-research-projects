# Vision Transformer (ViT) on CIFAR-10 — From Scratch (4 Model Versions)

This repository contains a complete experimental workflow where a Vision Transformer is trained **from scratch** on the CIFAR-10 dataset — without ImageNet pretraining, without transfer learning, and without external attention weights.

The goal of this repo is **not just to show the final accuracy**, but to document how the model evolved across multiple iterations, what changes were made, and how each version affected performance.

---

## 📌 Dataset

- **Dataset:** CIFAR-10  
- **Images:** 50,000 color images (32×32)  
- **Classes:** 10 (airplane, car, bird, cat, deer, dog, frog, horse, ship, truck)  
- **Why CIFAR-10?**
  - Small image size → forces ViT to learn without relying on high-res patch information
  - Widely used benchmark → easier to compare with CNNs (VGG, ResNet, etc.)
  - Ideal for studying *"Can ViT work without ImageNet pretraining?"*

---

## 🧠 Why Vision Transformer?

Traditional CNNs learn spatial locality through convolution, but Transformers learn global context via self-attention.  
However, ViTs **usually require large datasets (like ImageNet-21k) to converge well.**  
So this repo answers:

> ❓ “Can ViT truly learn from scratch on a small dataset like CIFAR-10?”  
> ❓ “What architecture tweaks make it actually work?”  
> ❓ “How much does data augmentation matter for ViTs?”

---

## 📂 Repository Structure

| File | Description |
|-------|-------------|
| `ViT_on_CIFAR10_01.ipynb` | **Baseline ViT** — no augmentation, fixed patch size, lower accuracy |
| `ViT_on_CIFAR10_02.ipynb` | Added **data augmentation**, + accuracy improvement |
| `ViT_on_CIFAR10_03.ipynb` | Tuned model depth, dropout, learning rate |
| `ViT_on_CIFAR10_04.ipynb` | **Final model** — best accuracy + stability |

---

## 🔄 Model Evolution Summary

### ✅ Model-1: Baseline ViT
- Patch size: 4×4
- No data augmentation
- Small embedding dim & shallow depth  
🔎 *Trains, but accuracy plateaus quickly → underfits*

---

### ✅ Model-2: Data Augmentation Added
- Added `RandomFlip`, `RandomRotation`, `ColorJitter`
- Train samples boosted from 40k → 49k  
📈 *Significant accuracy jump (≈ +10%)*  
💡 Data augmentation is **critical** for ViT on small datasets.

---

### ✅ Model-3: Architecture + Training Tuning
- Increased embedding dimension + number of heads
- Added dropout inside encoder blocks
- Adjusted LR scheduler  
📈 *Better generalization, reduced overfitting*

---

### ✅ Model-4: Final Optimized Model
- Larger model depth & embedding size
- Better regularization
- Trained for longer epochs  
🏁 **Best model so far, highest test accuracy achieved**

---

## 📊 Results Summary (High-Level)

| Model | Key Change | Effect |
|--------|------------|--------|
| 01 | Raw ViT | Low accuracy, high variance |
| 02 | + Augmentation | Big accuracy boost |
| 03 | + Tuned architecture | More stable training |
| 04 | Final optimized ViT | Best performance |

---

## 📝 Reference Blog

Full write-up, plots, breakdown, comparison with VGG16, reasoning, and conclusions:

👉 **Medium article:**   
*[Vision Transformer vs VGG16 on CIFAR-10: Training Both Models From Scratch](https://divyanshu1331.medium.com/why-vit-struggles-on-small-datasets-a-4-stage-experiment-on-cifar-10-7634ab2ae94c)*

---
