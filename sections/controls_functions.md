# Exercise 1: Random numbers and conditions

Let's use `runif()` again to generate three random numbers between 1 and 100.
Store the results to three variables called A, B and C

```R
A  <- runif(min=1, max=100, n=1)
B  <- runif(min=1, max=100, n=1)
C  <- runif(min=1, max=100, n=1)
```

Now, write a script that checks if A is greater than B and prints a message to
the console announcing that A is the greater number.

<details>
    <summary>Answers</summary>

```R

if(A >= B){

    print('A is the greater number')

}
```

</details>

# Exercise 2
Extend the script you just write to add another conditional statement. Now,
If A is not greater than B, print a message announcing it.


<details>
    <summary>Answers</summary>

```R

if(A >= B){

    print('A is the greater number')

}else{
    print('A is not the greater number')
}
```

</details>

# Exercise 3: Our first WHILE loop
Create a variable  called **start_point** and set it to 0. Then, write a **WHILE**
loop that checks if **start_point** is equal or greater than 60. If **start_point**
value is lower, increase it. Print the value of **start_point** in each
iteration.

<details>
    <summary>Answer</summary>

```R
start_point <- 0

while(start_point <= 60){

    print(paste('start_point value is:', start_point))

    start_point = start_point + 3

}
```

</details>

# Exercise 4
Taking the previous answer as a baseline, add  the following functionality:

1. Print **start_point** value  **ONLY** if its an uneven number.
2. Add a print message if **start_point** value is divisible by 5. 

<details>
    <summary>Answer</summary>

```R
start_point <- 0

while(start_point <= 60){

    if(start_point %% 2 != 0){
        print(paste('start_point value is:', start_point))
    }else if(start_point %% 5 == 0){
        print(paste(start_point, ' is divisible by 5'))
    }

    start_point = start_point + 3

}
```

</details>

# Exercise 5: Calculate the power of fifth
Write a function that takes **one argument**, called **number** and returns
its fifth power. Call the function **get_fifth_power**. Use it to calculate
the fifth power of 76.

<details>
    <summary>Answer</summary>

```R
get_fifth_power <- function(number){

    power_of_number <- number^5
    return(power_of_number)
}

fifth_power_of_76 <- get_fifth_power(76)
```
</details>

# Exercise 5: Division by 0 
Write a function that takes **two arguments**, called **A** and **B**, and 
returns the result of dividing A by B. **DO NOT ALLOW** the function to perform
a division by 0. Name the function **divide_numbers**. 

1. Try it by setting B to any number and also to 0. What kind of value are you getting as a result?
2. What would happen If we actually divided by 0?

<details>
    <summary>Answer</summary>

```R

divide_numbers <- function(A, B){

    if(B == 0){ ## Check if we are dividing by 0
        stop('You are dividing by zero!')
    }else{
        return(A / B)
    }
}
```
1. We would get NULL If we hadn't added the STOP.
2. R would return "Inf" as a result.

You probably tried to use IF/ELSE to prevent the function from dividing by zero.
However, you will soon find out that in that case, you are getting NULL as the result
of executing the function.

**stop** raises an **error message** instead of returning NULL, thus allowing us
to exit the function and tell the user we encountered an error, instead of silently 
returning NULL.

</details>

# Exercise 6: Counting words
Read the documentation for ```nchar()```. Then, write a function called 
**get_longest_word**. It must accept two arguments, **first_word** and **second_word**. 
Use ```nchar()``` to calculate which word has more characters and return the winner. If
both words are of equal length, return "TIE". 

<details>
        <summary>Answer</summary>

```R

get_longest_word <- function(first_word, second_word){

    char_difference <- nchar(first_word) - nchar(second_word)

    if(char_difference == 0){
        return('TIE')
    }else{
        result <- ifelse(char_difference > 0, first_word,  second_word)

        return(result)
    }
}
```

First of all, there are multiple valid solutions to this exercise. This answer
makes use of `ifelse()` to avoid writing a full IF/ELSE block. Alternatively, you could 
check if there is a tie, then write a nested IF/ELSE block to check which of the words is the longest
like below:

```R

get_longest_word <- function(first_word, second_word){

   if(nchar(first_word) == nchar(second_word)){
       return('TIE')
   }else{

       if(nchar(first_word) > nchar(second_word)){
           return(first_word)
       }else{
           return(second_word)
       }
   }
}
```
At this moment, focus on getting the exercises right. Brevity and readability will naturally
come to you later on.

</details>