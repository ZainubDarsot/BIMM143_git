# Class08 Mini Lab:

## Outline

Today we will apply the machine learning methods we introduced in the
last class on breast cancer biopsy data from fine needle aspiration
(FNA)

## Data Input

The data is supplied on CSV Format: Also omit first column (ID:

``` r
wisc.df <- read.csv("WisconsinCancer.csv", row.names=1)
head(wisc.df)
```

             diagnosis radius_mean texture_mean perimeter_mean area_mean
    842302           M       17.99        10.38         122.80    1001.0
    842517           M       20.57        17.77         132.90    1326.0
    84300903         M       19.69        21.25         130.00    1203.0
    84348301         M       11.42        20.38          77.58     386.1
    84358402         M       20.29        14.34         135.10    1297.0
    843786           M       12.45        15.70          82.57     477.1
             smoothness_mean compactness_mean concavity_mean concave.points_mean
    842302           0.11840          0.27760         0.3001             0.14710
    842517           0.08474          0.07864         0.0869             0.07017
    84300903         0.10960          0.15990         0.1974             0.12790
    84348301         0.14250          0.28390         0.2414             0.10520
    84358402         0.10030          0.13280         0.1980             0.10430
    843786           0.12780          0.17000         0.1578             0.08089
             symmetry_mean fractal_dimension_mean radius_se texture_se perimeter_se
    842302          0.2419                0.07871    1.0950     0.9053        8.589
    842517          0.1812                0.05667    0.5435     0.7339        3.398
    84300903        0.2069                0.05999    0.7456     0.7869        4.585
    84348301        0.2597                0.09744    0.4956     1.1560        3.445
    84358402        0.1809                0.05883    0.7572     0.7813        5.438
    843786          0.2087                0.07613    0.3345     0.8902        2.217
             area_se smoothness_se compactness_se concavity_se concave.points_se
    842302    153.40      0.006399        0.04904      0.05373           0.01587
    842517     74.08      0.005225        0.01308      0.01860           0.01340
    84300903   94.03      0.006150        0.04006      0.03832           0.02058
    84348301   27.23      0.009110        0.07458      0.05661           0.01867
    84358402   94.44      0.011490        0.02461      0.05688           0.01885
    843786     27.19      0.007510        0.03345      0.03672           0.01137
             symmetry_se fractal_dimension_se radius_worst texture_worst
    842302       0.03003             0.006193        25.38         17.33
    842517       0.01389             0.003532        24.99         23.41
    84300903     0.02250             0.004571        23.57         25.53
    84348301     0.05963             0.009208        14.91         26.50
    84358402     0.01756             0.005115        22.54         16.67
    843786       0.02165             0.005082        15.47         23.75
             perimeter_worst area_worst smoothness_worst compactness_worst
    842302            184.60     2019.0           0.1622            0.6656
    842517            158.80     1956.0           0.1238            0.1866
    84300903          152.50     1709.0           0.1444            0.4245
    84348301           98.87      567.7           0.2098            0.8663
    84358402          152.20     1575.0           0.1374            0.2050
    843786            103.40      741.6           0.1791            0.5249
             concavity_worst concave.points_worst symmetry_worst
    842302            0.7119               0.2654         0.4601
    842517            0.2416               0.1860         0.2750
    84300903          0.4504               0.2430         0.3613
    84348301          0.6869               0.2575         0.6638
    84358402          0.4000               0.1625         0.2364
    843786            0.5355               0.1741         0.3985
             fractal_dimension_worst
    842302                   0.11890
    842517                   0.08902
    84300903                 0.08758
    84348301                 0.17300
    84358402                 0.07678
    843786                   0.12440

\##Create Vector for Diagnosis then omit Diagnosis:

``` r
diagnosis <- as.factor(wisc.df$diagnosis)
diagnosis
```

      [1] M M M M M M M M M M M M M M M M M M M B B B M M M M M M M M M M M M M M M
     [38] B M M M M M M M M B M B B B B B M M B M M B B B B M B M M B B B B M B M M
     [75] B M B M M B B B M M B M M M B B B M B B M M B B B M M B B B B M B B M B B
    [112] B B B B B B M M M B M M B B B M M B M B M M B M M B B M B B M B B B B M B
    [149] B B B B B B B B M B B B B M M B M B B M M B B M M B B B B M B B M M M B M
    [186] B M B B B M B B M M B M M M M B M M M B M B M B B M B M M M M B B M M B B
    [223] B M B B B B B M M B B M B B M M B M B B B B M B B B B B M B M M M M M M M
    [260] M M M M M M M B B B B B B M B M B B M B B M B M M B B B B B B B B B B B B
    [297] B M B B M B M B B B B B B B B B B B B B B M B B B M B M B B B B M M M B B
    [334] B B M B M B M B B B M B B B B B B B M M M B B B B B B B B B B B M M B M M
    [371] M B M M B B B B B M B B B B B M B B B M B B M M B B B B B B M B B B B B B
    [408] B M B B B B B M B B M B B B B B B B B B B B B M B M M B M B B B B B M B B
    [445] M B M B B M B M B B B B B B B B M M B B B B B B M B B B B B B B B B B M B
    [482] B B B B B B M B M B B M B B B B B M M B M B M B B B B B M B B M B M B M M
    [519] B B B M B B B B B B B B B B B M B M M B B B B B B B B B B B B B B B B B B
    [556] B B B B B B B M M M M M M B
    Levels: B M

``` r
wisc.data <- wisc.df[,-1]
```

## 1. Exploratory Data Analysis:

> Question 1: How many observations are in this dataset?

``` r
observations <- nrow(wisc.df)
observations
```

    [1] 569

> Question 2: How many of the observations have a malignant diagnosis?

``` r
table(wisc.df$diagnosis)
```


      B   M 
    357 212 

OR

``` r
sum(wisc.df$diagnosis == "M")
```

    [1] 212

> Question 3: How many variables/features in the data are suffixed with
> \_mean?

``` r
x <- colnames(wisc.df)

length(grep("_mean", x))
```

    [1] 10

## 2. Principle Component Analysis:

Check the mean and standard deviations:

``` r
colMeans(wisc.data)
```

                radius_mean            texture_mean          perimeter_mean 
               1.412729e+01            1.928965e+01            9.196903e+01 
                  area_mean         smoothness_mean        compactness_mean 
               6.548891e+02            9.636028e-02            1.043410e-01 
             concavity_mean     concave.points_mean           symmetry_mean 
               8.879932e-02            4.891915e-02            1.811619e-01 
     fractal_dimension_mean               radius_se              texture_se 
               6.279761e-02            4.051721e-01            1.216853e+00 
               perimeter_se                 area_se           smoothness_se 
               2.866059e+00            4.033708e+01            7.040979e-03 
             compactness_se            concavity_se       concave.points_se 
               2.547814e-02            3.189372e-02            1.179614e-02 
                symmetry_se    fractal_dimension_se            radius_worst 
               2.054230e-02            3.794904e-03            1.626919e+01 
              texture_worst         perimeter_worst              area_worst 
               2.567722e+01            1.072612e+02            8.805831e+02 
           smoothness_worst       compactness_worst         concavity_worst 
               1.323686e-01            2.542650e-01            2.721885e-01 
       concave.points_worst          symmetry_worst fractal_dimension_worst 
               1.146062e-01            2.900756e-01            8.394582e-02 

``` r
apply(wisc.data, 2, sd)
```

                radius_mean            texture_mean          perimeter_mean 
               3.524049e+00            4.301036e+00            2.429898e+01 
                  area_mean         smoothness_mean        compactness_mean 
               3.519141e+02            1.406413e-02            5.281276e-02 
             concavity_mean     concave.points_mean           symmetry_mean 
               7.971981e-02            3.880284e-02            2.741428e-02 
     fractal_dimension_mean               radius_se              texture_se 
               7.060363e-03            2.773127e-01            5.516484e-01 
               perimeter_se                 area_se           smoothness_se 
               2.021855e+00            4.549101e+01            3.002518e-03 
             compactness_se            concavity_se       concave.points_se 
               1.790818e-02            3.018606e-02            6.170285e-03 
                symmetry_se    fractal_dimension_se            radius_worst 
               8.266372e-03            2.646071e-03            4.833242e+00 
              texture_worst         perimeter_worst              area_worst 
               6.146258e+00            3.360254e+01            5.693570e+02 
           smoothness_worst       compactness_worst         concavity_worst 
               2.283243e-02            1.573365e-01            2.086243e-01 
       concave.points_worst          symmetry_worst fractal_dimension_worst 
               6.573234e-02            6.186747e-02            1.806127e-02 

Now we need to scale the input data before PCA because some of the
columns are measured in different unite with different means and
variances. We set `scale=T` in `prcomp()`.

``` r
wisc.pr <- prcomp(wisc.data, scale.=T )
summary(wisc.pr)
```

    Importance of components:
                              PC1    PC2     PC3     PC4     PC5     PC6     PC7
    Standard deviation     3.6444 2.3857 1.67867 1.40735 1.28403 1.09880 0.82172
    Proportion of Variance 0.4427 0.1897 0.09393 0.06602 0.05496 0.04025 0.02251
    Cumulative Proportion  0.4427 0.6324 0.72636 0.79239 0.84734 0.88759 0.91010
                               PC8    PC9    PC10   PC11    PC12    PC13    PC14
    Standard deviation     0.69037 0.6457 0.59219 0.5421 0.51104 0.49128 0.39624
    Proportion of Variance 0.01589 0.0139 0.01169 0.0098 0.00871 0.00805 0.00523
    Cumulative Proportion  0.92598 0.9399 0.95157 0.9614 0.97007 0.97812 0.98335
                              PC15    PC16    PC17    PC18    PC19    PC20   PC21
    Standard deviation     0.30681 0.28260 0.24372 0.22939 0.22244 0.17652 0.1731
    Proportion of Variance 0.00314 0.00266 0.00198 0.00175 0.00165 0.00104 0.0010
    Cumulative Proportion  0.98649 0.98915 0.99113 0.99288 0.99453 0.99557 0.9966
                              PC22    PC23   PC24    PC25    PC26    PC27    PC28
    Standard deviation     0.16565 0.15602 0.1344 0.12442 0.09043 0.08307 0.03987
    Proportion of Variance 0.00091 0.00081 0.0006 0.00052 0.00027 0.00023 0.00005
    Cumulative Proportion  0.99749 0.99830 0.9989 0.99942 0.99969 0.99992 0.99997
                              PC29    PC30
    Standard deviation     0.02736 0.01153
    Proportion of Variance 0.00002 0.00000
    Cumulative Proportion  1.00000 1.00000

> Question 4: From your results, what proportion of the original
> variance is captured by the first principal components (PC1)?

``` r
proportion_variance_PC1 <- (wisc.pr$sdev[1]^2) / sum(wisc.pr$sdev^2)
proportion_variance_PC1
```

    [1] 0.4427203

> Question 5: How many principal components (PCs) are required to
> describe at least 70% of the original variance in the data?

``` r
cumm_variance <- cumsum(wisc.pr$sdev^2) / sum(wisc.pr$sdev^2) 
sum(cumm_variance <=0.7) +1 
```

    [1] 3

> Question 6: How many principal components (PCs) are required to
> describe at least 90% of the original variance in the data?

``` r
cumm_variance <- cumsum(wisc.pr$sdev^2) / sum(wisc.pr$sdev^2) 
sum(cumm_variance <=0.9) +1 
```

    [1] 7

> Question 7: What stands out to you about this plot? Is it easy or
> difficult to understand? Why?

This plot is messy, so I made my own biplot:

``` r
library(ggplot2)
  biplot(wisc.pr)
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-13-1.png)

``` r
# Scatter plot observations by components 1 and 2
plot(wisc.pr$x[, 1] , col = diagnosis , 
     xlab = "PC1", ylab = "PC2")
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-14-1.png)

``` r
plot(wisc.pr$x[, 3], col = diagnosis, 
     xlab = "PC1", ylab = "PC3")
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-15-1.png)

> Question 8: Generate a similar plot for principal components 1 and 3.
> What do you notice about these plots?

``` r
PC1 <- wisc.pr$x[,1]
PC3 <- wisc.pr$x[,3]
plot(wisc.pr$x, col=diagnosis, 
     xlab= "PC1", ylab="PC3")
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-16-1.png)

For Question 8, the first comparison between PC1 and PC2 had a better
separation between the two groups vs PC1 and PC3. This is because PC2
explains more variance in the original data.

``` r
# Create a data.frame for ggplot
df <- as.data.frame(wisc.pr$x)
df$diagnosis <- wisc.data$diagnosis


# Load the ggplot2 package
library(ggplot2)

# Make a scatter plot colored by diagnosis
PC1 <- wisc.pr$x[,1]
PC2 <- wisc.pr$x[,2]
ggplot(df$diagnosis, aes(PC1, PC2)) + 
  geom_point()
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-17-1.png)

\###Variance explained:

``` r
pr.var <- wisc.pr$sdev^2
head(pr.var)
```

    [1] 13.281608  5.691355  2.817949  1.980640  1.648731  1.207357

``` r
pve <- pr.var / sum(pr.var)

plot(pve, xlab= "Principle Component", ylab= "Proportion of Variance Explained", ylim= c(0,1), type = "o")
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-19-1.png)

``` r
barplot(pve, ylab = "Precent of Variance Explained",
     names.arg=paste0("PC",1:length(pve)), las=2, axes = FALSE)
axis(2, at=pve, labels=round(pve,2)*100 )
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-20-1.png)

\###Communicating PCA Results:

> Question 9: For the first principal component, what is the component
> of the loading vector (i.e. wisc.pr\$rotation\[,1\]) for the feature
> concave.points_mean?

``` r
wisc.pr$rotation["concave.points_mean", 1]
```

    [1] -0.2608538

> Q10. What is the minimum number of principal components required to
> explain 80% of the variance of the data?

``` r
cumm_variance <- cumsum(wisc.pr$sdev^2) / sum(wisc.pr$sdev^2) 
sum(cumm_variance <=0.8) +1
```

    [1] 5

## 3. Hierarchal Clustering

``` r
# distance matrix needed for hclust

data.scaled <- scale(wisc.data)

data.dist <- dist(data.scaled)
wisc.hclust <- hclust(data.dist, method= "complete")
plot(wisc.hclust)
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-23-1.png)

> Question 11: Using the plot() and abline() functions, what is the
> height at which the clustering model has 4 clusters?

``` r
plot(wisc.hclust)
abline(h=20, col="red", lty=2)
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-24-1.png)

For question 11, the height at which the clustering model has 4 clusters
is at about 20

> Question 12: Can you find a better cluster vs diagnoses match by
> cutting into a different number of clusters between 2 and 10?

``` r
wisc.pr.hclust <- hclust(data.dist, method="ward.D2")
wisc.hclust.clusters <- cutree(wisc.pr.hclust, k= 2:10)
wisc.hclust.clusters
```

              2 3 4 5 6 7 8 9 10
    842302    1 1 1 1 1 1 1 1  1
    842517    1 1 1 2 2 2 2 2  2
    84300903  1 1 1 1 1 1 1 1  1
    84348301  1 2 2 3 3 3 3 3  3
    84358402  1 1 1 2 2 2 2 2  2
    843786    1 2 2 3 3 3 3 3  3
    844359    1 1 1 2 2 2 2 2  2
    84458202  1 2 2 3 3 3 3 3  3
    844981    1 2 2 3 3 3 3 3  3
    84501001  1 2 2 3 3 3 3 3  3
    845636    2 3 3 4 4 4 4 4  4
    84610002  2 3 3 4 4 4 4 4  4
    846226    1 1 1 1 1 1 1 1  5
    846381    2 3 3 4 4 4 4 4  4
    84667401  1 2 2 3 3 3 3 3  3
    84799002  1 2 2 3 3 3 3 3  3
    848406    2 3 3 4 4 4 4 4  4
    84862001  1 2 2 3 3 3 3 3  3
    849014    1 1 1 2 2 2 2 2  2
    8510426   2 3 3 4 4 4 5 5  6
    8510653   2 3 3 4 4 4 5 5  6
    8510824   2 3 3 4 4 4 5 5  6
    8511133   1 2 2 3 3 3 3 3  3
    851509    1 1 1 2 2 2 2 2  2
    852552    1 1 1 1 1 1 1 1  1
    852631    1 1 1 1 1 1 1 1  1
    852763    1 2 2 3 3 3 3 3  3
    852781    1 1 1 2 2 2 2 2  2
    852973    1 2 2 3 3 3 3 3  3
    853201    1 1 1 2 2 2 2 2  2
    853401    1 1 1 1 1 1 1 1  1
    853612    1 2 2 3 3 3 3 3  3
    85382601  1 1 1 1 1 1 1 1  1
    854002    1 1 1 1 1 1 1 1  1
    854039    2 3 3 4 4 4 4 4  4
    854253    1 2 2 3 3 3 3 3  3
    854268    2 3 3 4 4 4 4 4  4
    854941    2 3 3 4 5 5 6 6  7
    855133    2 3 3 4 4 4 4 4  4
    855138    2 3 3 4 4 4 4 4  4
    855167    2 3 3 4 4 4 5 5  6
    855563    1 2 2 3 3 3 3 3  3
    855625    1 1 1 1 1 1 1 1  5
    856106    2 3 3 4 4 4 4 4  4
    85638502  2 3 3 4 4 4 4 4  4
    857010    1 1 1 1 1 1 1 1  1
    85713702  2 3 3 4 5 5 6 6  7
    85715     1 2 2 3 3 3 3 3  3
    857155    2 3 3 4 4 4 5 5  6
    857156    2 3 3 4 4 4 4 4  4
    857343    2 3 3 4 5 5 6 6  7
    857373    2 3 3 4 4 4 5 5  6
    857374    2 3 3 4 4 4 5 5  6
    857392    1 1 1 2 2 2 2 2  2
    857438    2 3 3 4 4 4 4 4  4
    85759902  2 3 3 4 4 4 5 5  6
    857637    1 1 1 2 2 2 2 2  2
    857793    2 3 3 4 4 4 4 4  4
    857810    2 3 3 4 5 5 6 6  7
    858477    2 3 3 4 4 4 5 5  6
    858970    2 3 3 4 5 5 6 7  8
    858981    2 3 3 4 5 5 6 7  8
    858986    1 2 2 3 3 3 3 3  3
    859196    2 3 3 4 4 4 5 5  6
    85922302  1 2 2 3 3 3 3 3  3
    859283    1 2 2 3 3 3 3 3  3
    859464    2 3 3 4 5 5 6 7  8
    859465    2 3 3 4 5 5 6 6  7
    859471    1 2 4 5 6 6 7 8  9
    859487    2 3 3 4 4 4 5 5  6
    859575    1 1 1 2 2 2 2 2  2
    859711    1 2 4 5 6 6 7 8  9
    859717    1 1 1 1 1 1 1 1  1
    859983    2 3 3 4 4 4 4 4  4
    8610175   2 3 3 4 4 4 5 5  6
    8610404   1 1 1 2 2 2 2 2  2
    8610629   2 3 3 4 5 5 6 7  8
    8610637   1 1 1 1 1 1 1 1  1
    8610862   1 1 1 1 1 1 1 1  5
    8610908   2 3 3 4 4 4 5 5  6
    861103    2 3 3 4 5 5 6 7  8
    8611161   2 3 3 4 4 4 4 4  4
    8611555   1 1 1 1 1 1 1 1  1
    8611792   1 1 1 1 1 1 1 1  1
    8612080   2 3 3 4 4 4 5 5  6
    8612399   1 1 1 2 2 2 2 2  2
    86135501  2 3 3 4 4 4 4 4  4
    86135502  1 1 1 1 1 1 1 1  1
    861597    2 3 3 4 4 4 4 4  4
    861598    1 2 2 3 3 3 3 3  3
    861648    2 3 3 4 4 4 4 4  4
    861799    2 3 3 4 4 4 4 4  4
    861853    2 3 3 4 4 4 5 5  6
    862009    2 3 3 4 4 4 5 5  6
    862028    1 2 2 3 3 3 3 3  3
    86208     1 1 1 2 2 2 2 2  2
    86211     2 3 3 4 4 4 5 5  6
    862261    2 3 3 4 4 4 5 5  6
    862485    2 3 3 4 4 4 5 5  6
    862548    2 3 3 4 4 4 4 4  4
    862717    2 3 3 4 4 4 4 4  4
    862722    2 3 3 4 5 5 6 7  8
    862965    2 3 3 4 5 5 6 6  7
    862980    2 3 3 4 4 4 5 5  6
    862989    2 3 3 4 5 5 6 6  7
    863030    1 2 2 3 3 3 3 3  3
    863031    1 2 2 3 3 3 3 3  3
    863270    2 3 3 4 4 4 5 5  6
    86355     1 1 1 1 1 1 1 1  5
    864018    2 3 3 4 5 5 6 6  7
    864033    2 3 3 4 5 5 6 7  8
    86408     2 3 3 4 5 5 6 7  8
    86409     1 2 4 5 6 6 7 8  9
    864292    2 3 3 4 5 5 6 7  8
    864496    2 3 3 4 4 4 5 5  6
    864685    2 3 3 4 4 4 5 5  6
    864726    2 3 3 4 5 5 6 7  8
    864729    1 2 2 3 3 3 3 3  3
    864877    1 2 2 3 3 3 3 3  3
    865128    2 3 3 4 4 4 4 4  4
    865137    2 3 3 4 4 4 5 5  6
    86517     1 1 1 2 2 2 2 2  2
    865423    1 1 1 1 1 1 1 1  5
    865432    2 3 3 4 4 4 5 5  6
    865468    2 3 3 4 4 4 5 5  6
    86561     2 3 3 4 4 4 5 5  6
    866083    2 3 3 4 4 4 4 4  4
    866203    2 3 3 4 4 4 4 4  4
    866458    1 2 2 3 3 3 3 3  3
    866674    1 1 1 1 1 1 1 1  1
    866714    2 3 3 4 4 4 5 5  6
    8670      1 2 2 3 3 3 3 3  3
    86730502  2 3 3 4 4 4 4 4  4
    867387    2 3 3 4 4 4 5 5  6
    867739    1 1 1 2 2 2 2 2  2
    868202    2 3 3 4 5 5 6 6  7
    868223    2 3 3 4 4 4 5 5  6
    868682    2 3 3 4 4 4 5 5  6
    868826    1 1 1 2 2 2 2 2  2
    868871    2 3 3 4 4 4 5 5  6
    868999    2 3 3 4 5 5 6 6  7
    869104    1 1 1 2 2 2 2 2  2
    869218    2 3 3 4 4 4 5 5  6
    869224    2 3 3 4 4 4 5 5  6
    869254    2 3 3 4 4 4 5 5  6
    869476    2 3 3 4 5 5 6 7  8
    869691    1 2 2 3 3 3 3 3  3
    86973701  2 3 3 4 4 4 5 5  6
    86973702  2 3 3 4 4 4 5 5  6
    869931    2 3 3 4 4 4 5 5  6
    871001501 2 3 3 4 5 5 6 7  8
    871001502 1 2 4 5 6 6 7 8  9
    8710441   1 2 4 5 6 6 7 8  9
    87106     2 3 3 4 4 4 5 5  6
    8711002   2 3 3 4 4 4 5 5  6
    8711003   2 3 3 4 4 4 5 5  6
    8711202   1 1 1 2 2 2 2 2  2
    8711216   2 3 3 4 4 4 4 4  4
    871122    2 3 3 4 4 4 5 5  6
    871149    2 3 3 4 4 4 5 5  6
    8711561   2 3 3 4 5 5 6 7  8
    8711803   1 1 1 2 2 2 2 2  2
    871201    1 1 1 1 1 1 1 1  1
    8712064   2 3 3 4 4 4 4 4  4
    8712289   1 1 1 2 2 2 2 2  2
    8712291   2 3 3 4 4 4 5 5  6
    87127     2 3 3 4 4 4 5 5  6
    8712729   1 1 1 2 2 2 2 2  2
    8712766   1 1 1 1 1 1 1 1  1
    8712853   2 3 3 4 4 4 5 5  6
    87139402  2 3 3 4 4 4 5 5  6
    87163     2 3 3 4 4 4 4 4  4
    87164     1 2 2 3 3 3 3 3  3
    871641    2 3 3 4 5 5 6 7  8
    871642    2 3 3 4 5 5 6 6  7
    872113    2 3 3 4 5 5 6 6  7
    872608    1 2 4 5 6 6 7 8  9
    87281702  1 2 2 3 3 3 3 3  3
    873357    2 3 3 4 4 4 5 5  6
    873586    2 3 3 4 4 4 5 5  6
    873592    1 1 1 1 1 1 1 1  1
    873593    1 1 1 1 1 1 1 1  1
    873701    2 3 3 4 4 4 4 4  4
    873843    2 3 3 4 4 4 5 5  6
    873885    2 3 3 4 4 4 4 4  4
    874158    2 3 3 4 5 5 6 6  7
    874217    1 1 1 2 2 2 2 2  2
    874373    2 3 3 4 4 4 5 5  6
    874662    2 3 3 4 5 5 6 6  7
    874839    2 3 3 4 4 4 5 5  6
    874858    1 2 2 3 3 3 3 3  3
    875093    2 3 3 4 4 4 5 5  6
    875099    2 3 3 4 5 5 6 6  7
    875263    1 2 2 3 3 3 3 3  3
    87556202  1 2 2 3 3 3 3 3  3
    875878    2 3 3 4 4 4 5 5  6
    875938    2 3 3 4 4 4 4 4  4
    877159    2 3 3 4 4 4 4 4  4
    877486    1 1 1 1 1 1 1 1  1
    877500    2 3 3 4 4 4 4 4  4
    877501    2 3 3 4 4 4 4 4  4
    877989    1 1 1 2 2 2 2 2  2
    878796    1 1 1 1 1 1 1 1  1
    87880     1 2 2 3 3 3 3 3  3
    87930     2 3 3 4 4 4 4 4  4
    879523    2 3 3 4 4 4 5 5  6
    879804    2 3 3 4 4 4 5 5  6
    879830    2 3 3 4 4 4 4 4  4
    8810158   2 3 3 4 4 4 4 4  4
    8810436   2 3 3 4 4 4 5 5  6
    881046502 1 1 1 2 2 2 2 2  2
    8810528   2 3 3 4 4 4 5 5  6
    8810703   1 1 1 1 1 7 8 9 10
    881094802 1 2 4 5 6 6 7 8  9
    8810955   1 2 2 3 3 3 3 3  3
    8810987   2 3 3 4 4 4 4 4  4
    8811523   2 3 3 4 5 5 6 7  8
    8811779   2 3 3 4 4 4 5 5  6
    8811842   1 1 1 2 2 2 2 2  2
    88119002  1 1 1 1 1 1 1 1  1
    8812816   2 3 3 4 4 4 5 5  6
    8812818   2 3 3 4 4 4 5 5  6
    8812844   2 3 3 4 4 4 5 5  6
    8812877   2 3 3 4 4 4 4 4  4
    8813129   2 3 3 4 4 4 5 5  6
    88143502  2 3 3 4 4 4 5 5  6
    88147101  2 3 3 4 4 4 5 5  6
    88147102  2 3 3 4 4 4 5 5  6
    88147202  2 3 3 4 4 4 4 4  4
    881861    1 2 2 3 3 3 3 3  3
    881972    1 2 2 3 3 3 3 3  3
    88199202  2 3 3 4 5 5 6 6  7
    88203002  2 3 3 4 5 5 6 6  7
    88206102  1 1 1 2 2 2 2 2  2
    882488    2 3 3 4 5 5 6 6  7
    88249602  2 3 3 4 4 4 4 4  4
    88299702  1 1 1 1 1 1 1 1  1
    883263    1 1 1 2 2 2 2 2  2
    883270    2 3 3 4 5 5 6 6  7
    88330202  1 1 1 2 2 2 2 2  2
    88350402  2 3 3 4 4 4 5 5  6
    883539    2 3 3 4 4 4 5 5  6
    883852    1 2 4 5 6 6 7 8  9
    88411702  2 3 3 4 4 4 5 5  6
    884180    1 1 1 2 2 2 2 2  2
    884437    2 3 3 4 5 5 6 7  8
    884448    2 3 3 4 4 4 5 5  6
    884626    2 3 3 4 4 4 5 5  6
    88466802  2 3 3 4 5 5 6 6  7
    884689    2 3 3 4 4 4 5 5  6
    884948    1 1 1 1 1 1 1 1  1
    88518501  2 3 3 4 4 4 5 5  6
    885429    1 1 1 1 1 1 1 1  1
    8860702   1 1 1 2 2 2 2 2  2
    886226    1 1 1 2 2 2 2 2  2
    886452    2 3 3 4 4 4 5 5  6
    88649001  1 1 1 1 1 1 1 1  1
    886776    1 2 2 3 3 3 3 3  3
    887181    1 1 1 1 1 1 1 1  5
    88725602  1 2 2 3 3 3 3 3  3
    887549    1 1 1 2 2 2 2 2  2
    888264    2 3 3 4 4 4 4 4  4
    888570    1 1 1 2 2 2 2 2  2
    889403    2 3 3 4 4 4 5 5  6
    889719    1 1 1 2 2 2 2 2  2
    88995002  1 1 1 1 1 1 1 1  1
    8910251   2 3 3 4 4 4 5 5  6
    8910499   2 3 3 4 4 4 4 4  4
    8910506   2 3 3 4 4 4 5 5  6
    8910720   2 3 3 4 5 5 6 7  8
    8910721   2 3 3 4 4 4 5 5  6
    8910748   2 3 3 4 4 4 5 5  6
    8910988   1 1 1 1 1 1 1 1  1
    8910996   2 3 3 4 5 5 6 6  7
    8911163   2 3 3 4 4 4 4 4  4
    8911164   2 3 3 4 5 5 6 7  8
    8911230   2 3 3 4 4 4 5 5  6
    8911670   2 3 3 4 4 4 4 4  4
    8911800   2 3 3 4 4 4 5 5  6
    8911834   2 3 3 4 4 4 5 5  6
    8912049   1 1 1 1 1 1 1 1  1
    8912055   2 3 3 4 4 4 5 5  6
    89122     1 1 1 2 2 2 2 2  2
    8912280   1 2 2 3 3 3 3 3  3
    8912284   2 3 3 4 4 4 5 5  6
    8912521   2 3 3 4 5 5 6 6  7
    8912909   2 3 3 4 4 4 5 5  6
    8913      2 3 3 4 4 4 5 5  6
    8913049   2 3 3 4 5 5 6 7  8
    89143601  2 3 3 4 5 5 6 6  7
    89143602  1 2 4 5 6 6 7 8  9
    8915      2 3 3 4 4 4 4 4  4
    891670    2 3 3 4 4 4 5 5  6
    891703    2 3 3 4 4 4 5 5  6
    891716    2 3 3 4 4 4 5 5  6
    891923    2 3 3 4 4 4 5 5  6
    891936    2 3 3 4 5 5 6 6  7
    892189    2 3 3 4 4 4 5 5  6
    892214    2 3 3 4 4 4 5 5  6
    892399    2 3 3 4 5 5 6 6  7
    892438    1 1 1 1 1 1 1 1  1
    892604    2 3 3 4 4 4 5 5  6
    89263202  1 1 1 1 1 1 1 1  1
    892657    2 3 3 4 4 4 5 5  6
    89296     2 3 3 4 4 4 5 5  6
    893061    2 3 3 4 5 5 6 6  7
    89344     2 3 3 4 4 4 5 5  6
    89346     2 3 3 4 5 5 6 6  7
    893526    2 3 3 4 4 4 5 5  6
    893548    2 3 3 4 4 4 5 5  6
    893783    2 3 3 4 4 4 5 5  6
    89382601  2 3 3 4 4 4 5 5  6
    89382602  2 3 3 4 4 4 5 5  6
    893988    2 3 3 4 4 4 5 5  6
    894047    2 3 3 4 5 5 6 7  8
    894089    2 3 3 4 4 4 5 5  6
    894090    2 3 3 4 4 4 5 5  6
    894326    1 1 1 2 2 2 2 2  2
    894329    1 2 4 5 6 6 7 8  9
    894335    2 3 3 4 5 5 6 6  7
    894604    2 3 3 4 5 5 6 7  8
    894618    2 3 3 4 4 4 4 4  4
    894855    2 3 3 4 4 4 5 5  6
    895100    1 1 1 1 1 1 1 1  1
    89511501  2 3 3 4 4 4 5 5  6
    89511502  2 3 3 4 4 4 5 5  6
    89524     2 3 3 4 4 4 5 5  6
    895299    2 3 3 4 4 4 5 5  6
    8953902   1 2 2 3 3 3 3 3  3
    895633    2 3 3 4 4 4 4 4  4
    896839    1 2 2 3 3 3 3 3  3
    896864    2 3 3 4 4 4 5 5  6
    897132    2 3 3 4 5 5 6 6  7
    897137    2 3 3 4 4 4 5 5  6
    897374    2 3 3 4 5 5 6 6  7
    89742801  1 1 1 2 2 2 2 2  2
    897604    2 3 3 4 4 4 5 5  6
    897630    1 1 1 1 1 1 1 1  1
    897880    2 3 3 4 4 4 5 5  6
    89812     1 1 1 1 1 1 1 1  1
    89813     2 3 3 4 4 4 5 5  6
    898143    2 3 3 4 4 4 5 5  6
    89827     2 3 3 4 4 4 5 5  6
    898431    1 1 1 2 2 2 2 2  2
    89864002  2 3 3 4 4 4 5 5  6
    898677    2 3 3 4 5 5 6 7  8
    898678    2 3 3 4 5 5 6 6  7
    89869     2 3 3 4 4 4 5 5  6
    898690    2 3 3 4 5 5 6 6  7
    899147    2 3 3 4 5 5 6 7  8
    899187    2 3 3 4 4 4 5 5  6
    899667    1 2 2 3 3 3 3 3  3
    899987    1 1 1 1 1 1 1 1  1
    9010018   2 3 3 4 4 4 4 4  4
    901011    2 3 3 4 4 4 5 5  6
    9010258   2 3 3 4 4 4 5 5  6
    9010259   2 3 3 4 5 5 6 7  8
    901028    2 3 3 4 4 4 5 5  6
    9010333   2 3 3 4 4 4 5 5  6
    901034301 2 3 3 4 4 4 5 5  6
    901034302 2 3 3 4 4 4 5 5  6
    901041    2 3 3 4 4 4 4 4  4
    9010598   2 3 3 4 4 4 5 5  6
    9010872   2 3 3 4 4 4 4 4  4
    9010877   2 3 3 4 4 4 5 5  6
    901088    1 1 1 2 2 2 2 2  2
    9011494   1 1 1 2 2 2 2 2  2
    9011495   2 3 3 4 4 4 5 5  6
    9011971   1 1 1 1 1 1 1 1  1
    9012000   1 1 1 1 1 1 1 1  1
    9012315   1 2 2 3 3 3 3 3  3
    9012568   2 3 3 4 4 4 5 5  6
    9012795   1 1 1 1 1 1 1 1  1
    901288    1 1 1 2 2 2 2 2  2
    9013005   2 3 3 4 4 4 5 5  6
    901303    2 3 3 4 4 4 5 5  6
    901315    1 2 4 5 6 6 7 8  9
    9013579   2 3 3 4 5 5 6 6  7
    9013594   2 3 3 4 4 4 5 5  6
    9013838   1 2 2 3 3 3 3 3  3
    901549    2 3 3 4 4 4 5 5  6
    901836    2 3 3 4 4 4 5 5  6
    90250     2 3 3 4 4 4 5 5  6
    90251     2 3 3 4 4 4 5 5  6
    902727    2 3 3 4 4 4 5 5  6
    90291     2 3 3 4 4 4 4 4  4
    902975    2 3 3 4 4 4 5 5  6
    902976    2 3 3 4 4 4 5 5  6
    903011    2 3 3 4 5 5 6 7  8
    90312     1 1 1 2 2 2 2 2  2
    90317302  2 3 3 4 4 4 5 5  6
    903483    2 3 3 4 5 5 6 7  8
    903507    1 2 2 3 3 3 3 3  3
    903516    1 1 1 1 1 1 1 1  1
    903554    2 3 3 4 4 4 5 5  6
    903811    2 3 3 4 4 4 5 5  6
    90401601  2 3 3 4 4 4 4 4  4
    90401602  2 3 3 4 4 4 5 5  6
    904302    2 3 3 4 4 4 5 5  6
    904357    2 3 3 4 4 4 5 5  6
    90439701  1 1 1 1 1 1 1 1  1
    904647    2 3 3 4 4 4 5 5  6
    904689    2 3 3 4 4 4 5 5  6
    9047      2 3 3 4 4 4 5 5  6
    904969    2 3 3 4 5 5 6 6  7
    904971    2 3 3 4 4 4 5 5  6
    905189    2 3 3 4 4 4 5 5  6
    905190    2 3 3 4 4 4 5 5  6
    90524101  1 1 1 2 2 2 2 2  2
    905501    2 3 3 4 5 5 6 6  7
    905502    2 3 3 4 5 5 6 6  7
    905520    2 3 3 4 4 4 5 5  6
    905539    2 3 3 4 5 5 6 6  7
    905557    2 3 3 4 4 4 4 4  4
    905680    2 3 3 4 5 5 6 6  7
    905686    2 3 3 4 4 4 5 5  6
    905978    2 3 3 4 5 5 6 7  8
    90602302  1 1 1 1 1 1 1 1  1
    906024    2 3 3 4 4 4 5 5  6
    906290    2 3 3 4 5 5 6 6  7
    906539    2 3 3 4 5 5 6 6  7
    906564    1 2 2 3 3 3 3 3  3
    906616    2 3 3 4 4 4 5 5  6
    906878    2 3 3 4 4 4 4 4  4
    907145    2 3 3 4 5 5 6 7  8
    907367    2 3 3 4 5 5 6 6  7
    907409    2 3 3 4 4 4 5 5  6
    90745     2 3 3 4 5 5 6 6  7
    90769601  2 3 3 4 4 4 5 5  6
    90769602  2 3 3 4 4 4 5 5  6
    907914    1 2 2 3 3 3 3 3  3
    907915    2 3 3 4 5 5 6 7  8
    908194    1 1 1 1 1 1 1 1  1
    908445    1 1 1 2 2 2 2 2  2
    908469    2 3 3 4 4 4 5 5  6
    908489    2 3 3 4 4 4 4 4  4
    908916    2 3 3 4 4 4 5 5  6
    909220    2 3 3 4 4 4 5 5  6
    909231    2 3 3 4 4 4 5 5  6
    909410    2 3 3 4 4 4 5 5  6
    909411    2 3 3 4 4 4 5 5  6
    909445    1 1 1 2 2 2 2 2  2
    90944601  2 3 3 4 4 4 5 5  6
    909777    2 3 3 4 5 5 6 6  7
    9110127   1 1 1 2 2 2 2 2  2
    9110720   2 3 3 4 4 4 4 4  4
    9110732   1 1 1 2 2 2 2 2  2
    9110944   2 3 3 4 4 4 5 5  6
    911150    2 3 3 4 4 4 4 4  4
    911157302 1 1 1 2 2 2 2 2  2
    9111596   2 3 3 4 4 4 5 5  6
    9111805   1 1 1 2 2 2 2 2  2
    9111843   2 3 3 4 5 5 6 6  7
    911201    2 3 3 4 4 4 5 5  6
    911202    2 3 3 4 4 4 5 5  6
    9112085   2 3 3 4 5 5 6 6  7
    9112366   2 3 3 4 5 5 6 6  7
    9112367   2 3 3 4 5 5 6 6  7
    9112594   2 3 3 4 5 5 6 6  7
    9112712   2 3 3 4 5 5 6 6  7
    911296201 1 1 1 1 1 1 1 1  1
    911296202 1 1 1 1 1 7 8 9 10
    9113156   2 3 3 4 5 5 6 6  7
    911320501 2 3 3 4 4 4 5 5  6
    911320502 2 3 3 4 4 4 5 5  6
    9113239   2 3 3 4 4 4 5 5  6
    9113455   2 3 3 4 4 4 4 4  4
    9113514   2 3 3 4 5 5 6 6  7
    9113538   1 1 1 1 1 1 1 1  1
    911366    1 2 2 3 3 3 3 3  3
    9113778   2 3 3 4 5 5 6 6  7
    9113816   2 3 3 4 5 5 6 6  7
    911384    2 3 3 4 4 4 5 5  6
    9113846   2 3 3 4 5 5 6 6  7
    911391    2 3 3 4 4 4 5 5  6
    911408    2 3 3 4 4 4 5 5  6
    911654    2 3 3 4 4 4 4 4  4
    911673    2 3 3 4 4 4 5 5  6
    911685    2 3 3 4 4 4 5 5  6
    911916    1 2 2 3 3 3 3 3  3
    912193    2 3 3 4 4 4 5 5  6
    91227     2 3 3 4 4 4 5 5  6
    912519    2 3 3 4 4 4 5 5  6
    912558    2 3 3 4 4 4 5 5  6
    912600    2 3 3 4 4 4 5 5  6
    913063    1 2 4 5 6 6 7 8  9
    913102    2 3 3 4 4 4 5 5  6
    913505    1 1 1 1 1 1 1 1  1
    913512    2 3 3 4 4 4 5 5  6
    913535    2 3 3 4 4 4 4 4  4
    91376701  2 3 3 4 5 5 6 6  7
    91376702  2 3 3 4 4 4 5 5  6
    914062    1 1 1 2 2 2 2 2  2
    914101    2 3 3 4 5 5 6 6  7
    914102    2 3 3 4 4 4 4 4  4
    914333    2 3 3 4 4 4 4 4  4
    914366    2 3 3 4 4 4 4 4  4
    914580    2 3 3 4 4 4 5 5  6
    914769    1 1 1 2 2 2 2 2  2
    91485     1 1 1 1 1 1 1 1  1
    914862    2 3 3 4 4 4 5 5  6
    91504     1 2 2 3 3 3 3 3  3
    91505     2 3 3 4 4 4 5 5  6
    915143    1 1 1 1 1 1 1 1  1
    915186    1 2 4 5 6 6 7 8  9
    915276    1 2 4 5 6 6 7 8  9
    91544001  2 3 3 4 4 4 4 4  4
    91544002  2 3 3 4 5 5 6 7  8
    915452    2 3 3 4 4 4 5 5  6
    915460    1 2 2 3 3 3 3 3  3
    91550     2 3 3 4 4 4 5 5  6
    915664    2 3 3 4 4 4 5 5  6
    915691    1 2 2 3 3 3 3 3  3
    915940    2 3 3 4 4 4 5 5  6
    91594602  2 3 3 4 4 4 4 4  4
    916221    2 3 3 4 4 4 5 5  6
    916799    1 1 1 2 2 2 2 2  2
    916838    1 1 1 2 2 2 2 2  2
    917062    2 3 3 4 4 4 5 5  6
    917080    2 3 3 4 4 4 5 5  6
    917092    2 3 3 4 5 5 6 7  8
    91762702  1 1 1 1 1 1 1 1  1
    91789     2 3 3 4 5 5 6 6  7
    917896    2 3 3 4 4 4 4 4  4
    917897    2 3 3 4 4 4 5 5  6
    91805     2 3 3 4 4 4 5 5  6
    91813701  2 3 3 4 4 4 4 4  4
    91813702  2 3 3 4 4 4 5 5  6
    918192    2 3 3 4 5 5 6 7  8
    918465    2 3 3 4 4 4 5 5  6
    91858     2 3 3 4 4 4 5 5  6
    91903901  2 3 3 4 4 4 4 4  4
    91903902  2 3 3 4 4 4 5 5  6
    91930402  1 1 1 2 2 2 2 2  2
    919537    2 3 3 4 4 4 5 5  6
    919555    1 1 1 1 1 1 1 1  1
    91979701  2 3 3 4 4 4 4 4  4
    919812    1 2 2 3 3 3 3 3  3
    921092    2 3 3 4 5 5 6 6  7
    921362    1 2 4 5 6 6 7 8  9
    921385    2 3 3 4 5 5 6 7  8
    921386    2 3 3 4 4 4 4 4  4
    921644    2 3 3 4 4 4 4 4  4
    922296    2 3 3 4 5 5 6 6  7
    922297    2 3 3 4 4 4 5 5  6
    922576    2 3 3 4 4 4 4 4  4
    922577    2 3 3 4 4 4 5 5  6
    922840    2 3 3 4 4 4 5 5  6
    923169    2 3 3 4 5 5 6 6  7
    923465    2 3 3 4 5 5 6 6  7
    923748    2 3 3 4 5 5 6 6  7
    923780    2 3 3 4 4 4 5 5  6
    924084    2 3 3 4 5 5 6 6  7
    924342    2 3 3 4 5 5 6 6  7
    924632    2 3 3 4 5 5 6 6  7
    924934    2 3 3 4 5 5 6 6  7
    924964    2 3 3 4 5 5 6 6  7
    925236    2 3 3 4 5 5 6 6  7
    925277    2 3 3 4 4 4 4 4  4
    925291    2 3 3 4 5 5 6 6  7
    925292    2 3 3 4 4 4 4 4  4
    925311    2 3 3 4 5 5 6 6  7
    925622    1 2 2 3 3 3 3 3  3
    926125    1 1 1 1 1 1 1 1  1
    926424    1 1 1 1 1 1 1 1  1
    926682    1 1 1 2 2 2 2 2  2
    926954    1 1 1 2 2 2 2 2  2
    927241    1 1 1 1 1 1 1 1  1
    92751     2 3 3 4 5 5 6 6  7

For Question 12, I think I can not find a better cluster vs diagnoses
match by cutting into different clusters.

> Question 13: Which method gives your favorite results for the same
> data.dist dataset? Explain your reasoning.

``` r
d <- dist(wisc.pr$x[,2:10])
wisc.pr.hclust <- hclust(d, method="ward.D2")
wisc.pr.hclust
```


    Call:
    hclust(d = d, method = "ward.D2")

    Cluster method   : ward.D2 
    Distance         : euclidean 
    Number of objects: 569 

For Question 13, `ward.d2` is the best method because it makes clusters
with smaller variance.

## 5. Combining Methods:

This approach will take PCA results and not our original data.

``` r
d <- dist(wisc.pr$x[,1:7])
wisc.pr.hclust <- hclust(d, method="ward.D2")
plot(wisc.pr.hclust)
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-27-1.png)

``` r
grps <- cutree(wisc.pr.hclust, k=2)
table(grps) 
```

    grps
      1   2 
    216 353 

``` r
plot(wisc.pr$x[,1], wisc.pr$x[,2], col=grps )
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-29-1.png)

``` r
g <- as.factor(grps)
levels(g)
```

    [1] "1" "2"

``` r
g <- relevel(g,2)
levels(g)
```

    [1] "2" "1"

``` r
plot(wisc.pr$x[,1:2], col=g)
```

![](Mini-lab_files/figure-commonmark/unnamed-chunk-31-1.png)

> Question 15: How well does the newly created model with four clusters
> separate out the two diagnoses?

``` r
wisc.pr.hclust.S <- dist(wisc.pr$x[,1:7])

wisc.pr.hclust <- hclust(wisc.pr.hclust.S, method="ward.D2")
wisc.pr.hclust
```


    Call:
    hclust(d = wisc.pr.hclust.S, method = "ward.D2")

    Cluster method   : ward.D2 
    Distance         : euclidean 
    Number of objects: 569 

``` r
wisc.pr.hclust.clusters <- cutree(wisc.pr.hclust, k=2)
wisc.pr.hclust.clusters
```

       842302    842517  84300903  84348301  84358402    843786    844359  84458202 
            1         1         1         1         1         1         1         1 
       844981  84501001    845636  84610002    846226    846381  84667401  84799002 
            1         1         2         1         1         1         1         1 
       848406  84862001    849014   8510426   8510653   8510824   8511133    851509 
            1         1         1         2         2         2         1         1 
       852552    852631    852763    852781    852973    853201    853401    853612 
            1         1         1         1         1         1         1         1 
     85382601    854002    854039    854253    854268    854941    855133    855138 
            1         1         1         1         2         2         1         2 
       855167    855563    855625    856106  85638502    857010  85713702     85715 
            2         1         1         1         2         1         2         1 
       857155    857156    857343    857373    857374    857392    857438  85759902 
            2         2         2         2         2         1         2         2 
       857637    857793    857810    858477    858970    858981    858986    859196 
            1         1         2         2         2         2         1         2 
     85922302    859283    859464    859465    859471    859487    859575    859711 
            1         1         2         2         1         2         1         1 
       859717    859983   8610175   8610404   8610629   8610637   8610862   8610908 
            1         2         2         1         2         1         1         2 
       861103   8611161   8611555   8611792   8612080   8612399  86135501  86135502 
            2         1         1         1         2         1         1         1 
       861597    861598    861648    861799    861853    862009    862028     86208 
            2         1         2         1         2         2         1         1 
        86211    862261    862485    862548    862717    862722    862965    862980 
            2         2         2         2         2         2         2         2 
       862989    863030    863031    863270     86355    864018    864033     86408 
            2         1         2         2         1         2         2         2 
        86409    864292    864496    864685    864726    864729    864877    865128 
            1         2         2         2         1         1         1         1 
       865137     86517    865423    865432    865468     86561    866083    866203 
            2         1         1         2         2         2         2         1 
       866458    866674    866714      8670  86730502    867387    867739    868202 
            1         1         2         1         1         2         1         2 
       868223    868682    868826    868871    868999    869104    869218    869224 
            2         2         1         2         2         1         2         2 
       869254    869476    869691  86973701  86973702    869931 871001501 871001502 
            2         2         1         2         2         2         2         1 
      8710441     87106   8711002   8711003   8711202   8711216    871122    871149 
            1         2         2         2         1         1         2         2 
      8711561   8711803    871201   8712064   8712289   8712291     87127   8712729 
            2         1         1         2         1         2         2         1 
      8712766   8712853  87139402     87163     87164    871641    871642    872113 
            1         2         2         2         1         2         2         2 
       872608  87281702    873357    873586    873592    873593    873701    873843 
            1         1         2         2         1         1         1         2 
       873885    874158    874217    874373    874662    874839    874858    875093 
            2         2         1         2         2         2         1         2 
       875099    875263  87556202    875878    875938    877159    877486    877500 
            2         1         1         2         1         1         1         1 
       877501    877989    878796     87880     87930    879523    879804    879830 
            2         1         1         1         2         2         2         1 
      8810158   8810436 881046502   8810528   8810703 881094802   8810955   8810987 
            1         2         1         2         1         1         1         1 
      8811523   8811779   8811842  88119002   8812816   8812818   8812844   8812877 
            2         2         1         1         2         2         2         1 
      8813129  88143502  88147101  88147102  88147202    881861    881972  88199202 
            2         2         2         2         2         1         1         2 
     88203002  88206102    882488  88249602  88299702    883263    883270  88330202 
            2         1         2         2         1         1         2         1 
     88350402    883539    883852  88411702    884180    884437    884448    884626 
            2         2         1         2         1         2         2         1 
     88466802    884689    884948  88518501    885429   8860702    886226    886452 
            2         2         1         2         1         1         1         2 
     88649001    886776    887181  88725602    887549    888264    888570    889403 
            1         1         1         1         1         2         1         2 
       889719  88995002   8910251   8910499   8910506   8910720   8910721   8910748 
            1         1         2         2         2         2         2         2 
      8910988   8910996   8911163   8911164   8911230   8911670   8911800   8911834 
            1         2         2         2         2         1         2         2 
      8912049   8912055     89122   8912280   8912284   8912521   8912909      8913 
            1         2         1         1         2         2         2         2 
      8913049  89143601  89143602      8915    891670    891703    891716    891923 
            1         2         1         2         2         2         2         2 
       891936    892189    892214    892399    892438    892604  89263202    892657 
            2         2         2         2         1         2         1         2 
        89296    893061     89344     89346    893526    893548    893783  89382601 
            2         2         2         2         2         2         2         2 
     89382602    893988    894047    894089    894090    894326    894329    894335 
            2         2         2         2         2         1         1         2 
       894604    894618    894855    895100  89511501  89511502     89524    895299 
            2         1         2         1         2         2         2         2 
      8953902    895633    896839    896864    897132    897137    897374  89742801 
            1         1         1         2         2         2         2         1 
       897604    897630    897880     89812     89813    898143     89827    898431 
            2         1         2         1         2         2         2         1 
     89864002    898677    898678     89869    898690    899147    899187    899667 
            2         2         2         2         2         2         2         1 
       899987   9010018    901011   9010258   9010259    901028   9010333 901034301 
            1         1         2         2         2         2         2         2 
    901034302    901041   9010598   9010872   9010877    901088   9011494   9011495 
            2         2         2         2         2         1         1         2 
      9011971   9012000   9012315   9012568   9012795    901288   9013005    901303 
            1         1         1         2         1         1         2         2 
       901315   9013579   9013594   9013838    901549    901836     90250     90251 
            1         2         2         1         2         2         2         2 
       902727     90291    902975    902976    903011     90312  90317302    903483 
            2         2         2         2         1         1         2         2 
       903507    903516    903554    903811  90401601  90401602    904302    904357 
            1         1         2         2         2         2         2         2 
     90439701    904647    904689      9047    904969    904971    905189    905190 
            1         2         2         2         2         2         2         2 
     90524101    905501    905502    905520    905539    905557    905680    905686 
            1         2         2         2         2         2         2         2 
       905978  90602302    906024    906290    906539    906564    906616    906878 
            2         1         2         2         2         1         2         2 
       907145    907367    907409     90745  90769601  90769602    907914    907915 
            2         2         2         2         2         2         1         2 
       908194    908445    908469    908489    908916    909220    909231    909410 
            1         1         2         2         2         2         2         2 
       909411    909445  90944601    909777   9110127   9110720   9110732   9110944 
            2         1         2         2         1         2         1         2 
       911150 911157302   9111596   9111805   9111843    911201    911202   9112085 
            2         1         2         1         2         2         2         2 
      9112366   9112367   9112594   9112712 911296201 911296202   9113156 911320501 
            2         2         2         2         1         1         2         2 
    911320502   9113239   9113455   9113514   9113538    911366   9113778   9113816 
            2         1         2         2         1         1         2         2 
       911384   9113846    911391    911408    911654    911673    911685    911916 
            2         2         2         2         2         2         2         1 
       912193     91227    912519    912558    912600    913063    913102    913505 
            2         2         2         2         2         1         2         1 
       913512    913535  91376701  91376702    914062    914101    914102    914333 
            2         1         2         1         1         2         2         2 
       914366    914580    914769     91485    914862     91504     91505    915143 
            2         2         1         1         2         1         2         1 
       915186    915276  91544001  91544002    915452    915460     91550    915664 
            1         1         2         2         2         1         2         2 
       915691    915940  91594602    916221    916799    916838    917062    917080 
            1         2         2         2         1         1         2         2 
       917092  91762702     91789    917896    917897     91805  91813701  91813702 
            2         1         2         2         2         2         2         2 
       918192    918465     91858  91903901  91903902  91930402    919537    919555 
            2         2         2         2         2         1         2         1 
     91979701    919812    921092    921362    921385    921386    921644    922296 
            2         1         2         1         2         2         2         2 
       922297    922576    922577    922840    923169    923465    923748    923780 
            2         2         2         2         2         2         2         2 
       924084    924342    924632    924934    924964    925236    925277    925291 
            2         2         2         2         2         2         2         2 
       925292    925311    925622    926125    926424    926682    926954    927241 
            2         2         1         1         1         1         1         1 
        92751 
            2 

For Qestion 15, I think the newly created model with four clusters helps
with visualization with better separation of the two diagnoses.
