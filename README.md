Maritime IR-Visible Image Fusion (v4/v5 Pipeline)

This repository contains an implementation and mathematical refinement of the image fusion algorithm proposed in the paper:
> **"Infrared and visible image fusion for shipborne electro-optical pod in maritime environment"**  
> Liu, Dong, Xu — *Infrared Physics & Technology 128 (2023) 104526*.

Since the authors did not publicly release their source code, the entire pipeline (Eq. 1–22) was reconstructed and mathematically debugged from the paper text.

## 🛠️ Key Pipeline Steps

1. **IR Background Reconstruction (Eq. 1–7):** Models the smooth sea-sky background using a sigmoid profile based on vertical luminance projection.
2. **IR Target Extraction (Eq. 8–12):** Separates high-frequency target components from the low-resolution background and suppresses sea clutter via a center-weighted convolution kernel.
3. **IR Degraded Image Synthesis (Eq. 13):** Combines the smooth background and target map.
4. **Visible Color Feature Extraction (Eq. 14–17):** Extracts a single-channel brightness essence (`ℜ`) and color residuals (`o_R, o_G, o_B`) using a covariance matrix and eigenvalue decomposition. 
   * *Fix implemented (v5):* Applied L1-normalization on the projection vector (`φ`) to prevent overflow and maintain physical scale consistency.
5. **Intensity Map & Initial Color Image (Eq. 18–19):** Merges the spatial structures of the infrared degraded image with color components.
6. **YUV Color Enhancement (Eq. 20–22):** Transfers the luminosity structure from the fused image while adapting color saturation statistics from the original visible image.

## 🚀 Requirements & Usage
* Python 3.x, NumPy, OpenCV, Matplotlib, Google Colab
* Run the Jupyter Notebook `maritime_fusion_v4.ipynb` end-to-end after providing paired `ir.jpg` and `vis.jpg` inputs.
