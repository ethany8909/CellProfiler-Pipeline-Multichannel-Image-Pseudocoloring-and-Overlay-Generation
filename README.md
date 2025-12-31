# CellProfiler-Pipeline-Multichannel-Image-Pseudocoloring-and-Overlay-Generation
Overview

This CellProfiler pipeline automates multichannel fluorescence image visualization by opening raw images, assigning standardized pseudocolors, applying user-defined brightness and contrast ranges, and exporting combined overlay images as JPEG files.

The pipeline supports 2-, 3-, and 4-channel imaging datasets and is designed to standardize visualization across experiments where channel naming conventions may differ.

Pipeline Objectives

Automatically load multichannel fluorescence images

Assign consistent pseudocolors to each channel

Allow user-defined brightness and contrast ranges for each channel

Combine channels into a single overlay image

Export overlay images as JPEG files for visualization and presentation

Supported Channel Configurations

This pipeline supports datasets with 2–4 channels, using the following pseudocolor conventions:

Number of Channels	Channel Assignment
1 channel	Blue
2 channels	Blue, Green
3 channels	Blue, Green, Red
4 channels	Blue, Green, Red, Grey
Channel Handling and Naming

Raw channel indices are acquired as d0 → d3, corresponding to the wavelength used during image acquisition.

All datasets are normalized to a 4-channel schema (d0–d3), even if fewer channels are present.

The d3 channel corresponds to near-infrared (NIR) when available.

The d3 channel is labeled as Marker 3 to maintain compatibility across datasets with varying channel annotations.

This approach ensures consistent pipeline behavior regardless of microscope-specific channel naming conventions.

Image Naming Convention

The pipeline assumes the following filename structure:

.*A(?P<Well>[0-9]{2})f(?P<Site>[0-9]{2})d(?P<Channel>[0-9]).TIF


Where:

Well indicates the well position

Site indicates the imaging site

Channel indicates the acquisition channel (d0–d3)

This metadata is used to correctly group channels and generate overlays.

Pipeline Logic

LoadImages
Automatically import images and parse well, site, and channel metadata from filenames.

Assign Pseudocolors
Apply standardized pseudocolors based on the number of channels present.

Adjust Brightness and Contrast
User-defined intensity ranges are applied independently to each channel.

Overlay Channels
Combine all active channels into a single composite image.

SaveImages
Export combined overlays as JPEG files.

Outputs

Combined multichannel overlay images

File format: .jpg

Output includes pseudocolored overlays with adjusted brightness/contrast

Saved to the designated output directory

Use Cases

Rapid visualization of multichannel fluorescence images

Standardized image presentation across experiments

Figure generation for posters, presentations, and reports

Quality control of imaging datasets

Notes

Brightness and contrast settings may need to be optimized per experiment.

The pipeline prioritizes visualization and does not perform quantitative measurements.

Channel labeling is intentionally generic to maximize cross-platform compatibility.
