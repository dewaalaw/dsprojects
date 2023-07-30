# Traffic Volume Forecast

## Table of Contents

1.  [About](#about)
2.  [Data](#data)
3.  [Objectives](#objectives)
4.  [Approach](#approach)
5.  [File Structure](#file-structure)
6.  [Evaluation and Conclusion](#evaluation-and-conclusion)
7.  [References](#references)

## About
Traffic volume forecasting is the process of predicting the future traffic flow on road networks, typically for a specific time period. It is an essential component of transport planning and management, since it affords stakeholders to make informed decisions about infrastructure development, traffic control strategies, and resource allocation. 

To perform traffic volume forecasting, various data sources and techniques are employed. Historical traffic data, such as traffic counts or travel time records, are commonly used as inputs. Externalities such as weather conditions, special events, and road construction are additionaly taken into account as these also impact traffic patterns. Machine learning algorithms, statistical models, and time series analysis are often applied to analyze the data and generate forecasts. These forecasts enable transportation agencies, city planners, and engineers to optimize road networks, design efficient transportation systems, and implement effective traffic management measures. By anticipating future traffic volumes, stakeholders can work towards alleviating congestion, improving safety, and enhancing overall mobility.

This project implement models based on architecture of a Convolutional Neural Network; a Recursive Neural Network by way of the Long Short-Term Memory (LSTM) Architecture; and an Auto-Regressive LSTM to predict traffic volume for a single- and 24-hour time-step. Additionally, a multi-output model was created that predicts temperature and traffic volume simultaneosly.

## Data
Hourly traffic volume, westboud on the I-94 highway, interconnecting Minneapolis and St.Paul, Minnesota, from 2012 to 2018.

## Objectives
- Predict hourly traffic volume and temperature.
- Develop a rigourous testing protocol to compare predictive capacity of model architecture.

## Approach
- Data wrangling and preprocessing
- Feature engineering
- Code helper functions
- Implement and train deep learning models 
- Analyse results

## File Structure
The `src` folder contains the Python codebooks (cb) numbered 0 to 2. 
- cb_0: Upload data; feature engineering &amp; data exploration; seasonality check; train &amp; test data split; train &amp; test data save.
- cb_1: Implement a linear- and deep-learning model for a single- &amp; multi-step prediction; as well as a multi-output model, showing a single-step prediction of temperature and traffic volume.
- cb_2: Implement the LSTM &amp; CNN architecture

The `images` folder contains model comparison plots — i.e., those seen in the [Evaluation and Conclusion](#evaluation-and-conclusion) section below.

## Evaluation and Conclusion
A better performing model does not imply a better neural-net architecture. Rather, it depends on the problem to be solved. Three predictive problems were solved, namely the prediction of a one hour timestep, a 24-hour timestep, and a multi-ouput prediction of tempearture and traffic volume for a one hour timestep. The results are displayed for each of these scenarious.

### Single-Step 
<img src="https://github.com/dewaalaw/dsprojects/blob/main/traffic-flow-forecast/images/compare_single_step_models.png" alt="Fig. 1 — Single Step Models" width="750"/>

### Multi-Step
<img src="https://github.com/dewaalaw/dsprojects/blob/main/traffic-flow-forecast/images/compare_multi_step_models.png" alt="Fig. 2 — Multi-Step Models" width="750"/>

### Multi-Output — i.e. temperature and traffic volume
<img src="https://github.com/dewaalaw/dsprojects/blob/main/traffic-flow-forecast/images/compare_multi_output_models.png" alt="Fig. 3 — Multi-Output Models" width="750"/>

## References
- Chollet, Francios. 2018. Deep Learning with Python. First. edited by T. Arritola, J. Gaines, A. Dragosavljevic, T. Taylor, and K. Tennant. Shelter Island, NY: Manning Publications Co.
- Lynch, Stephen. 2023. Python for Scientific Computing and Artificial Intelligence. Chapman and Hall/CRC.
- McKinney, Wes. 2022. Python for Data Analysis.
- Müller, Andreas C., and Sarah Guido. 2017. Introduction to Machine Learning with Python: A Guide for Beginners in Data Science. edited by D. Schanafelt. Sebastopol, CA: O’Reilly Media, Inc.
