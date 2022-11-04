# Introduction to ggplot2

## A florid example

Let's start by loading the tidyverse library and iris dataset
```R
library(tidyverse)
```

This is an empty initialization of ggplot. Loads the canvas, but it's empty.

```R
iris <- iris
iris_sepal_lm <- ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width))
```
Actual plots are composed of GEOMETRIES (geoms). Here we are adding a dot geom,
thus creating a scatter plot
```R
iris_sepal_lm <- ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width)) +
    geom_point()
```
Our dataset is composed of different species of flowers. To id. which dot
belongs to which flower, we'll be adding colors now.
```R
iris_sepal_lm <- ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width)) +
    geom_point(aes(color = Species)) 
```
    
We can even add a simple linear model to the mix, to see if there is a linear
correlation between sepal length and width
```R
iris_sepal_lm <- ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width)) +
    geom_point(aes(color = Species)) +
    geom_smooth(aes(color = Species), method = "lm")
```
Since our COLOR aesthetic is the same for both the geom point and the geom
smooth, we can add it to the ggplot call instead. Thus, both the geom 
point and the geom smooth will inherit the aes
```R
iris_sepal_lm <- ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
    geom_point() +
    geom_smooth(method = "lm")
```
Now we are going to create a boxplot using the same data.
```R
iris_sepals_box <- ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width)) +
    geom_boxplot() 
```
Again, a mixed boxplot is not very useful. Let's split it by species
```R
iris_sepals_box <- ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width)) +
    geom_boxplot(aes(color = Species)) 
```
Hmmm, the color aesthetic for boxplots only adds color for the outline of the geom,
let's add FILL instead
```R
iris_sepals_box <- ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width)) +
    geom_boxplot(aes(fill = Species)) 
```

Let's change some labels now. First, the x axis and the y axis names. Let's add
a title too. Also, we are changing the legend name
```R
iris_sepals_box <- ggplot(data = iris, aes(x = Sepal.Length, y = Sepal.Width)) +
    geom_boxplot(aes(fill = Species)) +
    xlab(label = "Sepal length") + # X axis label
    ylab(label = "Sepal width") + # Y axis label
    scale_fill_discrete("Flower") + # Legend name
    ggtitle(label = "This is a title", subtitle = "This is a subtitle")
```    

By default, ggplot2 "guesstimates" the coords. at which the X axis and the Y
axis meet. But we can change it too so that our plot starts at (0,0)
```R
iris_sepals_box <- ggplot(data = iris) +
    scale_x_continuous(limits = c(0, 10), n.breaks = 10) +
    scale_y_continuous(limits = c(0, 5), n.breaks = 10) +
    geom_boxplot(aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
    xlab(label = "Sepal length") +
    ylab(label = "Sepal width") +
    scale_fill_discrete("Flower") +
    ggtitle(label = "This is a title", subtitle = "This is a subtitle")
```

Let's keep the default origin instead of the previous one. Now, we are
going to split the plot by facets.
```R
iris_sepals_box <- ggplot(data = iris) +
    geom_boxplot(aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
    facet_grid(cols = vars(Species)) +
    xlab(label = "Sepal length") +
    ylab(label = "Sepal width") +
    scale_fill_discrete("Flower") +
    ggtitle(label = "This is a title", subtitle = "This is a subtitle")
```
The default ggplot2 theme is really ugly. We'll add a prebuilt theme, called
theme_bw
```R
iris_sepals_box <- ggplot(data = iris) +
    geom_boxplot(aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
    facet_grid(cols = vars(Species)) +
    xlab(label = "Sepal length") +
    ylab(label = "Sepal width") +
    scale_fill_discrete("Flower") +
    ggtitle(label = "This is a title", subtitle = "This is a subtitle") +
    theme_bw()
```

We can overwrite some of the theme's settings like the grid lines and the font.
In the following example, I'm removing both the major and the minor grid lines.
I'm also changing the font and the fontsize.
```R
iris_sepals_box <- ggplot(data = iris) +
    geom_boxplot(aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
    facet_grid(cols = vars(Species)) +
    xlab(label = "Sepal length") +
    ylab(label = "Sepal width") +
    scale_fill_discrete("Flower") +
    ggtitle(label = "This is a title", subtitle = "This is a subtitle") +
    theme_bw() +
    theme(
        panel.grid.major = element_blank(),
        panel.grid.minor = element_blank(),
        text = element_text(size = 11, family = "Comic Sans MS") ## This here changes the font for all of the text labels
    )
```

ggplot2 default palette is so-so. However, the RColorBrewer library extends
the base color pal. allowing us to change the full color set.
```R
## RColorBrewr
library(RColorBrewer)

iris_sepals_box <- ggplot(data = iris) +
    geom_boxplot(aes(x = Sepal.Length, y = Sepal.Width, fill = Species)) +
    facet_grid(cols = vars(Species)) +
    xlab(label = "Sepal length") +
    ylab(label = "Sepal width") +
    scale_fill_discrete("Flower") +
    scale_fill_brewer("New flower", palette = "Accent") + ## This here allows us to change the col. palette
    ggtitle(label = "This is a title", subtitle = "This is a subtitle") +
    theme_bw() +
    theme(
        panel.grid.major = element_blank(),
        panel.grid.minor = element_blank()
    )
```

## Exercise 1: deadly inequality
Load up the Titanic dataset, which is already installed in R. To do so, type

```R
titanic <- as.data.frame(Titanic)
```

1. Change the name of the column **Freq** to cases or create a new column with that name.
2. Draw a boxplot of the amount of cases (death) by:

a) By ticket class
b) By Sex
c) By Age

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
    facet_wrap(vars(Class))

  ```
</details>
