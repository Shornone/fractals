# Fractals
Create fractal art with R

## How to use

### Install the packages

```R
install.packages(c("devtools", "tidyverse"))
devtools::install_github("marcusvolz/fractals")
devtools::install_github("marcusvolz/ggart")
```

### Load the libraries

```R
library(fractals)
library(ggart)
library(tidyverse)
```

### Create fractal ferns

```R
n <- 250000

params1 <- data.frame(
  a <- c(0, 0.85, 0.2, -0.15),
  b <- c(0, 0.04, -0.26, 0.28),
  c <- c(0, -0.04, 0.23, 0.26),
  d <- c(0.16, 0.85, 0.22, 0.24),
  e <- c(0, 0, 0, 0),
  f <- c(0, 1.6, 1.6, 0.44),
  p <- c(0.01, 0.85, 0.07, 0.07)
)

params2 <- data.frame(
  a <- c(0, 0.85, 0.09, -0.09),
  b <- c(0, 0.02, -0.28, 0.28),
  c <- c(0, -0.02, 0.3, 0.3),
  d <- c(0.25, 0.83, 0.11, 0.09),
  e <- c(0, 0, 0, 0),
  f <- c(-0.14, 1, 0.6, 0.7),
  p <- c(0.02, 0.84, 0.07, 0.07)
)

df1 <- fractal_fern(n = n, a = params1$a, b = params1$b, c_ = params1$c, d = params1$d, e = params1$e,
                   f = params1$f, p = params1$p) %>% mutate(id = 1)

df2 <- fractal_fern(n = n, a = params2$a, b = params2$b, c_ = params2$c, d = params2$d, e = params2$e,
                    f = params2$f, p = params2$p) %>% mutate(id = 2)

df <- rbind(df1, df2 %>% mutate(x = x*1.75, y = y*1.75))

p <- ggplot() +
  geom_point(aes(x, y), df, size = 0.03, alpha = 0.06) +
  coord_equal() +
  facet_wrap(~id, nrow = 1) +
  theme_blankcanvas(margin_cm = 1)

ggsave("fern01.png", width = 20, height = 20, units = "cm")
```

![birds](https://github.com/marcusvolz/fractals/blob/master/plots/fern01.png "Ferns")
