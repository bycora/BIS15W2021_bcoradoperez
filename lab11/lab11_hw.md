---
title: "Lab 11 Homework"
author: "Byron Corado Perez"
date: "2021-02-17"
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
names(gapminder)
```

```
## [1] "country"   "continent" "year"      "lifeExp"   "pop"       "gdpPercap"
```

```r
glimpse(gapminder)
```

```
## Rows: 1,704
## Columns: 6
## $ country   <fct> Afghanistan, Afghanistan, Afghanistan, Afghanistan, Afgha...
## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asi...
## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 199...
## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 4...
## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372,...
## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.113...
```

```r
naniar::miss_var_summary(gapminder)
```

```
## # A tibble: 6 x 3
##   variable  n_miss pct_miss
##   <chr>      <int>    <dbl>
## 1 country        0        0
## 2 continent      0        0
## 3 year           0        0
## 4 lifeExp        0        0
## 5 pop            0        0
## 6 gdpPercap      0        0
```

**2. Among the interesting variables in gapminder is life expectancy. How has global life expectancy changed between 1952 and 2007?**

```r
gapminder %>% 
  group_by(year) %>% 
  filter(between(year,1952,2007)) %>% 
  summarize(avg_life_exp=mean(lifeExp))
```

```
## # A tibble: 12 x 2
##     year avg_life_exp
##    <int>        <dbl>
##  1  1952         49.1
##  2  1957         51.5
##  3  1962         53.6
##  4  1967         55.7
##  5  1972         57.6
##  6  1977         59.6
##  7  1982         61.5
##  8  1987         63.2
##  9  1992         64.2
## 10  1997         65.0
## 11  2002         65.7
## 12  2007         67.0
```
#Average Life expectancy has been slowly increasing from 1952 with 49 years being the average to 2007 with 67 years being the average.


```r
gapminder %>% 
  group_by(year) %>% 
  filter(between(year,1952,2007)) %>% 
  summarize(avg_life_exp=mean(lifeExp)) %>% 
  ggplot(aes(x= year, y= avg_life_exp)) + geom_point() + geom_smooth(method="lm", se=FALSE, color="blue") +
  labs(title="Global Life Expectancy between 1952 to 2007", x = "Year", y= "Global Life Expectancy")
```

```
## `geom_smooth()` using formula 'y ~ x'
```

![](lab11_hw_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

**3. How do the distributions of life expectancy compare for the years 1952 and 2007?**

```r
gapminder %>% 
  group_by(year) %>% 
  filter(year=="1952" | year=="2007") %>% 
  summarize(mean_lifeExp=mean(lifeExp),
            min_lifeExp=min(lifeExp),
            max_lifeExp=max(lifeExp),
            median_lifeExp=median(lifeExp))
```

```
## # A tibble: 2 x 5
##    year mean_lifeExp min_lifeExp max_lifeExp median_lifeExp
##   <int>        <dbl>       <dbl>       <dbl>          <dbl>
## 1  1952         49.1        28.8        72.7           45.1
## 2  2007         67.0        39.6        82.6           71.9
```

```r
gapminder %>% 
  group_by(year) %>% 
  filter(year=="1952" | year=="2007") %>% 
  ggplot(aes(group=year, x=year, y=lifeExp))+
  geom_boxplot(color="green4", fill="orange2") +
  labs(title = "Global Life Expectancy: 1952 versus 2007", x="Year", y= "Life Expectancy")
```

![](lab11_hw_files/figure-html/unnamed-chunk-9-1.png)<!-- -->
#The (min, mean, max and median) life expectancies of 1952 were all at a lesser age than the life expectancy of 2007 by about 10 or more years each.

**4. Your answer above doesn't tell the whole story since life expectancy varies by region. Make a summary that shows the min, mean, and max life expectancy by continent for all years represented in the data.**

```r
gapminder %>% 
  group_by(continent, year) %>%
  summarize(min_lifeExp=min(lifeExp),
            mean_lifeExp=mean(lifeExp),
            max_lifeExp=max(lifeExp))
```

```
## `summarise()` has grouped output by 'continent'. You can override using the `.groups` argument.
```

```
## # A tibble: 60 x 5
## # Groups:   continent [5]
##    continent  year min_lifeExp mean_lifeExp max_lifeExp
##    <fct>     <int>       <dbl>        <dbl>       <dbl>
##  1 Africa     1952        30           39.1        52.7
##  2 Africa     1957        31.6         41.3        58.1
##  3 Africa     1962        32.8         43.3        60.2
##  4 Africa     1967        34.1         45.3        61.6
##  5 Africa     1972        35.4         47.5        64.3
##  6 Africa     1977        36.8         49.6        67.1
##  7 Africa     1982        38.4         51.6        69.9
##  8 Africa     1987        39.9         53.3        71.9
##  9 Africa     1992        23.6         53.6        73.6
## 10 Africa     1997        36.1         53.6        74.8
## # ... with 50 more rows
```

```r
gapminder %>% 
  group_by(continent, year) %>%
  ggplot(aes(group=continent, x=continent, y=lifeExp, fill=continent)) +
  geom_boxplot() + facet_wrap(~year)+
  labs(title="Life Expectancy by Continent per Year", x="Continent", y="Life Expectancy")+
  theme(axis.text.x = element_text(angle = 45, hjust = 1), plot.title = element_text(hjust =0.5))
```

![](lab11_hw_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

**5. How has life expectancy changed between 1952-2007 for each continent?**

```r
gapminder %>% 
  group_by(continent, year) %>% 
  filter(between(year, 1952,2007)) %>% 
    summarize(mean_lifeExp=mean(lifeExp))
```

```
## `summarise()` has grouped output by 'continent'. You can override using the `.groups` argument.
```

```
## # A tibble: 60 x 3
## # Groups:   continent [5]
##    continent  year mean_lifeExp
##    <fct>     <int>        <dbl>
##  1 Africa     1952         39.1
##  2 Africa     1957         41.3
##  3 Africa     1962         43.3
##  4 Africa     1967         45.3
##  5 Africa     1972         47.5
##  6 Africa     1977         49.6
##  7 Africa     1982         51.6
##  8 Africa     1987         53.3
##  9 Africa     1992         53.6
## 10 Africa     1997         53.6
## # ... with 50 more rows
```

```r
gapminder %>%
  group_by(continent, year) %>%
  filter(between(year, 1952, 2007)) %>%
  summarize(mean_lifeExp=mean(lifeExp)) %>%
  ggplot(aes(x=year, y=mean_lifeExp)) +
  geom_line() + geom_point(shape=1, color="orange") + facet_wrap(~continent)+
  labs(title="Global Life Expectancy beteen 1952 to 2007",
       x="Year", y="Life Expectancy")+
   theme(axis.text.x = element_text(angle=45, hjust=1), plot.title=element_text(hjust=.5))
```

```
## `summarise()` has grouped output by 'continent'. You can override using the `.groups` argument.
```

![](lab11_hw_files/figure-html/unnamed-chunk-13-1.png)<!-- -->
#Once again we see that the life expectancies of each country increased throughout the years. It seems that Asia had the greatest change in life expectancy and Oceania had the lowest change in life expectancy.

**6. We are interested in the relationship between per capita GDP and life expectancy; i.e. does having more money help you live longer?**

```r
gapminder %>% 
  select(gdpPercap, lifeExp) %>% 
  arrange(gdpPercap)
```

```
## # A tibble: 1,704 x 2
##    gdpPercap lifeExp
##        <dbl>   <dbl>
##  1      241.    45.0
##  2      278.    46.5
##  3      299.    42.1
##  4      300.    32.5
##  5      312.    42.6
##  6      329.    35.9
##  7      331     36.3
##  8      336.    45.0
##  9      339.    39.0
## 10      344.    38.0
## # ... with 1,694 more rows
```

```r
gapminder %>%
  ggplot(aes(x=log10(gdpPercap), y=lifeExp, color=continent, shape=continent)) +
  geom_point(size=1) + geom_smooth(method="lm", se=FALSE)+
  labs(title="Per Capita GDP vs. Life Expectancy",
       x="Per Capita GDP",
       y="Life Expectancy")+
  theme(plot.title=element_text(hjust=.5))
```

```
## `geom_smooth()` using formula 'y ~ x'
```

![](lab11_hw_files/figure-html/unnamed-chunk-15-1.png)<!-- -->
#There does seem to be some benefit with having more money and having a higher life expectancy.

**7. Which countries have had the largest population growth since 1952?**

```r
gapminder %>%
  select(year, pop, country) %>%
  filter(year==1952|year==2007) %>%
  group_by(country) %>%
  summarize(pop_growth=diff(pop)) %>%
  arrange(desc(pop_growth))
```

```
## # A tibble: 142 x 2
##    country       pop_growth
##    <fct>              <int>
##  1 China          762419569
##  2 India          738396331
##  3 United States  143586947
##  4 Indonesia      141495000
##  5 Brazil         133408087
##  6 Pakistan       127924057
##  7 Bangladesh     103561480
##  8 Nigeria        101912068
##  9 Mexico          78556574
## 10 Philippines     68638596
## # ... with 132 more rows
```
# It seems that China and India had the largest population growth since 1952 with about .76 and .73 billion, respectively.

**8. Use your results from the question above to plot population growth for the top five countries since 1952.**

```r
gapminder %>% 
  filter(year==1952|year==2007) %>% 
  group_by(country) %>% 
  summarise(pop_growth=diff(pop)) %>% 
  arrange(desc(pop_growth)) %>% 
  head(n=5) %>% 
  ggplot(aes(x=country, y=pop_growth, fill=country)) + geom_col() +
  theme(plot.title=element_text(hjust=0.5), axis.text.x = element_text(angle = 45, hjust=1))+
  labs(title="Population Growth Since 1952",
       x="Country",
       y="Population Growth")
```

![](lab11_hw_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

**9. How does per-capita GDP growth compare between these same five countries?**

```r
gapminder %>%
  filter(between(year, 1952, 2007)) %>%
  filter(country=="Brazil"|country=="China"|country=="India"|country=="Indonesia"|country=="United States") %>%
  group_by(country) %>%
  summarize(sum_gdpPercap=sum(gdpPercap))
```

```
## # A tibble: 5 x 2
##   country       sum_gdpPercap
## * <fct>                 <dbl>
## 1 Brazil               69952.
## 2 China                17860.
## 3 India                12688.
## 4 Indonesia            20896.
## 5 United States       315134.
```

```r
gapminder %>% 
  filter(year==1952|year==2007) %>% 
  filter(country=="Brazil"|country=="China"|country== "India"|country== "Indonesia"|country== "United States") %>% 
  group_by(country) %>% 
  summarise(sum_gdpPercap=sum(gdpPercap)) %>%  
  ggplot(aes(x=country, y=sum_gdpPercap, fill=country))+geom_col()+ theme_linedraw() +
  theme(plot.title=element_text(hjust=0.5), axis.text.x = element_text(angle = 45, hjust=1))+
  labs(title="Per Capita GDP Growth Since 1952",
       x="Country",
       y="Per Capita GDP Growth")
```

![](lab11_hw_files/figure-html/unnamed-chunk-19-1.png)<!-- -->

**10. Make one plot of your choice that uses faceting!**

```r
names(gapminder)
```

```
## [1] "country"   "continent" "year"      "lifeExp"   "pop"       "gdpPercap"
```

```r
gapminder %>%
  ggplot(aes(x=gdpPercap))+geom_density()+facet_wrap(~year)+
  labs(title="Density of Per Capita GDP per year",
       x="Per Capita GDP",
       y="Density")+
  theme(plot.title=element_text(hjust=0.5), axis.text.x = element_text(angle=45, hjust=1))
```

![](lab11_hw_files/figure-html/unnamed-chunk-21-1.png)<!-- -->

##Was having issues with pushing this file which is why it's a little late

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
