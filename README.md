# The-sparks-foundation-task
> setwd("~/Desktop")
> library(caTools)
> dataset = read.csv('hours and scores.csv')
> View(dataset)
> plot(dataset$Hours~dataset$Scores)
> # Splitting the dataset into Training set and Test set
> # install.packages('catools)
> library(catools)
Error in library(catools) : there is no package called ‘catools’
> set.seed(123)
> split = sample.split(dataset$Scores, SplitRatio = 3/5)
> training_set = subset(dataset, split ==TRUE)
> test_set = subset(dataset, split ==FALSE)
> View(test_set)
> View(training_set)
> # Feature Scaling
> # training_set[, 2:3] = scale(training_set[, 2:3])
> #test_set[, 2:3] = scale(test_set[, 2:3])
> regressor = lm(formula = Scores ~ Hours,
+                data = training_set)
> summary(regressor)

Call:
lm(formula = Scores ~ Hours, data = training_set)

Residuals:
   Min     1Q Median     3Q    Max 
-6.886 -4.369  1.990  3.160  7.606 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)   2.9231     2.6470   1.104    0.289    
Hours         9.6758     0.5336  18.132  1.3e-10 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 5.158 on 13 degrees of freedom
Multiple R-squared:  0.962,	Adjusted R-squared:  0.959 
F-statistic: 328.8 on 1 and 13 DF,  p-value: 1.304e-10

> y_pred = predict(regressor, newdata = test_set)
> x_pred = predict(regressor, newdata = training_set)
> y_pred
       2        4        5        8       11       16       20       21       22       24 
52.26964 85.16733 36.78838 56.13996 77.42670 89.03764 74.52396 29.04775 49.36691 69.68606 
> x_pred
       1        3        6        7        9       10       12       13       14       15       17       18       19 
27.11259 33.88564 17.43680 91.94038 83.23217 29.04775 60.01027 46.46417 34.85322 13.56648 27.11259 21.30711 61.94543 
      23       25 
39.69112 78.39427 
> plot(training_set$Hours~training_set$Scores, main="abline")
> plot(test_set$Hours~test_set$Scores, main="scatterplot")
