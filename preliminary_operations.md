IBM employees predictions
================
Karol Roszak
5/5/2021

# Reading and preprocessing

### Reading raw data

``` r
# Reading raw data and entry preprocessing

raw_data = read.csv("data/raw_data.csv")
raw_data = na.omit(raw_data) # strict policy for missing values

# Reshaping raw data and saving it to inspect in Weka

raw_weka_data = raw_data %>% relocate(Attrition, .after=YearsWithCurrManager)
write.csv(raw_weka_data, "data/raw_weka_data.csv", row.names = FALSE)

# Raw data visualization to check out attribute values and their features

  # in Weka maybe......
```

### Data preprocessing

``` r
# Dropping irrelevant attributes

preprocessed_data = raw_weka_data %>%
  select(-EmployeeCount) %>%
  select(-EmployeeNumber) %>%
  select(-Over18) %>%
  select(-StandardHours)

# Discretizing some attributes

preprocessed_data = preprocessed_data %>% 
  mutate(Education=recode(Education,
                                 `1` = 'Below College',
                                 `2` = 'College',
                                 `3` = 'Bachelor',
                                 `4` = 'Master',
                                 `5` = 'Doctor')) %>%
  mutate(EnvironmentSatisfaction = recode(EnvironmentSatisfaction,
                                 `1` = 'Low',
                                 `2` = 'Medium',
                                 `3` = 'High',
                                 `4` = 'Very High')) %>%
  mutate(JobInvolvement = recode(JobInvolvement,
                                 `1` = 'Low',
                                 `2` = 'Medium',
                                 `3` = 'High',
                                 `4` = 'Very High')) %>%
  mutate(JobSatisfaction = recode(JobSatisfaction,
                                  `1` = 'Low',
                                 `2` = 'Medium',
                                 `3` = 'High',
                                 `4` = 'Very High')) %>%
  mutate(PerformanceRating = recode(PerformanceRating,
                                 `1` = 'Low',
                                 `2` = 'Good',
                                 `3` = 'Excellent',
                                 `4` = 'Outstanding')) %>%
  mutate(RelationshipSatisfaction = recode(RelationshipSatisfaction,
                                 `1` = 'Low',
                                 `2` = 'Medium',
                                 `3` = 'High',
                                 `4` = 'Very High')) %>%
  mutate(WorkLifeBalance = recode(WorkLifeBalance,
                                 `1` = 'Bad',
                                 `2` = 'Good',
                                 `3` = 'Better',
                                 `4` = 'Best'))

write.csv(preprocessed_data, "data/preprocessed_data.csv", row.names = FALSE)
```

``` r
# just a temporary table.....

#preprocessed_table = reactable(preprocessed_data, 
#      defaultColDef = colDef(
#      header = function(value) gsub(".", " ", value, fixed = TRUE),
#      cell = function(value) format(value),
#      align = "center",
#      headerStyle = list(background = "#edf8fb")
#    ),
#    defaultPageSize = 5,
#    bordered = TRUE,
#    highlight = TRUE,
#    filterable = TRUE,
#    searchable = TRUE,
#    resizable = TRUE
#    )

#preprocessed_table
```

# Finding correlations in data

# Taking care of outliers in data
