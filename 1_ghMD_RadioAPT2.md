Данные биораспределения РФП на основе <sup>68</sup>Ga
================

## Описание препарата

This is an R Markdown format used for publishing markdown documents to
GitHub. When you click the **Knit** button all R code chunks are run and
a markdown file (.md) suitable for publishing to GitHub is generated.

## Including Code

You can include R code in the document as follows:

``` r
library(readxl)
biod <- read_excel("Data/biod.xlsx", col_types = c("text", 
    "text", "text", "text", "text", "numeric", 
    "numeric", "numeric", "numeric", "skip", 
    "skip"))
# View(biod)
summary(biod)
```

    ##    MiceNum              Drug              Organ              Group          
    ##  Length:704         Length:704         Length:704         Length:704        
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##     Number               Mass             Dose             MD       
    ##  Length:704         Min.   :0.0000   Min.   :   38   Min.   :   38  
    ##  Class :character   1st Qu.:0.0550   1st Qu.:  157   1st Qu.: 1254  
    ##  Mode  :character   Median :0.1350   Median :  396   Median : 3513  
    ##                     Mean   :0.2293   Mean   : 1306   Mean   : 5786  
    ##                     3rd Qu.:0.3200   3rd Qu.:  985   3rd Qu.: 7571  
    ##                     Max.   :1.6650   Max.   :22602   Max.   :54700  
    ##                     NA's   :29       NA's   :1                      
    ##     MD_proc        
    ##  Min.   :  0.1143  
    ##  1st Qu.: 12.9039  
    ##  Median : 33.7001  
    ##  Mean   : 51.4171  
    ##  3rd Qu.: 68.1780  
    ##  Max.   :805.5952  
    ## 

## Группы Zr

Группа 1 (флакон 1) - что это было???

``` r
library(ggplot2)
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --

    ## v tibble  3.0.4     v dplyr   1.0.2
    ## v tidyr   1.1.2     v stringr 1.4.0
    ## v readr   1.4.0     v forcats 0.5.0
    ## v purrr   0.3.4

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
plot_biod <- biod %>% filter(Drug == "F1") %>%
  ggplot(aes(x = factor(Group, level = c('3h','24h','48h')), y = MD_proc)) +
  geom_boxplot() +
  facet_wrap(~ Organ, scale="free", ncol = 3) +
  theme_bw() +
  xlab ("Время после введения препарата, часы") +
  ggtitle("Данные биораспреления препарата Ф1")

plot_biod
```

![](1_ghMD_RadioAPT2_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

Группа 2 (флакон 3) - что это было???

``` r
library(ggplot2)
library(tidyverse)

plot_biod <- biod %>% filter(Drug == "F3") %>%
  ggplot(aes(x = factor(Group, level = c('3h','24h','48h')), y = MD_proc)) +
  geom_boxplot() +
  facet_wrap(~ Organ, scale="free", ncol = 3) +
  theme_bw() +
  xlab ("Время после введения препарата, часы") +
  ggtitle("Данные биораспреления препарата Ф3")

plot_biod
```

![](1_ghMD_RadioAPT2_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

Сравнение групп 1 и 2 (Ф1 и Ф3)

``` r
library(ggplot2)
library(tidyverse)

plot_biod <- biod %>% filter(Drug == "F1" | Drug == "F3") %>% 
  filter(Organ != "Первичный ОУ", Organ != "Кровь") %>% 
  ggplot(aes(x = factor(Group, level = c('3h','24h','48h')), y = MD_proc, color = Drug)) +
  geom_boxplot() +
  theme_bw() +
  facet_wrap(~ Organ, scale="free", ncol = 3) +
  xlab ("Время после введения препарата, часы") +
  ggtitle("Данные биораспреления препарата Ф3")

plot_biod
```

![](1_ghMD_RadioAPT2_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
