 # AI in Healthcare Project
Student Name: Tafadzwa hove 

Group Number: Group 9 

Title: AI-Driven Malaria Detection: Developing a Convolutional Neural Network for Blood Smear Analysis  

## ABSTRACT 

Malaria remains one of the most significant public health challenges globally, particularly in sub-Saharan Africa. According to the World Health Organization (WHO), there were an estimated 249 million malaria cases and 608,000 deaths worldwide in 2022, with Africa accounting for approximately 94% of all cases and 95% of deaths (WHO, 2023). Zimbabwe, where this project draws its contextual motivation, experiences substantial malaria burden, with transmission occurring primarily in rural and resource-limited areas where diagnostic infrastructure is often inadequate. 

The gold standard for malaria diagnosis remains microscopic examination of Giemsa-stained blood smears. This method requires trained microscopists, specialized equipment, and significant time investment resources that are frequently scarce in endemic regions. Manual microscopy is labor-intensive, subjective, and prone to human error, particularly when microscopists are fatigued or working under high-volume conditions (Mukhtar et al., 2023). Delayed or incorrect diagnosis can lead to inappropriate treatment, increased morbidity and mortality, and accelerated drug resistance. 

Artificial intelligence, particularly deep learning approaches such as convolutional neural networks (CNNs), offers a promising solution to these diagnostic challenges. Recent advances in computer vision have demonstrated that AI models can achieve accuracy comparable to expert microscopists in detecting malaria parasites in blood smear images (Rajaraman et al., 2018; Masud et al., 2020). These models can operate on standard computing hardware, making them suitable for deployment in resource-limited settings where expensive diagnostic equipment may not be available. 

This research project aims to develop a lightweight, efficient CNN-based system for automated malaria detection from blood smear images. The primary objective is to create a model that maintains high diagnostic accuracy while being computationally efficient enough to run on basic computer systems.  By leveraging transfer learning with MobileNetV2 a model specifically designed for mobile and edge deploymentwe seek to balance performance with accessibility. This progress report details the work completed to date, including literature review findings, dataset preparation, methodology development, and plans for future project stages
3. Methodology 

## 3.1 Project Approach 

This project follows a structured machine learning development lifecycle, encompassing data acquisition, preprocessing, model development, training, evaluation, and interpretation. The approach prioritizes simplicity and computational efficiency without compromising diagnostic accuracy. 

## 3.2 Model Architecture: Transfer Learning with MobileNetV2 

The core of our system is a convolutional neural network built using transfer learning with the MobileNetV2 architecture. Our specific implementation includes: 

 **Base Model** : MobileNetV2 pre-trained on ImageNet, with weights frozen during initial training. The include_top=False parameter removes the original classification layer, allowing us to add custom layers tailored to our binary classification task. 

**Input Shape:** Images resized to 128×128 pixels with three color channels (RGB). This resolution balances detail preservation with computational efficiency, reducing memory requirements compared to the 224×224 input typically used with MobileNetV2. 

**Custom Top Layers:** 

- Global Average Pooling 2D: Reduces each feature map to a single value, dramatically reducing parameters compared to flattening 

- Dense Layer: 128 neurons with ReLU activation for learning task-specific features 

- Dropout Layer: 0.5 dropout rate to prevent overfitting 

- Output Layer: Single neuron with sigmoid activation for binary classification (infected vs. uninfected) 

**Rationale for Architecture Choices:** MobileNetV2 was selected specifically because it is designed for mobile and edge deployment. Its depthwise separable convolutions require significantly fewer computations than standard convolutions, making it ideal for resource-limited settings. The 128×128 input size further reduces computational demands while prior research suggests this resolution is adequate for detecting Plasmodium parasites (Quinn et al., 2016). 

## 3.3 Training Strategy 

**Optimizer:** Adam optimizer with default learning rate (0.001). Adam adapts learning rates per parameter and has shown strong performance across diverse deep learning tasks. 

**Loss Function:** Binary cross-entropy, appropriate for two-class classification problems. 

**Metrics:** Accuracy, precision, and recall will be tracked during training. Recall is particularly important in medical diagnostics to minimize false negatives. 

**Callbacks:** 

- EarlyStopping: Monitors validation loss and stops training if no improvement for 5 epochs, restoring the best weights 

- ReduceLROnPlateau: Reduces learning rate by factor of 0.2 when validation loss plateaus for 3 epochs 

- ModelCheckpoint: Saves the best model based on validation loss 

- Epochs: Maximum 20 epochs, though early stopping likely to halt training earlier. 

## 3.4 Data Augmentation 

To improve model generalization and artificially expand the training dataset, I will apply the following augmentations during training: 

- Rotation range: ±20 degrees 

- Width and height shifts: ±20% 

- Shear transformations: ±20% 

- Zoom range: ±20% 

- Horizontal flip 

These augmentations simulate the natural variation present in real-world blood smear images, helping the model learn invariant features of parasites regardless of orientation or position. Importantly, validation and test data receive only rescaling  to provide unbiased performance estimates. 

## 3.5 Evaluation Strategy 

Model performance will be assessed using: 

- Accuracy: Overall proportion of correct predictions 

- Precision: Proportion of positive identifications that are correct (important for avoiding unnecessary treatment) 

- Recall: Proportion of actual positives correctly identified (critical for detecting infections) 

- F1-Score: Harmonic mean of precision and recall 

- Confusion Matrix: Visual representation of true vs. predicted classifications, showing false positives and false negatives 

Classification reports will provide detailed perclass metrics, and the confusion matrix will be visualized as a heatmap for clarity. 


## Project Presentation Video
[Watch the presentation on YouTube](https://youtu.be/5OyJY8X_II8)
## Data set
https://drive.google.com/file/d/1XrfrHbInDPQitpY5YwjsDxEjruxmOz-m/view?usp=sharing

## Code Execution 
https://colab.research.google.com/drive/1QsB3i2ByNS35yk1-1SSEhZ9AOhJepAwq?usp=sharing

