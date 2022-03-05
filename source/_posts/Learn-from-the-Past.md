---
title: Learn from the Past
date: 2021-12-12 19:58:18
tags: Computing System
categories: Computer Science 
---

# Learn from the Past

Experiment Report to ICS Lab6.

<!--more-->

## Task

The last lab might be the simplest one. Use a high-level programming language (e. g. C, Python, C++) to implement all the code that has been written before. The algorithm needs to be consistent with what was used before, e. g. a replication of the first experiment cannot be implemented with just one line of multiplication.

## Q&A

### Q1: How to evaluate the performance of my own high-level language programs?

There are 2 efficient methods to evaluate the performance of programmes. They are called time complexity and space complexity. Each of them can be measured sketchily or precisely. To measure time performance, I can get the commencing and the termination time of the programme, then get how long it takes to complete execution of the programme. But it is a rough result. To get precise result of how many clock cycle it takes, A significant method is assemble high level language into assembly. Then precise clock cycles can be measured. As for space performance, It is similar to the time one, which is roughly estimating with high level language itself or precisely calculating by assembly. 

### Q2: Why is a high-level language easier to write than LC3 assembly?

As is known to all, high level language has portability, which LC-3 assembly does not. In addition,  grammar of high level language is user-friendly, but assembly is machine-friendly. Without brace(C like language) or indent(Python), the structure of the programme is unclear in assembly, especially when reading others' programmes or debugging. With no type of variables, I can only operate storage of different type of variables inefficiently.   

### Q3: What instructions do I think need to be added to LC3? (I can think about the previous experiments and what instructions could be added to greatly simplify the previous programming)

I think that everyone using LC-3 wants to add a right-shift instruction. If there is no right-shift instruction, division is very difficult to operate. Cycling minus? Sequentially multiply? Maybe both are not a good method. Furthermore, a right-shift is easy to realised in fundamental circuit. With a bit-splice operator in Verilog HDL, Nexy4-DDR development board can do it.

### Q4: Is there anything I need to learn from LC3 for the high-level language I use?

Yes, a lot of things. After learning the process of assembling, some basic regulation of high level language is easer to represent. Additionally. I learned that some basic operations are slow and some are quick in realisation, but they are the same easy to write in a high level language. Due to high level language is developing from assembly and machine language, we should have learned low level language first. What a pity!👻

## Gains

No pains, no gains!

Thanks for Prof. Zhang and all TAs from the bottom of my heart.
