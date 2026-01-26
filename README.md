# Assignment 2 - Generative vs. Discriminative Models

**Course:** DS552 - Generative AI  
**Instructor:** Dr. Narahara Chari Dingari  
**Student:** Matthew Zujewski

---

## Overview

This assignment compares **Naive Bayes** (Generative Model) and **Logistic Regression** (Discriminative Model) on two datasets:

1. **Penguins** - Simple binary classification (Adelie vs Gentoo)
2. **Fashion MNIST** - Complex multi-class classification (10 clothing types)

---

## Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Run Jupyter
jupyter notebook

# Open and run: generative_vs_discriminative_models.ipynb
```

---

## Files

- `generative_vs_discriminative_models.ipynb` - Main notebook
- `penguins_size.csv` - Penguins data
- `requirements.txt` - Python packages
- `README.md` - This file

---

## Results

### Penguins Dataset
| Model | Train Accuracy | Test Accuracy |
|-------|----------------|---------------|
| Naive Bayes | 100% | 100% |
| Logistic Regression | 100% | 100% |

**Finding:** Both models perform perfectly on simple, well-separated data.

### Fashion MNIST Dataset
| Model | Train Accuracy | Test Accuracy |
|-------|----------------|---------------|
| Naive Bayes | 57.5% | 57.0% |
| Logistic Regression | 92.6% | 83.4% |

**Performance Gap:** Logistic Regression outperforms by **26%** on test data.

**Finding:** Discriminative models significantly outperform generative models on complex image data.

---

## Why the Difference?

**Fashion MNIST is challenging because:**
- 784 correlated features (pixels) violate Naive Bayes' independence assumption
- Complex patterns in clothing images
- Similar-looking items (e.g., T-shirt vs Shirt)

**Logistic Regression performs better because:**
- Directly models decision boundaries
- No independence assumptions
- Better handles correlated features

---

## Key Takeaway

**Model choice matters!** 
- Simple data → Both models work
- Complex data → Discriminative models (like Logistic Regression) are superior

---

## Datasets

**Penguins:** 276 samples, 4 features  
**Fashion MNIST:** 70,000 images (10,000 subset used), 784 features

---

## Requirements

- Python 3.8+
- pandas, numpy, scikit-learn
- matplotlib, seaborn
- tensorflow (for Fashion MNIST)
- jupyter

Install all: `pip install -r requirements.txt`
