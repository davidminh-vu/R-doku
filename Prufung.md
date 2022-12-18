## Scales of Measure
![image](https://user-images.githubusercontent.com/25742415/196103314-00a41e51-c6dd-4ca1-a771-fe464ffc6281.png)
![grafik](https://user-images.githubusercontent.com/25742415/208306464-4fe78463-0ad6-4ccd-a6e8-a8afdf5fde7b.png)
![grafik](https://user-images.githubusercontent.com/25742415/208321169-5b9c6f86-91e6-4b3b-8d01-f85a1d8ad987.png)

## Datatypes
![grafik](https://user-images.githubusercontent.com/25742415/208246240-e19c12ed-525e-43ef-93d3-c396758900db.png)

## Basic Dataset Methods
![grafik](https://user-images.githubusercontent.com/25742415/208249310-0aee88cb-de3d-4738-89f4-ab3f5d5fa1de.png)

### Subsetting
![grafik](https://user-images.githubusercontent.com/25742415/208249371-173b0b53-705f-4640-b5c7-cbbdbdffd7ac.png)

### Saving data
![grafik](https://user-images.githubusercontent.com/25742415/208249434-609e7812-9aa1-47b7-af5b-79320a370bf9.png)

### Graph types
![grafik](https://user-images.githubusercontent.com/25742415/208249468-ccdda1bc-9cd9-4bd5-ae4f-a0d46f397708.png)

## Tests
### Overview
![grafik](https://user-images.githubusercontent.com/25742415/208253680-922c3f6c-f4be-4602-8e77-42e5ab582555.png)

### Chi^2 Test
Meant to test the probability of independence of a distribution of data. Will not tell details about relationship between them.
![grafik](https://user-images.githubusercontent.com/25742415/208253697-c214c7b3-e4c6-482e-a110-7bfcde304205.png)

#### Chi Test of approximation
Tests whethera variable follows a hypothesized distribution.
Can be applied if variables is on a nominal scale

![grafik](https://user-images.githubusercontent.com/25742415/208253744-d0466350-a83c-4f2b-865b-43e1ad3ad042.png)

```R
# See expected proportions
chisq.test(table(rfm_clean$Satisfaction),p=rep(1/2,2))$expected

# Actual test
chisq.test(table(rfm_clean$Satisfaction),p=rep(1/2,2))
```
P < 0.05 => null Hypothesis rejected (Proportions are equal as the predicted)
![grafik](https://user-images.githubusercontent.com/25742415/208253809-3052a4e3-2559-4eb5-b110-5e1583ad98ce.png)

#### Chi Test of independence
Tests whether two variables are related
Can be applied to variables on a nominal scale
At least 5 observations each

H0: Variables are independent of each other
H1: Variables are dependent of each other
```R
# expected values for the two groups, check the assumption before conducting test
# if expected values are lower <5 the assumptions are not valid
chisq.test(table(rfm_clean$Satisfaction,rfm_clean$NRecency_5),correct=F)$expected

# test
chisq.test(table(rfm_clean$Satisfaction,rfm_clean$NRECENCY_5), correct=F)
```
H0 rejected, Variables depend on each other

![grafik](https://user-images.githubusercontent.com/25742415/208254140-c6d52852-da17-4efe-9a08-eb00cc563323.png)

#### Cramer's V
Measure of strength of association between two nominal variables between 0-1. 0 no assiciation, 1 strong.
U4 Folie

### Two sample t-test
Tests if means across two groups differ. One continuous variable, observed in both groups.

![grafik](https://user-images.githubusercontent.com/25742415/208307004-1a61a7a5-b85b-4726-9d20-fb22742ef589.png)

H0: Means do not differ
H1: Means differ

```R
t.test(Monetary~ Satisfaction, data= dataset)
```

![grafik](https://user-images.githubusercontent.com/25742415/208307066-21d7e4a9-1962-46b1-90de-dd35be13b6d1.png)

### Anova Test
Compare differences in means between groups (3 or more). Is at least one group different from the others?
Dependent variable should be continuous (interval or ratio).

Why not more T-Test => increases Type I (false positive) error
```R
result<-aov(metricvariable~groupingvariable,data=data)
summary(result)
```
![grafik](https://user-images.githubusercontent.com/25742415/208309625-d0e02843-1ea0-4cc2-b280-8468ad7553f9.png)

#### ETA 2
Explains how much variation is explained by the model (like R^2 in Linear Regression)
```R
library(effectsize)
eta_squared(result, partial = FALSE)
```

#### TurkeyHSD
Post hoc procedure to see which groups differ
Test if H0: group1 = group2, group1 = group 3, group2=group3

```R
TukeyHSD(aov2)
```
![grafik](https://user-images.githubusercontent.com/25742415/208310086-c9958c8b-2ccd-404b-973f-ace9a8a2aecd.png)

### Pearson Correlation analysis
Lineare association (r)
1 to -1, 1 perfect positive correlation, -1 perfect negative corrletion

![grafik](https://user-images.githubusercontent.com/25742415/208311582-879c64de-fb15-41f0-abee-6b5e90b1f13f.png)

```R
cor(rfm_profit$OverallSatisfaction, rfm_profit$Profit)
[1] 0. 556653

# r
rcorr(rfm_profit$OverallSatisfaction,rfm_profit$Profit)

#p-value
cor.test(rfm_profit$OverallSatisfaction,rfm_profit$Profit)
```
### Linear
![grafik](https://user-images.githubusercontent.com/25742415/208312180-78e53128-c401-437f-a969-822c29f588f1.png)

#### R^2 and Adjusted R^2
How good a model fits. R^2 rises with more variables, even if they don't contribute => adjusted R^2 accounts for that
