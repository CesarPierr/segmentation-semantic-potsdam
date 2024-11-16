# Semantic Segmentation of Aerial Images

## Overview
This project implements a deep learning model based on convolutional neural networks (CNN) to perform semantic segmentation on aerial images of Potsdam city. The model classifies different areas of the images into four categories:
- Buildings
- Roads
- Vegetation
- Other


## Model Architecture
The project uses the U-Net architecture, a specialized convolutional neural network designed for biomedical image segmentation. We chose this proven architecture due to its effectiveness in semantic segmentation tasks. For more information about U-Net, visit the [official documentation](https://lmb.informatik.uni-freiburg.de/people/ronneber/u-net/).

## Getting Started

### Prerequisites
- Google Drive access
- Python environment with deep learning libraries
- Dataset folder structure:
  ```
  potsdam/
  ├── models/
  │   └── modele_.h5
  └── Potsdam-data/
      └── Potsdam/
          └── 30cm/
  ```

### Using the Notebook
1. The notebook includes a "Test the last saved model" section for quick results visualization
2. This section uses a pre-trained model to avoid full retraining
3. Make sure to adjust the file paths according to your directory structure

## Training Details

### Configuration
The model's performance can be tuned using several global variables:
- `BATCH_SIZE`: Number of images processed in each training step
- `WINDOW_SIZE`: Size of image subdivisions
- `OVERLAP`: Overlap between subdivisions
- `LENGTH_EPOCH`: Number of training epochs

### Performance
- Training time: 20-60 minutes depending on hardware
- Test set accuracy: 87.2%
- Gradient steps are adaptively adjusted for optimal convergence

## Results Analysis

### Model Performance
The current accuracy of 87.2% represents a significant improvement over initial tests with custom architectures (which achieved 20-30% accuracy).

### Error Analysis
The model's mistakes typically occur in two scenarios:

1. Boundary Regions
   - Thin areas between different classification zones
   - Generally minimal impact on overall results

2. "Other" Category Classification
   - Less semantically distinct than main categories
   - Occasional misclassification of undefined areas
   - Rare false positives in "other" category

### Practical Impact
The current error patterns have minimal impact on practical applications, as the model maintains high accuracy in identifying critical features (buildings and roads).

## Future Improvements

### Potential Enhancements
1. Data Augmentation
   - Apply transformations to expand the training dataset
   - Increase variety in training examples

2. Additional Features
   - Incorporate building height data
   - Add complementary data sources
