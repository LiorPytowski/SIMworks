# SIMworks

**SIMworks – an integrated software suite for quality-controlled augmented quantitative structured illumination microscopy.**

---

## Table of Contents
- [Available Features](#available-features)
  - [1. Data Checks](#1-data-checks)
    - [1.1. Raw Data](#11-raw-data)
      - [0_Format Converter](#111-0_format-converter)
      - [1_Channel Intensity Profile](#112-1_channel-intensity-profile)
      - [2_Motion & Illumination Variation](#113-2_motion--illumination-variation)
      - [3_Fourier Projection](#114-3_fourier-projection)
      - [4_Modulation Contrast](#115-4_modulation-contrast)
      - [5_Raw SI Data to Projected-Widefield](#116-5_raw-si-data-to-projected-widefield)
    - [1.2. Reconstructed Data](#12-reconstructed-data)
      - [1_Intensity Histograms](#121-1_intensity-histograms)
      - [2_Spherical Aberration Mismatch](#122-2_spherical-aberration-mismatch)
      - [3_Fourier Plots](#123-3_fourier-plots)
  - [2. Image Pre-processing – Augmentation](#2-image-pre-processing--augmentation)
    - [1_Pre-processing – Augmentation](#21-1_pre-processing--augmentation)
    - [2_Nuclei Segmentation](#22-2_nuclei-segmentation)
  - [3. Image Analysis](#3-image-analysis)
    - [1_Foci Segmentation](#31-1_foci-segmentation)
    - [2_Chromatin Classification](#32-2_chromatin-classification)
    - [3_Foci vs Chromatin Analysis](#33-3-foci-vs-chromatin-analysis)
- [Dependencies](#dependencies)
- [Installation](#installation)
- [References](#References)

---

## Available Features

### 1. Data Checks
#### 1.1. Raw Data
- **1.1.1. 0_Format Converter**  
  This tool will convert raw data from Zeiss ELYRA or Nikon N-SIM to the DeltaVision OMX format (CPZAT).  
  **Options:**  
  - Input format: Zeiss ELYRA (CZAPT) or Nikon N-SIM (tiled)  
  - Batch processing: Select this option to convert all images in a given directory  

- **1.1.2. 1_Channel Intensity Profile**  
  Plots the average fluorescence intensity across slices for each channel. Helps to identify issues like photobleaching, unequal intensities between angles, or illumination flicker.  
  **Options:**  
  - Subtract background before plotting: Use this option if image has low signal-to-noise ratio. Draw a ROI in the background when prompted.  

- **1.1.3. 2_Motion & Illumination Variation**  
  Generates a false-colour CMY composite image—each illumination angle is assigned a different hue. Features consistent across angles appear white, while motion or uneven illumination appears colored.  

- **1.1.4. 3_Fourier Projection**  
  Computes maximum intensity projection of log-scaled 2D Fourier transforms across all phases and angles. Reveals distinct first and second order frequency spots indicating SIM pattern quality.  

- **1.1.5. 4_Modulation Contrast**  
  Evaluates SIM contrast by computing the normalized ratio of high- vs low-frequency content, highlighting suboptimal modulation or uneven illumination.  

- **1.1.6. 5_Raw SI Data to Projected-Widefield**  
  Computes projected-widefield images by averaging all phases and angles, enabling direct comparison between SIM and standard widefield.  
  **Options:**  
  - Do bleach correction? Normalize slice intensities  
  - Scale 2x? Scale to match typical reconstructed dimensions  

#### 1.2. Reconstructed Data
- **1.2.1. 1_Intensity Histograms**  
  Shows histograms (black and gray) indicating “negative” value contributions in reconstructions.  
  **Options:**  
  - Discard values below modal value  
  - Discard values below mean from ROI  

- **1.2.2. 2_Spherical Aberration Mismatch**  
  Shows variations in min/mean slice intensities. Dips may reveal mismatches between sample and PSF.  

- **1.2.3. 3_Fourier Plots**  
  Generates lateral Fourier Transform visualizations with resolution rings + radial decay profiles.  
  **Options:**  
  - Discard values below zero  
  - Discard values below manual threshold  

---

### 2. Image Pre-processing – Augmentation
- **2.1. 1_Pre-processing – Augmentation**  
  Batch options:  
  - Threshold + 16-bit Conversion  
  - Bandpass filtering  
  - Modulation Contrast masking  
  - Channel registration  

- **2.2. 2_Nuclei Segmentation**  
  Creates one file per nucleus, optionally excluding nuclei at edges or keeping only the largest.  
  **Options:**  
  - Split touching nuclei?  
  - Keep largest nucleus only?  
  - Remove nuclei touching image edges in X and Y?  

---

### 3. Image Analysis
- **3.1. 1_Foci Segmentation**  
  Segments two foci channels and measures nearest-neighbour distances. Units match pixel size in image properties.  

- **3.2. 2_Chromatin Classification**  
  Classifies chromatin (Miron, E. et al 2020).  
  **Options:**  
  - Gaussian blur: increase if chromatin has holes  
  - Thresholding method for smooth stack  
  - Optional erosion: erode by morphology, not intensity  

- **3.3. 3_Foci vs Chromatin Analysis**  
  Analyses foci position relative to chromatin classes. Distances use pixel size units.

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
     or use an archived version from this manuscript’s repository (GitHub link).  
   - To install, place the `DiAna_.jar` file in the **plugins** folder of your Fiji directory.  
     In Fiji, you can find this folder via:  
     `File › Show Folder › Plugins`.  

3. **Restart Fiji**  
   After restarting, **SIMworks** will appear in your main Fiji menu bar.  

---

## References
For references related to SIMworks dependencies, see this page: link.
