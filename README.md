Industrial Defect Detection using Deep Learning
Project Overview
This project implements a deep learning solution for detecting defects in industrial components using computer vision. The system combines two distinct datasets and employs data augmentation techniques to create a robust defect detection model.
Dataset Description
Dataset Sources

Industrial Tools Classification Dataset (Smaller Dataset)

Source: Kaggle (niharikaamritkar/industrial-tools-classification)
Contains images of industrial tools with defective and non-defective classifications
Initially smaller in size, enhanced through augmentation


Casting Product Dataset (Larger Dataset)

Source: Kaggle (ravirajsinh45/real-life-industrial-dataset-of-casting-product)
Comprises casting product images with defective ("def_front") and non-defective ("ok_front") samples
Larger dataset used to complement the first dataset



Data Augmentation Strategy
Augmentation Techniques
The smaller dataset was augmented using the following transformations:

Random Horizontal Flip (50% probability)
Random Vertical Flip (50% probability)
Random Rotation (up to 30 degrees)
Color Jitter

Brightness adjustment: ±20%
Contrast adjustment: ±20%
Saturation adjustment: ±20%
Hue adjustment: ±10%


Random Affine Transformation

Rotation: up to 20 degrees
Scale: 80% to 120%



For each original image, 5 augmented copies were generated, significantly increasing the dataset size and introducing valuable variations.
Dataset Integration and Split
Combination Process

Both datasets were merged into a unified structure
Maintained original class hierarchies:

defective/

original tools
casting


non-defective/

original tools
casting





Data Split
The combined dataset was split into:

Training set: 70%
Validation set: 15%
Test set: 15%

The split was performed while maintaining the stratification of subclasses to ensure balanced representation across all sets.
Model Architecture and Training
Model Details

Base Architecture: ResNet-18 (pretrained)
Modifications:

Adapted final fully connected layer for binary classification
Input size: 224x224 pixels
Output classes: 2 (defective, non-defective)



Training Configuration

Optimizer: Adam (Learning rate: 0.001)
Loss Function: Cross Entropy Loss
Batch Size: 32
Epochs: 10
Data Augmentation during training:

Random horizontal flips
Random rotations (10 degrees)
Normalization (mean=[0.5, 0.5, 0.5], std=[0.5, 0.5, 0.5])



Project Structure
CopyC:.
│   Defect_Detection.ipynb    # Main notebook for development and testing
│   model_best.pth           # Saved model weights
│   README.md                # Project documentation
│   requirement.txt          # Dependencies
│
└───src
        data_preparation.py  # Dataset processing and augmentation
        evaluate.py         # Model evaluation scripts
        model.py           # Model architecture definition
        train.py           # Training pipeline
Results and Evaluation
The model's performance was evaluated using:

Classification report with precision, recall, and F1-score
Confusion matrix for detailed error analysis
Visual prediction verification on test samples

Future Improvements

Experiment with other pretrained architectures (e.g., EfficientNet, Vision Transformer)
Implement more sophisticated augmentation techniques
Add support for multi-class defect classification
Integrate explainable AI techniques for better defect localization
Optimize model for deployment in production environments

Dependencies
The project requires the following main dependencies:

PyTorch
torchvision
PIL
scikit-learn
matplotlib
kagglehub

All dependencies are listed in requirement.txt.
