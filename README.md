# 🚲 Spatial Dependency Patterns in Weather-Enhanced Bike-Share Demand Forecasting
## A Washington DC Replication Study — Findings Journal (Revised Submission)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/YOUR_REPO/blob/main/DC_Bikeshare_Spatial_Dependency_REVISED.ipynb)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue)](https://python.org)
[![TensorFlow 2.x](https://img.shields.io/badge/TensorFlow-2.x-orange)](https://tensorflow.org)
[![Findings Journal](https://img.shields.io/badge/Submitted-Findings%20Journal-purple)](https://findingspress.org)

> **Paper:** Kabir & Kabir Zisha (2026), *Findings Journal* (Revised submission)  
> **Replicates:** Miao et al. (2025), SIGSPATIAL — extended to Washington DC with weather inputs  
> **Data:** 251,633 Capital Bikeshare trips, January 2026

---

## What this repository contains

| File | Description |
|------|-------------|
| `DC_Bikeshare_Spatial_Dependency_REVISED.ipynb` | **Main Colab notebook — run this to reproduce all results** |
| `README.md` | This file |
| `requirements.txt` | Python dependencies |
| `download_data.py` | Auto-downloads the January 2026 trip data |
| `references_bikeshare.bib` | BibTeX references |
| `outputs/` | Pre-computed outputs (Φ matrices, CSVs, figures) |

## Key Findings

| Metric | Member | Casual User |
|--------|--------|-------------|
| R² | **0.816** | 0.427 |
| MAE (trips/zone/30 min) | 0.292 | 0.112 |
| Proximity–influence correlation | −0.164 | −0.131 |
| Anisotropy index | **2.749** | 2.550 |
| Mean Φ ratio (member/casual) | **5.52×** | — |

**Core result:** Spatial influence in DC's bike-share system does not follow geographic proximity — replicating Miao et al. (2025) in a second North American city with weather augmentation.

## Run in Colab (recommended)

1. Click the **Open in Colab** badge above
2. Upload `202601-capitalbikeshare-tripdata.zip` to `/content/` (download from https://capitalbikeshare.com/system-data)
3. **Runtime → Run all** (GPU recommended: Runtime → Change runtime type → T4 GPU)
4. Download `/content/outputs/` when complete (~45–60 min on GPU)

## New Analysis Cells (Reviewer-Requested)

| Cell | Analysis | Produces |
|------|----------|---------|
| 12b | Weather ablation | Supplemental Table S4, Figure S3 |
| 12c | Baseline comparison | Supplemental Table S3 |
| 12d | Trip-duration sensitivity (4h/6h/12h) | Supplemental Table S1 |
| 12e | Grid-resolution sensitivity (6×6/10×10) | Supplemental Table S2 |
| 16b | Temperature vs. ridership | Supplemental Figure S4 |

## Run Locally

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
pip install -r requirements.txt
python download_data.py          # downloads January 2026 trip data
jupyter notebook DC_Bikeshare_Spatial_Dependency_REVISED.ipynb
```

## Requirements

```
tensorflow>=2.12
pandas>=2.0
numpy>=1.24
scikit-learn>=1.3
matplotlib>=3.7
seaborn>=0.12
folium>=0.14
requests>=2.31
openpyxl>=3.1
```

## Citation

If you use this code, please cite:

```bibtex
@article{kabir2026spatial,
  title   = {Spatial Dependency Patterns in Weather-Enhanced Bike-Share
             Demand Forecasting: A Washington DC Replication Study},
  author  = {Kabir, S M Redwan and {Kabir Zisha}, Farhana},
  journal = {Findings},
  year    = {2026},
  doi     = {[TO BE ASSIGNED]}
}

```

## Data Sources

| Source | URL |
|--------|-----|
| Capital Bikeshare trip data | https://capitalbikeshare.com/system-data |
| Open-Meteo Historical Weather API | https://open-meteo.com/en/docs/historical-weather-api |

---
<sub>Washington DC · 2026 · MIT License</sub>
