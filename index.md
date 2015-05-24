---
title       : Admission Decision Predictor 
subtitle    : Helping students plan for college
author      : walkerkq
job         : 5/23/15
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Background  

### The Situation  
As a moderately selecive college, we often find that prospective applicants often underestimate their chances of acceptance. We currently accept about 30% of applicants - a percentage that can be very intimidating.  

We are in need of a way for prospective students and their guidance counselors to understand the academic profile's effect on admissions decisions, as well as help students chart out where they need to score and rank during their senior year in order to become more competitive applicants.  

### The Solution

To meet our needs, we have designed a predictor where a prospective student or guidance counselor can input a student's academic profile and in return, receive an estimated chance of acceptance.

--- 

## How it Works

The predictor is based on a representative sample (50 fictional applicants) containing GPA, ACT score, class rank and whether the applicant was accepted or not.  

The data set contains the following variables:  
- ACT: ACT Score, int, range 15-36  
- GPA: grade point average, num, range 0-4.0  
- Class.Rank: student's academic rank, num, 0-1  
- Admission.Decision: where 1 represents admission granted and 0 represents denial of admission 

---

## How it Works  

A look at the sample data:  


```r
admission <- read.csv("assets/sample_admission_data.csv", stringsAsFactors=FALSE)
```

```
## Warning in file(file, "rt"): cannot open file
## 'assets/sample_admission_data.csv': No such file or directory
```

```
## Error in file(file, "rt"): cannot open the connection
```

```r
head(admission)
```

```
##   ACT  GPA Class.Rank Admission.Decision
## 1  15 1.94     0.4327                  0
## 2  16 2.88     0.4903                  0
## 3  17 2.34     0.5379                  0
## 4  18 3.45     0.1892                  1
## 5  19 3.01     0.2600                  0
## 6  20 2.95     0.5725                  0
```

--- 

## How it Works

We then fit a linear model to the data. The model accounts for 85% of admission variance. The remaining effect is partly due to the student's essay and recommendations.  


```r
fit <- lm(Admission.Decision ~ . - 1, admission)
summary(fit)
```

```
## 
## Call:
## lm(formula = Admission.Decision ~ . - 1, data = admission)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -0.77546 -0.07464 -0.02135  0.18506  0.87994 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## ACT         0.001440   0.009688   0.149  0.88252    
## GPA         0.256037   0.076183   3.361  0.00155 ** 
## Class.Rank -1.250604   0.219825  -5.689 7.93e-07 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.3208 on 47 degrees of freedom
## Multiple R-squared:  0.8535,	Adjusted R-squared:  0.8441 
## F-statistic: 91.24 on 3 and 47 DF,  p-value: < 2.2e-16
```

---  

## Summary  

This app is meant only to estimate a student's chances of being accepted based on their academic profile - in order to help students plan our their academic goals for their final year of high school or determine their plans for college applications. Students should not underestimate the effect of good recommendations and a strong essay.    

---  
