# STABLE GEO UPSCALER: ENHANCING GEOSPATIAL IMAGERY WITH LATENT DIFFUSION

![Project Type](https://img.shields.io/badge/Project_Type-Research%20%7C%20Computer%20Vision-blueviolet)
![Status](https://img.shields.io/badge/Status-Work%20In%20Progress-yellow)
![Language](https://img.shields.io/badge/Language-Python-3776AB)
![Framework](https://img.shields.io/badge/Framework-Hugging%20Face%20Diffusers-FFD21E)
![Models](https://img.shields.io/badge/Models-Stable%20Diffusion%20x4%20%7C%20LDM-orange)

## Overview
**Stable Geo Upscaler** is a computer vision project designed to enhance low-resolution geospatial and satellite imagery. Traditional interpolation methods often blur details in complex terrain; this project leverages state-of-the-art **Generative AI** models from Hugging Face—specifically **Latent Diffusion Models (LDM)** and the **Stable Diffusion x4 Upscaler**—to hallucinate realistic details and improve image fidelity.

The project currently focuses on datasets from **Corpus Christi** and **Arizona**, utilizing a custom tiling and stitching pipeline to handle high-resolution geospatial files.

## Key Features & Pipeline
To process large geospatial maps, we implemented a robust segmentation pipeline:
1.  **Tiling:** Large satellite images are split into **6x6 grids** to fit within the memory constraints of the diffusion models.
2.  **Preprocessing:** Each tile is resized and normalized for the model input.
3.  **Enhancement:**
    * **Latent Diffusion Model (LDM):** Used for initial detail recovery.
    * **Stable Diffusion x4 Upscaler:** Applied to quadruple the resolution while maintaining texture consistency.
4.  **Patching (Stitching):** The enhanced tiles are reassembled into a single cohesive map, ensuring seamless transitions between grid edges.

## Performance Metrics
We evaluate the quality of the upscaled images using distinct perceptual metrics:
* **SSIM (Structural Similarity Index):** Measures the preservation of structural information (edges, terrain features).
* **FSIM (Feature Similarity Index):** Focuses on low-level features critical for human visual perception.
* **LPIPS (Learned Perceptual Image Patch Similarity):** Uses deep features to assess how "natural" the upscaled image looks compared to ground truth.

**Current Status:** The pipeline achieves approximately **90% similarity** scores across test sets, demonstrating high fidelity in reconstructing urban and rural features.

## Project Contents
| File Name | Description |
| :--- | :--- |
| **README.md** | Project documentation, overview, and setup instructions. |
| **benchmark-gio-upscaler-1.ipynb** | **Phase 1: Model Benchmarking.** This notebook tests various upscaling models on standard (non-geospatial) benchmark data to evaluate baseline performance and select the optimal models for the thesis. |
| **benchmark-gio-upscaler-2.ipynb** | **Phase 2: Geospatial Pipeline.** The core research implementation. It contains the sample satellite images (Corpus Christi & Arizona), the 6x6 tiling logic, the Stable Diffusion enhancement pipeline, and the final stitching algorithm. |

## Setup and Execution

### Prerequisites
* Python 3.8+
* GPU with CUDA support (Recommended for Diffusion models)

### Dependencies
```bash
pip install torch diffusers transformers accelerate opencv-python image-similarity-measures lpips
