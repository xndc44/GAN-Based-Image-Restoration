# DeRestify: A Robust Image Restoration and Colorization Framework

## Overview

**DeRestify** is a general-purpose image restoration and colorization model designed to overcome the limitations of domain-specific and narrowly trained restoration systems. Built upon the DeOldify architecture, DeRestify incorporates:
- A synthetic degradation pipeline simulating real-world distortions,
- Curriculum learning with progressive resolution scaling,
- Final-stage GAN fine-tuning for photorealistic output.

This project explores DeRestify’s ability to restore corrupted images across diverse domains such as:
- Medical (X-ray imaging),
- Surveillance (CCTV footage),
- Astronomy (James Webb Telescope data),
- Natural photography (Tiny ImageNet).

---

## Key Contributions

- **Multi-domain Training**: Unified training across medical, forensic, astronomical, and general datasets.
- **Synthetic Distortion Engine**: Realistically simulates distortions like chromatic aberration, motion blur, compression artifacts, and cosmic ray interference.
- **Curriculum-based Resolution Scaling**: Trains progressively at 64×64 → 128×128 resolutions.
- **Post-processing Pipeline**: Ensures luminance consistency using YUV blending.
- **Adversarial Fine-Tuning**: Uses PatchGAN for texture refinement in the final training stage.

---

## Evaluation

DeRestify is evaluated using:
- **SSIM (Structural Similarity Index)**
- **PSNR (Peak Signal-to-Noise Ratio)**
- **LPIPS (Learned Perceptual Image Patch Similarity)**

Although DeOldify scores higher on these traditional metrics, DeRestify demonstrates stronger **generalization** and **cross-domain robustness**, especially on challenging synthetic distortions.

---

## Results Summary

| Model       | SSIM   | PSNR (dB) | LPIPS  |
|-------------|--------|-----------|--------|
| DeOldify    | 0.7400 | 25.1      | 0.2600 |
| DeRestify   | 0.6514 | 17.84     | 0.3394 |

*Note*: DeRestify is trained on a smaller but more diverse dataset and prioritizes robustness over specialization.

---

## Dataset Sources

- **Tiny ImageNet** (Natural images)
- **COVID‑19 Radiography Database** (Medical X-rays)
- **SpaceNet Dataset** (Astronomy)
- **Large-Scale Multi-Camera Detection Dataset** (CCTV footage)

All datasets are preprocessed for compatibility with the ResNet-based encoder and normalized using ImageNet statistics.

---

## Implementation Details

- **Framework**: [FastAI](https://www.fast.ai/) with PyTorch backend  
- **Hardware**: NVIDIA RTX 3060 (12GB VRAM)  
- **Backbone**: Pretrained ResNet + U-Net with Self-Attention  
- **Losses**: Perceptual (VGG), L1 Reconstruction, and PatchGAN Adversarial  
- **Optimizer**: AdamW with 1cycle learning policy

---

## Limitations

- Max training resolution: 128×128 (due to hardware limits)
- Dataset size: ~23,000 images (vs. ImageNet’s 1.2M)
- Fixed distortion parameters during training
- No compound distortion mixing during training

---

## Project PDF

The full thesis can be found in the file: [DeRestify: A Robust Image Restoration and Colorization Framework (PDF)](./Masters_Thesis.pdf)

