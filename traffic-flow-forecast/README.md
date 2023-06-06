# Traffic Volume Forecast

## Table of Contents

1.  [About](#about)
2.  [Data](#data)
3.  [Objectives](#objectives)
4.  [Approach](#approach)
5.  [Evaluation and Conclusion](#evaluation-and-conclusion)
6.  [References](#references)

## About
This project implement models based on architecture of a Convolutional Neural Network; a Recursive Neural Network by way of the Long Short-Term Memory (LSTM) Architecture; as well as an Auto-Regressive LSTM to predict traffic volume for a single- and 24-hour time-step. Additionally, a multi-output model was created that predicts temperature and traffic volume simultaneosly.

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
