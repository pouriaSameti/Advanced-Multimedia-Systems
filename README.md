# Advanced Multimedia Systems – Course Projects

This repository contains projects developed for the **Advanced Multimedia Systems** course at the **Isfahan University of Technology (IUT)**. The projects focus on fundamental and advanced concepts in image and multimedia compression, including **statistical redundancy, spatial redundancy, spectral redundancy, and temporal redundancy reduction** techniques.

All projects were completed under the supervision of **Dr. Nader Karimi**, and emphasize both theoretical foundations and practical implementation aspects of multimedia coding systems.

### Table of Contents
[Exercise 1: RGB to Grayscale Conversion]()<br>
[Exercise 2]()<br>
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
       
3. rayscale Conversion Methods. The following conversion approaches were implemented and compared:
     + Channel Averaging Method
     + Luminance-Based Perceptual Method (Weighted combination based on human visual sensitivity)
     + Linear Gamma Approximation Method (Approximate gamma correction before linear luminance projection)
       
4. Quantitative Evaluation of Methods. Each grayscale conversion method is evaluated using:
    + MSE between reconstructed RGB and original image
    + PSNR comparison
    + Entropy analysis
    + Visual inspection

The results provide insight into how perceptual weighting and gamma correction affect information preservation.



