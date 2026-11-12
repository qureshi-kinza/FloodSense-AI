# FloodSense-AI

### An Explainable Geospatial Machine Learning Framework for Satellite-Based Flood Mapping

**Study Area:** Nowshera District, Khyber Pakhtunkhwa, Pakistan  
**Event:** August 2025  
**Methods:** Sentinel-1 SAR, XGBoost, Spatial Validation, SHAP Explainability

---

## Project Overview

FloodSense-AI is a geospatial machine learning project that combines satellite radar observations, terrain information, vegetation indicators, and explainable AI to investigate flood-related surface changes.

The project focuses on Nowshera District, Pakistan, during the August 2025 flood event. It integrates Sentinel-1 Synthetic Aperture Radar (SAR) change detection with an XGBoost classification model and SHAP-based feature interpretation.

The workflow is designed to support transparent, reproducible geospatial analysis. Model predictions are interpreted as agreement with satellite-derived reference labels, not as independently verified flood observations.

## Objectives

- Identify potential flood-related surface changes using multi-temporal Sentinel-1 SAR imagery.
- Compare ascending and descending satellite observations.
- Compare satellite-derived candidate areas with an independent UNOSAT satellite reference.
- Develop an XGBoost classification model using geospatial predictors.
- Apply spatially grouped train/test splitting to reduce spatial leakage.
- Interpret model behaviour using SHAP explainability.

## Methodology

### 1. Study Area and Satellite Data
Nowshera District was selected as the study area. Sentinel-1 SAR imagery from August 2025 was processed using Google Earth Engine.

### 2. SAR Change Detection
Pre-event and event-period VV backscatter observations were compared for ascending and descending orbit acquisitions. Backscatter differences were used to identify potential flood-related changes.

### 3. Reference Comparison
The Sentinel-1 candidate output was compared with a UNOSAT Sentinel-2 flood reference dated 20 August 2025. The reference metadata indicates that it had not yet been field validated; therefore, it is treated as a satellite-derived reference rather than ground truth.

### 4. Machine Learning
An XGBoost classifier was trained using five predictors:

- Elevation
- Slope
- NDVI
- Ascending-orbit backscatter change
- Descending-orbit backscatter change

A spatial group-based train/test split was used to reduce the risk of nearby samples appearing in both training and testing datasets.

### 5. Explainable AI
SHAP (SHapley Additive exPlanations) was used to examine the contribution of input features to model predictions.

## Key Results

### XGBoost Model Evaluation

| Metric | Result |
|---|---:|
| Accuracy | 0.908 |
| Precision (class 1) | 0.90 |
| Recall (class 1) | 0.97 |
| F1-score (class 1) | 0.94 |
| ROC-AUC | 0.928 |

**Important interpretation:** These metrics measure model agreement with the UNOSAT-derived reference labels on the spatial test sample. They should not be interpreted as independently verified flood-detection accuracy.

### Sentinel-1 and UNOSAT Comparison

| Measure | Area |
|---|---:|
| Sentinel-1 candidate area | 13.476 km² |
| UNOSAT reference area | 13.557 km² |
| Spatial overlap | 3.792 km² |
| Spatial union | 23.241 km² |
| Intersection over Union (IoU) | 0.163 |

The IoU indicates a limited spatial overlap between the candidate and reference extents. This highlights the importance of interpreting SAR-derived flood candidates cautiously and considering differences in sensor characteristics, acquisition dates, and mapping methods.

## Project Outputs

The repository is intended to include:

- Study-area location map
- Sentinel-1 flood-related change-detection map
- Sentinel-1 and UNOSAT comparison map
- XGBoost probability and classified maps
- SHAP explainability visualisation
- Processed GeoTIFF outputs
- Model evaluation statistics and CSV files
- Google Colab analysis notebook

## Technologies and Tools

- Python
- Google Earth Engine
- Google Colab
- Sentinel-1 SAR
- GeoPandas
- Rasterio
- NumPy and Pandas
- Scikit-learn
- XGBoost
- SHAP
- Matplotlib
- Geemap
- QGIS / ArcGIS for geospatial visualisation

## Limitations

- The UNOSAT reference used in this project was not yet field validated.
- Satellite-derived candidate areas are not equivalent to confirmed flood boundaries.
- SAR backscatter changes can be influenced by vegetation, soil moisture, surface roughness, and acquisition geometry.
- Model performance reflects agreement with the selected reference labels and sampling strategy.
- Further validation with field observations and additional independent reference datasets is needed.

## Reproducibility

The analysis notebook, processed outputs, and supporting statistics will be organised in this repository. Large satellite datasets and intermediate files may be excluded where storage limits or data licensing require it.

## Research Note

This project demonstrates an explainable geospatial machine learning workflow for satellite-based flood analysis. Its emphasis is on integrating remote sensing, spatial validation, machine learning, and transparent interpretation rather than claiming a fully validated operational flood-mapping product.
