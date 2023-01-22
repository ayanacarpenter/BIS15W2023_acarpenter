---
title: "Lab 4 Homework"
author: "Ayana Carpenter"
date: "2023-01-22"
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

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
getwd()
```

```
## [1] "/Users/ayanacarpenter/Desktop/BIS15W2023_acarpenter/lab4"
```


```r
homerange <- readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```
**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.** 

Dimensions 569 rows, 24 columns

```r
dim(homerange)
```

```
## [1] 569  24
```

Column names

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

Classes for each variable

```r
glimpse(homerange)
```

```
## Rows: 569
## Columns: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fishe…
## $ common.name                <chr> "american eel", "blacktail redhorse", "cent…
## $ class                      <chr> "actinopterygii", "actinopterygii", "actino…
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprini…
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae"…
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cli…
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fundu…
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recapt…
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2", …
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00,…
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600,…
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, 3…
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437,…
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home range…
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic",…
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ect…
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimmi…
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "car…
## $ dimension                  <dbl> 3, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3…
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, N…
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA, …
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, NA…
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 20…
```

Statistical summary

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
class(homerange$taxon)
```

```
## [1] "character"
```

```r
class(homerange$order)
```

```
## [1] "character"
```

```r
homerange$taxon <- as.factor(homerange$taxon)
homerange$order <- as.factor(homerange$order)
```


```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"       "afrosoricida"          "anguilliformes"       
##  [4] "anseriformes"          "apterygiformes"        "artiodactyla"         
##  [7] "caprimulgiformes"      "carnivora"             "charadriiformes"      
## [10] "columbidormes"         "columbiformes"         "coraciiformes"        
## [13] "cuculiformes"          "cypriniformes"         "dasyuromorpha"        
## [16] "dasyuromorpia"         "didelphimorphia"       "diprodontia"          
## [19] "diprotodontia"         "erinaceomorpha"        "esociformes"          
## [22] "falconiformes"         "gadiformes"            "galliformes"          
## [25] "gruiformes"            "lagomorpha"            "macroscelidea"        
## [28] "monotrematae"          "passeriformes"         "pelecaniformes"       
## [31] "peramelemorphia"       "perciformes"           "perissodactyla"       
## [34] "piciformes"            "pilosa"                "proboscidea"          
## [37] "psittaciformes"        "rheiformes"            "roden"                
## [40] "rodentia"              "salmoniformes"         "scorpaeniformes"      
## [43] "siluriformes"          "soricomorpha"          "squamata"             
## [46] "strigiformes"          "struthioniformes"      "syngnathiformes"      
## [49] "testudines"            "tetraodontiformes\xa0" "tinamiformes"
```

**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  
The homerange data frame represents the taxa birds, lake fishes, lizards, mammals, marine fishes, river fishes, snakes, tortoises, and turtles. 


```r
taxa <- select(homerange, "taxon", "common.name", "class", "order", "family", "species")
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.** 

```r
table(homerange$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  
carnivore=342 herbivore=227

```r
filter(homerange, trophic.guild=="carnivore")
```

```
## # A tibble: 342 × 24
##    taxon  commo…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##    <fct>  <chr>   <chr> <fct> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
##  1 lake … americ… acti… angu… angui… angu… rostra… teleme… 16       887    2.95 
##  2 river… blackt… acti… cypr… catos… moxo… poecil… mark-r… <NA>     562    2.75 
##  3 river… centra… acti… cypr… cypri… camp… anomal… mark-r… 20        34    1.53 
##  4 river… rosysi… acti… cypr… cypri… clin… fundul… mark-r… 26         4    0.602
##  5 river… longno… acti… cypr… cypri… rhin… catara… mark-r… 17         4    0.602
##  6 river… muskel… acti… esoc… esoci… esox  masqui… teleme… 5       3525    3.55 
##  7 marin… pollack acti… gadi… gadid… poll… pollac… teleme… 2        737.   2.87 
##  8 marin… saithe  acti… gadi… gadid… poll… virens  teleme… 2        449.   2.65 
##  9 marin… giant … acti… perc… caran… cara… ignobi… teleme… 4        726.   2.86 
## 10 lake … rock b… acti… perc… centr… ambl… rupest… mark-r… 16       196    2.29 
## # … with 332 more rows, 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```

```r
filter(homerange, trophic.guild=="herbivore")
```

```
## # A tibble: 227 × 24
##    taxon  commo…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##    <fct>  <chr>   <chr> <fct> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
##  1 marin… lined … acti… perc… acant… acan… lineat… direct… <NA>   109.     2.04 
##  2 marin… orange… acti… perc… acant… naso  litura… teleme… 8      772.     2.89 
##  3 marin… bluesp… acti… perc… acant… naso  unicor… teleme… 7      152.     2.18 
##  4 marin… redlip… acti… perc… blenn… ophi… atlant… direct… 20       6.2    0.792
##  5 marin… bermud… acti… perc… kypho… kyph… sectat… teleme… 11    1087.     3.04 
##  6 marin… cherub… acti… perc… pomac… cent… argi    direct… <NA>     2.5    0.398
##  7 marin… damsel… acti… perc… pomac… chro… chromis direct… <NA>    28.4    1.45 
##  8 marin… twinsp… acti… perc… pomac… chry… biocel… direct… 18       9.19   0.963
##  9 marin… wards … acti… perc… pomac… poma… wardi   direct… <NA>    10.5    1.02 
## 10 marin… austra… acti… perc… pomac… steg… apical… direct… <NA>    45.3    1.66 
## # … with 217 more rows, 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```


**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
carnivore_homerange <- (filter(homerange, trophic.guild=="carnivore"))
```


```r
herbivore_homerange <- (filter(homerange, trophic.guild=="herbivore"))
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  
Herbivores have a larger mean homerange on average. 

```r
is.na(carnivore_homerange)
```

```
##        taxon common.name class order family genus species primarymethod     N
##   [1,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##   [2,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##   [3,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##   [4,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##   [5,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##   [6,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##   [7,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##   [8,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##   [9,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [10,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [11,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [12,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [13,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [14,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [15,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [16,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [17,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [18,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [19,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [20,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [21,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [22,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [23,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [24,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [25,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [26,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [27,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [28,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [29,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [30,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [31,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [32,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [33,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [34,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [35,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [36,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [37,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [38,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [39,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [40,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [41,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [42,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [43,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [44,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [45,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [46,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [47,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [48,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [49,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [50,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [51,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [52,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [53,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [54,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [55,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [56,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [57,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [58,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [59,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [60,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [61,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [62,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [63,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [64,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [65,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [66,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [67,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [68,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [69,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [70,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [71,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [72,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [73,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [74,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [75,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [76,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [77,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [78,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [79,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [80,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [81,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [82,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [83,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [84,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [85,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [86,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [87,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [88,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [89,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [90,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [91,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [92,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [93,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [94,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [95,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [96,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [97,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
##  [98,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##  [99,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [100,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [101,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [102,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [103,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [104,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [105,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [106,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [107,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [108,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [109,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [110,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [111,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [112,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [113,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [114,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [115,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [116,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [117,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [118,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [119,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [120,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [121,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [122,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [123,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [124,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [125,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE          TRUE  TRUE
## [126,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [127,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [128,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [129,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [130,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [131,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [132,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [133,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [134,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [135,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [136,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [137,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [138,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [139,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [140,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [141,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [142,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [143,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [144,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [145,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [146,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [147,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [148,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [149,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [150,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [151,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [152,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [153,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [154,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [155,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [156,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [157,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [158,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [159,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [160,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [161,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [162,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [163,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [164,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [165,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [166,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [167,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [168,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [169,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [170,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [171,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [172,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [173,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [174,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [175,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [176,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [177,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [178,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [179,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [180,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [181,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [182,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [183,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [184,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [185,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [186,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [187,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [188,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [189,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [190,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [191,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [192,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [193,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [194,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [195,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [196,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [197,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [198,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [199,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [200,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [201,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [202,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [203,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [204,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [205,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [206,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [207,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [208,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [209,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [210,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [211,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [212,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [213,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [214,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [215,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [216,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [217,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [218,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [219,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [220,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [221,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [222,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [223,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [224,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [225,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [226,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [227,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [228,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [229,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [230,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [231,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [232,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [233,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [234,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [235,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [236,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [237,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [238,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [239,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [240,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [241,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [242,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [243,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [244,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [245,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [246,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [247,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [248,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [249,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [250,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [251,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [252,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [253,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [254,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [255,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [256,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [257,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [258,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [259,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [260,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [261,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [262,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [263,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [264,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [265,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [266,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [267,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [268,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [269,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [270,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [271,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [272,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [273,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [274,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [275,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [276,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [277,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [278,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [279,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [280,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [281,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [282,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [283,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [284,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [285,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [286,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [287,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [288,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [289,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [290,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [291,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [292,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [293,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [294,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE  TRUE
## [295,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [296,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [297,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [298,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [299,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [300,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [301,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [302,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [303,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [304,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [305,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [306,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [307,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [308,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [309,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [310,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [311,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [312,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [313,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [314,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [315,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [316,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [317,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [318,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [319,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [320,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [321,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [322,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [323,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [324,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [325,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [326,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [327,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [328,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [329,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [330,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [331,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [332,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [333,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [334,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [335,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [336,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [337,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [338,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [339,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [340,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [341,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
## [342,] FALSE       FALSE FALSE FALSE  FALSE FALSE   FALSE         FALSE FALSE
##        mean.mass.g log10.mass alternative.mass.reference mean.hra.m2 log10.hra
##   [1,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##   [2,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##   [3,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##   [4,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##   [5,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##   [6,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##   [7,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##   [8,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##   [9,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [10,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [11,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [12,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [13,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [14,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [15,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [16,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [17,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [18,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [19,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [20,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [21,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [22,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [23,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [24,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [25,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [26,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [27,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [28,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [29,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [30,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [31,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [32,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [33,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [34,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [35,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [36,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [37,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [38,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [39,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [40,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [41,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [42,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [43,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [44,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [45,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [46,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [47,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [48,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [49,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [50,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [51,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [52,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [53,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [54,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [55,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [56,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [57,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [58,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [59,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [60,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [61,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [62,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [63,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [64,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [65,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [66,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [67,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [68,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [69,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [70,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [71,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [72,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [73,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [74,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [75,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [76,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [77,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [78,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [79,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [80,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [81,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [82,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [83,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [84,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [85,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [86,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [87,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [88,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [89,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [90,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [91,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [92,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [93,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [94,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [95,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [96,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [97,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [98,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##  [99,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [100,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [101,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [102,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [103,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [104,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [105,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [106,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [107,]       FALSE      FALSE                      FALSE       FALSE     FALSE
## [108,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [109,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [110,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [111,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [112,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [113,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [114,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [115,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [116,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [117,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [118,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [119,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [120,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [121,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [122,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [123,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [124,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [125,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [126,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [127,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [128,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [129,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [130,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [131,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [132,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [133,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [134,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [135,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [136,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [137,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [138,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [139,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [140,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [141,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [142,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [143,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [144,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [145,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [146,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [147,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [148,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [149,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [150,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [151,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [152,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [153,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [154,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [155,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [156,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [157,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [158,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [159,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [160,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [161,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [162,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [163,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [164,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [165,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [166,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [167,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [168,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [169,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [170,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [171,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [172,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [173,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [174,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [175,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [176,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [177,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [178,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [179,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [180,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [181,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [182,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [183,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [184,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [185,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [186,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [187,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [188,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [189,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [190,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [191,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [192,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [193,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [194,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [195,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [196,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [197,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [198,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [199,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [200,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [201,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [202,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [203,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [204,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [205,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [206,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [207,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [208,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [209,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [210,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [211,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [212,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [213,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [214,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [215,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [216,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [217,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [218,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [219,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [220,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [221,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [222,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [223,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [224,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [225,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [226,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [227,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [228,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [229,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [230,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [231,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [232,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [233,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [234,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [235,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [236,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [237,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [238,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [239,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [240,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [241,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [242,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [243,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [244,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [245,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [246,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [247,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [248,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [249,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [250,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [251,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [252,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [253,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [254,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [255,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [256,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [257,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [258,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [259,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [260,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [261,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [262,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [263,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [264,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [265,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [266,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [267,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [268,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [269,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [270,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [271,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [272,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [273,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [274,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [275,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [276,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [277,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [278,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [279,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [280,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [281,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [282,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [283,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [284,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [285,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [286,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [287,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [288,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [289,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [290,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [291,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [292,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [293,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [294,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [295,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [296,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [297,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [298,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [299,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [300,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [301,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [302,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [303,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [304,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [305,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [306,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [307,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [308,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [309,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [310,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [311,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [312,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [313,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [314,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [315,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [316,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [317,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [318,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [319,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [320,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [321,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [322,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [323,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [324,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [325,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [326,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [327,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [328,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [329,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [330,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [331,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [332,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [333,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [334,]       FALSE      FALSE                      FALSE       FALSE     FALSE
## [335,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [336,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [337,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [338,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [339,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [340,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [341,]       FALSE      FALSE                       TRUE       FALSE     FALSE
## [342,]       FALSE      FALSE                       TRUE       FALSE     FALSE
##        hra.reference realm thermoregulation locomotion trophic.guild dimension
##   [1,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##   [2,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##   [3,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##   [4,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##   [5,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##   [6,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##   [7,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##   [8,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##   [9,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [10,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [11,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [12,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [13,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [14,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [15,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [16,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [17,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [18,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [19,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [20,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [21,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [22,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [23,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [24,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [25,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [26,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [27,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [28,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [29,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [30,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [31,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [32,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [33,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [34,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [35,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [36,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [37,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [38,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [39,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [40,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [41,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [42,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [43,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [44,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [45,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [46,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [47,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [48,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [49,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [50,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [51,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [52,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [53,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [54,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [55,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [56,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [57,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [58,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [59,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [60,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [61,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [62,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [63,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [64,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [65,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [66,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [67,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [68,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [69,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [70,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [71,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [72,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [73,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [74,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [75,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [76,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [77,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [78,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [79,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [80,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [81,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [82,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [83,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [84,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [85,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [86,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [87,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [88,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [89,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [90,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [91,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [92,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [93,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [94,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [95,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [96,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [97,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [98,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##  [99,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [100,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [101,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [102,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [103,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [104,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [105,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [106,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [107,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [108,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [109,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [110,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [111,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [112,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [113,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [114,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [115,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [116,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [117,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [118,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [119,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [120,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [121,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [122,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [123,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [124,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [125,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [126,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [127,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [128,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [129,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [130,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [131,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [132,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [133,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [134,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [135,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [136,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [137,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [138,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [139,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [140,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [141,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [142,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [143,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [144,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [145,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [146,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [147,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [148,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [149,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [150,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [151,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [152,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [153,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [154,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [155,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [156,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [157,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [158,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [159,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [160,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [161,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [162,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [163,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [164,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [165,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [166,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [167,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [168,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [169,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [170,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [171,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [172,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [173,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [174,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [175,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [176,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [177,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [178,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [179,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [180,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [181,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [182,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [183,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [184,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [185,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [186,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [187,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [188,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [189,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [190,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [191,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [192,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [193,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [194,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [195,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [196,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [197,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [198,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [199,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [200,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [201,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [202,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [203,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [204,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [205,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [206,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [207,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [208,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [209,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [210,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [211,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [212,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [213,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [214,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [215,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [216,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [217,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [218,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [219,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [220,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [221,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [222,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [223,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [224,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [225,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [226,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [227,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [228,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [229,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [230,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [231,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [232,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [233,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [234,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [235,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [236,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [237,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [238,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [239,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [240,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [241,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [242,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [243,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [244,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [245,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [246,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [247,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [248,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [249,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [250,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [251,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [252,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [253,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [254,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [255,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [256,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [257,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [258,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [259,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [260,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [261,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [262,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [263,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [264,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [265,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [266,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [267,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [268,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [269,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [270,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [271,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [272,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [273,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [274,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [275,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [276,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [277,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [278,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [279,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [280,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [281,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [282,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [283,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [284,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [285,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [286,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [287,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [288,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [289,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [290,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [291,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [292,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [293,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [294,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [295,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [296,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [297,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [298,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [299,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [300,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [301,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [302,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [303,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [304,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [305,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [306,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [307,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [308,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [309,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [310,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [311,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [312,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [313,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [314,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [315,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [316,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [317,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [318,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [319,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [320,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [321,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [322,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [323,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [324,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [325,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [326,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [327,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [328,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [329,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [330,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [331,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [332,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [333,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [334,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [335,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [336,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [337,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [338,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [339,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [340,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [341,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
## [342,]         FALSE FALSE            FALSE      FALSE         FALSE     FALSE
##        preymass log10.preymass  PPMR prey.size.reference
##   [1,]     TRUE           TRUE  TRUE                TRUE
##   [2,]     TRUE           TRUE  TRUE                TRUE
##   [3,]     TRUE           TRUE  TRUE                TRUE
##   [4,]     TRUE           TRUE  TRUE                TRUE
##   [5,]     TRUE           TRUE  TRUE                TRUE
##   [6,]     TRUE           TRUE  TRUE                TRUE
##   [7,]    FALSE          FALSE FALSE               FALSE
##   [8,]     TRUE           TRUE  TRUE                TRUE
##   [9,]     TRUE           TRUE  TRUE                TRUE
##  [10,]     TRUE           TRUE  TRUE                TRUE
##  [11,]     TRUE           TRUE  TRUE                TRUE
##  [12,]     TRUE           TRUE  TRUE                TRUE
##  [13,]     TRUE           TRUE  TRUE                TRUE
##  [14,]     TRUE           TRUE  TRUE                TRUE
##  [15,]     TRUE           TRUE  TRUE                TRUE
##  [16,]     TRUE           TRUE  TRUE                TRUE
##  [17,]     TRUE           TRUE  TRUE                TRUE
##  [18,]     TRUE           TRUE  TRUE                TRUE
##  [19,]     TRUE           TRUE  TRUE                TRUE
##  [20,]     TRUE           TRUE  TRUE                TRUE
##  [21,]     TRUE           TRUE  TRUE                TRUE
##  [22,]     TRUE           TRUE  TRUE                TRUE
##  [23,]     TRUE           TRUE  TRUE                TRUE
##  [24,]     TRUE           TRUE  TRUE                TRUE
##  [25,]     TRUE           TRUE  TRUE                TRUE
##  [26,]     TRUE           TRUE  TRUE                TRUE
##  [27,]     TRUE           TRUE  TRUE                TRUE
##  [28,]     TRUE           TRUE  TRUE                TRUE
##  [29,]     TRUE           TRUE  TRUE                TRUE
##  [30,]     TRUE           TRUE  TRUE                TRUE
##  [31,]     TRUE           TRUE  TRUE                TRUE
##  [32,]     TRUE           TRUE  TRUE                TRUE
##  [33,]     TRUE           TRUE  TRUE                TRUE
##  [34,]     TRUE           TRUE  TRUE                TRUE
##  [35,]     TRUE           TRUE  TRUE                TRUE
##  [36,]     TRUE           TRUE  TRUE                TRUE
##  [37,]     TRUE           TRUE  TRUE                TRUE
##  [38,]     TRUE           TRUE  TRUE                TRUE
##  [39,]     TRUE           TRUE  TRUE                TRUE
##  [40,]     TRUE           TRUE  TRUE                TRUE
##  [41,]     TRUE           TRUE  TRUE                TRUE
##  [42,]     TRUE           TRUE  TRUE                TRUE
##  [43,]     TRUE           TRUE  TRUE                TRUE
##  [44,]     TRUE           TRUE  TRUE                TRUE
##  [45,]     TRUE           TRUE  TRUE                TRUE
##  [46,]     TRUE           TRUE  TRUE                TRUE
##  [47,]    FALSE          FALSE FALSE               FALSE
##  [48,]     TRUE           TRUE  TRUE                TRUE
##  [49,]     TRUE           TRUE  TRUE                TRUE
##  [50,]     TRUE           TRUE  TRUE                TRUE
##  [51,]     TRUE           TRUE  TRUE                TRUE
##  [52,]     TRUE           TRUE  TRUE                TRUE
##  [53,]     TRUE           TRUE  TRUE                TRUE
##  [54,]     TRUE           TRUE  TRUE                TRUE
##  [55,]     TRUE           TRUE  TRUE                TRUE
##  [56,]     TRUE           TRUE  TRUE                TRUE
##  [57,]     TRUE           TRUE  TRUE                TRUE
##  [58,]    FALSE          FALSE FALSE               FALSE
##  [59,]     TRUE           TRUE  TRUE                TRUE
##  [60,]     TRUE           TRUE  TRUE                TRUE
##  [61,]     TRUE           TRUE  TRUE                TRUE
##  [62,]     TRUE           TRUE  TRUE                TRUE
##  [63,]    FALSE          FALSE FALSE               FALSE
##  [64,]     TRUE           TRUE  TRUE                TRUE
##  [65,]    FALSE          FALSE FALSE               FALSE
##  [66,]     TRUE           TRUE  TRUE                TRUE
##  [67,]     TRUE           TRUE  TRUE                TRUE
##  [68,]     TRUE           TRUE  TRUE                TRUE
##  [69,]     TRUE           TRUE  TRUE                TRUE
##  [70,]     TRUE           TRUE  TRUE                TRUE
##  [71,]     TRUE           TRUE  TRUE                TRUE
##  [72,]     TRUE           TRUE  TRUE                TRUE
##  [73,]    FALSE          FALSE FALSE               FALSE
##  [74,]     TRUE           TRUE  TRUE                TRUE
##  [75,]     TRUE           TRUE  TRUE                TRUE
##  [76,]     TRUE           TRUE  TRUE                TRUE
##  [77,]     TRUE           TRUE  TRUE                TRUE
##  [78,]     TRUE           TRUE  TRUE                TRUE
##  [79,]     TRUE           TRUE  TRUE                TRUE
##  [80,]     TRUE           TRUE  TRUE                TRUE
##  [81,]    FALSE          FALSE FALSE               FALSE
##  [82,]     TRUE           TRUE  TRUE                TRUE
##  [83,]     TRUE           TRUE  TRUE                TRUE
##  [84,]     TRUE           TRUE  TRUE                TRUE
##  [85,]    FALSE          FALSE FALSE               FALSE
##  [86,]    FALSE          FALSE FALSE               FALSE
##  [87,]    FALSE          FALSE FALSE               FALSE
##  [88,]     TRUE           TRUE  TRUE                TRUE
##  [89,]     TRUE           TRUE  TRUE                TRUE
##  [90,]     TRUE           TRUE  TRUE                TRUE
##  [91,]     TRUE           TRUE  TRUE                TRUE
##  [92,]     TRUE           TRUE  TRUE                TRUE
##  [93,]     TRUE           TRUE  TRUE                TRUE
##  [94,]    FALSE          FALSE FALSE               FALSE
##  [95,]    FALSE          FALSE FALSE               FALSE
##  [96,]    FALSE          FALSE FALSE               FALSE
##  [97,]     TRUE           TRUE  TRUE                TRUE
##  [98,]    FALSE          FALSE FALSE               FALSE
##  [99,]     TRUE           TRUE  TRUE                TRUE
## [100,]     TRUE           TRUE  TRUE                TRUE
## [101,]     TRUE           TRUE  TRUE                TRUE
## [102,]     TRUE           TRUE  TRUE                TRUE
## [103,]     TRUE           TRUE  TRUE                TRUE
## [104,]     TRUE           TRUE  TRUE                TRUE
## [105,]     TRUE           TRUE  TRUE                TRUE
## [106,]     TRUE           TRUE  TRUE                TRUE
## [107,]     TRUE           TRUE  TRUE                TRUE
## [108,]     TRUE           TRUE  TRUE                TRUE
## [109,]    FALSE          FALSE FALSE               FALSE
## [110,]    FALSE          FALSE FALSE               FALSE
## [111,]     TRUE           TRUE  TRUE                TRUE
## [112,]    FALSE          FALSE FALSE               FALSE
## [113,]    FALSE          FALSE FALSE               FALSE
## [114,]    FALSE          FALSE FALSE               FALSE
## [115,]    FALSE          FALSE FALSE               FALSE
## [116,]    FALSE          FALSE FALSE               FALSE
## [117,]     TRUE           TRUE  TRUE                TRUE
## [118,]    FALSE          FALSE FALSE               FALSE
## [119,]     TRUE           TRUE  TRUE                TRUE
## [120,]     TRUE           TRUE  TRUE                TRUE
## [121,]     TRUE           TRUE  TRUE                TRUE
## [122,]    FALSE          FALSE FALSE               FALSE
## [123,]    FALSE          FALSE FALSE               FALSE
## [124,]    FALSE          FALSE FALSE               FALSE
## [125,]    FALSE          FALSE FALSE               FALSE
## [126,]     TRUE           TRUE  TRUE                TRUE
## [127,]     TRUE           TRUE  TRUE                TRUE
## [128,]     TRUE           TRUE  TRUE                TRUE
## [129,]     TRUE           TRUE  TRUE                TRUE
## [130,]     TRUE           TRUE  TRUE                TRUE
## [131,]     TRUE           TRUE  TRUE                TRUE
## [132,]     TRUE           TRUE  TRUE                TRUE
## [133,]     TRUE           TRUE  TRUE                TRUE
## [134,]     TRUE           TRUE  TRUE                TRUE
## [135,]     TRUE           TRUE  TRUE                TRUE
## [136,]     TRUE           TRUE  TRUE                TRUE
## [137,]     TRUE           TRUE  TRUE                TRUE
## [138,]     TRUE           TRUE  TRUE                TRUE
## [139,]     TRUE           TRUE  TRUE                TRUE
## [140,]     TRUE           TRUE  TRUE                TRUE
## [141,]     TRUE           TRUE  TRUE                TRUE
## [142,]     TRUE           TRUE  TRUE                TRUE
## [143,]     TRUE           TRUE  TRUE                TRUE
## [144,]     TRUE           TRUE  TRUE                TRUE
## [145,]     TRUE           TRUE  TRUE                TRUE
## [146,]     TRUE           TRUE  TRUE                TRUE
## [147,]     TRUE           TRUE  TRUE                TRUE
## [148,]     TRUE           TRUE  TRUE                TRUE
## [149,]     TRUE           TRUE  TRUE                TRUE
## [150,]     TRUE           TRUE  TRUE                TRUE
## [151,]     TRUE           TRUE  TRUE                TRUE
## [152,]     TRUE           TRUE  TRUE                TRUE
## [153,]     TRUE           TRUE  TRUE                TRUE
## [154,]     TRUE           TRUE  TRUE                TRUE
## [155,]     TRUE           TRUE  TRUE                TRUE
## [156,]     TRUE           TRUE  TRUE                TRUE
## [157,]     TRUE           TRUE  TRUE                TRUE
## [158,]     TRUE           TRUE  TRUE                TRUE
## [159,]     TRUE           TRUE  TRUE                TRUE
## [160,]     TRUE           TRUE  TRUE                TRUE
## [161,]     TRUE           TRUE  TRUE                TRUE
## [162,]     TRUE           TRUE  TRUE                TRUE
## [163,]     TRUE           TRUE  TRUE                TRUE
## [164,]     TRUE           TRUE  TRUE                TRUE
## [165,]     TRUE           TRUE  TRUE                TRUE
## [166,]     TRUE           TRUE  TRUE                TRUE
## [167,]     TRUE           TRUE  TRUE                TRUE
## [168,]     TRUE           TRUE  TRUE                TRUE
## [169,]     TRUE           TRUE  TRUE                TRUE
## [170,]     TRUE           TRUE  TRUE                TRUE
## [171,]     TRUE           TRUE  TRUE                TRUE
## [172,]     TRUE           TRUE  TRUE                TRUE
## [173,]     TRUE           TRUE  TRUE                TRUE
## [174,]     TRUE           TRUE  TRUE                TRUE
## [175,]     TRUE           TRUE  TRUE                TRUE
## [176,]     TRUE           TRUE  TRUE                TRUE
## [177,]     TRUE           TRUE  TRUE                TRUE
## [178,]     TRUE           TRUE  TRUE                TRUE
## [179,]     TRUE           TRUE  TRUE                TRUE
## [180,]     TRUE           TRUE  TRUE                TRUE
## [181,]     TRUE           TRUE  TRUE                TRUE
## [182,]     TRUE           TRUE  TRUE                TRUE
## [183,]     TRUE           TRUE  TRUE                TRUE
## [184,]     TRUE           TRUE  TRUE                TRUE
## [185,]     TRUE           TRUE  TRUE                TRUE
## [186,]     TRUE           TRUE  TRUE                TRUE
## [187,]     TRUE           TRUE  TRUE                TRUE
## [188,]     TRUE           TRUE  TRUE                TRUE
## [189,]     TRUE           TRUE  TRUE                TRUE
## [190,]     TRUE           TRUE  TRUE                TRUE
## [191,]     TRUE           TRUE  TRUE                TRUE
## [192,]     TRUE           TRUE  TRUE                TRUE
## [193,]     TRUE           TRUE  TRUE                TRUE
## [194,]     TRUE           TRUE  TRUE                TRUE
## [195,]     TRUE           TRUE  TRUE                TRUE
## [196,]     TRUE           TRUE  TRUE                TRUE
## [197,]     TRUE           TRUE  TRUE                TRUE
## [198,]     TRUE           TRUE  TRUE                TRUE
## [199,]     TRUE           TRUE  TRUE                TRUE
## [200,]     TRUE           TRUE  TRUE                TRUE
## [201,]     TRUE           TRUE  TRUE                TRUE
## [202,]    FALSE          FALSE FALSE               FALSE
## [203,]    FALSE          FALSE FALSE               FALSE
## [204,]    FALSE          FALSE FALSE               FALSE
## [205,]    FALSE          FALSE FALSE               FALSE
## [206,]    FALSE          FALSE FALSE               FALSE
## [207,]     TRUE           TRUE  TRUE                TRUE
## [208,]    FALSE          FALSE FALSE               FALSE
## [209,]    FALSE          FALSE FALSE               FALSE
## [210,]     TRUE           TRUE  TRUE                TRUE
## [211,]     TRUE           TRUE  TRUE                TRUE
## [212,]     TRUE           TRUE  TRUE                TRUE
## [213,]     TRUE           TRUE  TRUE                TRUE
## [214,]    FALSE          FALSE FALSE               FALSE
## [215,]     TRUE           TRUE  TRUE                TRUE
## [216,]     TRUE           TRUE  TRUE                TRUE
## [217,]     TRUE           TRUE  TRUE                TRUE
## [218,]     TRUE           TRUE  TRUE                TRUE
## [219,]     TRUE           TRUE  TRUE                TRUE
## [220,]     TRUE           TRUE  TRUE                TRUE
## [221,]    FALSE          FALSE FALSE               FALSE
## [222,]     TRUE           TRUE  TRUE                TRUE
## [223,]     TRUE           TRUE  TRUE                TRUE
## [224,]     TRUE           TRUE  TRUE                TRUE
## [225,]    FALSE          FALSE FALSE               FALSE
## [226,]    FALSE          FALSE FALSE               FALSE
## [227,]     TRUE           TRUE  TRUE                TRUE
## [228,]    FALSE          FALSE FALSE               FALSE
## [229,]    FALSE          FALSE FALSE               FALSE
## [230,]    FALSE          FALSE FALSE               FALSE
## [231,]     TRUE           TRUE  TRUE                TRUE
## [232,]    FALSE          FALSE FALSE               FALSE
## [233,]     TRUE           TRUE  TRUE                TRUE
## [234,]    FALSE          FALSE FALSE               FALSE
## [235,]    FALSE          FALSE FALSE               FALSE
## [236,]     TRUE           TRUE  TRUE                TRUE
## [237,]     TRUE           TRUE  TRUE                TRUE
## [238,]    FALSE          FALSE FALSE               FALSE
## [239,]     TRUE           TRUE  TRUE                TRUE
## [240,]     TRUE           TRUE  TRUE                TRUE
## [241,]     TRUE           TRUE  TRUE                TRUE
## [242,]    FALSE          FALSE FALSE               FALSE
## [243,]     TRUE           TRUE  TRUE                TRUE
## [244,]     TRUE           TRUE  TRUE                TRUE
## [245,]     TRUE           TRUE  TRUE                TRUE
## [246,]     TRUE           TRUE  TRUE                TRUE
## [247,]     TRUE           TRUE  TRUE                TRUE
## [248,]    FALSE          FALSE FALSE               FALSE
## [249,]     TRUE           TRUE  TRUE                TRUE
## [250,]    FALSE          FALSE FALSE               FALSE
## [251,]    FALSE          FALSE FALSE               FALSE
## [252,]    FALSE          FALSE FALSE               FALSE
## [253,]    FALSE          FALSE FALSE               FALSE
## [254,]     TRUE           TRUE  TRUE                TRUE
## [255,]     TRUE           TRUE  TRUE                TRUE
## [256,]     TRUE           TRUE  TRUE                TRUE
## [257,]    FALSE          FALSE FALSE               FALSE
## [258,]     TRUE           TRUE  TRUE                TRUE
## [259,]     TRUE           TRUE  TRUE                TRUE
## [260,]     TRUE           TRUE  TRUE                TRUE
## [261,]    FALSE          FALSE FALSE               FALSE
## [262,]     TRUE           TRUE  TRUE                TRUE
## [263,]     TRUE           TRUE  TRUE                TRUE
## [264,]     TRUE           TRUE  TRUE                TRUE
## [265,]     TRUE           TRUE  TRUE                TRUE
## [266,]     TRUE           TRUE  TRUE                TRUE
## [267,]     TRUE           TRUE  TRUE                TRUE
## [268,]     TRUE           TRUE  TRUE                TRUE
## [269,]     TRUE           TRUE  TRUE                TRUE
## [270,]     TRUE           TRUE  TRUE                TRUE
## [271,]     TRUE           TRUE  TRUE                TRUE
## [272,]     TRUE           TRUE  TRUE                TRUE
## [273,]     TRUE           TRUE  TRUE                TRUE
## [274,]     TRUE           TRUE  TRUE                TRUE
## [275,]     TRUE           TRUE  TRUE                TRUE
## [276,]     TRUE           TRUE  TRUE                TRUE
## [277,]     TRUE           TRUE  TRUE                TRUE
## [278,]     TRUE           TRUE  TRUE                TRUE
## [279,]     TRUE           TRUE  TRUE                TRUE
## [280,]     TRUE           TRUE  TRUE                TRUE
## [281,]     TRUE           TRUE  TRUE                TRUE
## [282,]     TRUE           TRUE  TRUE                TRUE
## [283,]     TRUE           TRUE  TRUE                TRUE
## [284,]     TRUE           TRUE  TRUE                TRUE
## [285,]     TRUE           TRUE  TRUE                TRUE
## [286,]     TRUE           TRUE  TRUE                TRUE
## [287,]     TRUE           TRUE  TRUE                TRUE
## [288,]     TRUE           TRUE  TRUE                TRUE
## [289,]     TRUE           TRUE  TRUE                TRUE
## [290,]     TRUE           TRUE  TRUE                TRUE
## [291,]     TRUE           TRUE  TRUE                TRUE
## [292,]    FALSE          FALSE FALSE               FALSE
## [293,]    FALSE          FALSE FALSE               FALSE
## [294,]     TRUE           TRUE  TRUE                TRUE
## [295,]     TRUE           TRUE  TRUE                TRUE
## [296,]     TRUE           TRUE  TRUE                TRUE
## [297,]    FALSE          FALSE FALSE               FALSE
## [298,]     TRUE           TRUE  TRUE                TRUE
## [299,]    FALSE          FALSE FALSE               FALSE
## [300,]     TRUE           TRUE  TRUE                TRUE
## [301,]     TRUE           TRUE  TRUE                TRUE
## [302,]     TRUE           TRUE  TRUE                TRUE
## [303,]    FALSE          FALSE FALSE               FALSE
## [304,]     TRUE           TRUE  TRUE                TRUE
## [305,]    FALSE          FALSE FALSE               FALSE
## [306,]     TRUE           TRUE  TRUE                TRUE
## [307,]     TRUE           TRUE  TRUE                TRUE
## [308,]    FALSE          FALSE FALSE               FALSE
## [309,]     TRUE           TRUE  TRUE                TRUE
## [310,]     TRUE           TRUE  TRUE                TRUE
## [311,]     TRUE           TRUE  TRUE                TRUE
## [312,]     TRUE           TRUE  TRUE                TRUE
## [313,]    FALSE          FALSE FALSE               FALSE
## [314,]     TRUE           TRUE  TRUE                TRUE
## [315,]     TRUE           TRUE  TRUE                TRUE
## [316,]     TRUE           TRUE  TRUE                TRUE
## [317,]    FALSE          FALSE FALSE               FALSE
## [318,]     TRUE           TRUE  TRUE                TRUE
## [319,]    FALSE          FALSE FALSE               FALSE
## [320,]    FALSE          FALSE FALSE               FALSE
## [321,]     TRUE           TRUE  TRUE                TRUE
## [322,]    FALSE          FALSE FALSE               FALSE
## [323,]     TRUE           TRUE  TRUE                TRUE
## [324,]    FALSE          FALSE FALSE               FALSE
## [325,]     TRUE           TRUE  TRUE                TRUE
## [326,]     TRUE           TRUE  TRUE                TRUE
## [327,]     TRUE           TRUE  TRUE                TRUE
## [328,]    FALSE          FALSE FALSE               FALSE
## [329,]     TRUE           TRUE  TRUE                TRUE
## [330,]    FALSE          FALSE FALSE               FALSE
## [331,]     TRUE           TRUE  TRUE                TRUE
## [332,]     TRUE           TRUE  TRUE                TRUE
## [333,]     TRUE           TRUE  TRUE                TRUE
## [334,]     TRUE           TRUE  TRUE                TRUE
## [335,]     TRUE           TRUE  TRUE                TRUE
## [336,]     TRUE           TRUE  TRUE                TRUE
## [337,]     TRUE           TRUE  TRUE                TRUE
## [338,]     TRUE           TRUE  TRUE                TRUE
## [339,]     TRUE           TRUE  TRUE                TRUE
## [340,]     TRUE           TRUE  TRUE                TRUE
## [341,]     TRUE           TRUE  TRUE                TRUE
## [342,]     TRUE           TRUE  TRUE                TRUE
```

```r
carnivore_meanhr <- carnivore_homerange[ ,13]
colMeans(carnivore_meanhr, na.rm=T)
```

```
## mean.hra.m2 
##    13039918
```

```r
herbivore_meanhr <- herbivore_homerange[ ,13]
colMeans(herbivore_meanhr, na.rm = T)
```

```
## mean.hra.m2 
##    34137012
```


**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  


```r
deer <- select (homerange, "family", "genus", "species", "mean.mass.g", "log10.mass")
```

```r
deer_new <- filter(deer, family=="cervidae")
```

```r
deer_new
```

```
## # A tibble: 12 × 5
##    family   genus      species     mean.mass.g log10.mass
##    <chr>    <chr>      <chr>             <dbl>      <dbl>
##  1 cervidae alces      alces           307227.       5.49
##  2 cervidae axis       axis             62823.       4.80
##  3 cervidae capreolus  capreolus        24050.       4.38
##  4 cervidae cervus     elaphus         234758.       5.37
##  5 cervidae cervus     nippon           29450.       4.47
##  6 cervidae dama       dama             71450.       4.85
##  7 cervidae muntiacus  reevesi          13500.       4.13
##  8 cervidae odocoileus hemionus         53864.       4.73
##  9 cervidae odocoileus virginianus      87884.       4.94
## 10 cervidae ozotoceros bezoarticus      35000.       4.54
## 11 cervidae pudu       puda              7500.       3.88
## 12 cervidae rangifer   tarandus        102059.       5.01
```

```r
arrange(deer_new, "log10base", by_group = F)
```

```
## # A tibble: 12 × 5
##    family   genus      species     mean.mass.g log10.mass
##    <chr>    <chr>      <chr>             <dbl>      <dbl>
##  1 cervidae alces      alces           307227.       5.49
##  2 cervidae axis       axis             62823.       4.80
##  3 cervidae capreolus  capreolus        24050.       4.38
##  4 cervidae cervus     elaphus         234758.       5.37
##  5 cervidae cervus     nippon           29450.       4.47
##  6 cervidae dama       dama             71450.       4.85
##  7 cervidae muntiacus  reevesi          13500.       4.13
##  8 cervidae odocoileus hemionus         53864.       4.73
##  9 cervidae odocoileus virginianus      87884.       4.94
## 10 cervidae ozotoceros bezoarticus      35000.       4.54
## 11 cervidae pudu       puda              7500.       3.88
## 12 cervidae rangifer   tarandus        102059.       5.01
```

```r
filter(homerange, species=="alces")
```

```
## # A tibble: 1 × 24
##   taxon   commo…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##   <fct>   <chr>   <chr> <fct> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
## 1 mammals moose   mamm… arti… cervi… alces alces   teleme… <NA>  307227.    5.49
## # … with 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```

The largest deer is the alces. The common name is moose.

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**    

The snake with the smallest homerange is the Namaqua dwarf adder, also known as Bitis schneideri. It is the smallest adder in the world and is primarily found in Africa in coastal Namaqua dunes and southern Namibia. 
https://www.africansnakebiteinstitute.com/snake/namaqua-dwarf-adder/ 



```r
snake <- filter(homerange, taxon=="snakes")
snake
```

```
## # A tibble: 41 × 24
##    taxon  commo…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##    <fct>  <chr>   <chr> <fct> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
##  1 snakes wester… rept… squa… colub… carp… vermis  radiot… 1        3.46   0.539
##  2 snakes easter… rept… squa… colub… carp… viridis radiot… 10       3.65   0.562
##  3 snakes racer   rept… squa… colub… colu… constr… teleme… 15     556.     2.75 
##  4 snakes yellow… rept… squa… colub… colu… constr… teleme… 12     144.     2.16 
##  5 snakes ringne… rept… squa… colub… diad… puncta… mark-r… <NA>     9      0.954
##  6 snakes easter… rept… squa… colub… drym… couperi teleme… 1      450      2.65 
##  7 snakes great … rept… squa… colub… elap… guttat… teleme… 12     257.     2.41 
##  8 snakes wester… rept… squa… colub… elap… obsole… teleme… 18     643.     2.81 
##  9 snakes hognos… rept… squa… colub… hete… platir… teleme… 8      147.     2.17 
## 10 snakes Europe… rept… squa… colub… hier… viridi… teleme… 32     234.     2.37 
## # … with 31 more rows, 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```

```r
snake_new <- select(snake, "family", "genus", "common.name", "mean.hra.m2", "species")
snake_new
```

```
## # A tibble: 41 × 5
##    family     genus      common.name           mean.hra.m2 species              
##    <chr>      <chr>      <chr>                       <dbl> <chr>                
##  1 colubridae carphopis  western worm snake            700 vermis               
##  2 colubridae carphopis  eastern worm snake            253 viridis              
##  3 colubridae coluber    racer                      151000 constrictor          
##  4 colubridae coluber    yellow bellied racer       114500 constrictor flaviven…
##  5 colubridae diadophis  ringneck snake               6476 punctatus            
##  6 colubridae drymarchon eastern indigo snake      1853000 couperi              
##  7 colubridae elaphe     great plains ratsnake      150600 guttata emoryi       
##  8 colubridae elaphe     western ratsnake            46000 obsoleta             
##  9 colubridae heterodon  hognose snake              516375 platirhinos          
## 10 colubridae hierophis  European whipsnake         110900 viridiflavus         
## # … with 31 more rows
```


```r
summary(snake_new)
```

```
##     family             genus           common.name         mean.hra.m2     
##  Length:41          Length:41          Length:41          Min.   :    200  
##  Class :character   Class :character   Class :character   1st Qu.:  22900  
##  Mode  :character   Mode  :character   Mode  :character   Median :  77400  
##                                                           Mean   : 258416  
##                                                           3rd Qu.: 240400  
##                                                           Max.   :2579600  
##    species         
##  Length:41         
##  Class :character  
##  Mode  :character  
##                    
##                    
## 
```

```r
filter(homerange, mean.hra.m2==200)
```

```
## # A tibble: 1 × 24
##   taxon  common…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##   <fct>  <chr>    <chr> <fct> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
## 1 snakes namaqua… rept… squa… viper… bitis schnei… teleme… 11       17.0    1.23
## # … with 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```
## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
