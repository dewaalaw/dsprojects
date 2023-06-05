# Traffic Volume Forecast

## Table of Contents

1.  [About](#about)
2.  [Data](#data)
3.  [Objectives](#objectives)
4.  [Approach](#approach)
5.  [Evaluation and Conclusion](#evaluation-and-conclusion)
6.  [References](#references)

## About
Implementation of models based on the architecture of a Convolutional Neural Network; a Recursive Neural Network by way of the Long Short-Term Memory (LSTM) Architecture; as well as an Auto-Regressive LSTM to predict traffic volume for a single- and 24 hour time-step. Additionally, a multi-output model that predicts temperature and traffic volume is created.

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

## Evaluation and Conclusion
A better performing model does not imply a better neural-net architecture. Rather, it depends on the problem to be solved. Three predictive problems were solved, namely the prediction of a one hour timestep, a 24-hour timestep, and a multi-ouput predction of one hour timestep. The results are displayed for each of these scenarious, respectively.

### Single-Step  

### Multi-Step
 
### Multi-Output — i.e. temperature and traffic volume

## References
