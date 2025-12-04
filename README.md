# SIMworks

**SIMworks – an integrated software suite for quality-controlled augmented quantitative structured illumination microscopy.**

---

## Table of Contents
- [Available Features](#available-features)
  - [1. Data Checks](#1-data-checks)
    - [1.1. Raw Data](#11-raw-data)
      - 0_Format Converter
      - 1_Channel Intensity Profile
      - 2_Motion & Illumination Variation
      - 3_Fourier Projection
      - 4_Modulation Contrast
    - [1.2. Reconstructed Data](#12-reconstructed-data)
      - 1_Intensity Histograms
      - 2_Spherical Aberration Mismatch
      - 3_Fourier Plots
	- [1.3. Utilities](#13-Utilities)
	   - 1_Reconstructed Bandpass Filter Optimisation
	   - 2_Reconstructed Threshold and 16-bit Conversion
	   - 3_Raw SI Data to Projected-Widefield
  - [2. Image Pre-processing & Augmentation](#2-image-pre-processing-&-augmentation)
    - 1_Pre-processing
    - 2_Main Object Segmentation
  - [3. Image Analysis](#3-image-analysis)
    - 1a_Foci Segmentation
	- 1b_Structure Segmentation
    - 2_Chromatin Classification
    - 3_Subobject vs Chromatin Analysis
	- 4_Foci Randomisation
- [Dependencies](#dependencies)
- [Installation](#installation)
- [Test Dataset](#test-dataset)
- [References](#References)

---

## Available Features

### 1. Data Checks
#### 1.1. Raw Data
- **1.1.0_Format Converter**  
 This tool will convert various commercial and custom raw data formats to the C; A(Z(P())); T format.  
  **Options:**  
  - Input formats:
   -C; Z; P           (e.g. Zeiss Lattice SIM or Elyra)
   -C; Z; A(P())      (e.g. MI-SIM)
   -C; Z(A(P()))      (e.g. openSIM or Lock-in-SIM)
   -C; A(Z(P())); T   (e.g. OMX)
   -C; -; A(Z(P()))   (e.g. ProSIM)
   -C; T(Z(A(P())))   (e.g. MRC)
   -Z(P*A), Tiled     (e.g. Nikon N-SIM)
  - Batch processing: Select this option to convert all images in a given directory  

- **1.1.1_Channel Intensity Profile**  
  Plots the average fluorescence intensity across slices for each channel. Helps to identify issues like photobleaching, unequal intensities between angles, or illumination flicker.  
  **Options:**  
  - Subtract background before plotting: Use this option if image has low signal-to-noise ratio. Draw a ROI in the background when prompted.  

- **1.1.2_Motion & Illumination Variation**  
  Generates a false-colour CMY composite image—each illumination angle is assigned a different hue. Features consistent across angles appear white, while motion or uneven illumination appears colored.  

- **1.1.3_Fourier Projection**  
  Computes maximum intensity projection of log-scaled 2D Fourier transforms across all phases and angles. Reveals distinct first and second order frequency spots indicating SIM pattern quality.  

- **1.1.4_Modulation Contrast**  
  Evaluates SIM contrast by computing the normalized ratio of high- vs low-frequency content, highlighting suboptimal modulation or uneven illumination.  

- **1.1.6. 5_Raw SI Data to Projected-Widefield**  
  Computes projected-widefield images by averaging all phases and angles, enabling direct comparison between SIM and standard widefield.  
  **Options:**  
  - Do bleach correction? Normalize slice intensities  
  - Scale 2x? Scale to match typical reconstructed dimensions  

#### 1.2. Reconstructed Data
- **1.2.1_Intensity Histograms**  
  Shows histograms (black and gray) indicating “negative” value contributions in reconstructions.  
  **Options:**  
  - Discard values below modal value  
  - Discard values below mean from ROI  

- **1.2.2_Spherical Aberration Mismatch**  
  Shows variations in min/mean slice intensities. Dips may reveal mismatches between sample and PSF.  

- **1.2.3_Fourier Plots**  
  Generates lateral Fourier Transform visualizations with resolution rings + radial decay profiles.  
  **Options:**  
  - Discard values below zero  
  - Discard values below manual threshold  

#### 1.3. Utilities
- **1.3.1_Reconstructed Bandpass Filter Optimisation**
- **1.3.2_Reconstructed Threshold and 16-bit Conversion**  
- **1.3.3_Raw SI Data to Projected-Widefield**  

---

### 2. Image Pre-processing & Augmentation
- **2.1_Pre-processing**  
  Batch options:  
  - Threshold + 16-bit Conversion  
  - Bandpass filtering  
  - Modulation Contrast masking  
  - Channel registration with option to crop margins

- **2.2_Main Object Segmentation**  
  Creates one file per main object, optionally excluding objects at edges or keeping only the largest.  
  **Options:**  
  - Split touching objects?  
  - Keep largest object only?  
  - Remove objects touching image edges in X and Y?  

---

### 3. Image Analysis
- **3.1a_Foci Segmentation**  
  Segments two foci channels and measures nearest-neighbour distances. Units match pixel size in image properties.  
  
- **3.1b_Structure Segmentation**  
  Segments a non-foci channel. Units match pixel size in image properties.  

- **3.2_Chromatin Classification**  
  Classifies chromatin (Miron, E. et al 2020).  
  **Options:**  
  - Gaussian blur: increase if chromatin has holes  
  - Thresholding method for smooth stack  
  - Optional erosion: erode by morphology, not intensity  

- **3.3_Subobject vs Chromatin Analysis**  
  Analyses foci position relative to chromatin classes. Distances use pixel size units.

- **3.4_Foci Randomisation**
  Generates synthetic images that contain the same number of foci as the original, but redistributes them to random positions within the chromatin.

  

---

  ## Dependencies

SIMworks requires the following update sites:

- **Java-8**  
- **3D ImageJ Suite**  
- **CLIJ ecosystem**:  
  - clij  
  - clij2  
  - clijx-assistant  
  - clijx-assistant-extensions
- **DIana** *(necessary but not available via Fiji's update sites; must be installed manually; see below)*  
- **IJBP-plugins**  
- **ImageScience**  
- **SIMcheck**  
- **SIMworks**  

---

## Installation

1. **Enable update sites**  
   Launch Fiji, navigate to:  
   `Help › Update...` → `Manage Update Sites` → select the update sites listed above.  

2. **Install the Distance Analysis (DiAna) plugin**  
   - Install **DiAna (Gilles et al., 2017)** from:  
     [https://imagej.net/plugins/distance-analysis](https://imagej.net/plugins/distance-analysis)  
     or use an archived version from this repository [(link)](https://github.com/LiorPytowski/SIMworks/tree/main/DiAna).  
   - To install, place the `DiAna_.jar` file in the **plugins** folder of your Fiji directory.  
     In Fiji, you can find this folder via:  
     `File › Show Folder › Plugins`.  

3. **Restart Fiji**  
   After restarting, **SIMworks** will appear in your main Fiji menu bar.  

---

## Test Dataset
A dataset containing raw and reconstructed SIM images can be found here: [link](https://drive.google.com/drive/folders/1j2XyW6UvynATGlBGK1NFazAUWwL1zBg6?usp=sharing).

---
## References
For references related to SIMworks dependencies, see this page: [link](https://github.com/LiorPytowski/SIMworks/blob/main/References.md).
