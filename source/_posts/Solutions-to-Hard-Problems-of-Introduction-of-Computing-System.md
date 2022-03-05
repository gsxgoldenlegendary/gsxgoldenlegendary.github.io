---
title: Solutions to Hard Problems of Introduction to Computing System
date: 2021-10-31 14:42:50
tags: Computing System
categories: Computer Science
mathjax: true
---

# Solutions to Hard Problems of Introduction to Computing System

In this page, I collect some hard problems of ICS homework in English, because the textbook, homework, and examination are all in English.

<!--more-->

## Floating Point Data Type

Problem: 

Convert the following floating point representation to its decimal equivalent:$$1 10000010 10101001100000000000000$$

Solution:

The 1 at 32nd bit means it is a negative number.

The 31 to 23 bits represent exponent, which should be abstracted by 8'd127, so the exponent is 4.

The last 23 bits represent fraction in binary and integer part of the fraction is 1.

So, 1 10000010 10101001100000000000000 means $(-(1.101010011)\times10^{10000010-01111111})_B=$

### $(-(2^0+2^{-1}+2^{-3}+2^{-5}+2^{-8}+2^{-9})\times2^3)_D=(-13.296875)_D$. 

## Hexadecimal Notation

Problem:

Change $675.625$ in the IEEE 754 floating point standard.

Solution:

$$675.625=2\times16^2+10\times16+3+10\times16^{-1}=(2A3.A)_H=(2.A3A\times10^2)_H$$$$=(1.0101000111010\times10^9)_B=0 10001000 010100011101000000000000=4428E800.$$

Notice: the exponent needs adding to 8'd127.

## Combinational Logic Circuits

Problem:

Logic circuit 1 in Figure 3.39 (page 102 of the book) has inputs A, B, C.  Logic circuit 2 in Figure 3.40 (page 102 of the book) has inputs A and B.  Both logic circuits have an output D. There is a fundamental difference  between the behavioural characteristics of these two circuits. What is  it? Hint: What happens when the voltage at input A goes from 0 to 1 in  both circuits?

Solution:

Figure 3.39 is a 2-input mux, which combinational logic D is the output of the circuit.

 Figure 3.40 is a storage element, which stores the data value previously stored in the latch.

To be continued.
