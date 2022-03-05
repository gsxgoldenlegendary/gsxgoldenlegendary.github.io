---
title: Assembler
date: 2021-12-12 10:54:43
tags: Computing System
categories: Computer Science
---

# Assembler

Experiment Report to ICS labA.

<!--more-->

## Tasks

1. learn how to use Makefile.
2. read the code, understand the framework of the program, and train the ability to read the program.
3. replace all `TO BE DONE` in the code with the correct code.

## Process

I tried use only vim to edit the code, but when the file is too long , efficiency went down. So I use CLion in Windows to edit the code, then use Ubuntu run the programme.

I read the codes line by line, and complete all `TO BE DONE` one by one. Because the code is very clear and understandable, there were not many problems in this stage. But most time used in debugging.😂 

## Debugging

I will write almost all bugs I met as follows. 

1. Originally, I misunderstood some codes about labels, so when meeting labels, the line was not printed in output file. Then I set the line with label `lOperation` and the problem diminished.
2. When almost all being done, I recognised that some 16-base number was mixed in 2-base numbers. Then I found that something was wrong in `ConvertBin2Hex` function. Using `DecToChar` function, the bug was fixed.
3. When I finished debugging in CLion, I made the programme in Ubuntu, but an error occurred. It is because I used `_atoi` function, but it isn't admitted in g++ compiler. So I write a function to replace the library function.

## Gains

1. Through this lab, I learned how to process command parameters, and how to set debug mode by TA's marvellous codes.👍
2. After finishing the assembler, I understand assembly language more deeply, and have known how it is converted to machine language.
3. Actually, I haven't use command to compile and run a single C++ programme. Thanks to this lab, I learned to do so.
4. I used almost 6 hours to complete the lab. No pains, no gains!
