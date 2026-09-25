# Adversarial Examples Experiments

Code and experiments for my bachelor's thesis on adversarial examples. The project compares FGSM (Fast Gradient Sign Method) attacks, regularization, and adversarial training across logistic regression, CNN, and ResNet models on MNIST and STL-10.

## Overview

We train and use: 
- Logistic regression models with no regularization, L1 regularization, and L2 regularization
- Convolutional neural networks
- Pretrained ResNet-18 models

The MNIST binary experiments classify the digits **3 and 8**, and the STL-10 binary experiments classify **cats and dogs**. Multiclass experiments use all 10 classes of each dataset.

And then investigate:
- FGSM adversarial attacks
- Changes in model accuracy as the perturbation strength increases
- Adversarial training as a defense against FGSM
- Comparison to Gaussian noise and random-sign noise as baselines


## Repository Structure

| File | Description |
|---|---|
| `data.py` | Loading MNIST and STL-10, binary/multiclass splits, DataLoaders, train/validation split, seeding, and device selection |
| `models.py` | Model definitions: `BinaryLogReg`, `MulticlassLogReg`, `BinaryCNNMNIST`, `MulticlassCNNMNIST`, `BinaryCNNSTL10`, `MulticlassCNNSTL10`, `BinaryResNetSTL10`, `MulticlassResNetSTL10` |
| `attacks.py` | Attack implementations: `fgsm_attack`, plus `gaussian_noise_attack` and `random_sign_attack` as random-noise baselines |
| `train.py` | Training and evaluation loops for standard, regularized, and adversarial training, for each model/dataset combination, plus FGSM/noise-robustness evaluation |
| `log_reg_adversarial_examples_final.ipynb` | Full experiment notebook for logistic regression models |
| `nns_adversarial_examples_final.ipynb` | Full experiment notebook for CNN and ResNet models |

### Notebooks

**`log_reg_adversarial_examples_final.ipynb`**

Logistic regression experiments (binary MNIST, multiclass MNIST, binary STL-10, multiclass STL-10), including:

- Training models with no regularization, L2, and L1
- Visualization of learned weight vectors
- FGSM accuracy-vs-epsilon curves
- Comparison with Gaussian-noise and random-sign-noise baselines
- Comparison of actual vs. theoretical-maximum output change
- Visualization of adversarial examples
- FGSM adversarial training

**`nns_adversarial_examples_final.ipynb`**

CNN and ResNet-18 experiments (MNIST CNNs, STL-10 CNNs, STL-10 ResNet-18 with frozen backbone), repeating the same experiment types as the logistic regression notebook, plotted with the logistic regression results for comparison:

- Binary and multiclass model training
- FGSM accuracy-vs-epsilon curves
- Comparison with random-noise baselines
- Visualization of adversarial examples
- FGSM adversarial training


## Usage

Open either notebook and run the cells top to bottom — they import from `data.py`, `models.py`, `attacks.py`, and `train.py`.

## Reproducibility

Random seeds are fixed in `data.py` (`SEED = 1234`) for NumPy, Python's `random`, and PyTorch (CPU and CUDA).

## Thesis

This code accompanies the bachelor's thesis *"A Theoretical and Empirical Study of Adversarial Vulnerabilities in Neural Networks"*, supervised by Prof. Dr. Felix Voigtlaender, Katholische Universität Eichstätt-Ingolstadt.
