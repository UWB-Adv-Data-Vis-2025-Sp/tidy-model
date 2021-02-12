# tidy-model
Template file for homework assignment to learn to use R syntax for creating models in tidyverse.

For this assignment we will learn how to represent data with a statistical model and take advantage of some of the tools in the tidyverse and base R that will make working with data easier. 

## Before you get started

Familiarize yourself with linear regression. 

If you aren't familiar with linear models or need  a refresher about linear models and how to interpret them, start here by watching these two YouTube videos:
* [Linear Regression: Very Basics](https://www.youtube.com/watch?v=ZkjP5RJLQF4)
* [Linear Regression, Algebra, Equations, and Patterns](https://www.youtube.com/watch?v=iAgYLRy7e20&list=PLIeGtxpvyG-LoKUpV0fSY8BGKIMIdmfCi&index=2). 

Additionally, you may want to read about [Software for modeling in *Tidy Modeling with R*](https://www.tmwr.org/software-modeling.html) by Max Kuhn and Julia Silge.

To supplement this assignment, use resources from [A review of R modeling fundamentals in *Tidy Modeling with R*](https://www.tmwr.org/base-r.html) and 
The sections on modeling form [*R for Data Science*](https://r4ds.had.co.nz) by Hadley and Grolemund: 

22.  [Introduction](https://r4ds.had.co.nz/model-intro.html)
23.  [Model basics](https://r4ds.had.co.nz/model-basics.html) 
24.  [Model building](https://r4ds.had.co.nz/model-building.html)

## Instructions

Make sure to write out the code to get in the habit of understanding the grammar of the code. Do not copy directly. The power of learning code is the creative avenues it unlocks. If you need help, remember there are lots of resources including:

- Discord
- Canvas Community Q&A
- The internet
- Prof. Trujillo

## Creating an Rmd file

For this assignment, we will begin by creating a new R Markdown document. Select **New File** and **R Markdown...** and then give the document the title "tidy-model" and add your name as the author. Save the new `.Rmd` file as `tidy-model.Rmd`.

Open the file and then use the **Knit** button to load the file as an html document.

At this point, save the file, write a commit message and ***commit***.

### Setup chunk

We will update the library. Update the *setup* chunk to load packages as shown below.

` ```{r setup, include=FALSE}`
`knitr::opts_chunk$set(echo = TRUE)`
`library('tidyverse') ; library('modeldata')``` `

You may not have these packages installed, so you will want to use the following code in the console to get the packages needed for this assignment. 

`install.packages(c('tidyverse', 'modeldata'))`

Save the file, write a commit message and ***commit***.

### Introduction

Underneath the setup chunk, replace the text with the following header and text.

`## Introduction`

`This R Markdown document demonstrates my abilities to use models for data analysis using a data set collected on crickets.`

Save the file, write a commit message and ***commit***.

### Load data chunk

Create a new chunk under your replaced text called `{r load data, include = FALSE}`.
 
Inside this chunk, load the data collected on different species of crickets.

` ```{r load data, include = FALSE}
data(crickets, package = "modeldata")
names(crickets)
``` `

Save the file, write a commit message and ***commit***.

### What factors affect chirp rate?

#### Graphing chirps

Remove the remaining text, header and code created by the template so we can code our own information.

Let's create a header `## What is that sound?`  and under this header we will write the text:
`In this report we examine what factors predict a cricket's chrip rate.`

Next we will add a chunk named *summary* that summarizes the data in the data set. Among the crickets in our data set we can examine the data at a glance using the `summary()` function. 

` ```{r summary, echo = FALSE}
summary(crickets)
``` `
Save the file, knit, write a commit message, and ***commit***.

Next, write in text to describe the general statistics by reporting the number of observations in the data set, the number of species, the temperature range (minimum and maximum), and the mean rate of chirping.

Add to the chunk to make a histogram of chirp rate based using ggplot.

` ```{r summary, echo = FALSE}
summary(crickets)
ggplot(crickets, aes(x = rate)) +
  geom_histogram(bins = 8) + 
  ggtitle("Distribution of the chirp rate of crickets") +
  xlab('Chirp rate (per min.)')
``` `
Save the file, knit, write a commit message, and ***commit***.

#### Graphing temperature and chirps

Let's create a new header `## Temperature affects chirp rate`

Next we will add a chunk named *temp* that will plot a scatter plot of temperature and chirp rate.

` ```{r temp, echo= FALSE}
ggplot(crickets, aes(x = temp, y = rate)) +
  geom_point() + 
  geom_smooth(method = 'lm') +
  ggtitle("Plot of temperature and chirp rate") +
  ylab('Chirp rate (per min.)') +
  xlab('Temperature (Celsius)')``` `
After making a graph, add some text below such as `Based on a scatter plot of temperature and chirping, it seems that as temperature increases, the rate of chirping also increases.`

Save the file, knit, write a commit message, and ***commit***.

#### Modeling temperature and chirps

In the `temp` chunk, create a new line below the ggplot commands to add a linear model using the functions `lm()` and `summary.lm()`. Notice that this line uses the formula format to calculate the model. 

Instead of ggplot's aesthetics function  `aes(x = temp, y = rate)`,  we can represent our variables as a formula `rate ~ temp` which states that the linear formula will try to predict chirp rate (the y-value) based on a linear relationship with temperature (the x-value). Typically the assumption of these models is that the dependent variable comes before your list of independent variables, `y ~ x`. Often the syntax will ask for a formula before you enter  the argument for data.  

Store the output of the `lm()` function as a new object `temp_lm`. And then call up the `summary.lm()` for a complete output of the linear model.

Update the chunk so it looks like the one below. 
` ```{r temp, echo= FALSE}
ggplot(crickets, aes(x = temp, y = rate)) +
  geom_point() + 
  geom_smooth(method = 'lm') +
  ggtitle("Plot of temperature and chirp rate") +
  ylab('Chirp rate (per min.)') +
  xlab('Temperature (Celsius)')

temp_lm <- lm(rate ~ temp, crickets)

summary.lm(temp_lm)
``` `

Notice that you get two values important from the linear model. The first is the intercept, the point at which the line of best fit would intersect the y-axis. Additionally we see a second value that represents the slope of the curve or the rate of the relationship. In this case we can see that as temperature raises 1 degree C, the crickets will chirp an additional 4 chirps per minute. 

In addition to the linear model giving us a sense of the relationship, we can also see the residual values (the distance between each point and the curve), the standard error of the measures, and even calculated probability values (p-values) for hypothesis testing. In fact this summary gives us great information if we are interested in t-values, R squared values, or F-statistics!

For now, let's revise our earlier sentence in the text to add more information.  `Based on a scatter plot of temperature and chirping and a correlation test, it seems that as temperature increases one degree, the rate of chirping increases about 4.2 chirps per minute.`

Save the file, knit, write a commit message, and ***commit***.

#### Temperture across species

Next we can see if an account of the different species of crickets have an effect on our model. Up to this point, we have grouped all crickets together and that may be an inappropriate assumption. Many animals use signals like chirping to communicate and, for mating behaviors, it's important to distinguish your call from other similar species. Now lets make a new header and chunk for graphing and separating these two values. 

`## Species-specific effects of temperature on chirping`

` ```{r species, echo= FALSE}
ggplot(crickets, aes(x = temp, y = rate, color = species)) +
  geom_point() + 
  geom_smooth(method = 'lm') +
  ggtitle("Plot of temperature and chirp rate for two species of crickets") +
  ylab('Chirp rate (per min.)') +
  xlab('Temperature (Celsius)')``` `

Wow! It looks like instead of one line of best fit, now we have two! The plot has added colors to separate the data by species. Now we can clearly see that both crickets have a positive relationship between temperature and chirping, but start at different places. So let's return to our linear model to see how values have changed. Add the `lm()` and `summary.lm()` functions to the chunk. This time we will extend our formula to account for the new variable. 

` ```{r species, echo= FALSE}
ggplot(crickets, aes(x = temp, y = rate, color = species)) +
  geom_point() + 
  geom_smooth(method = 'lm') +
  ggtitle("Plot of temperature and chirp rate for two species of crickets") +
  ylab('Chirp rate (per min.)') +
  xlab('Temperature (Celsius)')
  
  
species_lm <- lm(rate ~ temp + species, crickets)

summary.lm(species_lm)``` `

Let's check out the data of this model to see how it stacks up against the first model. Now we have three important values in the coefficients table. It helps us to think about the impact of the different variables on the line. The intercept again states where the line would cross the y-axis. The value gives us the temperature relationship to chirping like before. Notice that this has dropped to 3.6 as the slope so as temperature rises one degree (C) then the chirps increase 3.6 chirps per minute. Finally there is a third variable showing up as -10. This value represents the difference between species. Since we have only two species, we can treat this as the difference in the intercept between the two values. So the cricket species *O. exclamationis* has a chirp rate that is 10 chirps per minute higher than its counter part *O. niveus*. So we have a linear model that predicts the relationship between temperature, species and chirps. 

We can use any of the statistical methods collected from summary.lm() to compare the quality of the species-specific model to the general model we made earlier. For instance, let's compare the R-squared values which is a measure of the amount of variance explained by the model. In the temp_lm model, the R-Squared value was 0.9199, which means about 92 percent of the variance in the data is explained by the model, whereas in the species_lm model, the R-Squared value was 0.9896, which means about 99 percent of the variance in the data is explained by this model. Even though the first model might be good enough, the second one is much more reliable for making predictions. 
 
Add text to explain in your own words what the second graph and model show. 

Save the file, knit, write a commit message, and ***commit***.

#### Interactions between temperture and species

In addition to seeing the variables as contributing to the slope or intercept, we can also test for interactions. Perhaps we think that the effects of species and temperature might be interlinked because one species tends to live in a colder temperature than another species. 

For instance, let's examine the original histogram we made with a new sensitivity to the species variable. 

Create a new header `## Interactions`, new chunk called `species histogram`, modify the code from the `summary` chunk to add fill as a variable for species. This new graph should show that the species occupy different temperature zones, which we may want to account for in the model. Add text below that states that these species occupy different temperature ranges.

` ```{r species historgram, echo = FALSE}
ggplot(crickets, aes(x = rate, fill = species)) +
  geom_histogram(position = 'identity', alpha = 0.7, bins = 8) + 
  ggtitle("Distribution of the chirp rate of crickets") +
  xlab('Chirp rate (per min.)')
``` `

This time we will use our code from the `species` chunk to make a new chunk `interactions`, but we will update it to include an addition to the formula so it accounts for interactions `rate ~ temp + species + temp:species`. Alternatively you could represent interactions with `rate ~ (temp + species)^2`. We will store the new model as an object `species_x_temp_lm`. To compare this with our previous model, we will add an additional code of an ANOVA (Analysis of Variance) to compare the two linear models. This comparison produces a p-value far above 0.05 and suggests that the interaction model and the species-species model are not statistically significant in their difference. Therefore we can rely on the simpler `species_lm` results. 

` ```{r interactions, echo= FALSE}
ggplot(crickets, aes(x = temp, y = rate, color = species)) +
  geom_point() + 
  geom_smooth(method = 'lm') +
  ggtitle("Plot of temperature and chirp rate for two species of crickets") +
  ylab('Chirp rate (per min.)') +
  xlab('Temperature (Celsius)')
  
species_x_temp_lm <- lm(rate ~ temp + species + temp:species, crickets) 
summary.lm(species_x_temp_lm)

anova(species_lm, species_x_temp_lm)
``` `

Add text that states that you checked for interactions but decided to stay with the species model. 

Save the file, knit, write a commit message, and ***commit***.

## Going deeper

Congratulations! You wrote your first (in this class) code for performing a linear regression analysis on data. These methods can be easily adapted for modeling nearly any data set. The basic ideas and formulas used here can be adopted to run logistic regression models, multiple linear models, hierarchical models, and many other approaches.

Consider additional resources to deepen your knowledge for your particular area of interest. 

* [*Tidy Modeling with R*](https://www.tmwr.org/software-modeling.html) by Max Kuhn and Julia Silge.
* [*R for Data Science*](https://r4ds.had.co.nz) by Hadley and Grolemund:
  + [Introduction](https://r4ds.had.co.nz/model-intro.html)
  + [Model basics](https://r4ds.had.co.nz/model-basics.html) 
  + [Model building](https://r4ds.had.co.nz/model-building.html)
