---
title: Reveal Yourself
date: 2021-12-12 10:55:57
tags: Computing System
categories: Computer Science
mathjax: true
---

# Reveal  Yourself

Experiment Report to ICS Lab4.

<!--more-->

## Tasks

I ever met such a situation that your disk is broken and data is lost.

OK, in this lab, my task is to find out the missing bit in a program.

### task 1

In the first part, 4 bits in the code are missing. I need to find out the missing bits. Before the program starts, values in the registers(except PC) are 0. At the end of the program, the register status is as follow.

```
 R0 = 5, R1 = 0, R2 = 300f, R3 = 0
 R4 = 0, R5 = 0, R6 = 0, R7 = 3003
```

### task 2

The second part of the program is used to calculate the remainder. 15 bits int the code are missing. For 2,4,6,8 the remainder is easy to calculate, but for 7 the remainder needs some skills. Here is a quicker way to do the remainder for 7.

## Methods

### task1

1. The 1st x is easy to guess. If it is 0, the line is useless. So it is 1.
2. The 2nd x can be also guessed. The line used to add 1 into R2, so It is 0.
3. The 3rd x is easy to guess, too. In the programme, R1 is used, but R5 is not used. So it is 0.
4. The last x is easy to guess as well. If it is 1, the opcode is `LDR` , to load data in R2 into R7 , and a `RET` is in the next line, so it is 1.

### task2

1. The 4~6th x's are all 1, because if some of them are 0's, the programme will go to where before `x3000`,as is wrong.

2. The 3rd and 9th x's are 1, because of language grammar.

3. Other x's is hard to guess, but through read throughout and understand the programme,  I know that the core of the programme is used the following equation:

   $$
   8k+m\equiv k+m(\mod 7).
   $$

   And the main part of the programme is used to check whether k+m is less than 7, and put it into R1; the branch of the programme is used to get k by dividing R1 by 8. So the 10~12nd x's are 011 representing R3, used to multiply R3 2 times, and the last 3 x's are 100, to cycle branch whether R3 is left-overflowed.

4. Going Back to main part, we can see that there are also 2 groups of x's. The 1st and 2nd x's are 01, used to check whether to call branch. The 7th and 8th x's are also 01, used to check whether to minus 7 from R1, by checking R0, which stores R1-7, whether is larger than 7 or not, or not. (just 2 'or not' 's✌️)

## Gains

1. The machine language codes given have no comments, so it is hard to be read by other programmers. I learned the importance of writing comments for codes.
2. No pains, no gains!
