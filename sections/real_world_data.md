# A real dataset

The tidyr::who dataset contains tuberculosis (TB) cases broken down by year, country, age, gender, and diagnosis method.
The data comes from the [2014 World Health Organization Global Tuberculosis Report](https://www.who.int/teams/global-tuberculosis-programme/data). There’s a wealth
of epidemiological information in this dataset, but it’s challenging to work with the data in the form that it’s provided.

This is a very typical **real-life** example dataset. It contains redundant columns, odd variable codes, and many missing values.

# A short summary of the dataset

The columns **country, iso2, and iso3** are three variables that specify the country. Yes, these are **redundant**. We also have
a **Year** column.

What about the rest of the columns (e.g. new_sp_m014, new_ep_m014, new_ep_f014)?

1. The first three letters of each column denote whether the column contains new or old cases of TB. In this dataset, each column contains new cases.
2. The next two or three letters describe the type of TB:
    * rel stands for cases of relapse
    * ep stands for cases of extrapulmonary TB
    * sn stands for cases of pulmonary TB that could not be diagnosed by a pulmonary smear (smear negative)
    * sp stands for cases of pulmonary TB that could be diagnosed be a pulmonary smear (smear positive)
3. The sixth letter gives the sex of TB patients. The dataset groups cases by males (m) and females (f).
4. The remaining numbers gives the age group. The dataset groups cases into seven age groups:
    * 014 = 0 – 14 years old
    * 1524 = 15 – 24 years old
    * 2534 = 25 – 34 years old
    * 3544 = 35 – 44 years old
    * 4554 = 45 – 54 years old
    * 5564 = 55 – 64 years old
    * 65 = 65 or older


# First step: pivot_longer the dataset
Use `pivot_longer()` to to gather all columns from **new_sp_m014** to **newrel_f65**. Call the new **name** column
**tb_type** and **cases** to the value column. We have many **missing values**, but we are going to remove them. Look
at the documentation for `pivot_longer()` and find the relevant parameter.


# Second step: replace a minor typo
We need to make a minor fix to the format of the column names: unfortunately the names are slightly inconsistent because instead of **new_rel** we have newrel. 
Use `stringr::str_replace()` to replace the characters _newrel_ with **new_rel**. This makes all variable names consistent.

As a clue, look at the following **example**:

```R
mutate(tb_type = stringr::str_replace(tb_type, "newrel", "new_rel"))
```


# Third step: separating
Our resulting data frame after **pivot_longer** is much more tidy than before, but now we have a column called
**tb_type** which stores more than one variable.  Use `separate()` to create three columns from **tb_type**:
**new**, **type**, **sexage**.

Now, we need to **separate again** the column **sexage** into two columns: **sex and age**. To do so, use
another `separate()`.


**CLUE**: 
Notice that the **first** character in **sexage** is the sex data **AND** it is represented by a **single** character.
Therefore, you can **separate** by **the first** character.

# Fourth step: get rid of redundant columns
There are three redundant columns: **iso2**, **iso3**, and **new**. Remove them.



# Complete answer: with pipes

<details>
  <summary>Answers</summary>

```R

clean_data <- who %>%
    pivot_longer(names_to='tb_type',
                 cols=new_sp_m014:newrel_f65,
                 values_to = 'cases',
                 values_drop_na = TRUE) %>%
    mutate(tb_type = stringr::str_replace(tb_type, 'newrel', 'new_rel')) %>%
    separate(col=tb_type, into = c('new', 'type', 'sexage'), sep='_') %>%
    separate(col=sexage, into=c('sex', 'age'), sep=1) %>%
    select(-iso2, -iso3, -new) %>%
    mutate(country = as.factor(country))


```

</details>