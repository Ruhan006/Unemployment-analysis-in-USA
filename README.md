# Unemployment-analysis-in-USA

### Table of Contents

- [Project overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Improved Data Loading and Summary](#improved-data-loading-and-summary)
- [Data Cleaning](#data-cleaning)
- [Data Visualisations](#data-visualisations)
- [Model Interpretations](#model-interpretations)
- [Chow test explanation](#chow-test-explanation)
- [Conclusions](#conclusions)
- [References](#references)
  
### Project overview

This project analyzes the unemployment rate in USA from 2010 to 2023. We take the data from 2010 to 2023 to identify whether there is a structural break in the data or not and how it affects to the unemployment rate in USA. Here, we use Chowtest and linear regression to see if there this a significant shifts in unemployment rate.

### Data Sources

Unemployment data: This secondary data used for this analysis is the "unemployment.xlsx" file which is collected from Kaggle.

### Tools

- R

### Improved Data Loading and Summary

In this section, we are loading the dataset and finding the summary as well. 
```r
data <- read_excel("C:/Users/Ruhan/OneDrive/Desktop/unemployment.xlsx")
summary(data)
```
### Data Cleaning

We have to check whether there the data are consists of missing values or not.
```r
sum(is.na(data))
```
We have found that there are no missing values here.

### Data Visualisations

Scatter plot- Visualization of the relationships before and after 2020 with separate fitted regression lines for each period. Here we have ploted a fitted regression line for subgroups. Here the red line represents unemployment rate between 2010 to 2019 whereas, the green line represents uneployment rate after 2020.

```r
ggplot(data1, aes(x = Year, y = Unemployment_Rate)) +
  geom_point(color = "gray") +
  geom_smooth(data = data2, aes(y = Unemployment_Rate), method = "lm", color = "red", se = FALSE) +  
  geom_smooth(data = data3, aes(y = Unemployment_Rate), method = "lm", color = "green", se = FALSE) + 
  labs(title = "Unemployment Rate with Fitted Lines (Before and After 2020)",
       x = "Year",
       y = "Unemployment Rate (%)") +
  theme_minimal() +
  theme(plot.title = element_text(hjust = 0.5))
```
![Scatterplot](https://github.com/user-attachments/assets/9305dd86-37b2-4686-bfab-99ba4287ca3b)

### Model Interpretations

```r
model_summaries <- list(
  full = summary(model_full),
  before = summary(model_before),
  after = summary(model_after)
)
model_summaries
```
#### Full Model (2010-2023)

The full model captures the unemployment rate trend in New York from 2010 to 2023. The year coefficient -0.345 indicates a slight overall decrease in unemployment rates during this period, though it likely obscures different trends before and after 2020. R squared value suggests that the model explains 38.7% of the variation in unemployment rates, which suggests a moderate fit. The model is statistically significant (p-value < 2.2e-16), indicating a strong relationship between the year and unemployment rate.

#### Before 2020 Model (2010-2019)

The before 2020 model focuses on the period from 2010 to 2019. A more negative coefficient (-0.606) suggests a faster decline in unemployment rates during this period, likely reflecting steady economic growth. R squared value tells that the model explains 60.7% of the variation in unemployment rates, a much stronger fit than the full model. Finally, the model is highly significant (p-value < 2.2e-16), reflecting a clear downward trend in unemployment before 2020.

#### After 2020 Model (2020-2023)

A sharper negative coefficient (-1.353) reflects a significant drop in unemployment rates after 2020, possibly due to post-pandemic economic recovery. The model explains 54.8% of the variation in unemployment rates, indicating a reasonably strong fit for this period. Lastly, this model is also statistically significant (p-value < 2.2e-16), showing the substantial impact of external factors on unemployment rates post-2020.

### Chow test explanation

```r
cat("Chow Test Results:\n")
print(chow_test)
if(chow_test$p.value < 0.05) {
  cat("There is a significant structural break in the unemployment rate around 2020.\n")
} else {
  cat("No significant structural break detected.\n")
}
```
Here the p value is 0.000601 which is less than 0.05. Hence, there is a significant structural break in the unemployment rate around 2020.

### Conclusions

In this analysis, we explored the unemployment rates in New York from 2010 to 2023. Our findings indicate significant changes in the unemployment trend around the year 2020, likely due to the impact of the COVID-19 pandemic and the Chow test confirmed a structural break.

### References

1. [Kaggle](https://www.kaggle.com/datasets/casimircoulson/u-s-unemployment-rate-by-state-1976-2023)


