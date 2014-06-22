---
title       : Relationship between variables and MPG
subtitle    : mtcars dataset
author      : SwhGo_oN
job         : Part2 - Reproducible Pitch Presentation
logo        : logo.jpg
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [bootstrap]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Deployed App

### Part0: Regression Models Course Project  
- URL: *http://swhgoon.github.io/devdataprod-cp/part0_regmods-mtcars.html*
- Difference of the MPG between automatic and manual transmissions is focused in Part0.

### Part1: Shiny Application  
- URL: *https://swhgoon.shinyapps.io/part1_devdataprod-shiny/*
- A shiny-App shows the relationship between variables and miles per gallon (MPG).

### Part2: Reproducible Pitch Presentation  
- URL: *http://swhgoon.github.io/devdataprod-cp/part2_devdataprod-slidify*

### Get all SourceCode @Github:

```
git clone https://github.com/swhgoon/devdataprod-cp.git
```

--- .class #id 

## mtcars dataset - Description

### Motor Trend Car Road Tests

> The data was extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973–74 models).

### Source
> Henderson and Velleman (1981), Building multiple regression models interactively. Biometrics, 37, 391–411.


```r
library(datasets)
head(mtcars, 3)
```

```
##                mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4     21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag 21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710    22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
```

---

## mtcars dataset - Format

**A data frame with 32 observations on 11 variables.**

| Index | Field | Detail |
------- | ----- | ------ |
| [, 1] | mpg | Miles/(US) gallon |
| [, 2]  | cyl | Number of cylinders |
| [, 3]	| disp | Displacement (cu.in.) |
| [, 4]	| hp | Gross horsepower |
| [, 5]	| drat | Rear axle ratio |
| [, 6]	| wt | Weight (lb/1000) |
| [, 7]	| qsec | 1/4 mile time |
| [, 8]	| vs | V/S |
| [, 9]	| am | Transmission (0 = automatic, 1 = manual) |
| [,10]	| gear | Number of forward gears |
| [,11]	| carb | Number of carburetors |

---

## Analysis - main code

```r
  formulaTextPoint <- reactive({
    paste("mpg ~", "as.integer(", input$variable, ")")  })
  
  fit <- reactive({
    lm(as.formula(formulaTextPoint()), data=mpgData)  })
  ...
  output$fit <- renderPrint({
    summary(fit()) })
  
  output$mpgPlot <- renderPlot({
    with(mpgData, {
      plot(as.formula(formulaTextPoint()))
      abline(fit(), col=2)
    })  })

```

