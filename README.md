# FloodSense-AI

### An Explainable Geospatial Machine Learning Framework for Satellite-Based Flood Mapping

**Study Area:** Nowshera District, Khyber Pakhtunkhwa, Pakistan  
**Flood Event:** August 2025  
**Core Technologies:** Google Earth Engine, Sentinel-1 SAR, Python, XGBoost, SHAP

---

## 1. Project Overview

FloodSense-AI is an explainable geospatial machine learning project designed to investigate flood-related surface changes using satellite remote sensing and machine learning.

The project focuses on the August 2025 flood event in Nowshera District, Pakistan. It combines multi-temporal Sentinel-1 Synthetic Aperture Radar (SAR) observations, terrain characteristics, vegetation information, and an XGBoost classification model.

SHAP (SHapley Additive exPlanations) is used to interpret the contribution of individual predictor variables to model predictions.

The workflow integrates remote sensing, GIS, spatial validation, machine learning, and explainable AI in a reproducible analytical framework.

## 2. Project Objectives

- Identify potential flood-related surface changes using multi-temporal Sentinel-1 SAR imagery.
- Compare ascending and descending satellite observations.
- Evaluate spatial agreement between Sentinel-1-derived candidate areas and a UNOSAT satellite reference.
- Develop an XGBoost classification model using geospatial predictors.
- Apply spatially grouped training and testing to reduce spatial data leakage.
- Interpret model behaviour using SHAP explainability.

## 3. Study Area

The study focuses on Nowshera District in Khyber Pakhtunkhwa, Pakistan, an area affected by seasonal flooding and river-related flood hazards.

![Study Area Map](maps/FloodSense_Study_Area_Map.png)

## 4. Methodology

### 4.1 Sentinel-1 SAR Change Detection

Sentinel-1 Ground Range Detected (GRD) imagery was processed using Google Earth Engine.

Pre-event and event-period VV backscatter observations were compared using:

`VV Change = Post-event VV − Pre-event VV`

Negative backscatter changes were investigated as potential indicators of flood-related surface changes.

The main orbit comparisons included:

- Ascending orbit 173: 8 August and 20 August 2025.
- Descending orbit 5: 9 August and 21 August 2025.

An additional descending-orbit observation was used as supplementary analysis.

### 4.2 Multi-Orbit Agreement

Ascending and descending observations were compared to identify areas where both satellite viewing geometries indicated potential flood-related changes.

The resulting categories represent agreement between radar observations, not independently confirmed flood observations.

### 4.3 UNOSAT Reference Comparison

The Sentinel-1 candidate extent was compared with a UNOSAT Sentinel-2 flood reference dated 20 August 2025.

The reference metadata indicated that the flood extent had not yet been field validated. Therefore, it is treated as a satellite-derived reference dataset rather than definitive ground truth.

### 4.4 Geospatial Predictors

Five predictors were used in the XGBoost classification workflow:

| Predictor | Description |
|---|---|
| Elevation | Terrain elevation |
| Slope | Terrain slope in degrees |
| NDVI | Normalized Difference Vegetation Index |
| Ascending VV Change | Sentinel-1 ascending-orbit backscatter change |
| Descending VV Change | Sentinel-1 descending-orbit backscatter change |

### 4.5 XGBoost Classification

An XGBoost classifier was developed using the geospatial predictor variables and reference-derived class labels.

A spatial group-based train/test split was applied to reduce the risk of spatial leakage between training and testing samples.

The model's output represents its prediction of the reference-derived class. Its probability values should not be interpreted as independently calibrated probabilities of actual flooding.

### 4.6 SHAP Explainability

SHAP was applied to investigate how the five predictor variables contributed to the model's predictions.

This provides insight into model behaviour and feature importance rather than establishing causal relationships between environmental variables and flooding.

## 5. Key Results

### XGBoost Model Evaluation

| Evaluation Metric | Result |
|---|---:|
| Accuracy | 0.908 |
| Precision (Class 1) | 0.90 |
| Recall (Class 1) | 0.97 |
| F1-score (Class 1) | 0.94 |
| ROC-AUC | 0.928 |

**Interpretation:** These metrics represent agreement between the model predictions and UNOSAT-derived reference labels on the spatial test sample. They should not be interpreted as independently verified flood-detection accuracy.

### Sentinel-1 and UNOSAT Comparison

The spatial comparison evaluates the relationship between the Sentinel-1 candidate extent and the UNOSAT reference extent.

The comparison statistics, including area measurements and Intersection over Union (IoU), are provided in the results folder.

The spatial agreement should be interpreted cautiously because of differences in satellite sensors, acquisition dates, observation geometry, and mapping methods.

## 6. Project Outputs

### Maps and Visualizations

**Study Area**

![Study Area](maps/FloodSense_Study_Area_Map.png)

**Sentinel-1 Candidate Flood Extent**

![Sentinel-1 Candidate Map](maps/FloodSense_Sentinel1_Candidate_Map.png)

**Sentinel-1 and UNOSAT Comparison**

![UNOSAT Comparison Map](maps/FloodSense_UNOSAT_Comparison_Map.png)

**XGBoost Classified Map**

![XGBoost Classified Map](maps/FloodSense_XGBoost_Classified_Map.png)

**XGBoost Prediction Probability Map**

![XGBoost Probability Map](maps/FloodSense_XGBoost_Probability_Map.png)

**SHAP Explainability**

![SHAP Explainability](maps/FloodSense_SHAP_Explainability.png)

PDF versions of the maps are also included in the maps folder.

### Statistical Outputs

The results folder contains:

- XGBoost classification report.
- Confusion matrix.
- Sentinel-1 area statistics.
- UNOSAT comparison statistics.
- SHAP feature importance values.

## 7. Repository Structure

```text
FloodSense-AI/
│
├── notebooks/
│   └── FloodSense_AI.ipynb
│
├── maps/
│   ├── FloodSense_Study_Area_Map.png
│   ├── FloodSense_Study_Area_Map.pdf
│   ├── FloodSense_Sentinel1_Candidate_Map.png
│   ├── FloodSense_Sentinel1_Candidate_Map.pdf
│   ├── FloodSense_UNOSAT_Comparison_Map.pdf
│   ├── FloodSense_XGBoost_Classified_Map.png
│   ├── FloodSense_XGBoost_Classified_Map.pdf
│   ├── FloodSense_XGBoost_Probability_Map.png
│   ├── FloodSense_XGBoost_Probability_Map.pdf
│   ├── FloodSense_SHAP_Explainability.png
│   └── FloodSense_SHAP_Explainability.pdf
│
├── results/
│   ├── FloodSense_Classification_Report.csv
│   ├── FloodSense_Confusion_Matrix.csv
│   ├── FloodSense_UNOSAT_Comparison_Statistics.csv
│   ├── FloodSense_Sentinel1_Area_Statistics.csv
│   └── FloodSense_SHAP_Feature_Importance.csv
│
├── README.md
└── requirements.txt
```

## 8. Technologies and Tools

- Python
- Google Colab
- Google Earth Engine
- Sentinel-1 SAR
- GeoPandas
- Rasterio
- NumPy
- Pandas
- Scikit-learn
- XGBoost
- SHAP
- Matplotlib
- Geemap
- PyProj

## 9. Reproducibility

The main analytical workflow is provided in the Jupyter notebook:

`notebooks/FloodSense_AI.ipynb`

To reproduce the workflow:

1. Open the notebook in Google Colab.
2. Install the dependencies listed in `requirements.txt`.
3. Authenticate your Google account and Google Earth Engine access.
4. Configure your own Google Earth Engine project ID.
5. Provide the required UNOSAT reference data in your Google Drive project folder.
6. Run the notebook cells sequentially.

Large satellite datasets, intermediate rasters, and the XGBoost probability GeoTIFF are not included in this GitHub repository. Users must provide the required input data and generate these outputs by running the workflow.

## 10. Limitations

- The UNOSAT reference dataset used in this analysis was not yet field validated.
- Sentinel-1 backscatter changes are not exclusively caused by flooding; vegetation, soil moisture, surface roughness, and acquisition geometry can also influence radar responses.
- Satellite-derived candidate flood areas are not equivalent to confirmed flood boundaries.
- Model performance reflects agreement with the selected reference labels and sampling strategy.
- Balanced training samples may affect the interpretation and calibration of predicted probabilities.
- Additional field observations and independent reference datasets are required for stronger validation.

## 11. Research Significance

FloodSense-AI demonstrates an integrated geospatial workflow combining multi-orbit SAR change detection, terrain-based predictors, spatially grouped machine learning validation, and explainable AI.

Its emphasis is on transparent analytical methods and interpretable model behaviour for satellite-based flood analysis, rather than claiming a fully validated operational flood-warning system.

---

**Project Repository:** [FloodSense-AI on GitHub](https://github.com/qureshi-kinza/FloodSense-AI)

**Author:** Qureshi Kinza
