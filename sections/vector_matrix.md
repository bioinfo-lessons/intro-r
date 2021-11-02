# Exercise 1: Our first vector

Create a **numeric vector** that goes from 1 to 20. Then, divide it by 2 and store
the results to another vector, called **divided_by_two**. Finally, make a third **logical vector**
storing which values of  **divided_by_two** are greater than 5.

```R
print()
```


<details>
  <summary>Answer</summary>

 ```R
a <- c(1:20)
divided_by_two <- a / 2
greater_than_five <- divided_by_two > 5
 ```

</details>

# Exercise 2: Appending truth
Extend the last vector of exercise #1, by adding the following values: _TRUE, TRUE, FALSE_

<details>
  <summary>Answer</summary>

 ```R
greater_than_five <- c(greate_than_five, TRUE, TRUE, FALSE)
 ```
</details>

# Exercise 3: The longest vector
Write a function called **get_longest_vector** that takes two vectors as arguments. The function should check
which is the longest vector and return its name. If there is a tie, the second vector wins. 
<details>
  <summary>Answer</summary>

 ```R
 get_longest_vector <- function(v1, v2){
  if(length(v1) > length(v2)){
    return(paste(substitute(v1), 'is the winner vector'))
  }else{
    return(paste(substitute(v2), 'is the winner vector'))
  }
}

You may have noticed I have used the function `substitute`. It returns the
actual name of the object containing v1 and v2 respectively. 
 ```
 </details>

# Exercise 4: Random minimum and maximum
Use the functions `min()` and `max()` to find the minimum and maximum values
of the following vector:

```R
my_random_vector <- runif(n=200, min=0, max=400000000)
```

<details>
  <summary>Answer</summary>

 ```R
max_value <- max(my_random_vector)
min_value <- min(my_random_vector)
 ```
 </details>


# Exercise 5: basic statistics
Use the functions `mean()`, `median()` and `sd()` to calculate the mean, median
and standard deviation of **my_random_vector**.

<details>
  <summary>Answer</summary>

 ```R
mean_value   <- mean(my_random_vector)
median_value <- median(my_random_vector)
sd_value     <- sd(my_random_vector)

 ```
 </details>

# Exercise 6: greater than average
Use the previous **random vector** and the median you calculated to create a logic vector
of the values in **random_vector** greater than the median value. 

<details>
  <summary>Answer</summary>

 ```R
median_value <- median(my_random_vector)

greater_than_average <- random_vector > median_value

 ```
 </details>


# Exercise 7: Mixing types
Create the following vector:

```R
mixed_vector <- c(TRUE, 3, "KRAS", 4.00)
```
Check its class and answer the following questions:

1. Which data type are you getting? 
1. Why?


<details>
  <summary>Answer</summary>

  1. Character
  1. Because it is the only possibility. Every value in **mixed_vector** can be
  represented as `character`. There is no ot her posibility. 

 </details>

# Exercise 8
Create a 4x6 **numeric matrix** called **my_matrix** and fill it with values
ranging from 1 to 24. 

<details>
  <summary>Answer</summary>

  ```R
  my_matrix <- matrix(1:24, nrow=4, ncol=6)
  ```
 </details>

# Exercise 9
**Multiply** the previous matrix by 4. Print the result.

<details>
  <summary>Answer</summary>

  ```R
  my_matrix <- my_matrix * 4
  print(my_matrix)
  ```
 </details>

 # Exercise 10
Check which cells of the previous matrix are greater than 20. Store the results
in a **logical matrix**. Print the result.

<details>
  <summary>Answer</summary>

  ```R
  my_logic_matrix <- my_matrix > 20
  print(my_logic_matrix)
  ```
 </details>

# Exercise 11
**Create** the following matrix:

```R
too_many_cells <- matrix(1:12, nrow = 5, ncol = 4)
```

And answer the following questions:

1. Are you getting a warning? Why?
1. How did R solve the aforementioned warning?


<details>
  <summary>Answer</summary>

1. Yes, a warning is issued because the matrix has more cells than the amount of values we  supplied.
1. R recicled our vector! It repeated values from 1:12 until it filled the whole matrix. 
 </details>


# Exercise 12
**Create** the following matrix:

```R
all_ones <- matrix(1:2, nrow = 5, ncol = 4)
```

And answer the following questions:

1. Are you getting a warning?
1. We have 20 cells and only one value. What just happened? 


<details>
  <summary>Answer</summary>

1. No
1. R recicled our vector again. But It only complains If our number of cells is not divisible by
the amount of values we have. Otherwise, It will repeat the whole vector as many times as necessary
until it fills the matrix. In this case 20 cells by 2 values equals 10 repetitions.
 </details>

 # Exercise 13: An introduction to logical indexing
 Use the logic vector of exercise #6 to subset the values of 
 **random_vector** which are greater than the median value.

<details>
  <summary>Answer</summary>

 ```R
greater_than_average <- random_vector > median_value

subset_vector <- my_random_vector[greater_than_average]

Try to guess what happened here. If you are clueless, don't worry, since we will
be reviewing logical indexing in the next session.
 ```
 </details>
