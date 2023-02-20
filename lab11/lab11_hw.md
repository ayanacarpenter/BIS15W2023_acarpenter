---
title: "Lab 11 Homework"
author: "Ayana Carpenter"
date: "2023-02-19"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

**In this homework, you should make use of the aesthetics you have learned. It's OK to be flashy!**

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
library(naniar)
```

## Resources
The idea for this assignment came from [Rebecca Barter's](http://www.rebeccabarter.com/blog/2017-11-17-ggplot2_tutorial/) ggplot tutorial so if you get stuck this is a good place to have a look.  

## Gapminder
For this assignment, we are going to use the dataset [gapminder](https://cran.r-project.org/web/packages/gapminder/index.html). Gapminder includes information about economics, population, and life expectancy from countries all over the world. You will need to install it before use. This is the same data that we will use for midterm 2 so this is good practice.

```r
#install.packages("gapminder")
library("gapminder")
```

## Questions
The questions below are open-ended and have many possible solutions. Your approach should, where appropriate, include numerical summaries and visuals. Be creative; assume you are building an analysis that you would ultimately present to an audience of stakeholders. Feel free to try out different `geoms` if they more clearly present your results.  

**1. Use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc. As part of this, determine how NA's are treated in the data.**  


```r
glimpse(gapminder)
```

```
## Rows: 1,704
## Columns: 6
## $ country   <fct> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", …
## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, …
## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, …
## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.8…
## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 12…
## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134, …
```

```r
miss_var_summary(gapminder)
```

```
## # A tibble: 6 × 3
##   variable  n_miss pct_miss
##   <chr>      <int>    <dbl>
## 1 country        0        0
## 2 continent      0        0
## 3 year           0        0
## 4 lifeExp        0        0
## 5 pop            0        0
## 6 gdpPercap      0        0
```

```r
gapminder <- gapminder
```

```r
summary(gapminder)
```

```
##         country        continent        year         lifeExp     
##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
##  Australia  :  12                  Max.   :2007   Max.   :82.60  
##  (Other)    :1632                                                
##       pop              gdpPercap       
##  Min.   :6.001e+04   Min.   :   241.2  
##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
##  Median :7.024e+06   Median :  3531.8  
##  Mean   :2.960e+07   Mean   :  7215.3  
##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
##  Max.   :1.319e+09   Max.   :113523.1  
## 
```

**2. Among the interesting variables in gapminder is life expectancy. How has global life expectancy changed between 1952 and 2007?**


```r
gapminder %>% 
  ggplot(aes(x= year, y = lifeExp, group = year)) + geom_boxplot()
```

![](lab11_hw_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

**3. How do the distributions of life expectancy compare for the years 1952 and 2007?**


```r
gapminder %>% 
  ggplot(aes(x= year, y = lifeExp, group = year)) + geom_boxplot() + 
  labs(title = "Life expectancy 1952-2007", 
       x = "Year", 
       y = "Life expectancy")
```

![](lab11_hw_files/figure-html/unnamed-chunk-8-1.png)<!-- -->


**4. Your answer above doesn't tell the whole story since life expectancy varies by region. Make a summary that shows the min, mean, and max life expectancy by continent for all years represented in the data.**


```r
gapminder %>% 
  group_by(continent) %>% 
  select(continent, year, lifeExp) %>% 
  mutate(min_lifeExp = min(lifeExp), max_lifeExp = max(lifeExp), mean_lifeExp = mean(lifeExp)) %>% 
  arrange(continent)
```

```
## # A tibble: 1,704 × 6
## # Groups:   continent [5]
##    continent  year lifeExp min_lifeExp max_lifeExp mean_lifeExp
##    <fct>     <int>   <dbl>       <dbl>       <dbl>        <dbl>
##  1 Africa     1952    43.1        23.6        76.4         48.9
##  2 Africa     1957    45.7        23.6        76.4         48.9
##  3 Africa     1962    48.3        23.6        76.4         48.9
##  4 Africa     1967    51.4        23.6        76.4         48.9
##  5 Africa     1972    54.5        23.6        76.4         48.9
##  6 Africa     1977    58.0        23.6        76.4         48.9
##  7 Africa     1982    61.4        23.6        76.4         48.9
##  8 Africa     1987    65.8        23.6        76.4         48.9
##  9 Africa     1992    67.7        23.6        76.4         48.9
## 10 Africa     1997    69.2        23.6        76.4         48.9
## # … with 1,694 more rows
```


**5. How has life expectancy changed between 1952-2007 for each continent?**


```r
gapminder %>% 
  group_by(continent) %>% 
  select(continent, year, lifeExp) %>% 
  mutate(min_lifeExp = min(lifeExp), max_lifeExp = max(lifeExp), mean_lifeExp = mean(lifeExp)) %>% 
  ggplot(aes(x= year, y= lifeExp, color = continent)) + geom_point()
```

![](lab11_hw_files/figure-html/unnamed-chunk-10-1.png)<!-- -->


**6. We are interested in the relationship between per capita GDP and life expectancy; i.e. does having more money help you live longer?**


```r
options(scipen = 999)
```



```r
gapminder %>% 
  ggplot(aes(x= gdpPercap, y= lifeExp)) + geom_jitter() + scale_x_log10() + 
  labs(title = "Life expectancy across gdp per capita",
       x = "gdp per capita",
       y = "life expectancy")
```

![](lab11_hw_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

**7. Which countries have had the largest population growth since 1952?**


```r
gapminder %>% 
  group_by(continent, country) %>% 
  select(country, year, continent, pop, gdpPercap) %>% 
  mutate(population_growth = pop - lag(pop)) %>% 
  summarize(gdpPercap, largest_population_growth = max(population_growth, na.rm = T)) %>% 
  arrange(desc(largest_population_growth))
```

```
## `summarise()` has grouped output by 'continent', 'country'. You can override
## using the `.groups` argument.
```

```
## # A tibble: 1,704 × 4
## # Groups:   continent, country [142]
##    continent country gdpPercap largest_population_growth
##    <fct>     <fct>       <dbl>                     <int>
##  1 Asia      China        400.                 107480000
##  2 Asia      China        576.                 107480000
##  3 Asia      China        488.                 107480000
##  4 Asia      China        613.                 107480000
##  5 Asia      China        677.                 107480000
##  6 Asia      China        741.                 107480000
##  7 Asia      China        962.                 107480000
##  8 Asia      China       1379.                 107480000
##  9 Asia      China       1656.                 107480000
## 10 Asia      China       2289.                 107480000
## # … with 1,694 more rows
```

**8. Use your results from the question above to plot population growth for the top five countries since 1952.**


```r
largest_pop <- gapminder %>% 
  group_by(continent, country) %>% 
  mutate(population_growth = pop - lag(pop)) %>% 
  summarize(gdpPercap,
            year, 
            country, 
            continent,
            largest_population_growth = max(population_growth, na.rm = T)) %>% 
  group_by(largest_population_growth) %>% 
  arrange(desc(largest_population_growth))
```

```
## `summarise()` has grouped output by 'continent', 'country'. You can override
## using the `.groups` argument.
```


```r
five_fast_growing_countries <- largest_pop %>% 
  filter(largest_population_growth > 16017570)
```


```r
five_fast_growing_countries %>% 
  ggplot(aes(x=country, y=largest_population_growth, fill = country)) + geom_col() + 
  labs(title = "Top five countries with the largest population growth since 1952", 
       x = "Country",
       y = "Population growth")
```

![](lab11_hw_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

**9. How does per-capita GDP growth compare between these same five countries?**


```r
five_fast_growing_countries %>% 
  ggplot(aes(x=year, y=gdpPercap, fill = country)) + geom_area() + 
  facet_wrap(~country, ncol = 5) + theme(axis.text.x = element_text(angle = 60, hjust = 1)) + scale_y_log10() + 
  labs(title= "GDP per capita growth in top 5 growing countries",
       x = "Year",
       y = "GDP per capita")
```

![](lab11_hw_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

**10. Make one plot of your choice that uses faceting!**

GDP per capita in the top 5 countries that experienced periods of the highest population decline

```r
smallest_pop <- gapminder %>% 
  group_by(continent, country) %>% 
  mutate(population_growth = pop - lag(pop)) %>% 
  summarize(gdpPercap,
            year, 
            country, 
            continent,
            smallest_population_growth = min(population_growth, na.rm = T)) %>% 
  group_by(smallest_population_growth) %>% 
  arrange(smallest_population_growth)
```

```
## `summarise()` has grouped output by 'continent', 'country'. You can override
## using the `.groups` argument.
```


```r
five_slowest_growing_countries <- smallest_pop %>% 
  filter(smallest_population_growth < -592448)
```



```r
five_slowest_growing_countries %>% 
  ggplot(aes(x=year, y=gdpPercap, fill = country)) + geom_area() + 
  facet_wrap(~country, ncol = 5) + theme(axis.text.x = element_text(angle = 60, hjust = 1)) + scale_y_log10() + 
  labs(title= "GDP per capita growth in countries that experienced greatest population decline",
       x = "Year",
       y = "GDP per capita")
```

![](lab11_hw_files/figure-html/unnamed-chunk-20-1.png)<!-- -->


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
