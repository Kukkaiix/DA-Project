# Road Traffic Incident Prediction System

## Overview

This project implements an end-to-end data engineering and machine learning pipeline for analyzing and predicting road traffic incidents in Thailand. The system integrates large-scale GPS probe data, geographic reference datasets, and supplementary traffic information to extract meaningful traffic patterns and assess incident risk under different conditions.

The project is developed as an academic data engineering and machine learning project for a second-year Computer Engineering course, following industry-style practices in data ingestion, preprocessing, feature engineering, and model development.


## Project Presentation

A complete explanation of the project motivation, data pipeline, feature engineering, modeling approach, and results is available in the project presentation:

Project Presentation (Canva):
https://www.canva.com/design/DAG00wH8rtY/C6yAlVOl8Zhura3iEusSYQ/view

The presentation includes: 
- Problem statement and objectives
- Data source overview
- Data preprocessing and filtering workflow
- Geospatial mapping methodology
- Model design and evaluation
- Key findings and insights

## Objectives
- Process large-scale GPS probe data from real-world traffic sources
- Filter and clean raw vehicle movement data for realistic traffic representation
-	Map GPS coordinates to Thailand administrative areas
-	Engineer traffic, temporal, and weather-related features
-	Train machine learning models to predict traffic incident risk
-	Demonstrate a practical data engineering pipeline suitable for real-world datasets



## Data Sources

This project uses multiple publicly available datasets. All data sources are referenced and used strictly for educational and research purposes.

### 1. GPS Probe Traffic Data (Primary Dataset)

Provider: Longdo Traffic OpenData
Raw Data Access:
https://traffic.longdo.com/opendata/probe-data/

Description:
This dataset contains real-world GPS probe data collected from taxi fleets operating across Thailand. Each record represents a vehicle’s movement at a specific time and location.

Key Fields Include:
-	Vehicle identifier
-	Latitude and longitude
-	Timestamp
-	Speed (km/h)
-	Heading direction
-	Engine status (engine_acc)
-	For-hire light status (for_hire_light)

Data Format:
Compressed archives (.tar.bz2) containing daily CSV files

Minimum Data Requirement:
At least one week of data is sufficient to reproduce the core analysis pipeline.

Official Documentation:
https://traffic.longdo.com/opendata/probe-data/README.TXT



### 2. Traffic Analytics and Supporting Traffic Data

Provider: Longdo Traffic
Access Link:
https://traffic.longdo.com/download

Description:
This source provides aggregated traffic-related datasets and analytics, which can be used to validate traffic congestion patterns or supplement probe-based traffic indicators.

Additional Open Traffic Datasets:
https://traffic.longdo.com/opendata/

These datasets include:
- Traffic event information
- Speed and congestion statistics
- Road and traffic condition metadata



### 3. Thailand Province and Geographic Reference Data

Source:
https://github.com/dataengineercafe/thailand-province-latitude-longitude

Description:
This dataset provides latitude and longitude reference points for Thailand’s administrative regions. It is used to map GPS probe coordinates to provinces and support geospatial aggregation.

Usage in This Project:
- Assigning GPS points to provinces
- Aggregating traffic metrics at the provincial level
- Supporting spatial analysis and regional comparisons



### 4. Road Network Data (Optional / Future Extension)

Provider: Humanitarian OpenStreetMap (HOTOSM)
Access Link:
https://data.humdata.org/dataset/hotosm_tha_roads

Description:
This dataset contains detailed road network geometries for Thailand, including highways, primary roads, and local streets.

Potential Use Cases:
-	Road type classification
-	Intersection density analysis
-	High-risk road segment identification
-	Infrastructure-aware traffic modeling

This dataset is not mandatory for the current implementation but is recommended for future improvements.



## Data Processing Pipeline
1. Download and extract compressed GPS probe archives
2. Clean and standardize raw CSV files
3. Filter data based on vehicle operational status
   - Engine on (`engine_acc = 1`)
   - Vehicle in service (`for_hire_light = 0`)
4. Apply temporal filtering (weekends and selected months)
5. Map GPS coordinates to provinces using geographic reference data
6. Aggregate traffic statistics by date and province
7. Prepare final datasets for machine learning


## Machine Learning Approach

- **Task Type**
  - Binary classification (incident occurrence)
  - Regression (incident count estimation)

- **Models Used**
  - XGBoost Classifier
  - XGBoost Regressor

- **Features**
  - Traffic congestion indicators
  - Average vehicle speed
  - Temporal variables (month, day of week)
  - Weather-related indicators
  - Province-level encodings

- **Evaluation Metrics**
  - Accuracy, Precision, Recall, F1-score
  - AUC-ROC
  - MAE, RMSE, R² (for regression)



## Intended Use

This project is intended for:
-	Academic coursework and learning
-	Demonstrating real-world data engineering workflows
-	Exploring traffic data analytics and predictive modeling

It is not designed for production deployment, but follows professional design patterns used in industry.



## Acknowledgments
-	Longdo Traffic OpenData for GPS probe and traffic datasets
- Humanitarian OpenStreetMap contributors
- Open-source Python community



## License

This project is developed for educational and research purposes only.
Please review the individual data source licenses before reuse or redistribution.
