TEST¡ª¡ªTable
========================================================

This is an R Markdown document. Markdown is a simple formatting syntax for authoring web pages (click the **MD** toolbar button for help on Markdown).

When you click the **Knit HTML** button a web page will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```r
library(xtable)
xtable(head(mtcars[, 1:5]))
```

```
## % latex table generated in R 2.15.1 by xtable 1.7-0 package
## % Tue Sep 18 14:33:51 2012
## \begin{table}[ht]
## \begin{center}
## \begin{tabular}{rrrrrr}
##   \hline
##  & mpg & cyl & disp & hp & drat \\ 
##   \hline
## Mazda RX4 & 21.00 & 6.00 & 160.00 & 110.00 & 3.90 \\ 
##   Mazda RX4 Wag & 21.00 & 6.00 & 160.00 & 110.00 & 3.90 \\ 
##   Datsun 710 & 22.80 & 4.00 & 108.00 & 93.00 & 3.85 \\ 
##   Hornet 4 Drive & 21.40 & 6.00 & 258.00 & 110.00 & 3.08 \\ 
##   Hornet Sportabout & 18.70 & 8.00 & 360.00 & 175.00 & 3.15 \\ 
##   Valiant & 18.10 & 6.00 & 225.00 & 105.00 & 2.76 \\ 
##    \hline
## \end{tabular}
## \end{center}
## \end{table}
```



```r
summary(cars)
```

```
##      speed           dist    
##  Min.   : 4.0   Min.   :  2  
##  1st Qu.:12.0   1st Qu.: 26  
##  Median :15.0   Median : 36  
##  Mean   :15.4   Mean   : 43  
##  3rd Qu.:19.0   3rd Qu.: 56  
##  Max.   :25.0   Max.   :120
```


You can also embed plots, for example:


```r
plot(cars)
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 


