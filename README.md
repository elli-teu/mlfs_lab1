# mlfs-lab 1
Air quality prediction lab description

## Lab description
In this lab we have created a system that based on publicly available air quality and weather data predicts future air quality levels for Erstagatan in Stockholm.

Air quality data is collected from aqicn.org and weather data from open-meteo.com, with Hopsworks used for feature storage.

The code is divided into four different jupyter notebooks (available in notebooks/ch03/). A description of their respective funcionalities follows below:

## 1_air_quality_feature_backfill.ipynb
This notebook downloads historical air quality data and weather data, creates Hopsworks feature groups and data validation rules and then uploads this data.
The notebook is expected to run once when the system is put into use, and possibly later to recover from an outage or similar event that would result in missing data.

## 2_air_quality_feature_pipeline.ipynb
This notebook downloads the last day's air quality information as well as a weather forecast for the next week and uploads these into the Hopsworks feature store.
It is expected to run daily to keep the feature store up to date.

## 3_air_quality_training_pipeline.ipynb
This notebook trains a XGBoost regression model for predicting future air quality. It uses the last three days of air quality as well as meterological data as training features. This model is then uploaded into the feature store.
This notebook can be run on demand. The model will take all the historical data into account the first time, so subsequent training is only meaningful once a significant amount of data has been added.

## 4_air_quality_batch_inference.ipynb
This notebook uses the recent data uploaded by the second notebook and the model uploaded in the third to generate predictions for one week of future air quality levels and upload these back to Hopsworks for display in the dashboard.
This notebook is also expected to be run daily after the latest daily data has been uploaded by the second notebook.

## Dashboard
The dashboard is available at [https://elli-teu.github.io/mlfs_lab1/air-quality/]([url](https://elli-teu.github.io/mlfs_lab1/air-quality/)) and shows both one week's worth of future predictions as well as a hindcast useful for evaluating the model's dependability.
