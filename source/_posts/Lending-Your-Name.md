---
title: Lending Your Name
date: 2021-11-30 08:30:35
tags: Computing System
categories: Computer Science
mathjax: true
---

# Experiment Report of Lab2: Lending Your Name

From this lab, Prof. An ask TA to write guide in English, so I also try to write report in English.

<!--more-->

## Task

**In lab 2, the task is very simple.** Store the n-th number of a sequence into register R7. As the Fibonacci sequence grows quite rapidly, we made a little difference with the origin Fibonacci sequence: 
$$
F(0) = 1;\\
F(1) = 1;\\
F(2) = 2;\\
F(n) = F(n-1) + 2F(n-3) (\mod 1024) (1 \leqslant n \leqslant 16384)
$$
Divide my student number into four equal segments, labelling them with a, b, c and d. For example, my student ID is PB20111712, so a = 20, b = 11, c = 17, d=12. Store value of F(a), F(b), F(c) and F(d) at the end of your code with '.FILL' pseudo command.

## Method

1. If n is less than 3, the value can be gotten directly
2. When n is more than 2, I should use .recursion to get $F(n)$. I used two other registers to store $2F(n-3)$ and $F(n)$. 
   CAUTION: $F(n)$ may larger than 1024, but it cannot larger than 3072, which is 3 times of 1024. 
3. So I subtract 3072 from $F(n)$, and than add 1024 into it, until it is positive.
   CAUTION: Both 1024 and 3072 are larger than  what can be represented by a 5-bit immediate number, so they should be stored by '.FILL' instruction.
4. In every cycle, I subtract 1 from n, which is not negative. When n is negative, the $F(n)$ is gotten, then store it into register R7, and the programme finishes.

##  Gains

1. The first L-version took 32 lines, and the last one 30. I optimised the programme by firstly stored $F(0),F(1),F(2)$ all in R3.
2. No pains,no gains!

## Codes

```assembly
.ORIG x3000
ADD R3,R3,#1
ADD R0,R0,#-1
BRn LABLE2
ADD R1,R3,#0
ADD R0,R0,#-1
BRn LABLE2
ADD R2,R3,#0
ADD R3,R3,#1
ADD R0,R0,#-1
BRn LABLE2
LABLE4 ADD R4,R1,R1
ADD R4,R4,R3
LD R5,NUMBER1
LD R6,NUMBER0
ADD R4,R4,R6
LABLE3 ADD R4,R4,R5
BRn LABLE3
ADD R1,R2,#0
ADD R2,R3,#0
ADD R3,R4,#0
ADD R0,R0,#-1
BRzp LABLE4
BRn LABLE2
LABLE2 ADD R7,R3,#0
NUMBER0 .FILL #-3072
NUMBER1 .FILL #1024
Fa .FILL #930
Fb .FILL #246
Fc .FILL #742
Fd .FILL #418
.END
```



