---
title: "Midterm 1"
author: "Ayana Carpenter"
date: "2023-01-31"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above.  

After the first 50 minutes, please upload your code (5 points). During the second 50 minutes, you may get help from each other- but no copy/paste. Upload the last version at the end of this time, but be sure to indicate it as final. If you finish early, you are free to leave.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean! Use the tidyverse and pipes unless otherwise indicated. This exam is worth a total of 35 points. 

Please load the following libraries.

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.0 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ecs21351-sup-0003-SupplementS1.csv`. These data are from Soykan, C. U., J. Sauer, J. G. Schuetz, G. S. LeBaron, K. Dale, and G. M. Langham. 2016. Population trends for North American winter birds based on hierarchical models. Ecosphere 7(5):e01351. 10.1002/ecs2.1351.  

Please load these data as a new object called `ecosphere`. In this step, I am providing the code to load the data, clean the variable names, and remove a footer that the authors used as part of the original publication.

```r
ecosphere <- read_csv("data/ecs21351-sup-0003-SupplementS1.csv", skip=2) %>% 
  clean_names() %>%
  slice(1:(n() - 18)) # this removes the footer
```

Problem 1. (1 point) Let's start with some data exploration. What are the variable names?
order, family, common name, scientific name, diet, life expectancy, habitat, urban affiliate, migratory strategy...

```r
glimpse(ecosphere)
```

```
## Rows: 551
## Columns: 21
## $ order                       <chr> "Anseriformes", "Anseriformes", "Anserifor…
## $ family                      <chr> "Anatidae", "Anatidae", "Anatidae", "Anati…
## $ common_name                 <chr> "American Black Duck", "American Wigeon", …
## $ scientific_name             <chr> "Anas rubripes", "Anas americana", "Buceph…
## $ diet                        <chr> "Vegetation", "Vegetation", "Invertebrates…
## $ life_expectancy             <chr> "Long", "Middle", "Middle", "Long", "Middl…
## $ habitat                     <chr> "Wetland", "Wetland", "Wetland", "Wetland"…
## $ urban_affiliate             <chr> "No", "No", "No", "No", "No", "No", "No", …
## $ migratory_strategy          <chr> "Short", "Short", "Moderate", "Moderate", …
## $ log10_mass                  <dbl> 3.09, 2.88, 2.96, 3.11, 3.02, 2.88, 2.56, …
## $ mean_eggs_per_clutch        <dbl> 9.0, 7.5, 10.5, 3.5, 9.5, 13.5, 10.0, 8.5,…
## $ mean_age_at_sexual_maturity <dbl> 1.0, 1.0, 3.0, 2.5, 2.0, 1.0, 0.6, 2.0, 1.…
## $ population_size             <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ winter_range_area           <dbl> 3212473, 7145842, 1812841, 360134, 854350,…
## $ range_in_cbc                <dbl> 99.1, 61.7, 69.8, 53.7, 5.3, 0.5, 17.9, 72…
## $ strata                      <dbl> 82, 124, 37, 19, 36, 5, 26, 134, 145, 103,…
## $ circles                     <dbl> 1453, 1951, 502, 247, 470, 97, 479, 2189, …
## $ feeder_bird                 <chr> "No", "No", "No", "No", "No", "No", "No", …
## $ median_trend                <dbl> 1.014, 0.996, 1.039, 0.998, 1.004, 1.196, …
## $ lower_95_percent_ci         <dbl> 0.971, 0.964, 1.016, 0.956, 0.975, 1.152, …
## $ upper_95_percent_ci         <dbl> 1.055, 1.009, 1.104, 1.041, 1.036, 1.243, …
```

Problem 2. (1 point) Use the function of your choice to summarize the data.

```r
summary(ecosphere)
```

```
##     order              family          common_name        scientific_name   
##  Length:551         Length:551         Length:551         Length:551        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##      diet           life_expectancy      habitat          urban_affiliate   
##  Length:551         Length:551         Length:551         Length:551        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  migratory_strategy   log10_mass    mean_eggs_per_clutch
##  Length:551         Min.   :0.480   Min.   : 1.000      
##  Class :character   1st Qu.:1.365   1st Qu.: 3.000      
##  Mode  :character   Median :1.890   Median : 4.000      
##                     Mean   :2.012   Mean   : 4.527      
##                     3rd Qu.:2.685   3rd Qu.: 5.000      
##                     Max.   :4.040   Max.   :17.000      
##                                                         
##  mean_age_at_sexual_maturity population_size     winter_range_area  
##  Min.   : 0.200              Min.   :    15000   Min.   :       11  
##  1st Qu.: 1.000              1st Qu.:  1100000   1st Qu.:   819357  
##  Median : 1.000              Median :  4900000   Median :  2189639  
##  Mean   : 1.592              Mean   : 18446745   Mean   :  5051047  
##  3rd Qu.: 2.000              3rd Qu.: 18000000   3rd Qu.:  6778598  
##  Max.   :12.500              Max.   :300000000   Max.   :185968946  
##                              NA's   :273                            
##   range_in_cbc        strata          circles       feeder_bird       
##  Min.   :  0.00   Min.   :  1.00   Min.   :   2.0   Length:551        
##  1st Qu.:  2.35   1st Qu.:  3.00   1st Qu.:  46.5   Class :character  
##  Median : 30.30   Median : 11.00   Median : 184.0   Mode  :character  
##  Mean   : 38.48   Mean   : 32.43   Mean   : 558.9                     
##  3rd Qu.: 72.95   3rd Qu.: 42.00   3rd Qu.: 661.0                     
##  Max.   :100.00   Max.   :159.00   Max.   :3202.0                     
##                                                                       
##   median_trend   lower_95_percent_ci upper_95_percent_ci
##  Min.   :0.739   Min.   :0.5780      Min.   :    0.798  
##  1st Qu.:0.993   1st Qu.:0.9675      1st Qu.:    1.011  
##  Median :1.009   Median :0.9930      Median :    1.027  
##  Mean   :1.016   Mean   :0.9857      Mean   :   33.709  
##  3rd Qu.:1.030   3rd Qu.:1.0140      3rd Qu.:    1.055  
##  Max.   :1.396   Max.   :1.3080      Max.   :18000.000  
## 
```

Problem 3. (2 points) How many distinct orders of birds are represented in the data?
There are 19 distinct orders of birds represented in the data.

```r
ecosphere %>% 
  tabyl(order)
```

```
##              order   n     percent
##       Anseriformes  44 0.079854809
##        Apodiformes  15 0.027223230
##   Caprimulgiformes   5 0.009074410
##    Charadriiformes  81 0.147005445
##      Ciconiiformes  29 0.052631579
##      Columbiformes  11 0.019963702
##      Coraciiformes   3 0.005444646
##       Cuculiformes   3 0.005444646
##      Falconiformes  31 0.056261343
##        Galliformes  21 0.038112523
##        Gaviiformes   4 0.007259528
##         Gruiformes  12 0.021778584
##      Passeriformes 237 0.430127042
##         Piciformes  22 0.039927405
##   Podicipediformes   6 0.010889292
##  Procellariiformes   4 0.007259528
##     Psittaciformes   6 0.010889292
##       Strigiformes  16 0.029038113
##      Trogoniformes   1 0.001814882
```

```r
ecosphere %>% 
  count(order)
```

```
## # A tibble: 19 × 2
##    order                 n
##    <chr>             <int>
##  1 Anseriformes         44
##  2 Apodiformes          15
##  3 Caprimulgiformes      5
##  4 Charadriiformes      81
##  5 Ciconiiformes        29
##  6 Columbiformes        11
##  7 Coraciiformes         3
##  8 Cuculiformes          3
##  9 Falconiformes        31
## 10 Galliformes          21
## 11 Gaviiformes           4
## 12 Gruiformes           12
## 13 Passeriformes       237
## 14 Piciformes           22
## 15 Podicipediformes      6
## 16 Procellariiformes     4
## 17 Psittaciformes        6
## 18 Strigiformes         16
## 19 Trogoniformes         1
```

Problem 4. (2 points) Which habitat has the highest diversity (number of species) in the data?
The woodland habitat has the highest diversity in the data.

```r
ecosphere %>% 
  select(habitat, common_name, scientific_name) %>% 
  group_by(habitat) %>% 
  summarize(total=n())
```

```
## # A tibble: 7 × 2
##   habitat   total
##   <chr>     <int>
## 1 Grassland    36
## 2 Ocean        44
## 3 Shrubland    82
## 4 Various      45
## 5 Wetland     153
## 6 Woodland    177
## 7 <NA>         14
```

```r
grassland_diversity <- ecosphere %>% 
  select(habitat, common_name, scientific_name) %>% 
  filter(habitat=="Grassland")
```


```r
ocean_diversity <- ecosphere %>% 
  select(habitat, common_name, scientific_name) %>% 
  filter(habitat=="Ocean")
```


```r
shrubland_diversity <- ecosphere %>% 
  select(habitat, common_name, scientific_name) %>% 
  filter(habitat=="Shrubland")
```


```r
various_diversity <- ecosphere %>% 
  select(habitat, common_name, scientific_name) %>% 
  filter(habitat=="Various")
```




Run the code below to learn about the `slice` function. Look specifically at the examples (at the bottom) for `slice_max()` and `slice_min()`. If you are still unsure, try looking up examples online (https://rpubs.com/techanswers88/dplyr-slice). Use this new function to answer question 5 below.

```r
?slice_max
```

Problem 5. (4 points) Using the `slice_max()` or `slice_min()` function described above which species has the largest and smallest winter range?
The Sooty Shearwater or Puffinus griseus has the largest winter range and the Skylark or Alauda arvensis has the smallest winter range. 

```r
ecosphere %>% 
  select(common_name, scientific_name, winter_range_area) %>% 
  slice_max(winter_range_area)
```

```
## # A tibble: 1 × 3
##   common_name      scientific_name  winter_range_area
##   <chr>            <chr>                        <dbl>
## 1 Sooty Shearwater Puffinus griseus         185968946
```


```r
ecosphere %>% 
  select(common_name, scientific_name, winter_range_area) %>% 
  slice_min(winter_range_area)
```

```
## # A tibble: 1 × 3
##   common_name scientific_name winter_range_area
##   <chr>       <chr>                       <dbl>
## 1 Skylark     Alauda arvensis                11
```

Problem 6. (2 points) The family Anatidae includes ducks, geese, and swans. Make a new object `ducks` that only includes species in the family Anatidae. Restrict this new dataframe to include all variables except order and family.

```r
ducks <- ecosphere %>% 
  filter(family=="Anatidae")
```

```r
ducks <- ducks %>% 
  select(-order, -family)
```

Problem 7. (2 points) We might assume that all ducks live in wetland habitat. Is this true for the ducks in these data? If there are exceptions, list the species below.
There is one species that lives in the habitat ocean and it is the Common elder or the Somateria mollissima.

```r
ducks %>% 
  select(habitat, common_name, scientific_name) %>% 
  group_by(habitat) %>% 
  summarize(habitat, common_name, scientific_name, total=n())
```

```
## `summarise()` has grouped output by 'habitat'. You can override using the
## `.groups` argument.
```

```
## # A tibble: 44 × 4
## # Groups:   habitat [2]
##    habitat common_name                      scientific_name                total
##    <chr>   <chr>                            <chr>                          <int>
##  1 Ocean   "Common Eider"                   Somateria mollissima               1
##  2 Wetland "American Black Duck"            Anas rubripes                     43
##  3 Wetland "American Wigeon"                Anas americana                    43
##  4 Wetland "Barrow's Goldeneye"             Bucephala islandica               43
##  5 Wetland "Black Brant"                    Branta bernicla                   43
##  6 Wetland "Black Scoter"                   Melanitta americana               43
##  7 Wetland "Black-bellied Whistling-Duck"   Dendrocygna autumnalis            43
##  8 Wetland "Blue-winged Teal"               Anas discors                      43
##  9 Wetland "Bufflehead"                     Bucephala albeola                 43
## 10 Wetland "Cackling and Canada Goose \xa0" Branta hutchinsii and B. cana…    43
## # … with 34 more rows
```

Problem 8. (4 points) In ducks, how is mean body mass associated with migratory strategy? Do the ducks that migrate long distances have high or low average body mass?

The ducks that migrate long distances have a low average body mass. 

```r
ducks %>% 
  group_by(migratory_strategy) %>% 
  summarize(average_mass=mean(log10_mass)) %>% 
  arrange(desc(average_mass))
```

```
## # A tibble: 5 × 2
##   migratory_strategy average_mass
##   <chr>                     <dbl>
## 1 Resident                   4.03
## 2 Moderate                   3.11
## 3 Short                      2.98
## 4 Withdrawal                 2.92
## 5 Long                       2.87
```

Problem 9. (2 points) Accipitridae is the family that includes eagles, hawks, kites, and osprey. First, make a new object `eagles` that only includes species in the family Accipitridae. Next, restrict these data to only include the variables common_name, scientific_name, and population_size.

```r
eagles <- ecosphere %>% 
  filter(family=="Accipitridae")
```

```r
eagles <- eagles %>% 
  select(common_name, scientific_name, population_size)
```

Problem 10. (4 points) In the eagles data, any species with a population size less than 250,000 individuals is threatened. Make a new column `conservation_status` that shows whether or not a species is threatened.

```r
eagles %>% 
  mutate(conservation_status=ifelse(population_size<250000, "threatened", "safe"))
```

```
## # A tibble: 20 × 4
##    common_name         scientific_name          population_size conservation_s…¹
##    <chr>               <chr>                              <dbl> <chr>           
##  1 Bald Eagle          Haliaeetus leucocephalus              NA <NA>            
##  2 Broad-winged Hawk   Buteo platypterus                1700000 safe            
##  3 Cooper's Hawk       Accipiter cooperii                700000 safe            
##  4 Ferruginous Hawk    Buteo regalis                      80000 threatened      
##  5 Golden Eagle        Aquila chrysaetos                 130000 threatened      
##  6 Gray Hawk           Buteo nitidus                         NA <NA>            
##  7 Harris's Hawk       Parabuteo unicinctus               50000 threatened      
##  8 Hook-billed Kite    Chondrohierax uncinatus               NA <NA>            
##  9 Northern Goshawk    Accipiter gentilis                200000 threatened      
## 10 Northern Harrier    Circus cyaneus                    700000 safe            
## 11 Red-shouldered Hawk Buteo lineatus                   1100000 safe            
## 12 Red-tailed Hawk     Buteo jamaicensis                2000000 safe            
## 13 Rough-legged Hawk   Buteo lagopus                     300000 safe            
## 14 Sharp-shinned Hawk  Accipiter striatus                500000 safe            
## 15 Short-tailed Hawk   Buteo brachyurus                      NA <NA>            
## 16 Snail Kite          Rostrhamus sociabilis                 NA <NA>            
## 17 Swainson's Hawk     Buteo swainsoni                   540000 safe            
## 18 White-tailed Hawk   Buteo albicaudatus                    NA <NA>            
## 19 White-tailed Kite   Elanus leucurus                       NA <NA>            
## 20 Zone-tailed Hawk    Buteo albonotatus                     NA <NA>            
## # … with abbreviated variable name ¹​conservation_status
```

Problem 11. (2 points) Consider the results from questions 9 and 10. Are there any species for which their threatened status needs further study? How do you know? 
The Bald Eagle, Gray Hawk, Hook-billed Kite, Short-tailed Hawk, Snail Kite, White-tailed Hawk, White-tailed Kite, and Zone-tailed Hawk need further study because their conservation status is NA. 


```r
eagles %>% 
  mutate(conservation_status=ifelse(population_size<250000, "threatened", "safe")) %>% 
  arrange(desc(conservation_status))
```

```
## # A tibble: 20 × 4
##    common_name         scientific_name          population_size conservation_s…¹
##    <chr>               <chr>                              <dbl> <chr>           
##  1 Ferruginous Hawk    Buteo regalis                      80000 threatened      
##  2 Golden Eagle        Aquila chrysaetos                 130000 threatened      
##  3 Harris's Hawk       Parabuteo unicinctus               50000 threatened      
##  4 Northern Goshawk    Accipiter gentilis                200000 threatened      
##  5 Broad-winged Hawk   Buteo platypterus                1700000 safe            
##  6 Cooper's Hawk       Accipiter cooperii                700000 safe            
##  7 Northern Harrier    Circus cyaneus                    700000 safe            
##  8 Red-shouldered Hawk Buteo lineatus                   1100000 safe            
##  9 Red-tailed Hawk     Buteo jamaicensis                2000000 safe            
## 10 Rough-legged Hawk   Buteo lagopus                     300000 safe            
## 11 Sharp-shinned Hawk  Accipiter striatus                500000 safe            
## 12 Swainson's Hawk     Buteo swainsoni                   540000 safe            
## 13 Bald Eagle          Haliaeetus leucocephalus              NA <NA>            
## 14 Gray Hawk           Buteo nitidus                         NA <NA>            
## 15 Hook-billed Kite    Chondrohierax uncinatus               NA <NA>            
## 16 Short-tailed Hawk   Buteo brachyurus                      NA <NA>            
## 17 Snail Kite          Rostrhamus sociabilis                 NA <NA>            
## 18 White-tailed Hawk   Buteo albicaudatus                    NA <NA>            
## 19 White-tailed Kite   Elanus leucurus                       NA <NA>            
## 20 Zone-tailed Hawk    Buteo albonotatus                     NA <NA>            
## # … with abbreviated variable name ¹​conservation_status
```

Problem 12. (4 points) Use the `ecosphere` data to perform one exploratory analysis of your choice. The analysis must have a minimum of three lines and two functions. You must also clearly state the question you are attempting to answer.

Which habitat has the highest number of species with long life expectancies? 
The Wetland has the highest number of species with long life expectancies n=20. If you want to live long, move to the wetland.

```r
long_lifespan <- ecosphere %>% 
  select(habitat, life_expectancy, common_name, scientific_name) %>% 
  filter(life_expectancy=="Long") %>% 
  group_by(habitat) %>% 
  summarize(common_name, scientific_name)
```

```
## `summarise()` has grouped output by 'habitat'. You can override using the
## `.groups` argument.
```

```r
long_lifespan %>% 
  tabyl(habitat)
```

```
##    habitat  n    percent
##  Grassland  1 0.02127660
##      Ocean 18 0.38297872
##  Shrubland  1 0.02127660
##    Various  4 0.08510638
##    Wetland 20 0.42553191
##   Woodland  3 0.06382979
```

Please provide the names of the students you have worked with with during the exam:
Dominic De Quattra, Sidney Rang


Please be 100% sure your exam is saved, knitted, and pushed to your github repository. No need to submit a link on canvas, we will find your exam in your repository.
