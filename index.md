---
title       : Exploding 10s
subtitle    : 
author      : Jesse Peterson-Brandt
job         : 
framework   : io2012       # {io2012, html5slides, shower, dzslides, ...}
logo        : 7thSeaLogo.png
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- 

## The Exploding 10s System

Exploding tens is a dice system for the 7th Sea role playing game used to simulate randomness
in trying to complete a task and in combat. The system uses ten-sided dice with numbers 1-10. 
A player rolls a total number of dice and keeps a subset of the results, selecting the highest 
and adding them for a total. This total is compared to a set difficulty level to determine 
success or failure.

The name "Exploding Tens" comes from the result of a player rolling a 10. Whenever this 
happens, the player rolls that die again and adds it to the total while keeping the original 10. 
So if a player rolled 5 keep 3 and got 2, 10, 9, 7, 6, and rerolled the 10 for a 5, she would add
the 10, 9, 7 and the extra 5 for a total of 31. Of course, the extra roll might also result in 
a 10 which in turn "explodes" meaning a single die can add a lot to the total.

For more on 7th Sea and the exploding tens dice system, visit <a href="http://www.alderac.com/7thsea/">Alderac Entertainment</a>.

---  .class #id

## Kept Dice

A roll is referred to as "X keep Y", e.g. 4 keep 2 means roll 4 dice, keep the highest
two.


```r
roll <- sample(1:10, 4, replace = TRUE)
roll
```

```
## [1] 9 6 1 8
```

```r
keepers <- sort(roll, decreasing = TRUE)[1:2]
sum(keepers)
```

```
## [1] 17
```

--- 

## Exploding

Example code below. Let's say a player rolled three 10s on a particular roll (lucky player). This
code rolls the extra dice and caches the rolls as well as the totals.

```r
y = list()
z = 0

for(i in 1:3) {
      x <- 10
      while(x[1] == 10) {
        x[length(x)+1] <- x[1]  ##Move 10 to end of x vector
        x[1] <- sample(1:10, 1, replace = TRUE) ##New d10 roll
      }
      y[[i]] <- x ##save as element of a list
      z[i] <- sum(x) ##save sum in a vector
    }
```

---

## Adding It Up


```r
z
```

```
## [1] 16 18 18
```
Continuing with the numbers from the previous page, let's say the player was rolling 6 keep 4.
Then we would keep the three tens above and the highest remaining roll. If the roll matches
or exceeds the difficulty, the attempt is a success.


```r
roll2 <- sample(1:10, 3, replace=TRUE)
roll2
```

```
## [1] 1 8 9
```

```r
sum(z, max(roll2))
```

```
## [1] 61
```
