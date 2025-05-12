# Photogrammetry and Gaussian Splatting Assignment Report


**Author**: Harsh Padmalwar  
**ASU ID**: 1234549994

---

## Abstract

This assignment explores a hybrid 3D reconstruction pipeline that merges classical photogrammetry with data-driven rendering using Gaussian Splatting. In the first part, a 3D mesh was reconstructed from 10 images using Agisoft Metashape, and the visual similarity between actual photos and splatting-generated renderings was assessed using PSNR and SSIM metrics. In the second part, new viewpoints were synthesized via Gaussian Splatting and integrated into the dataset to observe their impact on the quality of the final photogrammetric model. The results confirm that these learned views can improve surface coverage and address gaps in geometry, making them valuable additions to traditional workflows.

---

## Objective

The goal of this assignment is to evaluate how neural rendering methods—specifically Gaussian Splatting—can complement traditional photogrammetry by enhancing input data with synthesized views. The assignment is divided into two phases:

- **Part A** focuses on using a limited image set to generate a textured mesh and evaluating how well Gaussian Splatting can replicate the original views.
- **Part B** investigates the potential benefits of incorporating artificially rendered views into the photogrammetry pipeline to improve the final model.

---

## Dataset

- **Name**: Agisoft_Dataset  
- **Total Images**: 10 PNG files (original)  
- **Resolution**: Approximately 1540 x 856 pixels  
- **Scene Description**: Simulated lunar terrain  

---

## Tools Used

- Agisoft Metashape Professional (Demo Version)  
- Gaussian Splatting (Inria GitHub repo, 2023)  
- Python 3.10, NumPy, OpenCV, scikit-image  
- GPU: NVIDIA RTX 3050
- OS: Ubuntu 22.04

---

## Part A: Photogrammetry and Neural Rendering Comparison

### Photogrammetric Reconstruction

The initial reconstruction was performed by importing 10 lunar terrain images into Agisoft Metashape. After aligning the cameras with high accuracy, a dense point cloud was generated with confidence estimation enabled. This dense cloud was subsequently converted into a textured mesh using default settings.

![Screenshot from 2025-05-12 10-17-49](https://github.com/user-attachments/assets/eb46cf77-73d2-4a42-ad3b-b20c1b41f8d8)

### Gaussian Splatting

A Gaussian Splatting model was trained using the same 10 images. The model reproduced renderings from the original camera poses, generating neural approximations of the input photos.

### Evaluation with PSNR and SSIM

To evaluate how closely the splatted outputs matched the original views, quantitative image similarity metrics were computed. PSNR and SSIM revealed that while the fidelity was limited by sparse data, the outputs were consistent enough to justify further integration.

![Screenshot from 2025-05-12 10-39-42](https://github.com/user-attachments/assets/95c85560-4f40-4bd7-9a9a-f3098b67daef)

---

## Part B: Augmenting with Novel Views

### Novel View Generation

Ten previously uncovered camera poses were calculated to diversify the visual input space. These poses were rendered using the already trained Gaussian Splatting model to synthesize new images from alternate perspectives.

### Combined Dataset and Second Reconstruction

The new images were merged with the existing set to create a 25-image dataset. A second photogrammetric reconstruction was performed using the same process as Part A. The resulting mesh showed improved continuity and reduced geometric gaps.

### Mesh Comparison and Insights

The updated model, even with fewer triangles, showed a more complete reconstruction of the scene. Occluded areas from the original model were now partially resolved, and surface smoothness improved.


### Discussion on Quantitative Comparison

Although most insights were qualitative (based on visual inspection of the mesh), the project proposes future implementation of quantitative mesh metrics like surface deviation, completeness percentage, or point-to-mesh error using tools such as CloudCompare or custom Python scripts.

---

## Conclusion

This assignment demonstrates that neural view synthesis—particularly via Gaussian Splatting—can meaningfully extend the capabilities of photogrammetry. While splatting alone is constrained by the quality and quantity of input images, it proves highly useful as a data augmentation tool. Integrating 10 synthetic images resulted in a significantly better 3D reconstruction with more complete geometry and fewer missing surfaces.

---


- Expand the original dataset with more diverse camera angles to improve splatting model training.
- Apply mesh-based comparison metrics like Hausdorff distance or nearest-neighbor error.
- Experiment with real-time SLAM integration using neural-rendered intermediate views.
- Investigate whether photogrammetry outputs can be used to guide or refine splatting outputs in a feedback loop.
