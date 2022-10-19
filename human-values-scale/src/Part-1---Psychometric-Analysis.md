Part 1 - Psychometric Analysis of the Human Value Scale
================

# Introduction

Values are an abstract orientation or belief that frame a behavioural ideal; are grounded in needs and norms; contextually stable yet time dependent; and hierarchical insofar as their (self or social) importance. For example, it is quite common for a person or a group of people to
hold certain values at higher regard than others. That values are grounded in needs and norms suggest that they are often a medium
through which needs and norms are communicated. Now, although values are contextually stable, changes within society, polity, and the economy
bring about changes within values. For this reason, values change with time—in turn bringing about changes within society, politics, and the economy
(Schwartz, 1994). Taken together, values influence as they are influenced. 

Valences, albeit linked, are often distinguished from values. The former is a latent preconditions understood in terms of attraction or aversion (Feather, 1995). Accordingly, and given the spread of people, values are conceivably as diverse as people.

## Swchartz’ Model of Basic Human Values

Shalom H. Schwartz contends that despite this diversity there are nonetheless a normative and indeed now regarded a canonical set of ten
transcendental human values, defined by the central goal they represent. The 10 values are derived from what Schwartz regard as universal amongst all people—i.e., ‘the needs of individuals as biological organisms’, ‘requisites of coordinated social interaction’, ‘and requirements for the smooth functioning and survival of groups’. For this reason the 10 values are underlayed by four motivational goals—i.e., self-transcendence, conservation, self-enhancement, and openness to change. As shown in Figure 1, Schwartz posits that the human value model obtains a circular structure according to the content of the value's underlying motivational goal. Adjacent values are more compatible than those further away, where those at opposite ends are likely at conflict (Schwartz, 1994).

<img src="https://github.com/dewaalaw/dsprojects/blob/39da999790a22d3a5ea14f5efcd707754a3fe059/human-values-scale/images/hvs.png" alt="Fig. 1 — Theoretical model of relations among motivational types of values, higher order value types, and bipolar value dimensions (Schwartz, 1994)" width="563"/>

The codebook below lists the 10 values on the right alongside the indicators for measurement. For example, the indicator *impenv*—the importance to care for nature and environment, measuring the value universalism—is derived from the need of individuals as biological organisms to survive.

## Codebook

| **Code** | **Indicator**                                                          | **Basic Value** |
|:---------|:-----------------------------------------------------------------------|:----------------|
| ipcrtiv  | Important to think new ideas and being creative                        | Self-Direction  |
| imprich  | Important to be rich, have money and expensive things                  | Power           |
| ipeqopt  | Important that people are treated equally and have equal opportunities | Universalism    |
| ipshabt  | Important to show abilities and be admired                             | Power           |
| impsafe  | Important to live in secure and safe surroundings                      | Security        |
| impdiff  | Important to try new and different things in life                      | Stimulation     |
| ipfrule  | Important to do what is told and follow rules                          | Conformity      |
| ipudrst  | Important to understand different people                               | Universalism    |
| ipmodst  | Important to be humble and modest, not draw attention                  | Tradition       |
| ipgdtim  | Important to have a good time                                          | Hedonism        |
| impfree  | Important to make own decisions and be free                            | Self-Direction  |
| iphlppl  | Important to help people and care for others’ well-being               | Benevolence     |
| ipsuces  | Important to be successful and that people recognize achievements      | Achievement     |
| ipstrgv  | Important that government is strong and ensures safety                 | Security        |
| ipadvnt  | Important to seek adventures and have an exciting life                 | Stimulation     |
| ipbhprp  | Important to behave properly                                           | Conformity      |
| iprspot  | Important to get respect from others                                   | Tradition       |
| iplylfr  | Important to be loyal to friends and devote to people close            | Security        |
| impenv   | Important to care for nature and environment                           | Universalism    |
| imptrad  | Important to follow traditions and customs                             | Tradition       |
| impfun   | Important to seek fun and things that give pleasure                    | Hedonism        |

The indicators are specific to an exemplary ‘value’. For instance *iphlppl*—the importance to help people and care for others’ well-being—measures the sense of *helpfulness* to gauge a person's orientation toward the basic value *benevolence* —whether they belief in the improvement of the welfare of others. But, there are of course other qualities such as *honesty* and *forgiveness* that equally orient within a benevolence frame.

Helpfulness, honesty, or forgiveness are conceivably abstract notions—their meaning which are socially constructed. For this reason, the indicator assumes that the respondent comports with the cultural and social meaning implied. Hence, the indicator assumes that the measured response indicates a connection with the ‘value’ (or in general terms, the trait) being measured. And it is indeed this assumption that yields to the un-observability of the trait—it being termed latent.

# Psychometric Analysis

The foregone assumption underpins the Item Response Theory (IRT)—which addresses the question whether what is measured is indeed what we are measuring with the scale at hand.

## Graded Response Model (GRM)

One way the above question be evaluated is by way of the graded response model. The GRM measures the probability of a response to an item as
a function of an individual’s ability (or predisposition). An individual's ability in terms of the IRT is the latent trait of interest (i.e., the codebook item in the Basic Value
column). Below we examine *imprich* which measures a person’s love of wealth, assuming that the latent trait—or motivational value—which gives rise to this behaviour is *power*. Respondents were asked how much they are like a person that hold in high regard the importance to be rich, wants a lot of money and expensive things. They had the option of selecting either: 1 = “very much like me”; 2 — “like me”; 3 — “somewhat
like me”; 4 — “a little like me”; 5 - “not like me”; 6 - “not like me at all”. (GRM’s are specifically suited for ordinal polytomous responses
such as these.)

We plot the relation between the item response probability and ability—hereafter termed the item response category characteristic curves or
IRCCC—in the first plot, followed by the item information curve (IIC) below.

``` r
# Item response category characteristic curve
model <- grm(data, constrained = FALSE)
plot(model, items = c(2), lwd = 1, cex = 1.4)
abline(v = -5:5, h = seq(0, 1, 0.1), col = "lightgray", lty = "dotted")
```

![IRCCC - item: imprich](https://github.com/dewaalaw/dsprojects/blob/39da999790a22d3a5ea14f5efcd707754a3fe059/human-values-scale/images/IRCCC_imprich.png)<!-- -->

``` r
# Item information curve (IIC)
plot(model, type= "IIC", items = c(2), legend = TRUE, lwd = 1, cx = "topright")
abline(v = -4:4, h = seq(0.11, 0.16, 0.005), col = "lightgray", lty = "dotted")
```

![IIC - item: imprich](https://github.com/dewaalaw/dsprojects/blob/39da999790a22d3a5ea14f5efcd707754a3fe059/human-values-scale/images/IIC_imprich.png)<!-- -->

Apart from 3, 4, 5, and 6, all response categories have a higher
probability of being selected when the respondent’s ability matching the
person depicted is high. A low ability in this instance indicates a high
predisposition for power. From the scale’s ordinal direction the IRCCC
shows the response of 6 (not like me at all), which has a higher
probability when the predisposition for power is low. This suggests that
people with a low ability of power have a high probability of choosing
6. Interestingly, individuals with a moderate ability of power are
likely to choose 5 ( not like me). The IRCCC shows that the probability
of choosing option 5 is highest at ability 1.

On the other hand, the IIC indicates that the item-test (*imprich*)
provides the greatest test information for the ability ranging from -4
to -2. That is, the item-test is most useful when an individual of that
ability-range (or predisposition to power interpreted in terms of the
love of wealth) is tested. Baker (2001) explains that the information
function is based on Sir R.A. Fisher’s definition of information: “the
reciprocal of the precision with which a parameter could be estimated”.
This, Baker informs, is the technical interpretation of the general
meaning of information, that you “know something about a particular
object” (Baker, 2001, p. 104). Baker’s description of the item
information interpretation is rather concise, so we will paraphrase it
here for our purpose: the amount of information the *imprich* item
provide decreases as the ability level departs from the item difficulty
![(-4\<\\theta\<=-2)](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%28-4%3C%5Ctheta%3C%3D-2%29 "(-4<\theta<=-2)"),
approaching naught at the positive extreme of the ability scale.

``` r
plot(model, type= "IIC", items = 0, 
     lwd = 1, cex.lab = 1.1, 
     sub = paste("Call: ", deparse(model$call)))
abline(v = -4:4, h = seq(2.5, 6, 0.1), col = "lightgray", lty = "dotted")
```

![Test Information Function](https://github.com/dewaalaw/dsprojects/blob/39da999790a22d3a5ea14f5efcd707754a3fe059/human-values-scale/images/TIF.png)<!-- -->

For the IIC a flattened peak suggest the test item captures precise
information for a range of examinees within the ability the flatness is
observed. Likewise, as several items constitute a larger test (in this
instance the human values test), as shown above, so can the information
function be determined for the entire test—hereafter termed the test
information function (TIF). The TIF’s peak plateaus at 5.1, for the
range
![(0\<= \\theta\<=1)](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%280%3C%3D%20%5Ctheta%3C%3D1%29 "(0<= \theta<=1)").
Hence the human values test provide accurate information of examinees’
ability within the said range—outside of which precision decreases.

``` r
vals <- plot(model, type = "IIC",  items = 0, plot = FALSE)
plot(vals[, "z"], 1/sqrt(vals[, "test.info"]),
     type = "l", lwd = 1, xlab = "Ability", ylab = "Standard Error",
     main = "Standard Error of Measurement")
abline(v = -4:4, h = seq(0.45, 0.65, 0.05), col = "lightgray", lty = "dotted")
```

![Standard Error of Measurment](https://github.com/dewaalaw/dsprojects/blob/39da999790a22d3a5ea14f5efcd707754a3fe059/human-values-scale/images/SEM.png)<!-- -->

# References

Baker, F. B. (2001). The Information Function. In Basics of Item
Response Theory.

Feather, N. T. (1995). Values, valences, and choice: The influences of
values on the perceived attractiveness and choice of alternatives.
Journal of Personality and Social Psychology, 68(6).

Schwartz, S. H., & Bilsky, W. (1987). Toward a Universal Psychological
Structure of Human Values. Journal of Personality and Social Psychology,
53(3).

# 
