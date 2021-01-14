---
title: "Lab 3 Homework"
author: "Byron Corado Perez"
date: "2021-01-14"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

```r
?msleep
#Taken from V. M. Savage and G. B. West. A quantitative, theoretical framework for understanding mammalian sleep. Proceedings of the National Academy of Sciences, 104 (3):1051-1056, 2007.
```

2. Store these data into a new data frame `sleep`.

```r
sleep<-msleep
sleep
```

```
## # A tibble: 83 x 11
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
##  1 Chee… Acin… carni Carn… lc                  12.1      NA        NA      11.9
##  2 Owl … Aotus omni  Prim… <NA>                17         1.8      NA       7  
##  3 Moun… Aplo… herbi Rode… nt                  14.4       2.4      NA       9.6
##  4 Grea… Blar… omni  Sori… lc                  14.9       2.3       0.133   9.1
##  5 Cow   Bos   herbi Arti… domesticated         4         0.7       0.667  20  
##  6 Thre… Brad… herbi Pilo… <NA>                14.4       2.2       0.767   9.6
##  7 Nort… Call… carni Carn… vu                   8.7       1.4       0.383  15.3
##  8 Vesp… Calo… <NA>  Rode… <NA>                 7        NA        NA      17  
##  9 Dog   Canis carni Carn… domesticated        10.1       2.9       0.333  13.9
## 10 Roe … Capr… herbi Arti… lc                   3        NA        NA      21  
## # … with 73 more rows, and 2 more variables: brainwt <dbl>, bodywt <dbl>
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  

```r
dim(sleep)
```

```
## [1] 83 11
```

```r
#The dimensions are 83 rows and 11 variables. I know by running the data through the function dim() which gave me a numerical output of the observations and the variables.
```

4. Are there any NAs in the data? How did you determine this? Please show your code.  

```r
no_sleep<-is.na(sleep)
no_sleep
```

```
##        name genus  vore order conservation sleep_total sleep_rem sleep_cycle
##  [1,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
##  [2,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
##  [3,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
##  [4,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
##  [5,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
##  [6,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
##  [7,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
##  [8,] FALSE FALSE  TRUE FALSE         TRUE       FALSE      TRUE        TRUE
##  [9,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [10,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [11,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [12,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [13,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [14,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [15,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [16,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [17,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [18,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [19,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [20,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [21,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [22,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [23,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [24,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [25,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [26,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [27,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [28,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [29,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [30,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [31,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [32,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [33,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [34,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [35,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [36,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [37,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [38,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [39,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [40,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [41,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [42,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [43,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [44,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [45,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [46,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [47,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [48,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [49,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [50,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [51,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [52,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [53,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [54,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [55,] FALSE FALSE  TRUE FALSE        FALSE       FALSE     FALSE        TRUE
## [56,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [57,] FALSE FALSE  TRUE FALSE         TRUE       FALSE      TRUE        TRUE
## [58,] FALSE FALSE  TRUE FALSE         TRUE       FALSE     FALSE        TRUE
## [59,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [60,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [61,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [62,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [63,] FALSE FALSE  TRUE FALSE        FALSE       FALSE     FALSE        TRUE
## [64,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [65,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [66,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [67,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [68,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [69,] FALSE FALSE  TRUE FALSE         TRUE       FALSE     FALSE        TRUE
## [70,] FALSE FALSE FALSE FALSE        FALSE       FALSE      TRUE        TRUE
## [71,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [72,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE        TRUE
## [73,] FALSE FALSE  TRUE FALSE         TRUE       FALSE     FALSE       FALSE
## [74,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [75,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [76,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [77,] FALSE FALSE FALSE FALSE        FALSE       FALSE     FALSE       FALSE
## [78,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [79,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
## [80,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [81,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE        TRUE
## [82,] FALSE FALSE FALSE FALSE         TRUE       FALSE      TRUE        TRUE
## [83,] FALSE FALSE FALSE FALSE         TRUE       FALSE     FALSE       FALSE
##       awake brainwt bodywt
##  [1,] FALSE    TRUE  FALSE
##  [2,] FALSE   FALSE  FALSE
##  [3,] FALSE    TRUE  FALSE
##  [4,] FALSE   FALSE  FALSE
##  [5,] FALSE   FALSE  FALSE
##  [6,] FALSE    TRUE  FALSE
##  [7,] FALSE    TRUE  FALSE
##  [8,] FALSE    TRUE  FALSE
##  [9,] FALSE   FALSE  FALSE
## [10,] FALSE   FALSE  FALSE
## [11,] FALSE   FALSE  FALSE
## [12,] FALSE   FALSE  FALSE
## [13,] FALSE    TRUE  FALSE
## [14,] FALSE   FALSE  FALSE
## [15,] FALSE   FALSE  FALSE
## [16,] FALSE   FALSE  FALSE
## [17,] FALSE   FALSE  FALSE
## [18,] FALSE   FALSE  FALSE
## [19,] FALSE   FALSE  FALSE
## [20,] FALSE   FALSE  FALSE
## [21,] FALSE   FALSE  FALSE
## [22,] FALSE   FALSE  FALSE
## [23,] FALSE   FALSE  FALSE
## [24,] FALSE   FALSE  FALSE
## [25,] FALSE   FALSE  FALSE
## [26,] FALSE   FALSE  FALSE
## [27,] FALSE    TRUE  FALSE
## [28,] FALSE   FALSE  FALSE
## [29,] FALSE   FALSE  FALSE
## [30,] FALSE    TRUE  FALSE
## [31,] FALSE    TRUE  FALSE
## [32,] FALSE   FALSE  FALSE
## [33,] FALSE   FALSE  FALSE
## [34,] FALSE   FALSE  FALSE
## [35,] FALSE    TRUE  FALSE
## [36,] FALSE   FALSE  FALSE
## [37,] FALSE    TRUE  FALSE
## [38,] FALSE   FALSE  FALSE
## [39,] FALSE    TRUE  FALSE
## [40,] FALSE   FALSE  FALSE
## [41,] FALSE    TRUE  FALSE
## [42,] FALSE   FALSE  FALSE
## [43,] FALSE   FALSE  FALSE
## [44,] FALSE    TRUE  FALSE
## [45,] FALSE   FALSE  FALSE
## [46,] FALSE    TRUE  FALSE
## [47,] FALSE    TRUE  FALSE
## [48,] FALSE   FALSE  FALSE
## [49,] FALSE   FALSE  FALSE
## [50,] FALSE   FALSE  FALSE
## [51,] FALSE    TRUE  FALSE
## [52,] FALSE   FALSE  FALSE
## [53,] FALSE    TRUE  FALSE
## [54,] FALSE   FALSE  FALSE
## [55,] FALSE   FALSE  FALSE
## [56,] FALSE    TRUE  FALSE
## [57,] FALSE    TRUE  FALSE
## [58,] FALSE   FALSE  FALSE
## [59,] FALSE    TRUE  FALSE
## [60,] FALSE    TRUE  FALSE
## [61,] FALSE    TRUE  FALSE
## [62,] FALSE   FALSE  FALSE
## [63,] FALSE   FALSE  FALSE
## [64,] FALSE   FALSE  FALSE
## [65,] FALSE    TRUE  FALSE
## [66,] FALSE   FALSE  FALSE
## [67,] FALSE   FALSE  FALSE
## [68,] FALSE   FALSE  FALSE
## [69,] FALSE   FALSE  FALSE
## [70,] FALSE   FALSE  FALSE
## [71,] FALSE   FALSE  FALSE
## [72,] FALSE    TRUE  FALSE
## [73,] FALSE   FALSE  FALSE
## [74,] FALSE   FALSE  FALSE
## [75,] FALSE   FALSE  FALSE
## [76,] FALSE    TRUE  FALSE
## [77,] FALSE   FALSE  FALSE
## [78,] FALSE   FALSE  FALSE
## [79,] FALSE   FALSE  FALSE
## [80,] FALSE    TRUE  FALSE
## [81,] FALSE   FALSE  FALSE
## [82,] FALSE   FALSE  FALSE
## [83,] FALSE   FALSE  FALSE
```

```r
?is.na
#Yes there are a few occasions of data that shows NA. I determined this by using the "is.na(x)" function to help indicate which elements are missing/have no data.
```

5. Show a list of the column names is this data frame.

```r
colnames(sleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```

6. How many herbivores are represented in the data?  

```r
grass_nommers<-subset(sleep, vore == "herbi")
grass_nommers
```

```
## # A tibble: 32 x 11
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
##  1 Moun… Aplo… herbi Rode… nt                  14.4       2.4      NA       9.6
##  2 Cow   Bos   herbi Arti… domesticated         4         0.7       0.667  20  
##  3 Thre… Brad… herbi Pilo… <NA>                14.4       2.2       0.767   9.6
##  4 Roe … Capr… herbi Arti… lc                   3        NA        NA      21  
##  5 Goat  Capri herbi Arti… lc                   5.3       0.6      NA      18.7
##  6 Guin… Cavis herbi Rode… domesticated         9.4       0.8       0.217  14.6
##  7 Chin… Chin… herbi Rode… domesticated        12.5       1.5       0.117  11.5
##  8 Tree… Dend… herbi Hyra… lc                   5.3       0.5      NA      18.7
##  9 Asia… Elep… herbi Prob… en                   3.9      NA        NA      20.1
## 10 Horse Equus herbi Peri… domesticated         2.9       0.6       1      21.1
## # … with 22 more rows, and 2 more variables: brainwt <dbl>, bodywt <dbl>
```
#There are 32 herbivores represented in this data

7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
names(sleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```

```r
big_sleepers<-subset(sleep, bodywt >= 200)
big_sleepers
```

```
## # A tibble: 7 x 11
##   name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##   <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
## 1 Cow   Bos   herbi Arti… domesticated         4         0.7       0.667  20  
## 2 Asia… Elep… herbi Prob… en                   3.9      NA        NA      20.1
## 3 Horse Equus herbi Peri… domesticated         2.9       0.6       1      21.1
## 4 Gira… Gira… herbi Arti… cd                   1.9       0.4      NA      22.1
## 5 Pilo… Glob… carni Ceta… cd                   2.7       0.1      NA      21.4
## 6 Afri… Loxo… herbi Prob… vu                   3.3      NA        NA      20.7
## 7 Braz… Tapi… herbi Peri… vu                   4.4       1         0.9    19.6
## # … with 2 more variables: brainwt <dbl>, bodywt <dbl>
```

```r
tiny_sleepers<-subset(sleep, bodywt <=1)
tiny_sleepers
```

```
## # A tibble: 36 x 11
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
##  1 Owl … Aotus omni  Prim… <NA>                17         1.8      NA       7  
##  2 Grea… Blar… omni  Sori… lc                  14.9       2.3       0.133   9.1
##  3 Vesp… Calo… <NA>  Rode… <NA>                 7        NA        NA      17  
##  4 Guin… Cavis herbi Rode… domesticated         9.4       0.8       0.217  14.6
##  5 Chin… Chin… herbi Rode… domesticated        12.5       1.5       0.117  11.5
##  6 Star… Cond… omni  Sori… lc                  10.3       2.2      NA      13.7
##  7 Afri… Cric… omni  Rode… <NA>                 8.3       2        NA      15.7
##  8 Less… Cryp… omni  Sori… lc                   9.1       1.4       0.15   14.9
##  9 Big … Epte… inse… Chir… lc                  19.7       3.9       0.117   4.3
## 10 Euro… Erin… omni  Erin… lc                  10.1       3.5       0.283  13.9
## # … with 26 more rows, and 2 more variables: brainwt <dbl>, bodywt <dbl>
```

```r
small<-data.frame(tiny_sleepers)
small
```

```
##                              name        genus    vore           order
## 1                      Owl monkey        Aotus    omni        Primates
## 2      Greater short-tailed shrew      Blarina    omni    Soricomorpha
## 3                    Vesper mouse      Calomys    <NA>        Rodentia
## 4                      Guinea pig        Cavis   herbi        Rodentia
## 5                      Chinchilla   Chinchilla   herbi        Rodentia
## 6                 Star-nosed mole    Condylura    omni    Soricomorpha
## 7       African giant pouched rat   Cricetomys    omni        Rodentia
## 8       Lesser short-tailed shrew    Cryptotis    omni    Soricomorpha
## 9                   Big brown bat    Eptesicus insecti      Chiroptera
## 10              European hedgehog    Erinaceus    omni  Erinaceomorpha
## 11      Western american chipmunk     Eutamias   herbi        Rodentia
## 12                         Galago       Galago    omni        Primates
## 13           Thick-tailed opposum   Lutreolina   carni Didelphimorphia
## 14               Mongolian gerbil     Meriones   herbi        Rodentia
## 15                 Golden hamster Mesocricetus   herbi        Rodentia
## 16                          Vole      Microtus   herbi        Rodentia
## 17                    House mouse          Mus   herbi        Rodentia
## 18               Little brown bat       Myotis insecti      Chiroptera
## 19           Round-tailed muskrat     Neofiber   herbi        Rodentia
## 20                           Degu      Octodon   herbi        Rodentia
## 21     Northern grasshopper mouse    Onychomys   carni        Rodentia
## 22                Desert hedgehog  Paraechinus    <NA>  Erinaceomorpha
## 23                     Deer mouse   Peromyscus    <NA>        Rodentia
## 24                 Laboratory rat       Rattus   herbi        Rodentia
## 25          African striped mouse    Rhabdomys    omni        Rodentia
## 26                Squirrel monkey      Saimiri    omni        Primates
## 27          Eastern american mole     Scalopus insecti    Soricomorpha
## 28                     Cotton rat     Sigmodon   herbi        Rodentia
## 29                       Mole rat       Spalax    <NA>        Rodentia
## 30         Arctic ground squirrel Spermophilus   herbi        Rodentia
## 31 Thirteen-lined ground squirrel Spermophilus   herbi        Rodentia
## 32 Golden-mantled ground squirrel Spermophilus   herbi        Rodentia
## 33                     Musk shrew       Suncus    <NA>    Soricomorpha
## 34      Eastern american chipmunk       Tamias   herbi        Rodentia
## 35                         Tenrec       Tenrec    omni    Afrosoricida
## 36                     Tree shrew       Tupaia    omni      Scandentia
##    conservation sleep_total sleep_rem sleep_cycle awake brainwt bodywt
## 1          <NA>        17.0       1.8          NA   7.0 0.01550  0.480
## 2            lc        14.9       2.3   0.1333333   9.1 0.00029  0.019
## 3          <NA>         7.0        NA          NA  17.0      NA  0.045
## 4  domesticated         9.4       0.8   0.2166667  14.6 0.00550  0.728
## 5  domesticated        12.5       1.5   0.1166667  11.5 0.00640  0.420
## 6            lc        10.3       2.2          NA  13.7 0.00100  0.060
## 7          <NA>         8.3       2.0          NA  15.7 0.00660  1.000
## 8            lc         9.1       1.4   0.1500000  14.9 0.00014  0.005
## 9            lc        19.7       3.9   0.1166667   4.3 0.00030  0.023
## 10           lc        10.1       3.5   0.2833333  13.9 0.00350  0.770
## 11         <NA>        14.9        NA          NA   9.1      NA  0.071
## 12         <NA>         9.8       1.1   0.5500000  14.2 0.00500  0.200
## 13           lc        19.4       6.6          NA   4.6      NA  0.370
## 14           lc        14.2       1.9          NA   9.8      NA  0.053
## 15           en        14.3       3.1   0.2000000   9.7 0.00100  0.120
## 16         <NA>        12.8        NA          NA  11.2      NA  0.035
## 17           nt        12.5       1.4   0.1833333  11.5 0.00040  0.022
## 18         <NA>        19.9       2.0   0.2000000   4.1 0.00025  0.010
## 19           nt        14.6        NA          NA   9.4      NA  0.266
## 20           lc         7.7       0.9          NA  16.3      NA  0.210
## 21           lc        14.5        NA          NA   9.5      NA  0.028
## 22           lc        10.3       2.7          NA  13.7 0.00240  0.550
## 23         <NA>        11.5        NA          NA  12.5      NA  0.021
## 24           lc        13.0       2.4   0.1833333  11.0 0.00190  0.320
## 25         <NA>         8.7        NA          NA  15.3      NA  0.044
## 26         <NA>         9.6       1.4          NA  14.4 0.02000  0.743
## 27           lc         8.4       2.1   0.1666667  15.6 0.00120  0.075
## 28         <NA>        11.3       1.1   0.1500000  12.7 0.00118  0.148
## 29         <NA>        10.6       2.4          NA  13.4 0.00300  0.122
## 30           lc        16.6        NA          NA   7.4 0.00570  0.920
## 31           lc        13.8       3.4   0.2166667  10.2 0.00400  0.101
## 32           lc        15.9       3.0          NA   8.1      NA  0.205
## 33         <NA>        12.8       2.0   0.1833333  11.2 0.00033  0.048
## 34         <NA>        15.8        NA          NA   8.2      NA  0.112
## 35         <NA>        15.6       2.3          NA   8.4 0.00260  0.900
## 36         <NA>         8.9       2.6   0.2333333  15.1 0.00250  0.104
```

```r
large<-data.frame(big_sleepers)
large
```

```
##               name         genus  vore          order conservation sleep_total
## 1              Cow           Bos herbi   Artiodactyla domesticated         4.0
## 2   Asian elephant       Elephas herbi    Proboscidea           en         3.9
## 3            Horse         Equus herbi Perissodactyla domesticated         2.9
## 4          Giraffe       Giraffa herbi   Artiodactyla           cd         1.9
## 5      Pilot whale Globicephalus carni        Cetacea           cd         2.7
## 6 African elephant     Loxodonta herbi    Proboscidea           vu         3.3
## 7  Brazilian tapir       Tapirus herbi Perissodactyla           vu         4.4
##   sleep_rem sleep_cycle awake brainwt   bodywt
## 1       0.7   0.6666667 20.00   0.423  600.000
## 2        NA          NA 20.10   4.603 2547.000
## 3       0.6   1.0000000 21.10   0.655  521.000
## 4       0.4          NA 22.10      NA  899.995
## 5       0.1          NA 21.35      NA  800.000
## 6        NA          NA 20.70   5.712 6654.000
## 7       1.0   0.9000000 19.60   0.169  207.501
```

8. What is the mean weight for both the small and large mammals?

```r
lweight<-large$bodywt
mean(lweight)
```

```
## [1] 1747.071
```


```r
sweight<-small$bodywt
mean(sweight)
```

```
## [1] 0.2596667
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  

```r
bigsleep<-large$sleep_total
mean(bigsleep)
```

```
## [1] 3.3
```


```r
smallsleep<-small$sleep_total
mean(smallsleep)
```

```
## [1] 12.65833
```
#On average, small animals sleep longer. They sleep ~9.36 hours longer

10. Which animal is the sleepiest among the entire dataframe?

```r
sleepiest_beans<-subset(sleep, sleep_total>=19)
gotta_nap<-data.frame(sleepiest_beans)
gotta_nap
```

```
##                   name      genus    vore           order conservation
## 1        Big brown bat  Eptesicus insecti      Chiroptera           lc
## 2 Thick-tailed opposum Lutreolina   carni Didelphimorphia           lc
## 3     Little brown bat     Myotis insecti      Chiroptera         <NA>
##   sleep_total sleep_rem sleep_cycle awake brainwt bodywt
## 1        19.7       3.9   0.1166667   4.3 0.00030  0.023
## 2        19.4       6.6          NA   4.6      NA  0.370
## 3        19.9       2.0   0.2000000   4.1 0.00025  0.010
```
#The sleepiest animal would be the Little brown bat, taking 19.9 hours of wonderful rest.

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
