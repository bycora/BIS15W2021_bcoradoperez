---
title: "Lab 2 Homework"
author: "Byron Corado Perez"
date: "2021-01-12"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

1. What is a vector in R?
#A vector is the simplest for of data in R, typically, one class of data. 

2. What is a data matrix in R?
#A data matrix is a set of the same class of vectors formatted in rows and columns.

3. Below are data collected by three scientists (Jill, Steve, Susan in order) measuring temperatures of eight hot springs. Run this code chunk to create the vectors.  

```r
spring_1 <- c(36.25, 35.40, 35.30)
spring_2 <- c(35.15, 35.35, 33.35)
spring_3 <- c(30.70, 29.65, 29.20)
spring_4 <- c(39.70, 40.05, 38.65)
spring_5 <- c(31.85, 31.40, 29.30)
spring_6 <- c(30.20, 30.65, 29.75)
spring_7 <- c(32.90, 32.50, 32.80)
spring_8 <- c(36.80, 36.45, 33.15)
```

4. Build a data matrix that has the springs as rows and the columns as scientists.  

```r
spring_list<-c(spring_1,spring_2,spring_3,spring_4,spring_5,spring_6,spring_7,spring_8)
spring_list
```

```
##  [1] 36.25 35.40 35.30 35.15 35.35 33.35 30.70 29.65 29.20 39.70 40.05 38.65
## [13] 31.85 31.40 29.30 30.20 30.65 29.75 32.90 32.50 32.80 36.80 36.45 33.15
```

```r
spring_matrix<-matrix(spring_list, nrow=8,byrow = T)
spring_matrix
```

```
##       [,1]  [,2]  [,3]
## [1,] 36.25 35.40 35.30
## [2,] 35.15 35.35 33.35
## [3,] 30.70 29.65 29.20
## [4,] 39.70 40.05 38.65
## [5,] 31.85 31.40 29.30
## [6,] 30.20 30.65 29.75
## [7,] 32.90 32.50 32.80
## [8,] 36.80 36.45 33.15
```

5. The names of the springs are 1.Bluebell Spring, 2.Opal Spring, 3.Riverside Spring, 4.Too Hot Spring, 5.Mystery Spring, 6.Emerald Spring, 7.Black Spring, 8.Pearl Spring. Name the rows and columns in the data matrix. Start by making two new vectors with the names, then use `colnames()` and `rownames()` to name the columns and rows.

```r
spring_names<-c("1.Bluebell Spring", "2.Opal Spring", "3.Riverside Spring", "4.Too Hot Spring", "5.Mystery Spring", "6.Emerald Spring", "7.Black Spring", "8.Pearl Spring")
rownames(spring_matrix)<-spring_names
spring_names
```

```
## [1] "1.Bluebell Spring"  "2.Opal Spring"      "3.Riverside Spring"
## [4] "4.Too Hot Spring"   "5.Mystery Spring"   "6.Emerald Spring"  
## [7] "7.Black Spring"     "8.Pearl Spring"
```

```r
scientist_names<-c("Jill", "Steve", "Susan")
colnames(spring_matrix)<-scientist_names
scientist_names
```

```
## [1] "Jill"  "Steve" "Susan"
```

```r
print(spring_matrix)
```

```
##                     Jill Steve Susan
## 1.Bluebell Spring  36.25 35.40 35.30
## 2.Opal Spring      35.15 35.35 33.35
## 3.Riverside Spring 30.70 29.65 29.20
## 4.Too Hot Spring   39.70 40.05 38.65
## 5.Mystery Spring   31.85 31.40 29.30
## 6.Emerald Spring   30.20 30.65 29.75
## 7.Black Spring     32.90 32.50 32.80
## 8.Pearl Spring     36.80 36.45 33.15
```

6. Calculate the mean temperature of all three springs.

```r
?rowSums()
rowSums(spring_matrix)
```

```
##  1.Bluebell Spring      2.Opal Spring 3.Riverside Spring   4.Too Hot Spring 
##             106.95             103.85              89.55             118.40 
##   5.Mystery Spring   6.Emerald Spring     7.Black Spring     8.Pearl Spring 
##              92.55              90.60              98.20             106.40
```

```r
Spring_Mean<-c(rowSums(spring_matrix)/3)
Spring_Mean
```

```
##  1.Bluebell Spring      2.Opal Spring 3.Riverside Spring   4.Too Hot Spring 
##           35.65000           34.61667           29.85000           39.46667 
##   5.Mystery Spring   6.Emerald Spring     7.Black Spring     8.Pearl Spring 
##           30.85000           30.20000           32.73333           35.46667
```

7. Add this as a new column in the data matrix.  

```r
spring_total<-cbind(spring_matrix,Spring_Mean)
spring_total
```

```
##                     Jill Steve Susan Spring_Mean
## 1.Bluebell Spring  36.25 35.40 35.30    35.65000
## 2.Opal Spring      35.15 35.35 33.35    34.61667
## 3.Riverside Spring 30.70 29.65 29.20    29.85000
## 4.Too Hot Spring   39.70 40.05 38.65    39.46667
## 5.Mystery Spring   31.85 31.40 29.30    30.85000
## 6.Emerald Spring   30.20 30.65 29.75    30.20000
## 7.Black Spring     32.90 32.50 32.80    32.73333
## 8.Pearl Spring     36.80 36.45 33.15    35.46667
```

8. Show Susan's value for Opal Spring only.

```r
spring_total[2,3]
```

```
## [1] 33.35
```

9. Calculate the mean for Jill's column only.  

```r
mean(spring_total[,1])
```

```
## [1] 34.19375
```

10. Use the data matrix to perform one calculation or operation of your interest.

```r
ind_sum<-c(colSums(spring_total))
ind_sum
```

```
##        Jill       Steve       Susan Spring_Mean 
##    273.5500    271.4500    261.5000    268.8333
```

```r
ind_avg<-(ind_sum/8)
ind_avg
```

```
##        Jill       Steve       Susan Spring_Mean 
##    34.19375    33.93125    32.68750    33.60417
```

```r
spring_final<-rbind(spring_total,ind_avg)
spring_final
```

```
##                        Jill    Steve   Susan Spring_Mean
## 1.Bluebell Spring  36.25000 35.40000 35.3000    35.65000
## 2.Opal Spring      35.15000 35.35000 33.3500    34.61667
## 3.Riverside Spring 30.70000 29.65000 29.2000    29.85000
## 4.Too Hot Spring   39.70000 40.05000 38.6500    39.46667
## 5.Mystery Spring   31.85000 31.40000 29.3000    30.85000
## 6.Emerald Spring   30.20000 30.65000 29.7500    30.20000
## 7.Black Spring     32.90000 32.50000 32.8000    32.73333
## 8.Pearl Spring     36.80000 36.45000 33.1500    35.46667
## ind_avg            34.19375 33.93125 32.6875    33.60417
```
#wanted to find the overall average spring temp for all the springs from each scientist.

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.  
