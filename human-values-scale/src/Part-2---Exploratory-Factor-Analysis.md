Part 2 - Exploratory Factor Analysis
================

# Factor Analysis—Exploratory Factor Analysis

Next we examine the underlying structure of a set of value-specific
indicators premised on Schwartz’s theory. The data was obtained from the
European Social Survey (ESS) for rounds 1 through 8, Sweden only.

``` r
cor.matrix <- cor(data, method="spearman")
corrplot(cor.matrix)
```

![correlation matrix](https://github.com/dewaalaw/dsprojects/blob/60ddcfe5bd0d2e94fd12f967435c0a52cd65c209/human-values-scale/images/cormat.png)<!-- -->

Several positive correlations of mid to higher range strength stand out:
notably ipshabt (the importance to show abilities and be admired)
correlates ipsuces (the importance to be successful and that people
recognise achievements); as does impdiff (the importance to try new and
different things in life) and ipadvnt (the importance to see adventures
and have an exciting life).

``` r
palette = colorRampPalette(c("green", "white", "red")) (20)
heatmap(x = cor.matrix, col = palette, symm = TRUE)
```

![heatmap of correlation matrix](https://github.com/dewaalaw/dsprojects/blob/9c01bb7b361e33e04d6d3c5fa4c467fab780518c/human-values-scale/images/heatmap.png)<!-- -->

## Correlation Matrix Factorability

### Bartlett’s Test of Sphericity

Check whether the data is suitable for Principle Component Analysis
(PCA), using the Barlett’s Test of Sphericity:
![X^2 = -(n-1-\\frac{2k+5}6)ln\|R\|](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;X%5E2%20%3D%20-%28n-1-%5Cfrac%7B2k%2B5%7D6%29ln%7CR%7C "X^2 = -(n-1-\frac{2k+5}6)ln|R|").
The test checks ‘for redundancy between variables that we can summarise
with lesser factors’ ([REF:
STATOLOGY](https://www.statology.org/bartletts-test-of-sphericity/)).
The null hypothesis tests whether the variables are orthogonal—i.e.,
they’re un-correlated. (Also interpreted as whether the correlation
matrix is an identity matrix). The significance level is set at 0.05,
hence if the
![p](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;p "p")-value
is lower than that threshold, the data is reducible insofar as a PCA can
meaningfully reduce the number of variables to capture the variance with
lesser variables.

``` r
n <- dim(data)[1]
cortest.bartlett(cor.matrix, n)
```

    ## $chisq
    ## [1] 6725.154
    ## 
    ## $p.value
    ## [1] 0
    ## 
    ## $df
    ## [1] 210

We make use of `psych` package’s `cortest.barlett` function and R’s base
`cor` function to calculate the test statistic and correlation matrix.
Since the data is ordinal we set the method of computation to
`spearman`.

The chi-square statistic
![X^2](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;X%5E2 "X^2")
for Barlett’s test is 6725.154, for
![p](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;p "p")
= 0 \< 0.05—thus the test rejects the null hypothesis that the
correlation matrix is an identity matrix. Hence a PCA is recommended.
One additional test to check whether the data is suited for factor
analysis is the Kaiser-Meyer-Olkin (KMO) measure of sampling adequacy is
recommended.

### Kaiser-Meyer-Olkin measure of Sampling Adequacy

``` r
KMO(cor.matrix)
```

    ## Kaiser-Meyer-Olkin factor adequacy
    ## Call: KMO(r = cor.matrix)
    ## Overall MSA =  0.84
    ## MSA for each item = 
    ## ipcrtiv imprich ipeqopt ipshabt impsafe impdiff ipfrule ipudrst ipmodst ipgdtim 
    ##    0.86    0.84    0.84    0.82    0.76    0.84    0.81    0.85    0.80    0.81 
    ## impfree iphlppl ipsuces ipstrgv ipadvnt ipbhprp iprspot iplylfr  impenv imptrad 
    ##    0.89    0.87    0.82    0.89    0.80    0.85    0.85    0.87    0.88    0.78 
    ##  impfun 
    ##    0.83

The test reveals a sampling adequacy of 0.84, the individual KMO values
near or above 0.8, placing the sampling adequacy well above the 0.5
threshold of poor factorability (Belhekar 2019).

## Number of Factors

``` r
fit <- principal(cor.matrix, nfactors = 6, rotate = "none")
eigen <- fit$values

pc_number <-1:21
plot(pc_number, eigen, pch = 10, cex = 1, 
    cex.lab = 1, cex.axis = 1, main = "Scree Plot", 
    type = "b")
abline(1, 0, 1, lty=3, col = 'blue')
```

![Scree Plot](https://github.com/dewaalaw/dsprojects/blob/466a7b2f85b1db4d70ce9c0f1e3c9c6536236c33/human-values-scale/images/screeplot.png)<!-- -->

Above we have the *Cattell’s* scree plot, the red line indicating the
Guttmann’s eigenvalue greater than 1 criterion, suggesting retention of
4 principle components.

    ## Loading required package: lattice

    ## 
    ## Attaching package: 'nFactors'

    ## The following object is masked from 'package:lattice':
    ## 
    ##     parallel

![Scree Plot Non-Graphical](https://github.com/dewaalaw/dsprojects/blob/466a7b2f85b1db4d70ce9c0f1e3c9c6536236c33/human-values-scale/images/screeplot_nongraph.png)<!-- -->

Without placing a-priori constraints on the number of factors to be
extracted, we now examine the underlying variable structure inasmuch as
statistically grouping highly interrelated variables into composite sets
called factors such that minimum information is lost. Common factor
analysis and the principle component analysis are two approaches common
in that regard.

## Common Factor Analysis (CFA)

When the primary objective is to identify the underlying latent factors
common in sets of variables then CFA is the first port of call. Data
reduction is thus not the primary concern, rather the summation of
variables to common factors by observing only the variance shared
amongst those correlated. The analysis leaves aside the *specific
variation* (i.e. the variance specific to a variable ) and the *error
variance* (i.e., the unexplained variance of correlated variables). In
this sense, CFA is an open model since it explains only the common
variance whilst more variance was explainable. Below we conclude a
factor analysis using the `psych` package’s (`fa`) functionto that of
R’s (`factanal)`. A varimax rotation is applied and loadings less than
0.3 are dropped. Taking into account the large sample size (n = 1441),
the said threshold (0.3) explains approximately 10 percent of the
variance, noting that the factor accounts for the squared loading which
is amount of the variable’s total variance.

``` r
# Factor analysis using fa function in psych package
factors.psych <- fa(data, nfactors = 4, rotate = "varimax", 
                    scores = "regression", fm = "ml")
print.psych(factors.psych, cut = 0.3, digits = 2, sort = TRUE)
```

    ## Factor Analysis using method =  ml
    ## Call: fa(r = data, nfactors = 4, rotate = "varimax", scores = "regression", 
    ##     fm = "ml")
    ## Standardized loadings (pattern matrix) based upon correlation matrix
    ##         item   ML1   ML3   ML2   ML4   h2   u2 com
    ## ipsuces   13  0.74                   0.61 0.39 1.3
    ## ipshabt    4  0.65                   0.47 0.53 1.2
    ## imprich    2  0.50                   0.33 0.67 1.6
    ## iprspot   17  0.48        0.39       0.40 0.60 2.1
    ## ipudrst    8        0.61             0.39 0.61 1.1
    ## iphlppl   12        0.56             0.39 0.61 1.5
    ## ipeqopt    3        0.51             0.27 0.73 1.0
    ## iplylfr   18        0.50             0.33 0.67 1.7
    ## impenv    19        0.40             0.21 0.79 1.5
    ## ipmodst    9        0.33             0.21 0.79 2.5
    ## impfree   11        0.32             0.20 0.80 2.6
    ## ipcrtiv    1                         0.21 0.79 3.2
    ## ipfrule    7              0.58       0.37 0.63 1.3
    ## ipbhprp   16              0.56       0.40 0.60 1.5
    ## impsafe    5              0.54       0.30 0.70 1.1
    ## imptrad   20              0.45       0.22 0.78 1.1
    ## ipstrgv   14              0.39       0.21 0.79 1.8
    ## impfun    21                    0.71 0.57 0.43 1.3
    ## ipgdtim   10                    0.56 0.35 0.65 1.2
    ## impdiff    6                    0.55 0.47 0.53 2.1
    ## ipadvnt   15  0.35              0.52 0.46 0.54 2.4
    ## 
    ##                        ML1  ML3  ML2  ML4
    ## SS loadings           1.91 1.89 1.79 1.76
    ## Proportion Var        0.09 0.09 0.09 0.08
    ## Cumulative Var        0.09 0.18 0.27 0.35
    ## Proportion Explained  0.26 0.26 0.24 0.24
    ## Cumulative Proportion 0.26 0.52 0.76 1.00
    ## 
    ## Mean item complexity =  1.7
    ## Test of the hypothesis that 4 factors are sufficient.
    ## 
    ## The degrees of freedom for the null model are  210  and the objective function was  4.59 with Chi Square of  6574.39
    ## The degrees of freedom for the model are 132  and the objective function was  0.41 
    ## 
    ## The root mean square of the residuals (RMSR) is  0.03 
    ## The df corrected root mean square of the residuals is  0.04 
    ## 
    ## The harmonic number of observations is  1441 with the empirical chi square  496.25  with prob <  1.3e-43 
    ## The total number of observations was  1441  with Likelihood Chi Square =  581.74  with prob <  1e-57 
    ## 
    ## Tucker Lewis Index of factoring reliability =  0.887
    ## RMSEA index =  0.049  and the 90 % confidence intervals are  0.045 0.053
    ## BIC =  -378.31
    ## Fit based upon off diagonal values = 0.98
    ## Measures of factor score adequacy             
    ##                                                    ML1  ML3  ML2  ML4
    ## Correlation of (regression) scores with factors   0.85 0.83 0.84 0.83
    ## Multiple R square of scores with factors          0.73 0.69 0.70 0.69
    ## Minimum correlation of possible factor scores     0.46 0.38 0.40 0.39

    ## 
    ## Call:
    ## factanal(x = data, factors = 4, scores = "regression", rotation = "varimax",     method = "mle")
    ## 
    ## Uniquenesses:
    ## ipcrtiv imprich ipeqopt ipshabt impsafe impdiff ipfrule ipudrst ipmodst ipgdtim 
    ##    0.79    0.67    0.73    0.53    0.70    0.53    0.63    0.61    0.79    0.65 
    ## impfree iphlppl ipsuces ipstrgv ipadvnt ipbhprp iprspot iplylfr  impenv imptrad 
    ##    0.80    0.61    0.39    0.79    0.54    0.60    0.60    0.67    0.79    0.78 
    ##  impfun 
    ##    0.43 
    ## 
    ## Loadings:
    ##         Factor1 Factor2 Factor3 Factor4
    ## imprich  0.50                          
    ## ipshabt  0.65                          
    ## ipsuces  0.74                          
    ## ipeqopt          0.51                  
    ## ipudrst          0.61                  
    ## iphlppl          0.56                  
    ## impsafe                  0.54          
    ## ipfrule                  0.58          
    ## ipbhprp                  0.56          
    ## impdiff                          0.55  
    ## ipgdtim                          0.56  
    ## ipadvnt  0.35                    0.52  
    ## impfun                           0.71  
    ## ipcrtiv                                
    ## ipmodst          0.33                  
    ## impfree          0.32                  
    ## ipstrgv                  0.39          
    ## iprspot  0.48            0.39          
    ## iplylfr          0.50                  
    ## impenv           0.40                  
    ## imptrad                  0.45          
    ## 
    ##                Factor1 Factor2 Factor3 Factor4
    ## SS loadings       1.91    1.89    1.79    1.76
    ## Proportion Var    0.09    0.09    0.09    0.08
    ## Cumulative Var    0.09    0.18    0.27    0.35
    ## 
    ## Test of the hypothesis that 4 factors are sufficient.
    ## The chi square statistic is 581.74 on 132 degrees of freedom.
    ## The p-value is 1.02e-57

The results between the common factor functions are comparable, but
interestingly `fa` removes *impfree* and *ipcrtiv* while `factanal`
removes only the latter. Hence the factor loading pattern match, with
the exception that `factanal` loads the latter as an additional variable
on one of the factors.

The importance for wealth (imprich), show abilities, be admired
(ipshabt), successful, and that people recognise achievements (ipsuces)
loaded on the first factor (Factor 1). Factor 1 thus capture values of
*power* and *achievement*, underlayed by the motivational goal of
self-enhancement (see the human values model above). However, adventure
seeking and having an exciting life (ipadvnt—underlayed by the
motivation goal of stimulation), as well as the importance to get
respect from others (iprspot—underlayed by the motivation goal of
tradition) also load on Factor 1.

While factor 2 resemble universalism (ipeqopt, ipudrst, impenv) and
benevolence (iphlppl), underlayed by the motivational goal of
self-transcendence, factor 3 is estimated by indicators causal of
security (iplylfr, impsafe), conformity (ipfrule, ipbhprp), and
tradition (iprspot, imptrad), underlayed by the motivational goal of
conservation.

Finally, factor 4 is loaded by indicators causal of stimulation (impdiff
, impadvnt) and hedonism (ipgdtim, ipadvnt), capturing the latent
construct of openness to change. The table below arranges the above
results firstly by the motivational goal, and then by the factor.

| Motivational Goal  | Value Type     | Factor | Indicator |
|--------------------|----------------|--------|-----------|
| Self-Enhancement   | Power          | 1      | imprich   |
| Self-Enhancement   | Power          | 1      | ipshabt   |
| Self-Enhancement   | Achievement    | 1      | ipsuces   |
| Openness to Change | Stimulation    | 1      | ipadvnt   |
| Conservation       | Tradition      | 1      | iprspot   |
| Self-Transcendence | Universalism   | 2      | ipeqopt   |
| Self-Transcendence | Universalism   | 2      | ipudrst   |
| Self-Transcendence | Universalism   | 2      | impenv    |
| Self-Transcendence | Benevolence    | 2      | iphlppl   |
| Conservation       | Tradition      | 2      | ipmodst   |
| Openness to Change | Self-Direction | 2      | impfree   |
| Conservation       | Security       | 2      | iplylfr   |
| Conservation       | Security       | 3      | impsafe   |
| Conservation       | Security       | 3      | ipstrgv   |
| Conservation       | Conformity     | 3      | ipfrule   |
| Conservation       | Conformity     | 3      | ipbhprp   |
| Conservation       | Tradition      | 3      | iprspot   |
| Conservation       | Tradition      | 3      | imptrad   |
| Openness to Change | Stimulation    | 4      | impdiff   |
| Openness to Change | Stimulation    | 4      | ipadvnt   |
| Openness to Change | Hedonism       | 4      | ipgdtim   |
| Openness to Change | Hedonism       | 4      | impfun    |

## Principal Component Analysis (PCA)

Contrary to CFA, PCA considers the total variance. This analysis sought
to summarise the data in the least amount of factors to explain the
maximum amount of variance. The code below executes a PCA, and the
results are discussed thereafter.

``` r
factors.principal <- principal(data, nfactors = 4, residuals = FALSE, 
          rotate = "varimax", n.obs = NA, 
          covar = FALSE,  scores = TRUE, 
          oblique.scores = TRUE, 
          method = "regression")

#print(holder$loadings, digits = 2, cutoff = 0.3, sort = TRUE)
print.psych(factors.principal)
```

    ## Principal Components Analysis
    ## Call: principal(r = data, nfactors = 4, residuals = FALSE, rotate = "varimax", 
    ##     n.obs = NA, covar = FALSE, scores = TRUE, oblique.scores = TRUE, 
    ##     method = "regression")
    ## Standardized loadings (pattern matrix) based upon correlation matrix
    ##           RC3   RC1   RC4   RC2   h2   u2 com
    ## ipcrtiv  0.32  0.28  0.31 -0.17 0.30 0.70 3.5
    ## imprich -0.19  0.58  0.31  0.06 0.47 0.53 1.8
    ## ipeqopt  0.65  0.09  0.00 -0.07 0.44 0.56 1.1
    ## ipshabt  0.06  0.74  0.12  0.10 0.58 0.42 1.1
    ## impsafe  0.05  0.08 -0.03  0.65 0.44 0.56 1.0
    ## impdiff  0.26  0.24  0.65 -0.09 0.55 0.45 1.7
    ## ipfrule  0.11  0.27 -0.10  0.63 0.49 0.51 1.5
    ## ipudrst  0.71  0.05  0.10 -0.02 0.51 0.49 1.1
    ## ipmodst  0.43 -0.14 -0.16  0.33 0.33 0.67 2.4
    ## ipgdtim  0.03  0.13  0.69  0.04 0.50 0.50 1.1
    ## impfree  0.37  0.25  0.27  0.00 0.27 0.73 2.6
    ## iphlppl  0.60 -0.10  0.26  0.23 0.49 0.51 1.8
    ## ipsuces  0.02  0.77  0.24  0.11 0.66 0.34 1.2
    ## ipstrgv  0.19  0.12  0.11  0.49 0.31 0.69 1.6
    ## ipadvnt  0.15  0.34  0.59 -0.22 0.54 0.46 2.1
    ## ipbhprp  0.18  0.34 -0.10  0.59 0.51 0.49 1.9
    ## iprspot  0.12  0.61  0.03  0.37 0.52 0.48 1.7
    ## iplylfr  0.54 -0.02  0.30  0.20 0.43 0.57 1.9
    ## impenv   0.52  0.02  0.01  0.22 0.32 0.68 1.4
    ## imptrad -0.09 -0.16  0.19  0.65 0.49 0.51 1.3
    ## impfun   0.08  0.04  0.77  0.24 0.66 0.34 1.2
    ## 
    ##                        RC3  RC1  RC4  RC2
    ## SS loadings           2.52 2.46 2.44 2.40
    ## Proportion Var        0.12 0.12 0.12 0.11
    ## Cumulative Var        0.12 0.24 0.35 0.47
    ## Proportion Explained  0.26 0.25 0.25 0.24
    ## Cumulative Proportion 0.26 0.51 0.76 1.00
    ## 
    ## Mean item complexity =  1.7
    ## Test of the hypothesis that 4 components are sufficient.
    ## 
    ## The root mean square of the residuals (RMSR) is  0.06 
    ##  with the empirical chi square  2425.67  with prob <  0 
    ## 
    ## Fit based upon off diagonal values = 0.9

A number of indicators split their loading on more than one factor, but
do not violate the simple structure objective (Belhekar, 2019). To be
sure, a simple structure is observed when an indicator load on only one
latent variable, or when an indicator has a higher loading on only one
factor and a smaller loading on the other. Finally, split loading is
avoided as it complicates theoretic interpretation (Belhekar, 2019).

Indicators *ipadvnt* load on factor 1 and 4, while and *iprspot* load on
factor 1 and 3. Although the literature suggest several descriptors to
identify cross-loadings (e.g., Howard, 2015; Costello et al., 2005;
Sandbrook, 2019), implementing an alternative rotation or removing the
split-load-indicator are common remedies. Since the the analysis obtain
a simple structure, the promax rotation below is not necessary, but
executed for the sake of interest.

~~Rosa, Pedro Joel. (2021). Re: How to deal with cross loadings in
Exploratory Factor Analysis?. Retrieved from:
<https://www.researchgate.net/post/How-to-deal-with-cross-loadings-in-Exploratory-Factor-Analysis/6181893de9d4af5931571d38/citation/download.>~~

    ## 
    ## Call:
    ## factanal(x = data, factors = 4, scores = "regression", rotation = "promax")
    ## 
    ## Uniquenesses:
    ## ipcrtiv imprich ipeqopt ipshabt impsafe impdiff ipfrule ipudrst ipmodst ipgdtim 
    ##    0.79    0.67    0.73    0.53    0.70    0.53    0.63    0.61    0.79    0.65 
    ## impfree iphlppl ipsuces ipstrgv ipadvnt ipbhprp iprspot iplylfr  impenv imptrad 
    ##    0.80    0.61    0.39    0.79    0.54    0.60    0.60    0.67    0.79    0.78 
    ##  impfun 
    ##    0.43 
    ## 
    ## Loadings:
    ##         Factor1 Factor2 Factor3 Factor4
    ## imprich  0.51                          
    ## ipshabt  0.71                          
    ## ipsuces  0.79                          
    ## iprspot  0.51            0.38          
    ## ipeqopt          0.57                  
    ## ipudrst          0.67                  
    ## iphlppl          0.56                  
    ## impsafe                  0.55          
    ## ipfrule                  0.58          
    ## ipbhprp                  0.56          
    ## ipgdtim                          0.60  
    ## impfun                           0.85  
    ## ipcrtiv                                
    ## impdiff                          0.47  
    ## ipmodst          0.35                  
    ## impfree                                
    ## ipstrgv                  0.37          
    ## ipadvnt                          0.39  
    ## iplylfr          0.48                  
    ## impenv           0.41                  
    ## imptrad                  0.46          
    ## 
    ##                Factor1 Factor2 Factor3 Factor4
    ## SS loadings        2.0    1.91    1.76    1.66
    ## Proportion Var     0.1    0.09    0.08    0.08
    ## Cumulative Var     0.1    0.19    0.27    0.35
    ## 
    ## Factor Correlations:
    ##         Factor1 Factor2 Factor3 Factor4
    ## Factor1   1.000  0.0484   -0.29 -0.5851
    ## Factor2   0.048  1.0000   -0.25  0.0063
    ## Factor3  -0.293 -0.2452    1.00  0.4582
    ## Factor4  -0.585  0.0063    0.46  1.0000
    ## 
    ## Test of the hypothesis that 4 factors are sufficient.
    ## The chi square statistic is 581.74 on 132 degrees of freedom.
    ## The p-value is 1.02e-57

The promax rotation gives a simpler structure than varimax; the latter
is an orthogonal rotation while the former an oblique rotation. While
orthogonal rotations assume un-correlated factors, oblique rotations
assume that factors are correlated. The analysis show that the oblique
rotation gives a simpler structure, but additionally show that Factor 3
and 4 obtains a negative correlation with Factor 1.
