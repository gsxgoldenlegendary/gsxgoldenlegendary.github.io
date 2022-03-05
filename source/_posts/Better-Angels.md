---
title: Better Angels
date: 2021-12-15 16:30:34
tags: Computing System
categories: Computer Science
mathjax: true
---

# Better Angels

Experiment Report for ICS lab3: 

<!--more-->

## Task

### task 1

Read and understand In lab 3, I will get a piece of machine code in 'foo.txt'. My first task is to translate machine code into assembly code. Store my program in 'translate.txt'. 

### task 2

Guess This code is some other's program in lab2. Guess the owner of the program by the last 4 lines of the program. Write down the owner's student id in 'id.txt'. 

### task 3

Optimize The code in lab2 is a L-version program. Of course it's performance is not very well. In this part, I need to optimize other's program. (Rewriting is also a legitimate optimization method) Store the optimized code in 'optimized.txt'.

## Process

### read

I read the code line by line, and translate it into assembly. Because machine language is very similar to assembly, there was not much programme.

### guess

I wrote a C++ programme to calculate the ID of the owner of the codes. Codes are as follows.

```C++
#include<iostream>

int F[100];

int main(){
	F[0]=1;
	F[1]=1;
	F[2]=2;
	for(int i=3;i<100;++i){
		F[i]=(F[i-1]+2*F[i-3])%1024;
		if(F[i]==486)
			std::cout<<i;
	}
	return 0;
}
```

### optimise

I optimise the code by changing fundamental structure. I wrote a C++ programme to write the codes. The programme is as follows.

```C++
#include<fstream>

int F[15001];
int main(){
	F[0]=1;
	F[1]=1;
	F[2]=2;
	std::ofstream file_writer("opt.txt");
	file_writer<<".ORIG x3000\nLEA R1,#0\nADD R2,R0,R1\nLDR R7,R2,#3\nTRAP x25\n"; 
	for(int i=0;i<15000;i++){
		if(i>2)
			F[i]=(F[i-1]+2*F[i-3])%1024;
		file_writer<<".FILL #"<<F[i]<<std::endl;
	}
	file_writer<<".END";
	file_writer.close();
	return 0;
}
```

 According to Prof. Zhang, a 15% performance optimising can be called a "splendid advance". The programme I got used 46506 instructions on average(tested in LIU Liangyu(PB20000180)'s LC-3 web). And my optimised programme used 3 instructions in all cases. Using the formula
$$
3=46506\times(1-15\%)^n,
$$
 So I have completed 59 "splendid advance"s at least. 

## Gains

It is difficult for a man to read machine language. So I can understand why advanced languages are invented.

No pains, no gains!
