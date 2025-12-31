# CellProfiler Pipeline: Multichannel Image Pseudocoloring and Overlay Generation

## Overview
This CellProfiler pipeline automates multichannel fluorescence image visualization by opening raw images, assigning standardized pseudocolors, applying user-defined brightness and contrast ranges, and exporting combined overlay images as JPEG files.

The pipeline supports 2-, 3-, and 4-channel imaging datasets and standardizes channel handling across experiments with differing acquisition conventions.

---

## Pipeline Objectives
- Automatically load multichannel fluorescence images
- Assign consistent pseudocolors to each channel
- Allow user-defined brightness and contrast ranges for each channel
- Combine channels into a single overlay image
- Export overlay images as JPEG files for visualization and presentation

---

## Supported Channel Configurations

| Number of Channels | Pseudocolor Assignment |
|-------------------|------------------------|
| 1 channel | DAPI |
| 2 channels | DAPI, GFP |
| 3 channels | DAPI, GFP, RFP |
| 4 channels | DAPI, GFP, RFP, NIR |

---

## Channel Handling and Naming
- Channels are indexed as `d0–d3`, corresponding to acquisition wavelengths.
- All datasets are normalized to a 4-channel schema (`d0–d3`) when present.
- `d3` corresponds to near-infrared (NIR) when available.
- To ensure compatibility across datasets, `d3` is generically labeled as **Marker 3**, independent of microscope-specific naming.

---

## Image Naming Convention
The pipeline expects image filenames matching the following pattern:
.*A(?P<Well>[0-9]{2})f(?P<Site>[0-9]{2})d(?P<Channel>[0-9]).TIF


Where:
- `Well` denotes the well position
- `Site` denotes the imaging site
- `Channel` denotes the acquisition channel (`d0–d3`)

This metadata is used to group channels correctly and generate overlays.

---

## Pipeline Logic
1. **LoadImages**  
   Automatically import images and extract metadata from filenames.

2. **Assign Pseudocolors**  
   Apply standardized pseudocolors based on channel number.

3. **Adjust Brightness and Contrast**  
   Apply user-defined intensity ranges independently for each channel.

4. **Overlay Channels**  
   Combine all active channels into a single composite image.

5. **SaveImages**  
   Export combined overlays as JPEG files.

---

## Outputs
- Combined multichannel overlay images
- File format: `.jpg`
- Overlays include applied pseudocolors and brightness/contrast adjustments
- Images are saved to the designated output directory

---

## Use Cases
- Rapid visualization of multichannel fluorescence images
- Standardized image presentation across experiments
- Figure generation for posters and presentations
- Imaging quality control

### Example Usage

Example input images are in `example_images/`.  
Example outputs (overlays and CSV results) are in `example_outputs/`.  

You can run the pipeline on the included images to reproduce the outputs.


---

## Notes
- Brightness and contrast parameters may require optimization per experiment.
- This pipeline is intended for visualization only and does not perform quantitative analysis.
- Generic channel labeling ensures robustness across imaging platforms.

