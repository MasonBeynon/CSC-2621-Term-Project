<!---
Designed by:
Chris Botzoc
Grant Fass
Edited by:
John Bukowy
--->

# Summary Information
*This describes the data set that you are going to use and what it was used for. You may choose to list models in here that used the data described in the card. The date is also important due to how data may change over time*

*Dataset cards do not necessarily describe all of the data provided by a sponsor or for the project, but they should describe all data __used__ for the project*

| Field             | Description                        |
| ----------------- | ---------------------------------- |
| Name              | predictive_maintenance_v3  |
| Curation Date     | Synthetic  |
| Sensitivity Level | Not Sensitive  | 
| Summary           | Synthetically generated data for CNC machines meant for predictive maintenance and remaining useful life (RUL) estimation.  |
| Source            | https://www.kaggle.com/datasets/tatheerabbas/industrial-machine-predictive-maintenance?resource=download  |

# Card Authors
*This describes the people that contributed to creating the dataset card.*

| Name | Email |
| ---- | ---- |
| Mason Beynon | beynonm@msoe.edu |
| Andrew Needham | needhama@msoe.edu |
|  |  |

# Data Overview
*General description of the data set. Such as number of features, how large the files are, number of observations etc...*

| Field | Value |
| ---- | ---- |
| Storage Size | 2.17 MB |
| Number of Rows | 24042 |
| Number of Features | 15 |
| Data Format | CSV |

# Numerical Features Summary
*This sections shows the summary statistics for all numerical features in the data set*

| Feature | Count | Mean | Std Dev | Min | 25% | Median | 75% | Max |
| ------- | ----- | ---- | ------- | --- | --- | ------ | --- | --- |
| vibration_rms | 23042 | 1.62 | 1.08 | 0.35 | 0.82 | 1.27 | 2.27 | 10.00 |
| temperature_motor | 23208 | 51.40 | 12.52 | 28.00 | 42.61 | 50.06 | 59.96 | 95.00 |
| current_phase_avg | 23311 | 8.82 | 5.37 | 2.20 | 4.63 | 6.43 | 13.12 | 35.00 |
| pressure_level | 23118 | 59.01 | 38.72 | 10.10 | 22.70 | 46.30 | 94.70 | 206.50 |
| rpm | 23509 | 1144.85 | 912.67 | 124.10 | 489.40 | 856.00 | 1676.00 | 4098.80 |
| hours_since_maintenance | 24042 | 172.63 | 150.72 | 0.00 | 42.87 | 121.61 | 295.58 | 575.63 |
| ambient_temp | 24042 | 12.99 | 2.88 | 8.00 | 10.50 | 13.00 | 15.50 | 18.00 |
| rul_hours | 24042 | 27.81 | 26.39 | 0.50 | 0.50 | 22.57 | 46.41 | 98.34 |
| estimated_repair_cost | 24042 | 608.87 | 1566.79 | 0.00 | 0.00 | 0.00 | 0.00 | 7995.00 |


# Categorical Features Summary
*This sections shows the equivalent summary statistic for all categorical features in the data set*

| Feature | Unique Values | Most Common Value |
| ------- | ------------- | ----------------- |
| machine_id | 20 | 6 |
| machine_type | 4 | Pump |
| operating_mode | 3 | normal |
| failure_within_24h | 2 | 0 |
| failure_type | 5 | none |

Note: failure_within_24h has 14.8% 1 values.

# Field Information
*Document the table that is encoded i.e. the table they are using to build the encoding*

| Feature Name | Data Type | Statistical Type | Description |
| ---- | ---- | ---- | ---- |
| timestamp | datetime | temporal | Date and time of observation. |
| machine_id | int | nominal | Unique identifier for each machine. |
| machine_type | string | nominal | Category of equipment (CNC, Pump, Compressor, Robotic Arm) |
| vibration_rms | float | continuous | Root mean square of the vibration velocity. |
| temperature_motor | float | continuous | Temperature of internal motor in Celcius. |
| current_phase_avg | float | continuous | Average electrical current draw across phases. |
| pressure_level | float | continuous | Fluid or pneumatic pressure within the system. |
| rpm | float | continuous | Revolutions per minute. |
| operating_mode | string | nominal | The current state of the machine (normal, idle, peak) |
| hours_since_maintenance | float | continuous | Time elapsed since the last service intervention. |
| ambient_temp | float | continuous | The surrounding environmental temperature. |
| rul_hours | float | continuous | Target variable: Remaining Useful Life until failure occurs. |
| failure_within_24h | int | binary | ndicator (0 or 1) if a failure occurs in the next 24 hours. |
| failure_type | string | nominal | Categorical label for the specific mode of failure (none, bearing, motor_overheat, hydraulic, electrical) |
| estimated_repair_cost | int | continuous | Estimated cost to fix the machine based on failure type. |

# Example Entry
*It is helpful to track a few observations that you are familiar with. Pick an "average" observations as well as a few that exhibit features or classes that you are interested in. E.g. for a cancer dataset you might choose a sample that has all of the classes that you want to predict or that shows severe progression of the disease.*

| timestamp | machine_id | machine_type | vibration_rms | temperature_motor | current_phase_avg | pressure_level | rpm | operating_mode | hours_since_maintenance | ambient_temp | rul_hours | failure_within_24h | failure_type | estimated_repair_cost |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| 2024-01-01 00:00:00 | 1 | CNC | 0.81 | 49.51 | 5.1 | 23.6 | 860.9 | idle | 273.8 | 13.9 | 61.0 | 0 | none | 0 |
| 2024-01-03 03:19:00 | 1 | CNC | 2.93 | 62.83 | 10.31 | 56.6 | 2868.7 | normal | 325.12 | 10.8 | 23.74 | 1 | hydraulic | 3403

# Exploratory Charts
*Include a scatter plot matrix of all of your numeric features. Show bargraphs for your categorical features. If you know what response you are interested in, you might choose to make a plot of the first two principal components (from PCA or similar feature reduction algorithm) vs your known response or classes*

# Notable Feature Processing
*If you decide to do feature scaling or if you are doing any feature engineering, the process should go here. Remember that the mean and standard deviation of features would be important for any future applications that might use this data.* 

vibration_rms, temperature_motor, current_phase_avg, pressure_level, and rpm all have missing values. Missing values were imputed with medians of that feature grouped by machine id.

Users should exclude failure_within_24h, failure_type, and estimated_repair_cost when training the RUL regression model to prevent data leakage. All 4 of those columns are directly correlated, failure_within_24h just being a boolean of if RUL < 24 and the other 2 being none and 0 if failure_within_24h is 0.

# Notes

*document any additional considerations, concerns, or otherwise here*