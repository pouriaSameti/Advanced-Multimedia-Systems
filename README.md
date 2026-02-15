# Advanced Multimedia Systems – Course Projects

This repository contains projects developed for the **Advanced Multimedia Systems** course at the **Isfahan University of Technology (IUT)**. The projects focus on fundamental and advanced concepts in image and multimedia compression, including **statistical redundancy, spatial redundancy, spectral redundancy, and temporal redundancy reduction** techniques.

All projects were completed under the supervision of **Dr. Nader Karimi**, and emphasize both theoretical foundations and practical implementation aspects of multimedia coding systems.

### Table of Contents
[Exercise 1: RGB to Grayscale Conversion](https://github.com/pouriaSameti/Advanced-Multimedia-Systems/tree/main?tab=readme-ov-file#exercise-1-rgb-to-grayscale-conversion)<br>
[Exercise 2: Spatial Redundancy Reduction]()<br>
[Exercise 3]()<br>
[Final Project]()<br>
<br>

### Installation

To run this project, install the required dependencies by executing the following commands:

```python
  pip install numpy
```
```python
  pip install pandas
```
```python
  pip install matplotlib
```
```python
  pip install opencv-python
```

## Exercise 1: RGB to Grayscale Conversion

### Objective
The objective of this exercise is to implement fundamental image quality assessment metrics and evaluate multiple **RGB-to-Grayscale conversion** methods with respect to information loss.

First, we implement core distortion and information measures including **MSE, PSNR, and Entropy** for both color and grayscale images.
Then, several grayscale conversion strategies are implemented and quantitatively compared to determine which method minimizes distortion relative to the original RGB image.

### Implementation Details
1. PPM Image Reader Implementation
   + Manual parsing of PPM image format
   + Extraction of header information and pixel data
     
2. Mean Squared Error (MSE)
   Implemented for:
     + RGB (multi-channel) images
     + Grayscale images
       
3. Grayscale Conversion Methods. The following conversion approaches were implemented and compared:
     + Channel Averaging Method
     + Luminance-Based Perceptual Method (Weighted combination based on human visual sensitivity)
     + Linear Gamma Approximation Method (Approximate gamma correction before linear luminance projection)
       
4. Quantitative Evaluation of Methods. Each grayscale conversion method is evaluated using:
    + MSE between reconstructed RGB and original image
    + PSNR comparison
    + Entropy analysis
    + Visual inspection

The results provide insight into how perceptual weighting and gamma correction affect information preservation.

## Exercise 2: Spatial Redundancy Reduction (Lossless Prediction)

### Objective
The objective of this exercise is to analyze and reduce spatial redundancy in images using **predictive coding techniques within a lossless compression** framework.

We implement several image predictors—including classical and optimized linear models—and evaluate their effectiveness in minimizing prediction error entropy. The core principle is to predict each pixel from its spatial neighbors, encode the residual (prediction error), and reconstruct the image perfectly at the decoder.

The performance of different predictors is compared in terms of compression efficiency, distortion, and computational complexity.

### Implementation Details
1. Implementation of the classical Median Edge Detector (MED) predictor
2. Third-Order Linear Predictor (Optimum Mode)
3. Designed Predictors (Hybrid and Adaptive Models)
     + Partitioning + MED: In this method, we combine the MED (Median Edge Detector) predictor with a partitioning technique for image prediction and reconstruction. The core idea is to predict each pixel’s value based on         its neighbors and then encode the prediction error, which often results in better compression efficiency.
     + Second-Order Optimum Least Squares Predictor with Partitioning: in this method, we combine a linear predictor with adaptive coefficients and a partitioning technique. The image is divided into several horizontal partitions, and for each partition, a coefficient ρ is computed to best capture the local correlation between neighboring pixels.
     + MED with Context Modeling: Using these contexts, the MED predictor is applied in a fully vectorized manner to generate a predicted value for each pixel. Prediction residuals (the difference between the original pixel and the prediction) are then separated into four lists, one for each context, using a fast Numba-optimized routine.
       
4. Evaluation and Comparison:
    + Reconstruction Accuracy (MSE between reconstructed image and original input)
    + Compression Efficiency (Entropy of prediction residuals)
    + Computational Complexity (Compression runtime & Decompression runtime)



