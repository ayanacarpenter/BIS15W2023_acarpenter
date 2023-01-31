---
title: "Lab 6 Homework"
author: "Ayana Carpenter"
date: "2023-01-30"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

Variables: country, common name, ISSCAAP group#, ISSCAAP taxonomic group, ASFIS species#, ASFIS species name, FAO major fishing area, Measure, and the years 1950-2012

17,692 rows and 71 columns
There are NAs
The classes are chr and dbl.

```r
glimpse(fisheries)
```

```
## Rows: 17,692
## Columns: 71
## $ Country                   <chr> "Albania", "Albania", "Albania", "Albania", …
## $ `Common name`             <chr> "Angelsharks, sand devils nei", "Atlantic bo…
## $ `ISSCAAP group#`          <dbl> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, 33, …
## $ `ISSCAAP taxonomic group` <chr> "Sharks, rays, chimaeras", "Tunas, bonitos, …
## $ `ASFIS species#`          <chr> "10903XXXXX", "1750100101", "17710001XX", "2…
## $ `ASFIS species name`      <chr> "Squatinidae", "Sarda sarda", "Sphyraena spp…
## $ `FAO major fishing area`  <dbl> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, …
## $ Measure                   <chr> "Quantity (tonnes)", "Quantity (tonnes)", "Q…
## $ `1950`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1951`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1952`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1953`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1954`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1955`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1956`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1957`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1958`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1959`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1960`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1961`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1962`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1963`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1964`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1965`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1966`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1967`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1968`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1969`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1970`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1971`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1972`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1973`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1974`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1975`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1976`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1977`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1978`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1979`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1980`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1981`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1982`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1983`                    <chr> NA, NA, NA, NA, NA, NA, "559", NA, NA, NA, N…
## $ `1984`                    <chr> NA, NA, NA, NA, NA, NA, "392", NA, NA, NA, N…
## $ `1985`                    <chr> NA, NA, NA, NA, NA, NA, "406", NA, NA, NA, N…
## $ `1986`                    <chr> NA, NA, NA, NA, NA, NA, "499", NA, NA, NA, N…
## $ `1987`                    <chr> NA, NA, NA, NA, NA, NA, "564", NA, NA, NA, N…
## $ `1988`                    <chr> NA, NA, NA, NA, NA, NA, "724", NA, NA, NA, N…
## $ `1989`                    <chr> NA, NA, NA, NA, NA, NA, "583", NA, NA, NA, N…
## $ `1990`                    <chr> NA, NA, NA, NA, NA, NA, "754", NA, NA, NA, N…
## $ `1991`                    <chr> NA, NA, NA, NA, NA, NA, "283", NA, NA, NA, N…
## $ `1992`                    <chr> NA, NA, NA, NA, NA, NA, "196", NA, NA, NA, N…
## $ `1993`                    <chr> NA, NA, NA, NA, NA, NA, "150 F", NA, NA, NA,…
## $ `1994`                    <chr> NA, NA, NA, NA, NA, NA, "100 F", NA, NA, NA,…
## $ `1995`                    <chr> "0 0", "1", NA, "0 0", "0 0", NA, "52", "30"…
## $ `1996`                    <chr> "53", "2", NA, "3", "2", NA, "104", "8", NA,…
## $ `1997`                    <chr> "20", "0 0", NA, "0 0", "0 0", NA, "65", "4"…
## $ `1998`                    <chr> "31", "12", NA, NA, NA, NA, "220", "18", NA,…
## $ `1999`                    <chr> "30", "30", NA, NA, NA, NA, "220", "18", NA,…
## $ `2000`                    <chr> "30", "25", "2", NA, NA, NA, "220", "20", NA…
## $ `2001`                    <chr> "16", "30", NA, NA, NA, NA, "120", "23", NA,…
## $ `2002`                    <chr> "79", "24", NA, "34", "6", NA, "150", "84", …
## $ `2003`                    <chr> "1", "4", NA, "22", NA, NA, "84", "178", NA,…
## $ `2004`                    <chr> "4", "2", "2", "15", "1", "2", "76", "285", …
## $ `2005`                    <chr> "68", "23", "4", "12", "5", "6", "68", "150"…
## $ `2006`                    <chr> "55", "30", "7", "18", "8", "9", "86", "102"…
## $ `2007`                    <chr> "12", "19", NA, NA, NA, NA, "132", "18", NA,…
## $ `2008`                    <chr> "23", "27", NA, NA, NA, NA, "132", "23", NA,…
## $ `2009`                    <chr> "14", "21", NA, NA, NA, NA, "154", "20", NA,…
## $ `2010`                    <chr> "78", "23", "7", NA, NA, NA, "80", "228", NA…
## $ `2011`                    <chr> "12", "12", NA, NA, NA, NA, "88", "9", NA, "…
## $ `2012`                    <chr> "5", "5", NA, NA, NA, NA, "129", "290", NA, …
```

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
fisheries <- clean_names(fisheries)
```


```r
fisheries$country <- as.factor(fisheries$country)
fisheries$isscaap_group_number <- as.factor(fisheries$isscaap_group_number)
fisheries$asfis_species_number <- as.factor(fisheries$asfis_species_number)
fisheries$fao_major_fishing_area <- as.factor(fisheries$fao_major_fishing_area)
            
class(fisheries$country)
```

```
## [1] "factor"
```

```r
class(fisheries$isscaap_group_number)
```

```
## [1] "factor"
```

```r
class(fisheries$asfis_species_number)
```

```
## [1] "factor"
```

```r
class(fisheries$fao_major_fishing_area)
```

```
## [1] "factor"
```

```r
fisheries
```

```
## # A tibble: 17,692 × 71
##    country common_…¹ issca…² issca…³ asfis…⁴ asfis…⁵ fao_m…⁶ measure x1950 x1951
##    <fct>   <chr>     <fct>   <chr>   <fct>   <chr>   <fct>   <chr>   <chr> <chr>
##  1 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti… <NA>  <NA> 
##  2 Albania Atlantic… 36      Tunas,… 175010… Sarda … 37      Quanti… <NA>  <NA> 
##  3 Albania Barracud… 37      Miscel… 177100… Sphyra… 37      Quanti… <NA>  <NA> 
##  4 Albania Blue and… 45      Shrimp… 228020… Ariste… 37      Quanti… <NA>  <NA> 
##  5 Albania Blue whi… 32      Cods, … 148040… Microm… 37      Quanti… <NA>  <NA> 
##  6 Albania Bluefish  37      Miscel… 170202… Pomato… 37      Quanti… <NA>  <NA> 
##  7 Albania Bogue     33      Miscel… 170392… Boops … 37      Quanti… <NA>  <NA> 
##  8 Albania Caramote… 45      Shrimp… 228010… Penaeu… 37      Quanti… <NA>  <NA> 
##  9 Albania Catshark… 38      Sharks… 108010… Scylio… 37      Quanti… <NA>  <NA> 
## 10 Albania Common c… 57      Squids… 321020… Sepia … 37      Quanti… <NA>  <NA> 
## # … with 17,682 more rows, 61 more variables: x1952 <chr>, x1953 <chr>,
## #   x1954 <chr>, x1955 <chr>, x1956 <chr>, x1957 <chr>, x1958 <chr>,
## #   x1959 <chr>, x1960 <chr>, x1961 <chr>, x1962 <chr>, x1963 <chr>,
## #   x1964 <chr>, x1965 <chr>, x1966 <chr>, x1967 <chr>, x1968 <chr>,
## #   x1969 <chr>, x1970 <chr>, x1971 <chr>, x1972 <chr>, x1973 <chr>,
## #   x1974 <chr>, x1975 <chr>, x1976 <chr>, x1977 <chr>, x1978 <chr>,
## #   x1979 <chr>, x1980 <chr>, x1981 <chr>, x1982 <chr>, x1983 <chr>, …
```

We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!

```r
fisheries_tidy <- fisheries %>% 
  pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE) %>% 
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```


```r
fisheries_tidy
```

```
## # A tibble: 376,771 × 10
##    country common_…¹ issca…² issca…³ asfis…⁴ asfis…⁵ fao_m…⁶ measure  year catch
##    <fct>   <chr>     <fct>   <chr>   <fct>   <chr>   <fct>   <chr>   <dbl> <dbl>
##  1 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti…  1995    NA
##  2 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti…  1996    53
##  3 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti…  1997    20
##  4 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti…  1998    31
##  5 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti…  1999    30
##  6 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti…  2000    30
##  7 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti…  2001    16
##  8 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti…  2002    79
##  9 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti…  2003     1
## 10 Albania Angelsha… 38      Sharks… 10903X… Squati… 37      Quanti…  2004     4
## # … with 376,761 more rows, and abbreviated variable names ¹​common_name,
## #   ²​isscaap_group_number, ³​isscaap_taxonomic_group, ⁴​asfis_species_number,
## #   ⁵​asfis_species_name, ⁶​fao_major_fishing_area
```


3. How many countries are represented in the data? Provide a count and list their names.
203 countries are represented in the data.

```r
fisheries_tidy %>% 
  count(country, sort=T)
```

```
## # A tibble: 203 × 2
##    country                      n
##    <fct>                    <int>
##  1 United States of America 18080
##  2 Spain                    17482
##  3 Japan                    15429
##  4 Portugal                 11570
##  5 Korea, Republic of       10824
##  6 France                   10639
##  7 Taiwan Province of China  9927
##  8 Indonesia                 9274
##  9 Australia                 8183
## 10 Un. Sov. Soc. Rep.        7084
## # … with 193 more rows
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fisheries_new <- fisheries_tidy %>% 
  select(country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch)
fisheries_new
```

```
## # A tibble: 376,771 × 6
##    country isscaap_taxonomic_group asfis_species_name asfis_specie…¹  year catch
##    <fct>   <chr>                   <chr>              <fct>          <dbl> <dbl>
##  1 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1995    NA
##  2 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1996    53
##  3 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1997    20
##  4 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1998    31
##  5 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      1999    30
##  6 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2000    30
##  7 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2001    16
##  8 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2002    79
##  9 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2003     1
## 10 Albania Sharks, rays, chimaeras Squatinidae        10903XXXXX      2004     4
## # … with 376,761 more rows, and abbreviated variable name ¹​asfis_species_number
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?
1,553 distinct fish species were caught. 

```r
fisheries %>% 
  group_by(asfis_species_number) %>% 
  summarize(n=n())
```

```
## # A tibble: 1,553 × 2
##    asfis_species_number     n
##    <fct>                <int>
##  1 1020100101               5
##  2 1020100201               1
##  3 10201XXXXX               2
##  4 1030300603               1
##  5 10303XXXXX               4
##  6 1050200201               9
##  7 1050200301               1
##  8 1050200502               3
##  9 1060100301               7
## 10 1060200501               3
## # … with 1,543 more rows
```

6. Which country had the largest overall catch in the year 2000?
China had the largest overall catch in the year 2000 at 9,068 tonnes.

```r
fisheries_new %>% 
  select(country, year, catch) %>% 
  filter(year=="2000") %>% 
  group_by(country) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 8,793 × 3
## # Groups:   country [193]
##    country                   year catch
##    <fct>                    <dbl> <dbl>
##  1 China                     2000  9068
##  2 Peru                      2000  5717
##  3 Russian Federation        2000  5065
##  4 Viet Nam                  2000  4945
##  5 Chile                     2000  4299
##  6 China                     2000  3288
##  7 China                     2000  2782
##  8 United States of America  2000  2438
##  9 China                     2000  1234
## 10 Philippines               2000   999
## # … with 8,783 more rows
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?
Morocco caught the most sardines between the years 1990-2000. 

```r
sardine_catcher <- fisheries_tidy%>% 
  select(country, year, catch, asfis_species_name) %>% 
  filter(between(year,1990,2000)) %>% 
  filter(asfis_species_name=="Sardina pilchardus") %>% 
  group_by(country) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(desc(catch_total))
```



8. Which five countries caught the most cephalopods between 2008-2012?
India, China, Spain, Algeria, and France caught the most cephalopods between 2008-2012.

```r
cephalopod_catcher <- fisheries_tidy %>% 
  select(country, year, catch, asfis_species_name) %>% 
  filter(between(year,2008,2012)) %>% 
  filter(asfis_species_name=="Cephalopoda") %>% 
  group_by(country) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(desc(catch_total))
```



9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)
Theragra chalcogramma had the highest catch total between 2008-2012.

```r
highest_species_catch <- fisheries_tidy %>% 
  select(country, year, catch, asfis_species_name) %>% 
  filter(between(year,2008,2012)) %>% 
  filter(asfis_species_name !="Osteichthyes") %>% 
  group_by(asfis_species_name) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(desc(catch_total))
```

```r
wronghighest_species_catch <- fisheries_tidy %>% 
  select(country, year, catch, asfis_species_name) %>% 
  filter(between(year,2008,2012)) %>% 
  group_by(asfis_species_name) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(desc(catch_total))
```

10. Use the data to do at least one analysis of your choice.
I will find the most caught species in the year that I was born (2004).

The Engraulis ringens, which fall into the taxonomical group of herrings, sardines, anchovies
was the most caught species in 2004. 

```r
highest_caught_2004 <- fisheries_tidy %>% 
  select(country, year, catch, asfis_species_name) %>% 
  filter(year==2004) %>% 
  filter(asfis_species_name !="Osteichthyes") %>% 
  group_by(asfis_species_name) %>% 
  summarize(catch_total=sum(catch, na.rm=T)) %>% 
  arrange(desc(catch_total))
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
