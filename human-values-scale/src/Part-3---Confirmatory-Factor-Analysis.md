Part 3 - Confirmatory Factor Analysis
================

# Factor Analysis—Confirmatory Factor Analysis

The model below postulates that the four underlying latent variables
(self-transcendence, conservation, change, and self-enhancement) are
generated by the observed variables (or indicators). Further, no
correlation is assumed between the latent variables. Estimated by the
model are the structural coefficients
(![\\lambda](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Clambda "\lambda")),
measuring the association between the latent variable and its
indicators, and variances
(![\\mu](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cmu "\mu"))—noting
that the *“importance to think new ideas and being creative”* (ipcrtiv)
has loaded below the 0.3 threshold and thus removed.

``` r
confirm.fact <- ' f1.self.enhance =~ imprich + ipshabt + ipsuces + iprspot
f2.self.trancend =~ ipeqopt + ipudrst + iphlppl +ipmodst + impfree + 
                    iplylfr + impenv
f3.conservation =~ impsafe + ipfrule + ipbhprp + ipstrgv + imptrad
f4.change =~ impdiff + ipgdtim + ipadvnt + impfun
'
fit.lavaan <- cfa(confirm.fact, data = data, orthogonal=TRUE)

inspect(fit.lavaan, what="std")$lambda
```

    ##         f1.sl. f2.sl. f3.cns f4.chn
    ## imprich  0.517  0.000  0.000  0.000
    ## ipshabt  0.673  0.000  0.000  0.000
    ## ipsuces  0.833  0.000  0.000  0.000
    ## iprspot  0.519  0.000  0.000  0.000
    ## ipeqopt  0.000  0.491  0.000  0.000
    ## ipudrst  0.000  0.600  0.000  0.000
    ## iphlppl  0.000  0.636  0.000  0.000
    ## ipmodst  0.000  0.311  0.000  0.000
    ## impfree  0.000  0.360  0.000  0.000
    ## iplylfr  0.000  0.588  0.000  0.000
    ## impenv   0.000  0.413  0.000  0.000
    ## impsafe  0.000  0.000  0.531  0.000
    ## ipfrule  0.000  0.000  0.635  0.000
    ## ipbhprp  0.000  0.000  0.598  0.000
    ## ipstrgv  0.000  0.000  0.452  0.000
    ## imptrad  0.000  0.000  0.396  0.000
    ## impdiff  0.000  0.000  0.000  0.719
    ## ipgdtim  0.000  0.000  0.000  0.543
    ## ipadvnt  0.000  0.000  0.000  0.664
    ## impfun   0.000  0.000  0.000  0.616

``` r
semPaths(fit.lavaan, title = FALSE, curvePivot = TRUE, what="std")
```

![Structural Equation Model](https://github.com/dewaalaw/dsprojects/blob/0b0ad42d7fdd201172dde6f6dbbcc36c71acb0b8/human-values-scale/images/sem_model.png)<!-- -->

``` r
summary(fit.lavaan)
```

    ## lavaan 0.6-12 ended normally after 46 iterations
    ## 
    ##   Estimator                                         ML
    ##   Optimization method                           NLMINB
    ##   Number of model parameters                        40
    ## 
    ##   Number of observations                          1441
    ## 
    ## Model Test User Model:
    ##                                                       
    ##   Test statistic                              1964.776
    ##   Degrees of freedom                               170
    ##   P-value (Chi-square)                           0.000
    ## 
    ## Parameter Estimates:
    ## 
    ##   Standard errors                             Standard
    ##   Information                                 Expected
    ##   Information saturated (h1) model          Structured
    ## 
    ## Latent Variables:
    ##                       Estimate  Std.Err  z-value  P(>|z|)
    ##   f1.self.enhance =~                                     
    ##     imprich              1.000                           
    ##     ipshabt              1.557    0.095   16.330    0.000
    ##     ipsuces              1.881    0.115   16.424    0.000
    ##     iprspot              1.129    0.080   14.136    0.000
    ##   f2.self.trancend =~                                    
    ##     ipeqopt              1.000                           
    ##     ipudrst              1.194    0.088   13.594    0.000
    ##     iphlppl              1.213    0.087   13.907    0.000
    ##     ipmodst              0.754    0.085    8.920    0.000
    ##     impfree              0.870    0.087    9.968    0.000
    ##     iplylfr              0.983    0.073   13.478    0.000
    ##     impenv               0.898    0.082   10.987    0.000
    ##   f3.conservation =~                                     
    ##     impsafe              1.000                           
    ##     ipfrule              1.233    0.092   13.451    0.000
    ##     ipbhprp              1.123    0.085   13.255    0.000
    ##     ipstrgv              0.814    0.071   11.476    0.000
    ##     imptrad              0.793    0.076   10.497    0.000
    ##   f4.change =~                                           
    ##     impdiff              1.000                           
    ##     ipgdtim              0.692    0.043   16.117    0.000
    ##     ipadvnt              0.960    0.053   18.248    0.000
    ##     impfun               0.731    0.042   17.602    0.000
    ## 
    ## Covariances:
    ##                       Estimate  Std.Err  z-value  P(>|z|)
    ##   f1.self.enhance ~~                                     
    ##     f2.self.trncnd       0.000                           
    ##     f3.conservatin       0.000                           
    ##     f4.change            0.000                           
    ##   f2.self.trancend ~~                                    
    ##     f3.conservatin       0.000                           
    ##     f4.change            0.000                           
    ##   f3.conservation ~~                                     
    ##     f4.change            0.000                           
    ## 
    ## Variances:
    ##                    Estimate  Std.Err  z-value  P(>|z|)
    ##    .imprich           0.951    0.040   23.986    0.000
    ##    .ipshabt           1.015    0.053   19.254    0.000
    ##    .ipsuces           0.540    0.055    9.784    0.000
    ##    .iprspot           1.195    0.050   23.942    0.000
    ##    .ipeqopt           0.693    0.030   23.433    0.000
    ##    .ipudrst           0.560    0.027   20.752    0.000
    ##    .iphlppl           0.477    0.024   19.468    0.000
    ##    .ipmodst           1.172    0.046   25.708    0.000
    ##    .impfree           1.124    0.044   25.267    0.000
    ##    .iplylfr           0.403    0.019   21.119    0.000
    ##    .impenv            0.866    0.035   24.660    0.000
    ##    .impsafe           1.265    0.059   21.556    0.000
    ##    .ipfrule           1.112    0.063   17.621    0.000
    ##    .ipbhprp           1.126    0.058   19.248    0.000
    ##    .ipstrgv           1.279    0.055   23.428    0.000
    ##    .imptrad           1.675    0.069   24.385    0.000
    ##    .impdiff           0.868    0.053   16.256    0.000
    ##    .ipgdtim           1.067    0.047   22.821    0.000
    ##    .ipadvnt           1.086    0.057   18.966    0.000
    ##    .impfun            0.813    0.039   20.835    0.000
    ##     f1.self.enhanc    0.346    0.037    9.268    0.000
    ##     f2.self.trncnd    0.221    0.026    8.338    0.000
    ##     f3.conservatin    0.496    0.057    8.622    0.000
    ##     f4.change         0.930    0.072   12.833    0.000

``` r
fitMeasures(fit.lavaan, c("chisq", "gfi", "agfi", "gfi", "nfi", "nnfi", "cfi", "pgfi", "pnfi", "srmr", "RMSEA"), output = "matrix")
```

    ##               
    ## chisq 1964.776
    ## gfi      0.882
    ## agfi     0.854
    ## gfi      0.882
    ## nfi      0.688
    ## nnfi     0.672
    ## cfi      0.706
    ## pgfi     0.714
    ## pnfi     0.616
    ## srmr     0.129
    ## rmsea    0.086

The standardised root mean square residual (SRMR), root means square
error of approximation (RMSEA), (adjusted) goodness of fit index
((A)GFI), suggest inadequate model fit (for model fit thresholds, see
Belhekar, 2019, p. 45).
