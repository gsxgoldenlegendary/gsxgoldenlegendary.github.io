---
title: String
date: 2021-12-28 16:02:43
tags: Data Structure
categories: Computer Science
mathjax: true
---

串ADT的逻辑结构、存储结构及基本操作：

<!--more-->

# 逻辑结构

ADT String{

数据对象：
$$
D=\{a_i|a_i\in ElemSet,i=1,2,\cdots,n,n\geqslant 0\}
$$


数据关系：
$$
R1=\{<a_{i-1},a_i>|a_i-1,a_1\in D,i=1,2,\cdots,n\}
$$
基本操作：

```c
StrAssign(&T,chars);
StrCopy(&T,S);
StrEmpty(S);
StrCompare(S,T);
StrLength(S);
ClearString(&S);
Concat(&T,S1,S2);
SubString(&Sub,S,pos,len);
Index(S,T,pos);
Repalce(&S,T,V);
StrInsert(&S,pos,T);
StrDelete(&S,pos,len);
DestroyString(&S);
```

}ADT String

# 存储结构

## 定长顺序存储表示

```c
#define MAXSTRLEN 255
typedef unsigned char SString[MAXSTRLEN+1];
```

## 堆分配存储表示

```c
typedef struct {
    char *ch;	//若非空，按长度分配，否则为NULL
    int length	//串的长度
}HString;
```

## 块链存储表示

```c
#define CHUNKSIZE 80
typedef struct Chunk{
    char ch[CHUNKSIZE];
    struct Chunk* next;
}Chunk;
typedef struct{
    Chunk* head;
    Chunk* tail;
    int curlen;
}LString;
```

# 基本操作

## 定长顺序存储表示

### 在内存中的表示

```c
#define MAX_STRLEN 256
typedef struct {
    char str[MAX_STRLEN];
    int length;
}StringType;
```

### 将一个串拼接在另一个串后

```c
Status StrConcat(StringType &S,StringType T){
    if(S.length+T.length>MAX_STRLEN)
        return ERROR;
    for(i=0;i<T.length;++i)
        S.ch[i+S.length]=T.ch[i];
    S.length+=T.length;
    return OK;
}//StrConcat
```

### 求主串给定起点和长度的子串

```c
Status SubString(StringType &S,int pos,int len,StringType &sub){
    if(pos<0||pos>=S.length||len<0||len>S.length-pos)
        return ERROR;
    for(i=pos;i<pos+len;++i)
        sub.ch[i-pos]=S.ch[i];
    sub.length=len;
    return OK;
}//SubString
```

## 堆分配存储表示

### 连接

```c
Status StrConcat(HString &T, HString S1,HString S2){
    if(T.ch)
        free(T.ch);
    T.ch=(char*)malloc((S1.length+S2.length)*sizeof(char));
    if(!T.ch)
        exit(OVERFLOW);
    for(i=0;i<S1.length;++i)
        T.ch[i]=S1.ch[i];
    for(i=S1.length;i<S1.length+S2.length;++i)
        T.ch[i]=S2.ch[i-S1.length];
    return OK;
}//StrConcat
```

