Statistical analysis of the Charity hospital database
================
Authors: 
I. Maslova
I. Tsepeleva
A. Bydanov
P. Pchelintseva
E.Tomilov

# Introduction

Charity hospital is a non-profit organization that provides medical and
social assistance to homeless people in Saint Petersburg. Volunteer
doctors consult patients, vaccinate them, provide them with glasses,
etc. Since 2021, the REDCap electronic data capture system has been
collecting information about all the Charity hospital patients. The aim
of this study was to analyze the patient database of the Charity
hospital which contains information about 1633 unique patients and 4427
visits.

# Objectives: 
1. to prepare data for the analysis 
2. to create the report
with descriptive statistics 
3. to create a universal portrait of the
homeless person 
4. to find relationship between place of appointment and
other variables 
5. to analyze HIV-positive population distinctly 
6. to search for indicators on which the call to the ambulance depends

# Methods and Approaches
Statistical analysis was performed using R package (version 4.2 or higher) with specialized software Rstudio.
Standard parametric criteria were used to compare quantitative data: Student's t-test for dependent/independent samples, analysis of variance (ANOVA) for repeated measures. Frequencies between groups were compared using Pearson's χ2 test or Fisher's exact test.
If any of the baseline data revealed significant noncomparability of the study groups (statistically and clinically significant differences in demographic and other baseline data between the groups), we additionally performed analysis using multivariate statistics (linear or logistic regression depending on the type of parameter under study). 

In describing all estimated values, both p-values and point estimates with corresponding 95% confidence intervals are presented. 
To perform a one-factor analysis of variance, we tested the groups for normality of the distribution. If the analysis of variance showed statistically significant differences between the groups, the TukeyHSD test was performed. 
In case of normality violation the Kruskal-Wallis test was performed. Dunn's test was conducted to determine the difference between the groups. 
The strength of the relationship between the two nominal variables was assessed using Cramer's criterion (Cramer's V).

Regression analysis was performed using lm and glm functions. 
The data was visualized using ggplot, plotly package. 

# Descriptive statistics and a universal portrait of the homeless person
Visit analysis.
We were provided with data on 1633 unique patients. Patients had the following goals for the visit:
-first appointment (mandatory for all)  
-main appointment  
-vaccination  
-for homeless women   
-vision assessment  
-social support  
-photobase (wounds, rashes, extracts, documents)  
-express testing  
The mode for each of the categories was equal to one (most often, patients for any purpose came only once). Some patients had a large number of visits for the same purpose. Thus, the maximum number of main appointments for one person was 35, maximum number of the reception for the photobase - 18. The other categories did not have such high rates.


![](final_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

## A universal portrait of the homeless person

One of the objectives of our project is to draw up a universal portrait of a homeless person. The analysis carried out showed the following results: most people without a fixed place of residence who applied to ANO "Charity Hospital" are male, with Russian citizenship, have a basic set of documents (Passport, SNILS, compulsory medical insurance policy), have a permanent registration or do not have it at all. For the majority of patients, consent to the processing of personal data was not filled out at the first appointment. Most patients do not have socially significant diseases, allergies, but have bad habits (nicotine and alcohol addiction). Of the diseases, the most common are diseases of the skin and subcutaneous tissue, diseases of the musculoskeletal system and connective tissue, diseases of the respiratory system, diseases of the digestive system and diseases of the circulatory system. Patients are mostly unmarried. Approximately equally there were patients who were and were not in places of detention. 




![](final_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->![](final_files/figure-gfm/unnamed-chunk-23-2.png)<!-- -->

# Visual acuity analysis


Data on the visual acuity of the 111 homeless patients were also analyzed. 74% had farsightedness. The most demanded glasses are 2.5 diopters.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](final_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

# HIV
We conducted an analysis of HIV-infected people to investigate the assosiation with this infection and another factors. Among all patients included in the database, 87 people were infected with HIV. Of these, 53 are registered. Performing regression analysis we revealed statistically significant correlation with HIV infection and some predictors. For instance, every year the chance of contracting HIV decreases by 0.94 times compared to the previous year. The male gender also reduces the chance to be infected by 0.3 times. The presence of diagnosed hepatitis C increases the chance by 3 times, and hepatitis B - by 5 times which is fully consistent with 
literature data (Mohsen A. et al., 2002). 

![](final_files/figure-gfm/HIV.png)<!-- -->

The HIV patients are divided into two groups - those who are on the dispensary registry and those who confirmed the disease on the patient's word. This plot shows that patients who are on the dispensary registry take therapy more often than other. 

![](final_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->



# Hepatitis C

 A similar regression analysis was carried out to search for associations with Hepatitis C. It was found that every year the chance of infection with hepatitis C decreases by 0.96 times, relative to the previous year. Gender in this case does not play a significant role, p-value>0.05. At the same time, the presence of HIV infection increases the chance to be infected by 3 times, and hepatitis B by 10 times.

# Cramer\`s V

To search for indicators on which the call to the emergency medical
services to the patient depends, we used Cramér’s V for nominal
variables. Regression analysis was unavailable due to lack of data.  
To calculate the strength of association, we built a table, the values
of which were then divided into three categories: weak, moderate and
strong connection. No strong association between the variables was
found. A moderate association was observed between hospitalization and
the following variables: complaints, edema (anasarca), vomiting
(uncontrollable), SpO2 saturation.





# Reception place

For further analysis, we identified several places of reception with the highest attendance, between which some differences were found.

The place of reception that stands out most in terms of a number of indicators was designated as MS.

The graphs below show systolic and diastolic blood pressure readings. Significant differences in systolic pressure were between the points of reception of MS and NP, diastolic - between MS and all other points of reception.

## Systolic pressure



    ## # A tibble: 5 x 2
    ##   Место.приема      Систолическое
    ##   <fct>                     <dbl>
    ## 1 "АМ Тухачевского"    0.0185    
    ## 2 "АМ\\НА Лесная"      0.100     
    ## 3 "Атаманская, 6"      0.106     
    ## 4 "МС"                 0.00000149
    ## 5 "НП"                 0.000763

    ## [1] 0.00473854

    ## # A tibble: 10 x 9
    ##    .y.           group1       group2    n1    n2 stati~1       p   p.adj p.adj~2
    ##  * <chr>         <chr>        <chr>  <int> <int>   <dbl>   <dbl>   <dbl> <chr>  
    ##  1 Систолическое "АМ Тухачев~ "АМ\\~    47    45   0.567 5.71e-1 1       ns     
    ##  2 Систолическое "АМ Тухачев~ "Атам~    47    40  -0.126 8.99e-1 1       ns     
    ##  3 Систолическое "АМ Тухачев~ "МС"      47   138  -1.90  5.72e-2 0.458   ns     
    ##  4 Систолическое "АМ Тухачев~ "НП"      47    86   0.859 3.90e-1 1       ns     
    ##  5 Систолическое "АМ\\НА Лес~ "Атам~    45    40  -0.669 5.03e-1 1       ns     
    ##  6 Систолическое "АМ\\НА Лес~ "МС"      45   138  -2.56  1.05e-2 0.0944  ns     
    ##  7 Систолическое "АМ\\НА Лес~ "НП"      45    86   0.205 8.38e-1 1       ns     
    ##  8 Систолическое "Атаманская~ "МС"      40   138  -1.64  1.02e-1 0.711   ns     
    ##  9 Систолическое "Атаманская~ "НП"      40    86   0.957 3.39e-1 1       ns     
    ## 10 Систолическое "МС"         "НП"     138    86   3.47  5.16e-4 0.00516 **     
    ## # ... with abbreviated variable names 1: statistic, 2: p.adj.signif

![](final_files/figure-gfm/unnamed-chunk-58-1.png)<!-- -->

## Diastolic pressure:

    ## # A tibble: 5 x 2
    ##   Место.приема      диастолическое
    ##   <fct>                      <dbl>
    ## 1 "АМ Тухачевского"    0.00618    
    ## 2 "АМ\\НА Лесная"      0.0469     
    ## 3 "Атаманская, 6"      0.0342     
    ## 4 "МС"                 0.000000267
    ## 5 "НП"                 0.00757

    ## [1] 3.028218e-11

    ## # A tibble: 10 x 9
    ##    .y.            group1      group2    n1    n2 stati~1       p   p.adj p.adj~2
    ##  * <chr>          <chr>       <chr>  <int> <int>   <dbl>   <dbl>   <dbl> <chr>  
    ##  1 диастолическое "АМ Тухаче~ "АМ\\~    47    43  0.461  6.45e-1 1   e+0 ns     
    ##  2 диастолическое "АМ Тухаче~ "Атам~    47    40 -0.181  8.57e-1 1   e+0 ns     
    ##  3 диастолическое "АМ Тухаче~ "МС"      47   138 -4.70   2.62e-6 2.09e-5 ****   
    ##  4 диастолическое "АМ Тухаче~ "НП"      47    85  0.0146 9.88e-1 1   e+0 ns     
    ##  5 диастолическое "АМ\\НА Ле~ "Атам~    43    40 -0.620  5.35e-1 1   e+0 ns     
    ##  6 диастолическое "АМ\\НА Ле~ "МС"      43   138 -5.10   3.38e-7 3.04e-6 ****   
    ##  7 диастолическое "АМ\\НА Ле~ "НП"      43    85 -0.506  6.13e-1 1   e+0 ns     
    ##  8 диастолическое "Атаманска~ "МС"      40   138 -4.20   2.64e-5 1.85e-4 ***    
    ##  9 диастолическое "Атаманска~ "НП"      40    85  0.217  8.28e-1 1   e+0 ns     
    ## 10 диастолическое "МС"        "НП"     138    85  5.77   7.71e-9 7.71e-8 ****   
    ## # ... with abbreviated variable names 1: statistic, 2: p.adj.signif

![](final_files/figure-gfm/unnamed-chunk-60-1.png)<!-- -->

![](final_files/figure-gfm/unnamed-chunk-63-1.png)<!-- -->![](final_files/figure-gfm/unnamed-chunk-63-2.png)<!-- -->



Most of the MS visitors are residents of permanent homeless shelters (278 out of 293 visitors), and most visitors of NP are residents of low-threshold homeless shelters (night with heating points - 276 out of 337 visitors).



![](final_files/figure-gfm/unnamed-chunk-50-1.png)<!-- -->

The largest flow at all reception points was observed in the summer except for MS.


![](final_files/figure-gfm/unnamed-chunk-51-1.png)<!-- -->

The greatest load on reception places was generally observed in the evening (8-10 pm). 

![](final_files/figure-gfm/unnamed-chunk-53-1.png)<!-- -->

However, in the picture or when constructing the table, we can see that, apparently, the receptions were available at different times, probably alternately. Again, with the exception of MS.

![](final_files/figure-gfm/unnamed-chunk-54-1.png)<!-- -->

   
    ##  до 9  9-10  10-11 11-12 12-13 13-14 14-15 15-16 17-18 18-19 19-20 20-21 21-22 22-23 23-24 
    ##   12    35    152   115   157   162    59    27   102   121    98   350   247    55    14   
 
    
## Literature
1. Mohsen AH, Easterbrook P, Taylor CB, Norris S. Hepatitis C and HIV-1 coinfection. Gut. 2002 Oct;51(4):601-8. doi: 10.1136/gut.51.4.601. PMID: 12235089; PMCID: PMC1773386.
2. https://tsamsonov.github.io/r-geo-course/index.html
3. http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/
4. https://r-graph-gallery.com/index.html
5. https://habr.com/ru/post/469215/
6. https://stackoverflow.com/questions/37506934/calculations-with-minutes-and-seconds-in-r
7. https://medstatistic.ru/articles/analiz_dannyh.pdf

