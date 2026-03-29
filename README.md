# 🚲 Spatial Dependency Patterns in Weather-Enhanced Bike-Share Demand Forecasting
## A Washington DC Replication Study — Findings Journal (Revised Submission)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/YOUR_REPO/blob/main/DC_Bikeshare_Spatial_Dependency_REVISED.ipynb)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue)](https://python.org)
[![TensorFlow 2.x](https://img.shields.io/badge/TensorFlow-2.x-orange)](https://tensorflow.org)
[![Findings Journal](https://img.shields.io/badge/Submitted-Findings%20Journal-purple)](https://findingspress.org)

> **Paper:** Kabir & Zisha (2026), *Findings Journal* (Revised submission)  
> **Replicates:** Miao et al. (2025), SIGSPATIAL — extended to Washington DC with weather inputs  
> **Data:** 251,633 Capital Bikeshare trips, January 2026

---
## 📌 Overview

This repository contains the full implementation of a **spatially-adapted permutation-based dependency analysis** framework for urban bike-sharing demand, applied to Washington DC Capital Bikeshare trip data from January 2026. It accompanies the paper:

> **"Beyond Proximity: Spatial Dependency in Washington DC Bike-Sharing — Weather-Augmented ConvLSTM Evidence"**  
> *Findings Journal — Transport Research (Submitted 2026)*

The core question: **do spatial dependencies in bike-sharing demand follow geographic proximity, or are they governed by functional urban linkages?** We answer this by training ConvLSTM models for member and casual users separately, augmenting them with real weather data, and computing a 64×64 permutation-based spatial dependency matrix Φ for each user type.

---

## 🎯 Aim & Scope

| | |
|---|---|
| **Study area** | Washington DC, USA |
| **Data source** | [Capital Bikeshare Open Data](https://capitalbikeshare.com/system-data) |
| **Period** | January 2026 (251,633 trips) |
| **Spatial resolution** | 8×8 regular grid (64 cells, ≈1,500 m each) |
| **Temporal resolution** | 30-minute intervals |
| **User types** | Member (205,329 trips) and Casual (46,304 trips) |
| **Weather source** | [Open-Meteo Historical Archive API](https://open-meteo.com/) |

### What this project establishes:
1. Whether spatial influence in bike-sharing conforms to the **geographic proximity assumption**
2. How **member and casual users differ** in their spatial dependency structures
3. Whether **weather augmentation** improves winter demand prediction beyond spatiotemporal models alone
4. A replication and extension of [Miao et al. (2025)](https://doi.org/10.1145/3748636.3763207) from NYC to a structurally distinct city
   
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

## ⚙️ How the Script Works

The pipeline runs in **18 sequential cells** in Google Colab:

```
 DATA               FEATURES              MODEL              ANALYSIS
  │                    │                    │                    │
  ▼                    ▼                    ▼                    ▼
Capital           Weather API          ConvLSTM           Permutation
Bikeshare    ──►  (Open-Meteo)   ──►  (3 layers)    ──►  Dependency
Trip CSV          + Temporal           + Dense             Matrix Φ
                    Features            Branch           (64×64 per
                  (7 inputs)          Separate            user type)
                                    Member/Casual
```
## 🧠 Model Architecture

```
Spatial Input                    External Input
[batch, 4, 8, 8, 2]             [batch, 7]
        │                              │
   ConvLSTM2D (64)                Dense (32, ReLU)
   BatchNorm + Dropout(0.2)       BatchNorm
        │                         Dense (64, ReLU)
   ConvLSTM2D (64)                     │
   BatchNorm + Dropout(0.2)       Reshape (1,1,64)
        │                         UpSampling2D (8×8)
   ConvLSTM2D (64)                     │
   BatchNorm                           │
        └──────────┬────────────────────┘
                   │
              Concatenate
                   │
            Conv2D(2, 1×1, ReLU)
                   │
           Output [batch, 8, 8, 2]
           (pickups + dropoffs)
```

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
