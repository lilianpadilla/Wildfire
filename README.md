# Wildfire
## Hotspot Identification & Fire-Spread Warning Model

Machine learning analysis of 17M+ U.S. wildfire records (2012–2018) using spatial clustering and decision trees.  
We aim to identify wildfire hotspots and predict fire spread using environmental, vegetation, and weather features from WildfireDB.

Link to Colab Notebook: https://colab.research.google.com/github/lilianpadilla/Wildfire/blob/main/wildfire.ipynb

## Overview

Wildfires are increasing in frequency, intensity, and economic impact. Beyond immediate damage, wildfire smoke contributes to long-term respiratory, cardiovascular, and mental health issues.

This project analyzes over 17 million wildfire observations to:

- Identify wildfire hotspots using spatial clustering  
- Predict wildfire spread using environmental and weather variables  
- Evaluate model performance under class imbalance  

The dataset integrates Fire Radiative Power (FRP), vegetation metrics, elevation, and weather features from **WildfireDB**, combined with satellite detections from NASA’s VIIRS instrument.


## Dataset

- **Source:** WildfireDB (NeurIPS Dataset & Benchmarks Track)  
- **Satellite Data:** VIIRS 375m active fire detections  
- **Years Covered:** 2012–2018  
- **Observations:** 17M+ wildfire cell pairs  
- **Features:** 140+ environmental, geographic, and meteorological variables  

Each row represents:
- A 375m × 375m wildfire cell  
- Fire Radiative Power (FRP)  
- Neighboring cell data (to model spread)  
- Vegetation, fuel, elevation, and weather statistics  

Dataset Repo: https://wildfire-modeling.github.io/

## Preprocessing

- Removed collection metadata (polygon IDs, acquisition time, shape)  
- Removed `temperature_avg` due to missing data 
- Imputed missing values using column means  
- Converted neighbor FRP into binary spread label  
- Addressed class imbalance using inverse class weighting  


## Hotspot Detection

**Algorithm:** Weighted K-Means Clustering  
**Features Used:** Latitude, Longitude, Fire Intensity (FRP)

### Results

- Optimal K (by silhouette score): **2 clusters**
- Higher-resolution hotspot analysis: **25 clusters**
- Identified dense wildfire regions corresponding to:
  - Ozark Mountains region  
  - North Dakota grassland region  



## Wildfire Spread Prediction

**Problem:** Binary Classification (Spread vs No Spread)  
**Algorithm:** Decision Tree  

### Class Imbalance

- ~90% of fires did not spread  
- Addressed using inverse class representation weighting  

### Model Performance

| Model | Accuracy | F1 Score |
|-------|----------|----------|
| Unweighted Tree | 92.2% | 0.00 |
| Weighted Tree (Depth = 6) | 72.3% | **0.78** |



## Important Predictive Features

Features frequently used in the decision tree:

- Latitude & Longitude  
- Temperature  
- Canopy height  
- Elevation  
- Vegetation cover  



## Limitations
  
- Coordinate projection system unavailable (limited precise geographic mapping)  
- Model complexity constrained by hardware resources  


## Libraries / Tech Stack

- Pyspark 
- Pandas  
- Numpy  
- Matplotlib  

---

## Contribution

This wildfire spread and detection project was created by Owen Flynn and Lilian Padilla.