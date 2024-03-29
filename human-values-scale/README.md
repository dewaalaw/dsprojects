# Human Values Scale Analysis

## Table of Contents

1.  [About the Human Values Scale](#about-the-human-values-scale)
2.  [Data](#data)
3.  [Objectives](#objectives)
4.  [Approach](#approach)
5.  [Evaluation and Conclusion](#evaluation-and-conclusion)
6.  [References](#references)

## About the Human Values Scale

The basic human value scale is a 21-item scale developed by Shalom H. Schwartz. The scale measures 10 basic human values that classify respondents according to their basic value orientation. The human value model posits a circular structure where adjacent values are more compatible than those further away, and those at opposite ends are likely at conflict (Schwartz, 1994). While all people recognise the 10 values, their hierarchical arrangement differ to the extend where (cultural or socially constructed) opinions or behaviours influence values higher up in the hierarchy.

<img src="https://github.com/dewaalaw/dsprojects/blob/46a14436d020a4bd32db72435c71863df257776c/human-values-scale/images/hvs.png" alt="Fig. 1 — Theoretical model of relations among motivational types of values, higher order value types, and bipolar value dimensions (Schwartz, 1994)" width="563"/>

## Data
The data was obtained from the European Social Survey (ESS) for Sweden, rounds 1 through 8. After removing missing values, 1441 entries remained.

## Objectives

Firstly, the indicators were examined to determine whether the human value scale measure what it was intended to measure (see part 1). Thereafter the data's dimensionality or underlying factors were examined—whether there are sets of variables that are highly intercorrelated. Hence, rather than a Q factor analysis, an R factor analysis was used to determine dimensions (or constructs) that are latent within the data. To that end, the data was summarised rather than reduced, noting that these are the two outcomes provisioned by factor analysis (see part 2). Lastly, the factor analysis was validated by way of a confirmatory factor analysis to answer whether the data explains the posited theoretic model.

## Approach

-   Psychometric Analysis (Part 1)
-   Exploratory Factor Analysis (Part 2)
-   Confirmatory Factor Analysis (Part 3)

## Evaluation and Conclusion

**Psychometric Analysis:** The Test information function plateaus at 5.1, for the range $(0<= \theta<=1)$. Hence the human value scale provides accurate information of respondents' ability within the said range—outside of which precision decreases.

<img src="https://github.com/dewaalaw/dsprojects/blob/c018022949591f72742f6bbdc859138074dc7bac/human-values-scale/images/TIF.png" alt="Test Information Function for the Human Values Scale" width="643"/>

**Exploratory Factor Analysis:** The analysis obtains an optimal structure revealing four latent factors.

**Confirmatory Factor Analysis:** The fit metrics suggest inadequate model fit.

## References

European Social Survey Cumulative File, ESS 1-8 (2018). Data file edition 1.0 NSD - Norweigian Centre for Research Data, Norway - Data Archive and distributor of ESS data for ESS REIC.

Schwartz, S. H., & Bilsky, W. (1987). Toward a Universal Psychological Structure of Human Values. Journal of Personality and Social Psychology, 53(3).
