# Introduction to ggplot2

## A florid example

Let's start by loading the tidyverse library and the iris dataset.
```R
library(tidyverse)
iris <- iris
```

This is an **empty initialization of ggplot2**. It just loads the canvas.

```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width))
```
Actual plots are composed of **geometries** (`geom_`). Here we create a scatter 
plot.
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width)) +
  geom_point()
```
Our dataset is composed of different species of flowers. To identify which dot
belongs to which flower, we add colors.
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point() 
```
    
We can add a simple linear model to the mix, to see if there is a linear
correlation between sepal length and width.
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point() +
  geom_smooth(method = "lm")
```

Now we create a boxplot using the same data.
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width)) +
  geom_boxplot() 
```

A mixed boxplot is not very useful. Let's split it by species.
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_boxplot() 
```
Hmmm, the color aesthetic for boxplots only adds color for the outline of the 
`geom_`, let's fill it instead.
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
  geom_boxplot() 
```

Let's change the x and y axis labels and add a title and a subtitle. Also, we 
are changing the legend name.
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
  geom_boxplot() +
  ggtitle(label = "This is a title", subtitle = "This is a subtitle") +
  labs(x = "Sepal length", y = "Sepal width", fill = "Flower")
```    

By default, ggplot2 "guesstimates" the axis limits. But we can force our plot 
to start at (0,0).
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
  geom_boxplot() +
  scale_x_continuous(limits = c(0, 10), n.breaks = 10) +
  scale_y_continuous(limits = c(0, 5), n.breaks = 10) +
  ggtitle(label = "This is a title", subtitle = "This is a subtitle") +
  labs(x = "Sepal length", y = "Sepal width", fill = "Flower")
```

Let's keep the default origin and split the plot by facets.
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
  geom_boxplot() +
  ggtitle(label = "This is a title", subtitle = "This is a subtitle") +
  labs(x = "Sepal length", y = "Sepal width", fill = "Flower") +
  facet_grid(~Species)
```
The default ggplot2 theme is really ugly. We'll add a prebuilt theme, called
`theme_bw`.
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
  geom_boxplot() +
  ggtitle(label = "This is a title", subtitle = "This is a subtitle") +
  labs(x = "Sepal length", y = "Sepal width", fill = "Flower") +
  facet_grid(~Species) +
  theme_bw()
```

We can overwrite some of the theme's settings like the grid lines and the font.
In the following example, we are removing both the major and the minor grid lines. We are also changing the font and the fontsize.
```R
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
  geom_boxplot() +
  ggtitle(label = "This is a title", subtitle = "This is a subtitle") +
  labs(x = "Sepal length", y = "Sepal width", fill = "Flower") +
  facet_grid(~Species) +
  theme_bw() +
  theme(
        panel.grid.major = element_blank(),
        panel.grid.minor = element_blank(),
        text = element_text(size = 11, family = "Comic Sans MS")
    )
```

ggplot2 default palette is so-so. We are using an `RColorBrewer` palette 
instead.
```R
library(RColorBrewer)
ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
  geom_boxplot() +
  scale_fill_brewer(palette = "Accent") +
  ggtitle(label = "This is a title", subtitle = "This is a subtitle") +
  labs(x = "Sepal length", y = "Sepal width", fill = "Flower") +
  facet_grid(~Species) +
  theme_bw() +
  theme(
        panel.grid.major = element_blank(),
        panel.grid.minor = element_blank(),
        text = element_text(size = 11, family = "Comic Sans MS")
    )
```

## Exercise 1: deadly inequality
Load up the Titanic dataset, which is already loaded into R. To do so, type

```R
titanic <- as.data.frame(Titanic)
```

1. Change the name of the column **Freq** to cases or create a new column with 
that name.
2. Draw a boxplot of the amount of cases (deaths):

a) By ticket class.
b) By Sex.
c) By Age.

It must be a **single plot**. As a tip, try to play around with:

a) Which column is represented in the X axis.
b) The color/fill grouping of the box plots.
c) The facet argument we saw earlier.


<details>
  <summary>Answer</summary>

  ```R
titanic <- as.data.frame(Titanic)
titanic$cases <- titanic$Freq

the_plot <- ggplot(data = titanic, aes(x = Age, y = cases, fill = Sex)) +
  geom_boxplot() +
  facet_wrap(~Class)
the_plot

  ```
</details>
