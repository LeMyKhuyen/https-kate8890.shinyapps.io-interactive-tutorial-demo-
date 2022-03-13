---
title: "Tutorial"
output: 
  learnr::tutorial:
    fig_caption: no
    progressive: true
    allow_skip: true

runtime: shiny_prerendered
---

```{r setup, include=FALSE}

# load packages
library(learnr)
library(tidyverse)

# options
knitr::opts_chunk$set(echo = FALSE)

# code checking
checker <- function(label, user_code, check_code, envir_result, evaluate_result, ...) {list(message = check_code, correct = TRUE, location = "append")
}
tutorial_options(exercise.timelimit = 10,
exercise.checker = checker)
```

## Topic 1
Hello, today we learn about 'learnr'.


some math! $a^2 + b^2 = c^2$

### Exercise 

*Here's a simple exercise with an empty code chunk provided for entering the answer.*

Write the R code required to add two plus two:

```{r two-plus-two, exercise=TRUE}

```

### Exercise with Code

*Here's an exercise with some prepopulated code as well as `exercise.lines = 5` to provide a bit more initial room to work.*

Now write a function that adds any two numbers and then call it:

```{r add-function, exercise=TRUE, exercise.lines = 5}
add <- function() {
  
}
```

## Topic 2

### Exercise with Hint

*Here's an exercise where the chunk is pre-evaulated via the `exercise.eval` option (so the user can see the default output we'd like them to customize). We also add a "hint" to the correct solution via the chunk immediate below labeled `print-limit-hint`.*

Modify the following code to limit the number of rows printed to 5:

```{r print-limit, exercise=TRUE, exercise.eval=TRUE}
mtcars
```

```{r print-limit-hint}
sum(mtcars)
```

## Topic 3

### Exercise checking

You can use the 'count' function to count the number of observations in each level of a categorical variable.

How many automatic and how many manual transmission cars in the data?

```{r count, exercise=TRUE}

```

```{r count-solution, exercise=TRUE}
mtcars %>%
  count(am)
```

```{r count-check}
"great job!"
```

## Quiz

*You can include any number of single or multiple choice questions as a quiz. Use the `question` function to define a question and the `quiz` function for grouping multiple questions together.*

Some questions to verify that you understand the purposes of various base and recommended R packages:

```{r quiz}
quiz(
  question("scatter plot show...",
    answer("One categorial varible"),
    answer("Two categorial varibles"),
    answer("Two continuous varibles", correct = TRUE),
    answer("The frequency of values of variables")
    ),
  question("In a scatterplot, an outlier...?",
    answer("...is something we didn't learn 8th grade"),
    answer("...is a point that is far outside the main cluster of points/ordered pairs", correct = TRUE),
    answer("...is a puppet with a long nose named Pinocchio"),
    answer("...is a really naughty point who doesn't tell the truth when outside")
)
)
```

```{r var-types}
question(
  "Which of the following is a numerical variable?",
  answer("zip code", message = "zip code is recorded using numbers, but it's not numerical."),
  answer("height"),
  answer("handedness", correct = TRUE),
  allow_retry = TRUE,
  correct = "great"
)
```
## Videos
![video](https://www.youtube.com/watch?v=gwu63_WO7O8&t=654s){width = 50%}

## Shiny

```{r, echo= FALSE}
sliderInput(
  "binwidth",
  "Binwidth:",
  min = 1, max = 30, value = 3
)
plotOutput("hist")
```

```{r, context = "server"}
output$hist <- renderPlot({
  ggplot(data = mtcars, aes(x=mpg)) +
    geom_histogram(binwidth = input$binwidth) +
    labs(
      x = "Miles per galon",
      y = "Frequency",
      title = "Distribution of MPG"
    )
})
```

