---
title: The graphing philosophy of ggplot2
author: Feng Wang
date: '2020-05-09'
slug: the-graphing-philosophy-of-ggplot2
categories:
  - R
tags:
  - Tidyverse
toc: no
images: ~
---

```{r}
library(tidyverse)
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class))
```

## The common workflow for making graphs with ggplot2

1. Start the graph with `ggplot()`
2. Add elements to the graph with a `geom_` function
3. Select variables with the `mapping = aes()` argument

`ggplot()` creates a coordinate system that you can add layers to. The first argument of `ggplot()` is the dataset to use in the graph. `geom_point()` adds a layer of points to the empty plot created by `ggplot()`. This gives us a scatterplot. `geom_point()` takes a `mapping` argument that defines which **variables** in your dataset are mapped to which axes in your graph. The mapping argument is always paired with the function `aes()`, which you use to gather together all of the mappings that you want to create.


A **geom** is the geometrical object that a plot uses to represent observations. People often describe plots by the type of geom that the plot uses. 

An **aesthetic** is a visual property of the objects in your plot. Aesthetics include things like the size, the shape, or the color of your points. You can display a point in different ways by changing the **levels** of its aesthetic properties. To map an aesthetic to a variable, set the name of the aesthetic equal to the name of the variable, and do this inside `mapping = aes()`. ggplot2 will automatically assign a unique level of the aesthetic (here a unique color) to each unique value of the variable. ggplot2 will also add a legend that explains which levels correspond to which values. This insight gives us a new way to think about the mapping argument. Mappings tell ggplot2 more than which variables to put on which axes, they tell ggplot2 which variables to map to which visual properties. The x and y locations of each point are just two of the many visual properties displayed by a point.


## Setting vs. Mapping

Setting works for every aesthetic in ggplot2. If you want to manually **set** the aesthetic to a **value** in the visual space, set the aesthetic _outside of `aes()`_. If you want to **map** the aesthetic to a variable in the data space, map the aesthetic _inside `aes()`_. Putting an aesthetic in the wrong location is one of the most common graphing errors. Sometimes it helps to think of legends. If you will need a legend to understand what the color/shape/etc. means, then you should probably put the aesthetic inside `aes()` --- ggplot2 will build a legend for every aesthetic mapped here. If the aesthetic has no meaning and is just... well, aesthetic, then set it outside of `aes()`. For each aesthetic, you associate the name of the aesthetic with a variable to display, and you do this within aes(). Once you map a variable to an aesthetic, ggplot2 takes care of the rest. It selects a reasonable scale to use with the aesthetic, and it constructs a legend that explains the mapping between levels and values. For x and y aesthetics, ggplot2 does not create a legend, but it creates an axis line with tick marks and a label. The axis line acts as a legend; it explains the mapping between locations and values.

Ref: *Rstudio icloud primer*
