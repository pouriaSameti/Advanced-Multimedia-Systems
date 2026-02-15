# Advanced Multimedia Systems – Course Projects

This repository contains projects developed for the **Advanced Multimedia Systems** course at the **Isfahan University of Technology (IUT)**. The projects focus on fundamental and advanced concepts in image and multimedia compression, including **statistical redundancy, spatial redundancy, spectral redundancy, and temporal redundancy reduction** techniques.

All projects were completed under the supervision of **Dr. Nader Karimi**, and emphasize both theoretical foundations and practical implementation aspects of multimedia coding systems.

### Table of Contents
[Exercise 1: RGB to Grayscale Conversion](https://github.com/pouriaSameti/Advanced-Multimedia-Systems/tree/main?tab=readme-ov-file#exercise-1-rgb-to-grayscale-conversion)<br>
[Exercise 2: Spatial Redundancy Reduction](https://github.com/pouriaSameti/Advanced-Multimedia-Systems/blob/main/README.md#exercise-2-spatial-redundancy-reduction-lossless-prediction)<br>
[Exercise 3: Spectral Redundancy Reduction](https://github.com/pouriaSameti/Advanced-Multimedia-Systems/tree/main?tab=readme-ov-file#exercise-3-spectral-redundancy-reduction-transform-based-compression)<br>
[Final Project: Stereo Image Compression](https://github.com/pouriaSameti/Advanced-Multimedia-Systems/blob/main/README.md#final-project-stereo-image-compression-lossless-framework)<br>
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
     + **Partitioning + MED**: In this method, we combine the MED (Median Edge Detector) predictor with a partitioning technique for image prediction and reconstruction. The core idea is to predict each pixel’s value based on         its neighbors and then encode the prediction error, which often results in better compression efficiency.
     + **Second-Order Optimum Least Squares Predictor with Partitioning**: in this method, we combine a linear predictor with adaptive coefficients and a partitioning technique. The image is divided into several horizontal partitions, and for each partition, a coefficient ρ is computed to best capture the local correlation between neighboring pixels.
     + **MED with Context Modeling**: Using these contexts, the MED predictor is applied in a fully vectorized manner to generate a predicted value for each pixel. Prediction residuals (the difference between the original pixel and the prediction) are then separated into four lists, one for each context, using a fast Numba-optimized routine.
       
4. Evaluation and Comparison:
    + Reconstruction Accuracy (MSE between reconstructed image and original input)
    + Compression Efficiency (Entropy of prediction residuals)
    + Computational Complexity (Compression runtime & Decompression runtime)


## Exercise 3: Spectral Redundancy Reduction (Transform-Based Compression)

### Objective
In this exercise, we focus on reducing **spectral redundancy** using transform-domain and color-space compression techniques.
The primary tools employed are:
  + **Discrete Cosine Transform (DCT)**
  + **YCbCr color space transformation**
  + **Chrominance downsampling (4:4:0 and 4:2:0 modes)**

We begin with baseline implementations and progressively design improved compression strategies aimed at maximizing PSNR while maintaining efficient redundancy reduction. Evaluation is conducted on standard benchmark images, including Barbara and other commonly used test images.

### Implementation Details
1. DCT-Based Transform Coding. Implementation of:
    + 2D Discrete Cosine Transform (DCT)
    + Inverse DCT (IDCT)
    + Complete encoder–decoder pipeline
    + Block-based processing (8x8 Blocks)

2. High-Frequency Masking in DCT Domain. Designed a compression approach by:
     + Transforming the image into DCT domain
     + Suppressing (masking) high-frequency coefficients
     + Reconstruction using IDCT
     + Analysis of distortion vs. energy compaction trade-off
  
3. YCbCr-Based Compression with Chrominance Subsampling. RGB to YCbCr transformation. Implementation of:
     + 4:4:0 subsampling
     + 4:2:0 subsampling
     + Decoder pipeline (Upsampling & YCbCr → RGB reconstruction)
     + Evaluation of chrominance redundancy removal
       
4. Improved YCbCr (4:2:0) with Gaussian Smoothing
     + Encoder (RGB → YCbCr & 4:2:0 chrominance subsampling)
     + Decoder (Chrominance upsampling & Gaussian smoothing filter applied to reduce aliasing artifacts & YCbCr to RGB reconstruction)
     + This approach improves visual quality and PSNR compared to naive upsampling

5. Enhanced YCbCr (4:2:0) with Mean Pooling + Gaussian Smoothing
     + Encoder (RGB → YCbCr 4:2:0 subsampling using Mean Pooling for chroma downsampling chrominance subsampling)
     + Decoder (Chrominance upsampling & Gaussian smoothing filter applied to reduce aliasing artifacts & YCbCr to RGB reconstruction)
     + This approach improves visual quality and PSNR compared to naive upsampling
  
6. Evaluation Criteria. Each method was evaluated using:
    + Channel-wise Entropy
    + Red channel entropy
    + Green channel entropy
    + Blue channel entropy
    + Average Channel Entropy

## Final Project: Stereo Image Compression (Lossless Framework)
### Objective
The objective of this project is to design a lossless stereo image compression system by exploiting inter-view (temporal-like) redundancy between left and right images. Stereo image pairs exhibit strong correlation between views. We leverage this redundancy by:
  + Using the left image as a reference
  + Reconstructing the right image via motion estimation and compensation
  + Encoding only the residual information
    
![4-Encoder + Quantization + Hyperprior + T-CA + Decoder - Page 1](https://github.com/user-attachments/assets/ff8a19b4-399a-4f9a-83b8-d0ef44d88083)

### Key Design Characteristics
  + Fully lossless reconstruction
  + Inter-view prediction reduces stereo redundancy
  + Combination of:
    + Predictive coding (MED)
    + Block-based motion estimation
    + Residual entropy reduction

Efficient decorrelation in both spatial and inter-view domains

Our framework integrates techniques targeting:
  + **Spatial redundancy** (predictive coding using MED)
  + **Statistical redundancy** (entropy reduction of residuals)
  + **Spectral redundancy** (color space transformation)
  + **Inter-view redundancy** (motion estimation between stereo pairs)

The overall design follows a predictive lossless compression paradigm inspired by motion-compensated coding and JPEG lossless principles.

### Implementation Details
The system consists of an encoder–decoder architecture described below.

**Encoder:**
1. Color Space Transformation
   + Convert both left and right images from RGB to YUV
   + Improves decorrelation between luminance and chrominance components
2. Level Shifting
   + Pixel values shifted to center the dynamic range around zero
   + Facilitates prediction and residual modeling 
3. Right Image Padding
    + Padding applied according to block size
    + Ensures compatibility with block-based motion estimation
4. Motion Estimation (Inter-View Prediction)
    + Block-based motion estimation between left (reference) and right images
    + Implemented using Three-Step Search (3SS) algorithm
    + Motion vectors computed for each block
5. Motion Compensation & Residual Computation
    + Predicted right image generated using motion vectors
    + Only residual and motion vectors are encoded
6. Left Image Predictive Coding
     + Median Edge Predictor (MED) applied to the left image
     + Residual computed and entropy-coded
     + Ensures lossless reconstruction

**Decoder:**
1. Left Image Reconstruction
    + MED-based decoding of left image residual
    + Perfect reconstruction of reference image

2. Right Image Reconstruction
    + Motion compensation using:
    + Motion vectors
    + Right residual
    + Exact reconstruction of the right image

3. Cropping
    + Removal of padding
4. Inverse Level Shifting
5. YUV to RGB Conversion

Final reconstruction of both images in RGB space
