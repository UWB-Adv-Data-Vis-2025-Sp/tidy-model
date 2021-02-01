# tidy-model
Template file for homework assignment to learn to use R syntax for creating models in tidyverse.

For this assignment we will learn how to represent data with a model and take advantage of some of the tools in the tidyverse that will make working with data easier. 

## Before you get started

Familiarize yourself with linear regression. Watch the YouTube videos, [Linear Regression: Vary Basics](https://www.youtube.com/watch?v=ZkjP5RJLQF4) and [Linear Regression, Algebra, Equations, and Patterns](https://www.youtube.com/watch?v=iAgYLRy7e20&list=PLIeGtxpvyG-LoKUpV0fSY8BGKIMIdmfCi&index=2), about linear models and how to interpret them. Additionally, you may want to read about [Software for modeling in *Tidy Modeling with R*](https://www.tmwr.org/software-modeling.html) by Max Kuhn and Julia Silge.

For this assignment we will be using resources from [A review of R modeling fundamentals in *Tidy Modeling with R*](https://www.tmwr.org/base-r.html) and 
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

## Creating a Rmd file

For this assignment, we will begin by creating a new R Markdown document. Select **New File** and **R Markdown...** and then give the document the title "tidy-model" and add your name as the author. Save the new `.Rmd` file as `tidy-model.Rmd`.

Open the file and then use the **Knit** button to load the file as an html document.

At this point, save the file, write a commit message and ***commit***.

### Setup chunk

We will update the library. Update the *setup* chunk to load packages as shown below.

```
{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
library('tidyverse') ; library('modeldata')
```

You may not have these packages installed, so you will want to use the following code in the console to get the packages needed for this assignment. 

```
install.packages(c('tidyverse', 'modeldata'))
```

Save the file, write a commit message and ***commit***.

### Introduction

Underneath the setup chunk, replace the text with the following header and text.

```## Introduction```

`This R Markdown document demonstrates my abilities to use models for data analysis using a data set collected on crickets.`

Save the file, write a commit message and ***commit***.

### Load data chunk

Create a new chunk under your replaced text called `{r load data, include = FALSE}`
 
Inside this chunk, load the data collected on different species of crickets

```
{r load data, include = FALSE}
data(crickets, package = "modeldata")
names(crickets)
```

Save the file, write a commit message and ***commit***.

### What factors effects chirp rate?

Remove the remaining text, header and code created by the template so we can code our own information.

Let's create a header `## What is that sound?`  and under this header we will write the text.
`In this report we examine what factors predict a crickets chrip rate.`

Next we will add a chunk named *summary* that summarizes the data in the data set. Among the crickets in our data set we can examine the data at glance using the `summary()` function. 
```
{r summary, echo = FALSE}
summary(crickets)
```
Save the file, knit, write a commit message, and ***commit***.

Next, write in text to descriptive the general statistics including the number of observations in the data set, the number of species, the temperature range (minimum and maximum), and the mean rate of chriping.

Add to the chunk to make a histogram of chirp rate based using ggplot.

```
{r summary, echo = FALSE}
summary(crickets)
ggplot(crickets, aes(x = rate)) +
  geom_histogram(bins = 8) + 
  ggtitle("Distribution of the chirp rate of crickets") +
  xlab('Chirp rate (per min.)')
```
Save the file, knit, write a commit message, and ***commit***.

Let's create a new header `## Temperature affects chirp rate`

Next we will add a chunk named *temp* that will plot a scatter plot of temperature and chirp rate.

```
{r temp, echo= FALSE}
ggplot(crickets, aes(x = temp, y = rate)) +
  geom_point() + 
  geom_smooth(method = 'lm') +
  ggtitle("Plot of temperature and chirp rate") +
  ylab('Chirp rate (per min.)') +
  xlab('Temperature (Celsius)')
```
After making a graph, add some text below such as `Based on a scatter plot of temperature and chirping, it seems that as temperature increases, the rate of chirping also increases.`

Save the file, knit, write a commit message, and ***commit***.

Next we are going to remake this graph with short hand formula popularized by tidyverse. Replace `aes(x = temp, y = rate)` with a formula `rate ~ temp` which states that the linear formula is predicts chirp rate (the y-value) based on a linear relationship with temperature (the x-value).

```
{r temp, echo= FALSE}
ggplot(crickets, rate ~ temp)) +
  geom_point() + 
  geom_smooth(method = 'lm') +
  ggtitle("Plot of temperature and chirp rate") +
  ylab('Chirp rate (per min.)') +
  xlab('Temperature (Celsius)')
```


