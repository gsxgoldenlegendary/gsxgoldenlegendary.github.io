---
title: Array and Generalized List
date: 2021-12-28 16:03:31
tags: Data Structure
categories: Computer Science
mathjax: true
---

数组和广义表的逻辑结构、存储结构及基本操作：

<!--more-->

# 逻辑结构

## 数组

ADT Array{

数据对象：
$$
j_i=0,\cdots,b_i-1,i=1,2,\cdots,n.
$$

$$
D=\{a_{j_1j_2\cdots j_n}|n(n>0),a_{j_1j_2\cdots j_n}\in ElemSet\}
$$

$n$称为数组的维数，$b_i$是数组第$i$维的长度，$j_i$是数组元素第$i$维下标。

数据关系：
$$
R=\{R1,R2,\cdots,Rn\}
$$

$$
R1=\{<a_{j_1\cdots j_i\cdots j_n},a_{j_1\cdots j_{i+1}\cdots j_n}>|0\leqslant j_k\leqslant b_k-1,i\leqslant k\leqslant n, 且k\neq i,0\leqslant j_i\leqslant b_i-2,a_{j_1\cdots j_i\cdots j_n},a_{j_1\cdots j_{i+1}\cdots j_n}\in D,i=2,\cdots,n\}
$$



基本操作：

```c
InitArray(&A,n,bound1,•••,boundn);
DestroyArray(&A);
Value(A,&e,index1,•••,indexn);
Assign(&A,e,index1,•••,indexn);
```

}ADT Array

## 广义表

ADT GList{

数据对象：
$$
D=\{e_i|i=1,2,\cdots,n;n\geqslant0;e_i\in AtomSet或e_i\in GList\}
$$
数据关系：
$$
R1=\{<e_{i-1},e_i>|e_{i-1},e_i\in D,2\leqslant i\leqslant n\}
$$
基本操作：

```c
InitGList(&L);
CreateGList(&L,S);
DestroyGList(&L);
CopyGList(&T,L);
GListLength(L);
GListDepth(L);
GListEmpty(L);
GetHead(L);
GetTail(L);
InsertFirst_GL(&L,e);
DeleteFirst_GL(&L,&e);
Traverse_GL(L,Visit());
```

}ADT GList

# 存储结构

## 数组

### 数组的顺序存储表示

```C
#include<stdarg.h>
#define MAX_ARRAY_DIM 8
typedef struct{
    ElemType*base;
    int dim;
    int*bounds;
    int*constants;
}Array;
```

### 稀疏矩阵的三元顺序表存储表示

```c
#define MAXSIZE 12500
typedef struct{
    int i,j;				//非零元的行下标和列下标
    ElemType e;
}Triple;
typedef struct{
    Triple data[MAXSIZE+1];	 //非零元三元组表，以行序为主序
    int mn,nu,tu;			//矩阵的行数、列数、非零元个数
}TSMatrix;
```

### 稀疏矩阵的行逻辑链接的顺序表存储表示

```c
#define MAXSIZE 12500
typedef struct{
    int i,j;				
    ElemType e;
}Triple;
typedef struct{
    Triple data[MAXSIZE+1];   
    int rpos[MAXRC+1];       
    int mu,nu,tu;
}RLSMatrix;
```

### 稀疏矩阵的十字链表存储表示

```c
typedef struct OLNode{
    int i,j;					//行号和列号
    ElemType e;					//元素值
    struct OLNode*right,*down;	 
}OLNode,*OLink;					//非零元素结点
typedef struct{
    OLink*rhead,chead;
    int mu,nu,tu;				//行数、列数、非零元个数
}CrossList;
```

## 广义表

### 广义表的头尾链表存储表示

```c
typedef enum{
    ATOM,
    LIST
}ElemTag;
typedef struct GLNode{
    ElemTag tag;
    union{
        AtomType atom;
        struct{
            struct GLNode *hp,*tpl
        }ptr;
    };
}*GList;
```

### 广义表的扩展线性链表存储表示

```c
typedef enum{
    ATOM,
    LIST
}ElemTag;
typedef struct GLNode{
    ElemTag tag;
    union{
        AtomType atom;
        struct GLNode *hp;
    };
    struct GLNode *tp;
}*GList;
```

# 基本操作

## 数组

### 数组的顺序存储表示

#### 初始化

```c
Status InitArray(Array &A,int dim,...){
    A.dim=dim;
    A.bounds=(int*)malloc(dim*sizeof(int));
    elemtotal=1;
    va_start(ap,dim);
    for(i=0;i<dim;++i){
        A.bounds[i]=va_arg(ap,int);
        elemtotal*=A.bounds[i];
    }//for
    var_end(ap);
    A.base=(ElemType*)malloc(elemtotal*sizeof(ElemType));
    A.constants=(int*)malloc(dim*sizeof(int));
    A.constant[dim-1]=1;
    for(i=dim-1;i>=0;--i)
        A.constants[i]=A.bounds[i+1]*A.constants[i+1];
    return OK;
}//InitArray
```

#### 映像函数

```c
Status Locate(Array A,va_list ap,int &off){
    off=0;
    for(0;i<A.dim;++i){
        ind=va_arg(ap,int);
        off+=A.constants[i]*ind;
    }//for
}//Locate
```

## 矩阵

### 稀疏矩阵的三元顺序表存储表示

#### 转置

```c
void TransMatrix(TSMatrix a,TSMatrix &b){
    //时间复杂度O(a.nu*a.tu)
    {b.mu,b.nu,b.tu}={a.nu,a.mu,a.tu};
   if(b.tu){
    q=0;
    for(col=1;col<a.nu;++col)
        for(p=0;p<a.tu;++p)
            if(a.data[p].col==col){
                b.data[q].i=a.data[p].j;
                b.data[q].j=a.data[p].i;
                b.data[q].value=a.data[p].value;
                ++q;
            }//if
   }//if
}//TransMatrix
```

#### 快速转置

```c
Status FastTransMatrix(TSMatrix a,TSMatrix &b){
    //时间复杂度O(a.nu+a.tu)
    {b.mu,b.nu,b.tu}={a.nu,a.mu,a.tu};
    if(b.tu){
        for(col=0;col<a.nu;++col)
            num[col]=0;
        for(t=0;t<a.tu;++t)
            ++num[a.data[t].col];
        cpot[0]=0;
        for(col=1;col<a.nu,++col)
            cpot[col]=cpot[col-1]+cum[col-1];
        for(p=0;p<a.tu;++p){
            col=a.data[p].j;
            q=cpot[col];
            b.data[q].i=a.data[p].j;
            b.data[q].j=a.data[p].i;
            b.data[q].value=a.data.value;
            ++cpot[col];
        }//for
    }//if
}//TastTransMatrix
```

