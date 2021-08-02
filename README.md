
<!-- README.md is generated from README.Rmd. Please edit that file -->

# ggbrookings <img src="man/figures/logo.png" align="right" alt="" width="120" />

## Installation

``` r
install.packages("devtools")
devtools::install_github("Hutchins-Center/ggbrookings", build_vignettes = TRUE)
```

## Usage

Currently, the `ggbrokings` package only has a few simple user facing
functions:

-   `theme_brookings()` overrides the default `ggplot2` theme for a
    custom one which adheres to the Brookings style guide.

-   `scale_color_brookings()` and `scale_fill_brookings()` provide
    several color palettes that are consistent with the Brookings brand
    and designed to provide color accessiblity.

-   `brookings_view_palette` is a helper function to see the colors from
    each palette and extract their hex codes.

``` r
librarian::shelf(tidyverse, palmerpenguins, ggbrookings)
```

### Scatterplot

``` r
ggplot(data = penguins,
       aes(x = bill_length_mm,
           y = bill_depth_mm,
           group = species)) +
  geom_point(aes(color = species,
                 shape = species),
             size = 3,
             alpha = 0.8) +
  geom_smooth(method = "lm", se = FALSE, aes(color = species)) +
  theme_brookings() +
  scale_color_brookings(palette = "misc") +
  labs(
    title = "Penguin bill dimensions",
    subtitle = "Bill length and depth for Adelie, Chinstrap and Gentoo Penguins at Palmer Station LTER",
    x = "Bill length (mm)",
    y = "Bill depth (mm)",
    color = "Penguin species",
    shape = "Penguin species"
  )
```

<img src="man/figures/unnamed-chunk-2-1.png" style="display: block; margin: auto;" />

### Histogram

``` r
ggplot(data = penguins, aes(x = flipper_length_mm)) +
  geom_histogram(aes(fill = species),
                 alpha = 0.5,
                 position = "identity",
                 bins = 30) +
  scale_fill_brookings(palette = "semantic3") +
  theme_brookings() +
  labs(x = "Flipper length (mm)",
       y = "Frequency",
       title = "Penguin flipper lengths")
```

<img src="man/figures/unnamed-chunk-3-1.png" style="display: block; margin: auto;" />

### Line plot

``` r
library('gapminder')
library('ggtext')

gapminder_filtered <-
  gapminder %>% 
  filter(country %in% c('Argentina', 'Brazil', 'Uruguay'))  

gapminder_filtered %>% 
  ggplot(aes(x = year, gdpPercap, color = country, label = country)) +
  geom_line() +
  geom_label(data = gapminder_filtered %>% filter(year == last(year)), aes(label = country, 
                                                           x = year + 3, 
                                                           y = gdpPercap + 250, 
                                                           color = country)) +
  theme_brookings() +
  guides(color = 'none') +
  scale_x_continuous(breaks = seq(1952, 2007, 5),
      limits  = c(1952, 2012),
      expand = expansion(mult = c(0, 0.1))) +
    scale_y_continuous(
      labels = scales::label_dollar(), 
                     limits = c(0, 15000), breaks = seq(0, 15000, 2500),
                     expand = expansion(0)) +
  scale_color_brookings() +
  labs(title = 'Economic growth in South America',
       subtitle = 'GDP per capita, 1952-2007',
       x = NULL, 
       y = NULL, 
       caption = '**Source:** Gapminder')
```

<img src="man/figures/unnamed-chunk-4-1.png" style="display: block; margin: auto;" />

### Faceting

``` r
ggplot(penguins, aes(x = flipper_length_mm,
                            y = body_mass_g)) +
  geom_point(aes(color = sex),
             show.legend = FALSE) +
  theme_brookings() +
  scale_color_brookings('brand1', na.translate = FALSE) +
  labs(title = "Penguin flipper and body mass",
       subtitle = "Dimensions for  <span style = 'color:#FF9E1B;'>**male**</span> and <span style = 'color:#003A79;'>**female**</span> Adelie, Chinstrap and Gentoo Penguins at Palmer Station LTER",
       x = "Flipper length (mm)",
       y = "Body mass (g)",
       color = "Penguin sex") +
  facet_wrap(~species)
```

<img src="man/figures/unnamed-chunk-5-1.png" style="display: block; margin: auto;" />
