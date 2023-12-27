+++
title = "A Jelly Bean Probablity Model"
date = "2023-11-09T14:10:55-07:00"
author = "Andrew Attilio"
authorTwitter = "" #do not include @
cover = ""
tags = ["statistics", "modeling", "python"]
keywords = ["", ""]
description = "Determing the most likely outcome of a jelly-bean experiment using Python."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++

## Jelly Bean Probability

In this problem, we are exploring the most probable outcome
after a jelly bean experiment. The experiment proceeds as follows:

- Stir together 2023 red jelly beans and 2023 green jelly beans.
  
- Pull 3 jelly beans out of the jar at a time.
  
- If they are all the same color, eat all 3 jelly beans.
  
- If there are 2 of one color, eat 1 of the majority color and put the
  other 2 jelly beans back in the jar.
  

After following this process, there are 4 distinct ways for the
experiment to end:

1. No beans.
  
2. One bean (either color is equally probable).
  
3. Two beans of the same color (either color is equally probable).
  
4. One red and one green. 

## Solution 

Calculating the probabilities of hundreds of consecutive
draws seemed impossibly complicated, so I coded a Python program that
simulates the stated problem, drawing three beans at a time until no
more than 2 remain.

The code for my `bean_jar_experiment()` function is listed below. There
are two global variables, `red_count` and `green_count`. The
`bean_jar_experiment()` continuously calls the `draw_beans` function
until there are 2 or less beans left in the virtual jar. Each instance
of `draw_beans` generates three random numbers, each of which
corresponds to either a red or green bean. Depending on the results of
the 3 randomly-generated beans, the function subtracts the proper amount
of beans from `red_count` or `green_count`, simulating consumption of
those beans. The `draw_count` is initialized to 0, and I simulated each
red bean as $-1$ for the `draw_count` and each green bean as $+1$. For
example, the following line represents consuming three red beans, given
that the `draw_count` is equal to -3:

```
    case (-3): # all red
            red_count -= 3
```

The following is the full code for the program:

```
red_count = 2023    
green_count = 2023

def bean_jar_experiment():  
    while (red_count + green_count) > 2:
        draw_beans(red_count, green_count)

    print('Red: ', red_count)
    print('Green: ', green_count)

def draw_beans(red, green):
    global red_count
    global green_count

    draw_count = 0 # if < 0: red, if > 0: green
    for i in range(3):
        random_int = randint(1, (red + green))
        if random_int <= red:
            draw_count -= 1
        else: 
            draw_count += 1
    match draw_count:
        case (-3): # all red
            red_count -= 3
        case (-1): # 2 red, 1 green
            red_count -= 1
        case (1): # 2 green, 1 red
            green_count -= 1
        case (3): # all green
            green_count -= 3
```

Great, but this would be most useful by running the program hundreds,
thousands, or millions of times and collecting all of the results. Let's
do that.

I created a dictionary for the program that stores the results of each
occurrence of the `bean_jar_experiment` function. The mappings are based
on the 4 cases $\{a, b, c, d\}$ defined in the intro section of this
paper. The initial dictionary is:

```
    results = {'a': 0, 'b': 0, 'c': 0, 'd': 0}
```

Each time the program runs, it will add 1 to the corresponding case
result. I ran the program 1000 times, then 10000 times, then 100000
times. Here are the results:

```
    RESULTS FROM 10000 EXPERIMENTS
    {'a': 1057, 'b': 3335, 'c': 2885, 'd': 2723}
    Runtime: 72.10 seconds

    RESULTS FROM 100000 EXPERIMENTS:
    {'a': 10258, 'b': 33810, 'c': 28834, 'd': 27098}
    Runtime: 754.85 seconds
```

The results are consistent. According to the Python program, **case 2
is most likely to occur**, which corresponds to ending with either one
green or one red bean in the jar. **Case 1 is the least likely
outcome**, which is the case in which we end with no beans.

Let's consider the data from running the experiment 100000 times. The
probabilities of each case are:

1. No beans = **10.3%**
  
2. One bean = **33.8%**
  
3. Two beans of the same color = **28.8%**
  
4. One red and one green = **27.1%**
