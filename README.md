# Waste-Identifier-Project
This repository contains the code, experiments, and final report for the Waste Identification project (Machine Learning course- 2026). The main objective of this project is to train and evaluate a neural network designed to accurately categorize different types of waste. 

## Dataset and Preprocessing
The original dataset was affected by a severe class imbalance, with "Clothing" being heavily over-represented (7,302 images) and classes like "Undifferentiated" being under-represented (697 images). To prevent accuracy paradox and model overfitting, the following strategies were implemented: 
- **Targeted data augmentation**: Geometric and chromatic transformations were applied exclusively to the training set, scaling inversely to class size.
- **Weighted Loss Function**: A Weighted Cross-Entropy (WCE) loss function was used to heavily penalize misclassifications on minority classes.

## Model Architecture
After evaluating multiple architectures, including YOLOv5 and Trash-net, the project focused on two primary networks: 
- **ResNet-18** (Baseline): Utilized Transfer Learning with weights pre-trained on ImageNet. The optimized baseline achieved a Balanced Accuracy of 96.67% and an F1-Score of 0.9651
- **EfficientNet-B0** (Final Model): Selected for advanced optimization due to its Mobile Inverted Bottleneck Convolution (MBConv) blocks and Swish (SiLU) activation functions, which mitigate the dying ReLU problem.

## Training and optimization
The final and best-performing model was achieved by migrating to EfficientNet-B0 and applying the following optimizations: 
- **Fine-tuning depth:** Only the last 5 layers of the network were unblocked for fine-tuning. Freezing the primary convolutional blocks acted as a structural regularizer, forcing the network to leverage pre-trained ImageNet filters for basic textures.
- **Label Smoothing**: Applied with a value of &alpha;=0.1 to prevent the model from becoming overconfident and overfitting on fine background details
- **Hyperparameters**: The network was trained using a batch size of 32, an initial learning rate of 0.0001, a weight decay of 0.0001, and a dropout rate of 0.2. A learning rate scheduler (ReduceLROnPlateau) was implemented with a patience of 3 epochs.

## Results
The optimized 5-layer Unlocked EfficientNet-B0 achieved the highest predictive performance: 
- **Balanced Accuracy**: 97.45%
- **F1-Score**: 0.9695
The configuration outperformed the fully fine-tuned ResNet-18 benchmark while operating with less than half the total parameters, proving that strategic architectural constraints are highly effective.

## Team 
This project and its dataset were originally developed and hosted collaboratively on a shared Google Drive workspace. The team members who contributed to this work are: 
- Beatrice Rebecca
- Gaeta Michela
- Genito Fabio
