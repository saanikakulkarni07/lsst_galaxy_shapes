[README.md](https://github.com/user-attachments/files/27188863/README.md)
# Measuring Galaxy Shapes and Colours from Images

Extracting galaxy shapes and photometric redshifts from images using the
LSST Science Pipelines, with data from the Rubin Observatory and the
Hyper Suprime-Cam (HSC) survey.

**Project:** P5 — proposed by Shadab Alam, mentored by Arun Kannawadi (Duke University)

## Background

Gravitational lensing maps the invisible dark matter distribution through
the apparent distortion of background galaxies. This project focuses on
the critical skill of measuring galaxy shapes (ellipticities) and
photometric redshifts from survey images — the foundation of weak lensing
cosmology.

## Project Structure

```
├── notebooks/          # Jupyter notebooks (analysis & exploration)
│   ├── 01_background/  # Theory and literature review
│   ├── 02_pipeline/    # LSST pipeline walkthroughs
│   ├── 03_shapes/      # Shape measurement experiments
│   └── 04_photoz/      # Photometric redshift estimation
├── src/                # Reusable Python modules
├── data/               # Data directory (large files gitignored)
│   ├── raw/
│   └── processed/
├── figures/            # Plots and figures for writeups
├── references/         # Notes on key papers
└── environment.yml     # Conda environment specification
```

## Key References

- Mandelbaum (2018), "Weak Lensing for Precision Cosmology", ARA&A 56, 393 — [arXiv:1710.03235](https://arxiv.org/abs/1710.03235)
- Mandelbaum et al. (2015), "GREAT3 results I", MNRAS 450, 2963 — [arXiv:1412.1825](https://arxiv.org/abs/1412.1825)
- Lupton, Gunn & Szalay (1999), "A Modified Magnitude System", AJ 118, 1406 — [arXiv:astro-ph/9903081](https://arxiv.org/abs/astro-ph/9903081)
- Bosch et al. (2018), "The Hyper Suprime-Cam Software Pipeline", PASJ 70, S5 — [arXiv:1705.06766](https://arxiv.org/abs/1705.06766)

## Setup

### Option 1: Rubin Science Platform (recommended for data access)
Access at [data.lsst.cloud](https://data.lsst.cloud) — pipelines pre-installed with DP0.2/DP1 data.

### Option 2: Docker
```bash
docker pull lsstsqre/centos:7-stack-lsst_distrib-v29_2_1
docker run -it -v $(pwd):/home/lsst/work lsstsqre/centos:7-stack-lsst_distrib-v29_2_1
```

### Option 3: Local install
```bash
conda env create -f environment.yml
conda activate lsst-shapes
```
