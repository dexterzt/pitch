---
title       : Web app for maintenance daily caloric intake
subtitle    : 
author      : 
job         : Developer
framework   : io2012       # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : bootstrap           # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
output: 
  html_document: 
    toc: yes
---

## Should I Count Calories? Yes!

*Lauren Popeck, R.D., Orlando Health*

“Counting calories provides structure, and that personal tracking is what some people need to meet their health-related goals. People also usually experience success right away when they begin tracking calories, which is a great way to help become more aware of habits and encourage behavioral change.

While calories are not the whole picture when it comes to nutrition and weight loss, for some, counting calories is easier than actually understanding the complex effects food has on our bodies. It’s also especially helpful if you hit a plateau in weight loss; it can help point out if you're eating too much or not enough. You may ever be surprised at how many calories you consume even when you're following a healthy diet.

Source: [Should You Count Calories to Lose Weight?] (http://www.shape.com/weight-loss/weight-loss-strategies/should-you-count-calories-lose-weight)

--- .class #id 

## FORMULA FOR BMR

To determine your basal metabolic rate (BMR), aka how many calories your body burns at rest, use the following formula:

W = weight in lbs
H = height in cms
A = age in years

### Men: 
BMR=66.47+ (6.25 x W) + (5.0 x H) - (6.75 x A)
### Women: 
BMR=665.09 + (4.35 x W) + (1.84 x H) - (4.67 x A)


Source: Amirkalali, Bahareh, et al. "Comparison of Harris Benedict and Mifflin-ST Jeor equations with indirect calorimetry in evaluating resting energy expenditure." Indian Journal Of Medical Sciences 62.7 (2008): 283-290. MEDLINE with Full Text. EBSCO. Web. 28 June 2010. 

--- .class #id 

## Calories burned during exercise.

Once you calculate your BMR factor in activity to account for calories burned during exercise.

BMR x 1.2 for low intensity activities and leisure activities (primarily sedentary)

BMR x 1.375 for light exercise (leisurely walking for 30-50 minutes 3-4 days/week, golfing, house chores)

BMR x 1.55 for moderate exercise 3-5 days per week (60-70% MHR for 30-60 minutes/session)

BMR x 1.725 for active individuals (exercising 6-7 days/week at moderate to high intensity (70-85% MHR) for 45-60 minutes/session)

BMR x 1.9 for the extremely active individuals (engaged in heavy/intense exercise like heavy manual labor, heavy lifting, endurance athletes, and competitive team sports athletes 6-7 days/week for 90 + minutes/session)

--- .class #id 

## R code and example output

Here is the R code in the shiny app that implements the formula for daily caloric intake:


```r
daily_cal <- function(input) {ifelse(input$gender=="male" , 
           round(as.numeric(input$active)*(66.47+ (6.25 * input$weight) + 
           (5.0 * input$height) - (6.75 * input$age))),
           round(as.numeric(input$active)*(665.09 + (4.35 * input$weight) + 
           (1.84 * input$height) - (4.67 * input$age))))}
```

Using the author's information for demo:


```r
input=list(gender="male", active=1.725, weight=164, height=171, age=30)
cat("The author needs to consume", daily_cal(input), 
    "calories per day to maintain his body weight.")
```

```
## The author needs to consume 3008 calories per day to maintain his body weight.
```
