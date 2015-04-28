# wakefield





[![Project Status: Wip - Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](http://www.repostatus.org/badges/0.1.0/wip.svg)](http://www.repostatus.org/#wip)
[![Build Status](https://travis-ci.org/trinker/wakefield.svg?branch=master)](https://travis-ci.org/trinker/wakefield)
[![Coverage Status](https://coveralls.io/repos/trinker/wakefield/badge.svg?branch=master)](https://coveralls.io/r/trinker/wakefield?branch=master)
[![DOI](https://zenodo.org/badge/5398/trinker/wakefield.svg)](http://dx.doi.org/10.5281/zenodo.17172)
<a href="https://img.shields.io/badge/Version-0.1.0-orange.svg"><img src="https://img.shields.io/badge/Version-0.1.0-orange.svg" alt="Version"/></a></p>

**wakefield** is designed to quickly generate random data sets.  The user passes `n` (number of rows) and predefined vectors to the `r_data_frame` function to produce a `dplyr::tbl_df` object.

<img src="inst/wakefield_logo/r_wakefield.png" width="60%", alt="">  

## Installation

To download the development version of **wakefield**:

Download the [zip ball](https://github.com/trinker/wakefield/zipball/master) or [tar ball](https://github.com/trinker/wakefield/tarball/master), decompress and run `R CMD INSTALL` on it, or use the **pacman** package to install the development version:

```r
if (!require("pacman")) install.packages("pacman")
pacman::p_load_gh("trinker/wakefield")
```

## Help
    
- [Package PDF Help Manual](https://dl.dropboxusercontent.com/u/61803503/wakefield.pdf)   


## Contact

You are welcome to:
* submit suggestions and bug-reports at: <https://github.com/trinker/wakefield/issues>
* send a pull request on: <https://github.com/trinker/wakefield/>
* compose a friendly e-mail to: <tyler.rinker@gmail.com>

## Demonstration

The `r_data_frame` function (random data frame) takes `n` (the number of rows) and any number of variables (columns).  These columns are typically produced from a **wakefield** variable function.  Each of these variable functions has a pre-set behavior that produces a named vector of n length, allowing the user to lazily pass unnamed functions (optionally, without call parenthesis).  The column name is hidden as a `varname` attribute.  For example here we see the `race` variable function:


```r
race(n=10)
```

```
##  [1] White White White White White White White White White Black
## Levels: White Hispanic Black Asian Bi-Racial Native Other Hawaiian
```

```r
attributes(race(n=10))
```

```
## $levels
## [1] "White"     "Hispanic"  "Black"     "Asian"     "Bi-Racial" "Native"   
## [7] "Other"     "Hawaiian" 
## 
## $class
## [1] "variable" "factor"  
## 
## $varname
## [1] "Race"
```

When this variable is used inside of `r_data_frame` the `varname` is used as a column name.  Additionally, the `n` argument is not set within variable functions but is set once in `r_data_frame`:


```r
r_data_frame(
    n = 500,
    race
)
```

```
## Source: local data frame [500 x 1]
## 
##        Race
## 1  Hispanic
## 2     White
## 3     White
## 4     White
## 5     Black
## 6     White
## 7     White
## 8     White
## 9     White
## 10    White
## ..      ...
```

The power of `r_data_frame` is apparent when we use many modular variable functions:


```r
r_data_frame(
    n = 500,
    id,
    race,
    age,
    sex,
    hour,
    iq,
    height,
    died
)
```

```
## Source: local data frame [500 x 8]
## 
##     ID  Race Age    Sex     Hour  IQ Height  Died
## 1  001 White  34 Female 00:00:00  97     71  TRUE
## 2  002 White  30 Female 00:00:00 120     68 FALSE
## 3  003 White  28 Female 00:00:00  97     69 FALSE
## 4  004 White  34 Female 00:00:00 116     65  TRUE
## 5  005 White  34   Male 00:00:00  97     66 FALSE
## 6  006 White  26   Male 00:00:00 102     69 FALSE
## 7  007 White  21   Male 00:00:00 100     75 FALSE
## 8  008 White  23   Male 00:00:00 105     66 FALSE
## 9  009 White  24 Female 00:00:00  94     65  TRUE
## 10 010 White  22 Female 00:00:00 101     67 FALSE
## .. ...   ... ...    ...      ... ...    ...   ...
```


There are a plethora of **wakefield** based variable functions to chose from, spanning **R**'s various data types (see `?variables` details).  

<!-- html table generated in R 3.1.2 by xtable 1.7-4 package -->
<!-- Tue Apr 28 10:26:13 2015 -->
<table >
  <tr> <td> age </td> <td> dna </td> <td> height </td> <td> marital </td> <td> sentence </td> </tr>
  <tr> <td> animal </td> <td> dob </td> <td> height_cm </td> <td> military </td> <td> sex </td> </tr>
  <tr> <td> answer </td> <td> dummy </td> <td> height_in </td> <td> month </td> <td> smokes </td> </tr>
  <tr> <td> area </td> <td> education </td> <td> income </td> <td> name </td> <td> speed </td> </tr>
  <tr> <td> birth </td> <td> employment </td> <td> iq </td> <td> normal </td> <td> speed_kph </td> </tr>
  <tr> <td> car </td> <td> eye </td> <td> language </td> <td> normal_round </td> <td> speed_mph </td> </tr>
  <tr> <td> children </td> <td> gender </td> <td> level </td> <td> paragraph </td> <td> state </td> </tr>
  <tr> <td> coin </td> <td> gpa </td> <td> likert </td> <td> pet </td> <td> string </td> </tr>
  <tr> <td> color </td> <td> grade </td> <td> likert_5 </td> <td> political </td> <td> upper </td> </tr>
  <tr> <td> date_stamp </td> <td> grade_letter </td> <td> likert_7 </td> <td> primary </td> <td> upper_factor </td> </tr>
  <tr> <td> death </td> <td> grade_level </td> <td> lorem_ipsum </td> <td> race </td> <td> valid </td> </tr>
  <tr> <td> dice </td> <td> group </td> <td> lower </td> <td> religion </td> <td> year </td> </tr>
  <tr> <td> died </td> <td> hair </td> <td> lower_factor </td> <td> sat </td> <td> zip_code </td> </tr>
   </table>
<p class="caption"><b><em>Available Variable Functions</em></b></p>

However, the user may also pass their own vector producing functions or vectors to `r_data_frame`.  Those with an `n` argument can be set by `r_data_table`:


```r
r_data_frame(
    n = 500,
    id,
    Scoring = rnorm,
    Smoker = valid,
    race,
    age,
    sex,
    hour,
    iq,
    height,
    died
)
```

```
## Source: local data frame [500 x 10]
## 
##     ID    Scoring Smoker      Race Age    Sex     Hour  IQ Height  Died
## 1  001 -1.8119033  FALSE  Hispanic  32   Male 00:00:00 101     66 FALSE
## 2  002  0.9498269   TRUE     White  28 Female 00:00:00  82     70  TRUE
## 3  003 -0.5136030   TRUE Bi-Racial  35 Female 00:00:00 105     70  TRUE
## 4  004  1.0479862   TRUE     White  21   Male 00:00:00  88     62 FALSE
## 5  005  0.9799570   TRUE     White  33 Female 00:00:00 102     67  TRUE
## 6  006  0.4633803  FALSE     White  25   Male 00:00:00 112     65 FALSE
## 7  007  0.9352116   TRUE     Black  26   Male 00:00:00  87     70 FALSE
## 8  008  1.0417534   TRUE  Hispanic  30 Female 00:00:00  86     65 FALSE
## 9  009  1.5911324  FALSE     White  25 Female 00:00:00 100     73  TRUE
## 10 010  0.5782358   TRUE     White  27 Female 00:00:00  68     75  TRUE
## .. ...        ...    ...       ... ...    ...      ... ...    ...   ...
```



```r
r_data_frame(
    n = 500,
    id,
    age, age, age,
    grade, grade, grade
)
```

```
## Source: local data frame [500 x 7]
## 
##     ID Age_1 Age_2 Age_3 Grade_1 Grade_2 Grade_3
## 1  001    35    20    27    86.0    86.4    85.8
## 2  002    34    32    22    91.7    86.8    85.5
## 3  003    29    33    24    81.8    87.9    83.0
## 4  004    23    26    20    85.2    87.8    95.3
## 5  005    22    26    20    86.0    90.5    88.2
## 6  006    33    25    25    85.6    87.5    88.1
## 7  007    20    27    32    89.8    86.2    86.0
## 8  008    30    20    35    88.8    87.1    81.1
## 9  009    31    35    35    84.5    83.7    86.1
## 10 010    27    22    22    88.6    88.5    88.0
## .. ...   ...   ...   ...     ...     ...     ...
```


While, passing variable functions to `r_data_frame` without call parenthesis is handy the user may wish to set arguments.  This can be done through call parenthesis as we do with `data.frame` or `dplyr::data_frame`:


```r
r_data_frame(
    n = 500,
    id,
    Scoring = rnorm,
    Smoker = valid,
    `Reading(mins)` = rpois(lambda=20),  
    race,
    age(x = 8:14),
    sex,
    hour,
    iq,
    height(mean=50, sd = 10),
    died
)
```

```
## Source: local data frame [500 x 11]
## 
##     ID    Scoring Smoker Reading(mins)     Race Age    Sex     Hour  IQ
## 1  001  0.2497512  FALSE            24    White  11   Male 00:00:00 104
## 2  002 -0.8343042  FALSE            24    White   9   Male 00:00:00 108
## 3  003 -0.1742447  FALSE            24    Black  11 Female 00:00:00  98
## 4  004 -0.4499174  FALSE            22    White  10   Male 00:00:00 113
## 5  005 -0.3184578  FALSE            15    White  10 Female 00:00:00  90
## 6  006 -0.2226919   TRUE            13    White   8   Male 00:00:00 104
## 7  007  2.8099459   TRUE            24    White  13   Male 00:00:00  91
## 8  008  1.1467895   TRUE            21    White  14   Male 00:00:00 100
## 9  009 -2.1747491   TRUE            25    White  13 Female 00:00:00 102
## 10 010  1.1131318  FALSE            24 Hispanic  10   Male 00:00:00  97
## .. ...        ...    ...           ...      ... ...    ...      ... ...
## Variables not shown: Height (dbl), Died (lgl)
```

## Random Missing Observations

Often data contains missing values.  **wakefield** allows the user to add a proportion of missing values per column/vector via the `r_na` (random `NA`).  This works nicely within a **dplyr**/**magrittr** `%>%` *then* pipeline:


```r
r_data_frame(
    n = 30,
    id,
    race,
    age,
    sex,
    hour,
    iq,
    height,
    died,
    Scoring = rnorm,
    Smoker = valid
) %>%
    r_na(prob=.4)
```

```
## Source: local data frame [30 x 10]
## 
##    ID     Race Age    Sex     Hour  IQ Height  Died     Scoring Smoker
## 1  01       NA  28     NA 01:00:00  NA     NA FALSE          NA     NA
## 2  02    White  NA   Male     <NA>  NA     71  TRUE          NA  FALSE
## 3  03 Hispanic  26     NA 03:00:00 113     67    NA  1.14184734  FALSE
## 4  04    White  22   Male     <NA> 115     66    NA -0.15419787  FALSE
## 5  05    White  NA   Male 05:30:00 111     NA  TRUE          NA  FALSE
## 6  06    Black  23 Female 06:00:00  NA     63  TRUE  0.75050285     NA
## 7  07       NA  31 Female 06:30:00  97     65  TRUE  1.83423280     NA
## 8  08    Asian  32   Male 08:00:00  NA     69 FALSE  0.82476149  FALSE
## 9  09       NA  21     NA 10:00:00 115     NA    NA  0.01029551     NA
## 10 10       NA  22   Male 11:00:00  99     66    NA          NA     NA
## .. ..      ... ...    ...      ... ...    ...   ...         ...    ...
```

## Repeated Measures & Time Series

The `r_series` function allows the user to pass a single **wakefield** function and dictate how many columns (`j`) to produce.  


```r
set.seed(10)

r_series(likert, j = 3, n=10)
```

```
## Source: local data frame [10 x 3]
## 
##           Likert_1          Likert_2          Likert_3
## 1          Neutral          Disagree Strongly Disagree
## 2            Agree           Neutral          Disagree
## 3          Neutral   Strongly Agree           Disagree
## 4         Disagree           Neutral             Agree
## 5  Strongly Agree              Agree           Neutral
## 6            Agree           Neutral          Disagree
## 7            Agree   Strongly Agree  Strongly Disagree
## 8            Agree             Agree             Agree
## 9         Disagree             Agree          Disagree
## 10         Neutral Strongly Disagree             Agree
```

Often the user wants a numeric score for Likert type columns and similar variables.  For series with multiple factors the `as_integer` converts all columns to integer values.  Additionally, we may want to specify column name prefixes. This can be accomplished via the variable function's `name` argument.  Both of these features are demonstrated here.


```r
set.seed(10)

as_integer(r_series(likert, j = 5, n=10, name = "Item"))
```

```
## Source: local data frame [10 x 5]
## 
##    Item_1 Item_2 Item_3 Item_4 Item_5
## 1       3      2      1      3      4
## 2       4      3      2      5      4
## 3       3      5      2      5      5
## 4       2      3      4      1      2
## 5       5      4      3      3      4
## 6       4      3      2      2      5
## 7       4      5      1      1      5
## 8       4      4      4      1      3
## 9       2      4      2      2      5
## 10      3      1      4      3      1
```

`r_series` can be used within a `r_data_frame` as well.  


```r
set.seed(10)

r_data_frame(n=100,
    id,
    age,
    sex,
    r_series(likert, 3, name = "Question")
)
```

```
## Source: local data frame [100 x 6]
## 
##     ID Age    Sex        Question_1        Question_2        Question_3
## 1  001  28   Male             Agree             Agree Strongly Disagree
## 2  002  24   Male           Neutral   Strongly Agree           Disagree
## 3  003  26   Male          Disagree           Neutral          Disagree
## 4  004  31   Male Strongly Disagree           Neutral          Disagree
## 5  005  21 Female   Strongly Agree  Strongly Disagree Strongly Disagree
## 6  006  23 Female          Disagree          Disagree             Agree
## 7  007  24 Female          Disagree   Strongly Agree  Strongly Disagree
## 8  008  24   Male Strongly Disagree             Agree             Agree
## 9  009  29 Female             Agree   Strongly Agree    Strongly Agree 
## 10 010  26   Male Strongly Disagree Strongly Disagree             Agree
## .. ... ...    ...               ...               ...               ...
```



```r
set.seed(10)

r_data_frame(n=100,
    id,
    age,
    sex,
    r_series(likert, 5, name = "Item", integer = TRUE)
)
```

```
## Source: local data frame [100 x 8]
## 
##     ID Age    Sex Item_1 Item_2 Item_3 Item_4 Item_5
## 1  001  28   Male      4      4      1      1      1
## 2  002  24   Male      3      5      2      1      2
## 3  003  26   Male      2      3      2      1      2
## 4  004  31   Male      1      3      2      4      3
## 5  005  21 Female      5      1      1      5      4
## 6  006  23 Female      2      2      4      3      4
## 7  007  24 Female      2      5      1      5      2
## 8  008  24   Male      1      4      4      5      5
## 9  009  29 Female      4      5      5      4      3
## 10 010  26   Male      1      1      4      1      2
## .. ... ...    ...    ...    ...    ...    ...    ...
```

## Expanded Dummy Coding

The user may wish to expand a `factor` into `j` dummy coded columns.  The `r_dummy` function expands a factor into `j` columns and works similar to the `r_series` function.  The user may wish to use the original factor name as the prefix to the `j` columns.  Setting `prefix = TRUE` within `r_dummy` accomplishes this.



```r
set.seed(10)
r_data_frame(n=100,
    id,
    age,
    r_dummy(sex, prefix = TRUE),
    r_dummy(political)
)
```

```
## Source: local data frame [100 x 9]
## 
##     ID Age Sex_Male Sex_Female Constitution Democrat Green Libertarian
## 1  001  28        1          0            1        0     0           0
## 2  002  24        1          0            1        0     0           0
## 3  003  26        1          0            0        1     0           0
## 4  004  31        1          0            0        1     0           0
## 5  005  21        0          1            1        0     0           0
## 6  006  23        0          1            0        1     0           0
## 7  007  24        0          1            0        1     0           0
## 8  008  24        1          0            0        0     0           0
## 9  009  29        0          1            1        0     0           0
## 10 010  26        1          0            0        1     0           0
## .. ... ...      ...        ...          ...      ...   ...         ...
## Variables not shown: Republican (int)
```


## Visualizing Column Types

It is helpful to see the column types and `NA`s as a visualization.  The `table_heat` (the `plot` method assigned to `tbl_df` as well).


```r
set.seed(10)

r_data_frame(n=100,
    id,
    dob,
    animal,
    grade, grade,
    death,
    dummy,
    grade_letter,
    gender,
    paragraph,
    sentence
) %>%
   r_na() %>%
   plot(palette = "Set1")
```

![plot of chunk unnamed-chunk-16](inst/figure/unnamed-chunk-16-1.png) 







