# Semi-Supervised Learning with Hybrid Generative Models

**Author:** Vincent Sham

**Date:** January 2026

## 📌 Abstract

This repository contains the implementation and research associated with my Master's thesis: **"Semi-Supervised Learning with Hybrid Generative Models"**.

Supervised learning requires large amounts of labeled data, while Semi-Supervised Learning (SSL) attempts to leverage abundant unlabeled data. Generally, generative models (like Normalizing Flows) perform worse in SSL tasks than discriminative models. This is largely because the Negative Log-Likelihood (NLL) objective forces models to cover all modes, often ignoring low-density regions where decision boundaries should lie.

**My Solution:** I propose a **Hybrid Generative Model** that combines likelihood-based learning with adversarial training. By including adversarial learning in the unsupervised loss, the model better fits low-density areas of the target distribution, yielding competitive SSL performance while preserving generative advantages.

## 🚀 Key Contributions

1. **Hybrid Unsupervised Loss:** Developed a novel objective combining **Negative Log-Likelihood** and **Adversarial Learning** to improve decision boundary fitting.

2. **Addressing Cluster Collapse:** Identified that standard FlowGMMs suffer from cluster collapse during initialization. I introduced a **Supervised Likelihood** loss to force clusters to separate effectively.

3. **Boundary-Aware Sampling:** Engineered an interpolation sampling method to generate synthetic points near decision boundaries, forcing the model to learn low-density separation.

4. **Multi-Scale Architecture:** Adopted a multi-scale Normalizing Flow architecture to mitigate the curse of dimensionality in high-dimensional image data.

## 🏗️ Architecture

The system consists of two primary components trained jointly:

### 1. Conditional Normalizing Flow (Generator)

* **Backbone:** RealNVP with Actnorm and Affine Coupling layers.

* **Latent Space:** Gaussian Mixture Model (GMM), where each component corresponds to a class label.

* **Objective:** Minimizes a weighted combination of supervised likelihood, NLL, and adversarial generator loss.

### 2. (K+1)-Class Discriminator

* **Structure:** A discriminative network classifying inputs into $K$ real classes or a $K+1$-th "fake" class.

* **Objective:** Differentiates between real unlabeled data and generated samples from the Flow model.

## 📊 Experimental Results

The method was benchmarked against state-of-the-art Generative and Discriminative classifiers on **MNIST**, **SVHN**, and **CIFAR-10**.

| Model | MNIST (100 labels) | SVHN (1k labels) | CIFAR-10 (4k labels) | 
 | ----- | ----- | ----- | ----- | 
| **FlowGMM (Baseline)** | 91.7% | 67.2% | 42.1% | 
| **Our Hybrid Model** | **99.1%** | **93.2%** | **73.6%** | 
| *Improvement* | *+7.4%* | *+26.0%* | *+31.5%* | 

*Note: Results represent classification accuracy. See Table 5.1 in the thesis for full comparisons.*

### Generated Samples

The model retains high-quality conditional sampling capabilities, producing diverse samples for MNIST, SVHN, and CIFAR-10.


## 📚 References

Key literature referenced in this work includes:

* **FlowGMM:** Izmailov et al., "Semi-Supervised Learning with Normalizing Flows" (ICML 2020).

* **RealNVP:** Dinh et al., "Density Estimation using Real NVP" (ICLR 2017).

* **BadGAN:** Dai et al., "Good Semi-Supervised Learning that Requires a Bad GAN" (NIPS 2017).
