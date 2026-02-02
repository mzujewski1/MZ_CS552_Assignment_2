# Assignment 3: Variational Autoencoders - README

**Student:** Matt Zujewski  
**Course:** DS552 - Generative AI  
**Submission Date:** February 1, 2026

---

## Assignment Overview

This notebook implements and analyzes Variational Autoencoders (VAEs) across three main tasks:
1. Convolutional VAE on CIFAR-10 with fully connected baseline comparison
2. Latent space interpolation analysis
3. VAE training on CelebA face dataset

---

## File Information

**Primary Submission File:** `MZ_VAE_Assignment.ipynb`

**Contents:**
- Theory questions (4/4 answered)
- All three coding tasks complete
- 27 executed code cells
- 14 embedded visualizations
- Comprehensive analysis with real training results

**File Size:** ~8-10 MB (with embedded images)  
**Format:** Jupyter Notebook (.ipynb)

---


total

### Model Architectures

**Convolutional VAE (CIFAR-10):**
- Input: 32×32×3
- Encoder: 4 conv layers (stride-2 downsampling)
- Latent dim: 128
- Decoder: 4 transposed conv layers
- Parameters: 6,304,131

**Fully Connected VAE (Baseline):**
- Input: 3072 flattened pixels
- Encoder: 3 dense layers
- Latent dim: 128
- Decoder: 3 dense layers
- Parameters: 3,511,040

**CelebA VAE:**
- Input: 64×64×3
- Encoder: 4 conv layers
- Latent dim: 256 (larger for facial variation)
- Decoder: 4 transposed conv layers
- Parameters: ~25M

### Training Configuration
- **Optimizer:** Adam (lr=1e-3)
- **Loss:** BCE reconstruction + KL divergence (β=1.0)
- **Batch Size:** 128 (CIFAR-10), 64 (CelebA)
- **Epochs:** 10 per model

---

## Key Findings Summary

### Architecture Comparison
**Why Convolutional Beats Fully Connected:**
- Conv layers exploit spatial locality through local receptive fields
- FC treats pixel (0,0) and pixel (31,31) as equally distant
- Conv has translation invariance (same feature detected anywhere)
- Result: Conv loss (1824) < FC loss (1867)

### Interpolation Analysis
- Smooth transitions for coarse features (color, shape)
- Fine details (edges, textures) wash out mid-transition
- Quantitative smoothness: 0.000615 avg frame difference
- Quality varies by class pair (similar objects interpolate better)

### CelebA Observations
- Larger latent space (256) needed for facial variation
- High-variance dimensions encode multiple attributes (not disentangled)
- Sampling near center (low σ) → average faces
- Sampling at extremes (high σ) → distorted proportions
- Missing: fine details like individual hairs, specific expressions

---

## Limitations Acknowledged

### Model Performance
- Generated images are blurry (inherent to VAE objective)
- BCE loss optimizes reconstruction likelihood, not perceptual quality
- 10 epochs sufficient for concept demonstration, not publication-quality
- No attribute control without post-hoc manipulation


### Architecture Limitations
- Interpolation blurs fine details in middle frames
- Sampling outside training distribution (σ > 2) produces artifacts
- No clean disentanglement in latent dimensions
- VAEs not current SOTA (GANs/diffusion models sharper)

---


All visualizations embedded in notebook with clear labels.

---

## How to Run (If Needed)

### Prerequisites
```bash
pip install torch torchvision matplotlib numpy tqdm
```

### Execution
1. Open `MZ_VAE_Assignment.ipynb` in Jupyter
2. All cells already executed with outputs
3. To rerun: Kernel → Restart & Run All
4. Expected runtime: ~35-40 minutes on M2 Max

### For Faster Testing
Change epoch counts:
- Line ~459: `num_epochs = 10` (CIFAR-10 Conv)
- Line ~713: `for epoch in range(10)` (CIFAR-10 FC)
- Line ~1424: `celeba_epochs = 10` (CelebA)

Reduce to 5 epochs each for quick verification (~15 minutes total).

---

## Results Summary

### Quantitative Metrics
| Model | Dataset | Epochs | Loss | KL | Runtime |
|-------|---------|--------|------|-----|---------|
| Conv VAE | CIFAR-10 | 10 | 1824 | 40 | ~10 min |
| FC VAE | CIFAR-10 | 10 | 1867 | 18 | ~10 min |
| Conv VAE | CelebA | 10 | 6290 | 121 | ~15 min |

**Interpolation Smoothness:** 0.000615 avg frame difference  
**Total Runtime:** ~35 minutes  
**Visualizations:** 14 plots embedded

### Qualitative Observations
- Conv VAE generates spatially coherent objects
- FC VAE produces scattered, unstructured pixels
- Interpolation smooth for coarse features, blurs fine details
- CelebA model captures pose/lighting but not fine textures
- All models exhibit expected VAE blurriness

---

## Potential Improvements

If continuing this work:
1. **β-VAE** - Higher β for better disentanglement (trades off reconstruction)
2. **Perceptual Loss** - LPIPS instead of BCE (more expensive but sharper)
3. **More Epochs** - 30-50 epochs for production quality
4. **Hierarchical VAE** - Multi-scale generation
5. **VQ-VAE** - Discrete latents for sharper images
6. **VAE-GAN Hybrid** - Combine VAE structure with adversarial training

Current implementation prioritizes clarity and concept demonstration over SOTA performance.
w

---

## Contact Information

**Student:** Matt Zujewski  
**Course:** DS552 - Generative AI  
**Institution:** Worcester Polytechnic Institute (WPI)

---

## Acknowledgments

- CIFAR-10 dataset: Krizhevsky, 2009
- CelebA dataset: Liu et al., 2015
- PyTorch framework: Paszke et al., 2019
- VAE paper: Kingma & Welling, 2013

All code is original implementation based on course materials and understanding of published VAE architectures.

---

