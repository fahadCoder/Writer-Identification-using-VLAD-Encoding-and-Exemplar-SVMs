# Raw Image Demosaicing and HDR Reconstruction

This project implements a raw image processing pipeline for converting camera sensor data into enhanced RGB images. It covers Bayer pattern analysis, demosaicing, luminosity correction, white balance, sensor linearity verification, HDR reconstruction, and iCAM06-inspired tone mapping.

The goal of this project is to understand how raw camera data is processed before it becomes a final viewable image.

---

## Project Overview

Digital cameras do not directly capture full RGB images. Instead, raw camera sensors store intensity values through a Bayer color filter array, where each pixel records only one color component: red, green, or blue.

In this project, I worked directly with raw CR3 camera files and NumPy sensor arrays to reconstruct color images and improve their visual quality. I also combined multiple exposure images to generate HDR results with better detail in both dark and bright regions.

---

## Features

- Bayer pattern investigation from raw sensor data
- Custom demosaicing algorithm using convolution-based interpolation
- RGB image reconstruction from raw Bayer mosaics
- Percentile-based image normalization
- Gamma correction and logarithmic luminosity enhancement
- Gray-world white balance correction
- Sensor linearity analysis using different exposure times
- HDR image reconstruction from multiple raw exposures
- iCAM06-inspired tone mapping
- Image enhancement using contrast adjustment, sharpening, denoising, and filtering
- Final `process_raw()` function for converting CR3 files into high-quality JPEG images

---

## Technologies Used

- Python
- NumPy
- Matplotlib
- SciPy
- OpenCV
- rawpy
- Pillow
- imageio

---

## Project Workflow

### 1. Bayer Pattern Analysis

The first step was to inspect the raw sensor data and identify the Bayer pattern. I visualized small sections of the raw image as heatmaps and analyzed pixel intensity arrangements to understand how red, green, and blue samples were distributed across the sensor.

### 2. Demosaicing

After identifying the Bayer structure, I implemented a custom demosaicing algorithm. I created separate masks for red, green, and blue pixels and used convolution-based interpolation to estimate missing color values.

This step reconstructed a full RGB image from the single-channel raw Bayer mosaic.

### 3. Luminosity Enhancement

The demosaiced image was initially dark, so I applied brightness correction techniques. I used percentile normalization to reduce the effect of extreme values, followed by gamma correction and logarithmic transformation to improve image visibility.

### 4. White Balance

I implemented gray-world white balance to correct color casts. The method adjusts the RGB channels so that their average values become balanced, producing a more natural-looking image.

### 5. Sensor Linearity Verification

To verify that raw sensor data behaves linearly with exposure time, I analyzed multiple images captured with different exposure settings. I calculated average raw intensity values and plotted them against exposure duration.

This helped confirm that raw sensor values are approximately proportional to the amount of light captured.

### 6. HDR Reconstruction

I combined multiple exposure-bracketed raw images to create a high-dynamic-range image. This allowed details from both underexposed and overexposed regions to be preserved in a single image.

### 7. iCAM06-Inspired Tone Mapping

To make the HDR image viewable on a standard display, I implemented an iCAM06-inspired tone mapping approach. This included luminance processing, logarithmic compression, bilateral filtering, base-detail separation, and final image reconstruction.

### 8. Final Raw Processing Function

At the end of the project, I created a reusable function:

```python
process_raw("input.CR3", "output.jpg")
```

This function takes a CR3 raw image as input and saves a processed high-quality JPEG image as output.

---

## Results

The project produces several output images at different stages of the pipeline, including:

- Demosaiced RGB image
- Gamma-corrected image
- White-balanced image
- Simple HDR image
- Tone-mapped HDR image
- Final enhanced JPEG output

---

## How to Run

Install the required dependencies:

```bash
pip install numpy matplotlib scipy imageio pillow rawpy opencv-contrib-python
```

Run the Jupyter notebook:

```bash
jupyter notebook Ex-2-Solution.ipynb
```

To process a raw CR3 image using the final function:

```python
process_raw("input.CR3", "output.jpg")
```

---

## Repository Structure

```text
.
├── Ex-2-Solution.ipynb
├── README.md
├── results/
│   ├── demosaiced_image.jpg
│   ├── gamma_corrected_image.jpg
│   ├── simple_hdr.jpg
│   ├── tone_mapped_image.jpg
│   └── final_processed_image.jpg
└── requirements.txt
```

---

## What I Learned

Through this project, I learned how raw camera images are formed and processed before becoming standard RGB images. I gained practical experience with Bayer filters, demosaicing, white balance, tone correction, HDR image formation, and tone mapping.

I also learned why raw sensor data is useful for HDR imaging, because it maintains a more linear relationship between pixel intensity and exposure time compared to processed JPEG images.

---

## Conclusion

This project gave me hands-on experience with computational photography and raw image processing. It helped me understand the steps involved in transforming raw sensor data into visually enhanced images and how HDR techniques can be used to preserve image details across a wider brightness range.
