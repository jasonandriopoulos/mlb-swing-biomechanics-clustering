# Data-Driven Clustering of MLB Swing Mechanics

**Carnegie Mellon University — Master of Applied Data Science**  
**Capstone Project | Major League Baseball**  
[View Technical Spec PDF](./Technical%20Specification.pdf)

## Overview

This project presents a data-driven approach for clustering Major League Baseball hitters using high-frequency 3D motion capture data (Hawk-Eye). We model each batter’s swing as a set of functional trajectories and apply unsupervised learning to uncover biomechanical archetypes. Our objective is to create an interpretable framework that groups hitters based on their movement mechanics and allows coaches or analysts to compare swing styles and identify training opportunities.

## Repository Structure

- **`mlb_swing_clustering.qmd`**: Main Quarto notebook that runs the full analysis pipeline—from preprocessing joint trajectories to final clustering, visualization, and predictive modeling.
- **`Technical Specification.pdf`**: A formal specification document outlining assumptions, dependencies, process flow, pseudo code, and setup instructions.
- **`Figures/`**: Output plots and visualizations (e.g., cluster embeddings, swing profiles, confusion matrices).
- **`data/`**: Expected location for parquet files from Hawk-Eye and the derived condensed datasets.
- **`README.md`**: This file.

## Setup & Dependencies

- R ≥ 4.1.0
- RStudio ≥ 2022.07.1
- Quarto ≥ 1.3
- Required R packages:
  - `tidyverse`, `randomForest`, `fda`, `ggplot2`, `umap`, `mclust`, `gridExtra`, `patchwork`, `arrow`, `reshape2`

Install all dependencies in R using:

```r
install.packages(c("tidyverse", "randomForest", "fda", "ggplot2", "umap", "mclust", "gridExtra", "patchwork", "arrow", "reshape2"))
```

## How It Works

### Data Preprocessing
- Joint trajectories are extracted and reduced to the most informative axis via PCA.
- Each trajectory is smoothed using B-splines and converted into a functional representation.

### Feature Extraction
- Functional Principal Component Analysis (FPCA) reduces the functional curves to scores.
- Summary statistics are computed across swings to create batter-level profiles.

### Clustering Pipeline
- UMAP is used for nonlinear dimensionality reduction.
- Gaussian Mixture Models (GMM) are applied for probabilistic clustering.
- Consensus clustering ensures robustness across multiple runs.

### Interpretation & Modeling
- Random Forests are used to profile clusters and predict group assignments for new data.
- Parallel coordinate plots visualize cluster-specific biomechanical trends.
- Classification accuracy is evaluated on both representative and full datasets.

## Reproducibility Notes

- Because UMAP is stochastic and may differ across machines even with the same seed, consensus clustering is used to ensure robust groupings.
- Kernel PCA is proposed in the discussion as a future direction to improve reproducibility and interpretability.

## Results

- Four distinct clusters of hitters were identified based on swing mechanics.
- Cluster profiles include rotational hitters, upright contact hitters, power loaders, and compact, timed swingers.
- No significant differences were observed in swing or hit outcomes across clusters, suggesting biomechanics may reflect style rather than performance outcomes alone.

## Usage

To run the full pipeline:

1. Place batter swing data (private data) in the expected `data/` directory.
2. Open `mlb_swing_clustering.qmd` in RStudio.
3. Follow the step-by-step chunk instructions, including setting paths and parameters.
4. Outputs will include cluster labels, diagnostic plots, and classification reports.

## Citation

If you use or refer to this work, please cite:

> Jason Andriopoulos, Andrew Shih, Malcolm Ehlers. *Data-Driven Clustering of MLB Swing Mechanics Using High-Frequency Motion Tracking Data*. Carnegie Mellon University, 2025.
