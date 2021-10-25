# Exercise 1: Hello world

Let's dive in R with an iconic programming example: 

Write a simple script to say hello to the world. To do that, first
create a variable called **greetings** and assign it the value _Hello world!_.
Then, print **greetings** to the screen with the function:

```R
print()
```


<details>
  <summary>Answer</summary>

 ```R

 greetings <- 'Hello world!'
 print(greetings)
 ```

</details>

# Exercise 2: Check the documentation of print

_print_ is not a complicated function, but reading documentation is a good programming habit.
Let's check the documentation available for print. To do so, type:

```R
?print
```

and look at the left panel in RStudio. Try to answer the following questions:

1. How many named arguments does print have? 
1. How do you control if strings should be print with or without quotes?

<details>
  <summary>Answers</summary>

1. 10
2. By setting the argument 'quote' to TRUE if quotes are desired and FALSE otherwise.

</details>

# Exercise 3: Check the basic type of a variable

An easy way to check the type of a given variable is by using the function

```R
class()
```

Now define the following variables and set them to the values below

```R
a <- 10
b <- FALSE
c <- "Hola mundo"
d <- 10.00
```

and check the class of all of them.

<details>
  <summary>Answer</summary>

  1. numeric
  1. logical
  1. character
  1. numeric

</details>

# Exercise 4: numeric vs integer

Write the following code
```R
a <- 10.3333
b <- as.integer(a)
```

Now answer the following questions:

1. What is the type of a?
1. What is the type of b?
1. What's the difference between the values of a and b. Why?
1. What is as.integer doing?

<details>
  <summary>Answers</summary>

  1. Numeric
  1. Integer
  1. A is a numeric type variable whose value is a decimal number.
  1. as.integer is converting a numeric variable into an integer. Since an integer cannot have a fractional component, it is discarded.

</details>


# Exercise 5: basic calculus
Write a script that:

1. Calculates and stores the result of: 126 * 37
1. Checks If the result of 126 * 37 is greater than 4660


<details>
  <summary>Answer</summary>

  ```R
  result     <- 126 * 37
  comparison <- (result > 4660)
  print(comparison)
  ```

</details>

## Exercise 6: the remainder of the division

Write a script that divides 1600 by 1250 and retrieves the remainder of the 
operation. Then, check if the remainder is less than 30. Print the result.

<details>
  <summary>Answer</summary>

  ```R
  remainder  <- 1600 %% 1250
  comparison <- reminder < 30
  print(comparison)
  ```

</details>

## Exercise 7: Randomness madness

We can use `runif()` to generate random numbers. For instance, to generate a
random rational number between 1 and 20, we can type:

```R
a <- runif(min=1, max=20, n=1)
```

Write a script that uses the aforementioned function to generate three numbers, 
from 1 to 100, and save them to three variables called **first**, **second** and **third** respectively.

Now check if first is greater than or equal to second. Store the result to a variable called
**first_vs_second**. Print its value.

After that, divide second by third and multiply it by first. Store and print the result.

<details>
  <summary>Answer</summary>

  ```R
  first  <- runif(min=1, max=100, n=1)
  second <- runif(min=1, max=100, n=1)
  third  <- runif(min=1, max=100, n=1)

  first_vs_second <- first >= second
  print(first_vs_second)

  result <- second / third * first
  print(result)
  ```
</details>

## Exercise 8: Order matters
Define in  a script the following variables:

```R
a <- 10
b <- 15
d <- 2
```
Then, write a script that performs the following arithmethic operations:

1. Sum a and b
2. Divide the result by d
3. Print the result

You cannot write more than one line of code for both arithmethic operations.

<details>
  <summary>Answer</summary>

  ```R
 a <- 10
 b <- 15
 d <- 2

 result <- (a + b) / d # One line of code
 print(result)


  ```
  **Remember**: In programming, arithmethic operators work the same as their mathemathic
counterparts. That means that, unless you are using parenthesis, division is performed
before sum.
</details>



