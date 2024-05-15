# R-For-Linguists
This is the resulting repository for a course entitled "R For Linguists" at University Leipzig.

## Useful Features of R For Linguists
#### Piping
Pipes can significantly improve readability.
```R
# This is the equivalent of max(dat$meanWeightRating).
dat$meanWeightRating %>% max()
dat$meanWeightRating %>% mean()
```

So far, we can't see the advantage. However, remember that R is a functional language and so your expressions will become very complicated very quickly.
```R
round(exp(diff(log(x))), 1)

# Can also be written as:

x %>% log() %>%
    diff() %>%
    exp() %>%
    round(1)
```

#### Group By
GroupBy is akin to GROUPBY in SQL and aggregates the data into the distinct values of a particular column. It returns the data as a *tibble*.
A *tibble* is like a dataframe, but one advantage is it can have a specified *group_by* function.
```R
library(dplyr)
 
df = read.csv("Sample_Superstore.csv")
 
df_grp_region = df %>% group_by(Region)  %>%
                    summarise(total_sales = sum(Sales), 
                              total_profits = sum(Profit), 
                              .groups = 'drop')
 
View(df_grp_region)
```

#### Mutate
The mutate functions allows you to create a new column in a dataframe.
```R
dat %>% 
  mutate(uniqueWord = FamilySize==0) %>% #this means: add a new column named uniqueWord, defined by the formula on the right of the = sign
  group_by(uniqueWord) %>%
  summarize(mean(meanFamiliarity))
```
