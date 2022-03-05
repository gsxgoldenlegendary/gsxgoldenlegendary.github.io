---
title: Riddle
date: 2021-12-12 10:54:52
tags: Computing System
categories: Computer Science
mathjax: true
---

# Riddle

Experiment Report to ICS Lab5

<!--more-->

## Task

For this experiment I need to functionally reproduce a c++ programs. Program A:

```
 int judge(int r0) {
     int i = 2;
     r1 = 1;
     while (i * i <= r0) {
         if (r0 % i == 0) {
             r1 = 0;
             break;
             }
         i++;
         }
     return r1;
 }
```

My program should follow a specific framework:

```
 .ORIG x3000
 ... ; TO BE DONE
 HALT
 JUDGE ... ; TO BE DONE
 ... ; TO BE DONE
 RET
 ... ; TO BE DONE
 .END
 
```

r0(an integer, ) is given before program executes(just like lab1), and store the final result in r1. (no need to print out with TRAP)

## Methods

There are two significant parts of the assembly programme:

1. `i*i` was realized by what was used in lab1l. If I wanted to get a faster one, I can use what was used in lab1p.
2. `r0%i` was realized by subtracting `r0` until it turned not positive. Because I just needed to know whether it is zero or not, this simple function is OK. 

## Debugging

With last 4 labs, I can write assembly codes more efficiently, so I just met one bug.

1. When I wrote

   ```
    BREAK AND R1,R1,#0
   ```

   , I carelessly made `R1` `R2`. So a bug appeared. I used `step over` in LC-3 tools and found it finally.

## Gains

1. When I saw the C code, I think the programme was very easy. But as I translated it into assembly, it was more complex than I thought. I can feel advantage of advanced programming language over assembly Also, I knew how a C programme executive, of which I was confused in my fresh year.
2. Mo pains, no gains!
