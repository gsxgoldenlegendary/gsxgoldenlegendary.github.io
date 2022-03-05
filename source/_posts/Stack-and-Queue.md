---
title: Stack and Queue
date: 2021-12-28 16:02:25
tags: Data Structure
categories: Computer Science
mathjax: tr
---

栈和队列ADT的逻辑结构、存储结构及基本操作：

<!--more-->

# 逻辑结构

## 栈

ADT Stack{

数据对象：
$$
D=\{a_i|a_i\in ElemSet,i=1,2,\cdots,n,n\geqslant 0\}
$$


数据关系：
$$
R1=\{<a_{i-1},a_i>|a_i-1,a_1\in D,i=1,2,\cdots,n\}
$$
约定$a_n$端为栈顶，$a_i$端为栈底。

基本操作：

```c
InitStack(&S);
DestroyStack(&S);
ClearStack(&S);
StackEmpty(S);
StackLength(S);
GetTop(S,&e);
Push(&S,e);
Pop(&S,&e);
StackTraverse(S,visit());
```

}ADT Stack

## 队列

ADT Queue{

数据对象：
$$
D=\{a_i|a_i\in ElemSet,i=1,2,\cdots,n,n\geqslant 0\}
$$


数据关系：
$$
R1=\{<a_{i-1},a_i>|a_i-1,a_1\in D,i=1,2,\cdots,n\}
$$
约定$a_1$端为队列头，$a_n$端为d队列尾。

基本操作：

```c
InitQueue(&Q);
DestroyQueue(&Q);
ClearQueue(&Q);
QueueEmpty(Q);
QueueLength(Q);
GetHead(Q,&e);
EnQueue(&Q,e);
DeQueue(&Q,&e);
QueueTranverse(Q,visit());
```

}ADT Queue

# 存储结构

## 栈

### 栈的顺序存储表示

```c
#define STACK_INIT_SIZE 100;
#define STACKINCREMENT 10;
typedef struct{
    SElemType* base;
    SElemType* top;
    int stacksize;
}SqStack;
```

## 队列

### 单链队列——队列的链式存储结构

```c
typedef struct QNode{
    QElemType data;
    struct QNode* next;
}QNode,*QueuePtr;
typedef struct{
    QueuePtr front;
    QueuePtr rear;
}LinkQueue;
```

### 循环队列——队列的顺序存储结构

```c
#define MAXQSIZE 100
typedef struct{
    QElemType* base;
    int front;
    int rear;
}SqQueue;
```

# 基本操作

## 顺序栈

### 在内存中的表示

```c
#define STACK_INIT_SIZE 100
#define STACKINCREMENT 10
typedef char SElemType;
typedef struct {	//顺序栈的定义
    SElemType *base;//栈底指针
    SElemType *top; //栈顶指针
    int stacksize;	//当前已分配的存储空间
} SqStack;
```

### 初始化

```c
Status InitStack(SqStack &S){
    //置空栈
    S.base=(SElemType*)malloc(STACK_INIT_SIZE*sizeof(SElemType));
    if(!S.base)
        exit(OVERFLOW);
    S.top=S.base;
    S.stacksize=STACK_INIT_SIZE;
    return OK;
}
```

### 判定栈空

```c
Status StackEmpty(SqStack S){
    if(S.top==S.base)
        return TRUE;
    else
        return FALSE;
}//StackEmpty
```

### 取栈顶元素

```c
Status GetTop(SqStack S,SElemType &e){
    if(S.top==S.base)
        return ERROR;
    e=*(S.top-1);
    return OK;
}//GetTop
```

### 出栈

```c
Status Pop(SqStack &S，SElemType &e){
    if(S.top==S.base)
        return ERROR;
    e=*--S.top;
    return OK;
}//Pop
```

### 入栈

```c
Status Push(SqStack &S,SElemType e){
    if(S.top-S.base>=S.stacksize){
        newbase=(SElemType*)realloc((STACK_INIT_SIZE+STACKINCREMENT)*sizeof(SElemType));
        if!newbase)
            exit(OVERFLOW);
        S.base=newbase;
        S.top=S.base+S.stacksize;
        S.stacksize+=STACKINCREMENT;
    }//if
    *S.top++=e;
    return OK;
}//Push
```

## 链式栈

### 在内存中的表示

```c
typedef int StackData;
typedef struct node {
    StackData data;		//结点
    struct node *link;	//链指针
}StackNode;
typedef struct {
    StackNode *top;		//栈顶指针
}LinkStack;
```

### 初始化

```c
Status InitStack(LinkStack &S){
    S.top=NULL;
}//InitStack
```

### 入栈

```c
Status Push(LinkList &S,StackData e){
    StackNode*p=(StackData*)malloc(sizeof(StackData));
    if(!p)
        exit(OVERFLOW);
    p->data=e;
    p->link=S.top;
    S.top=p;
    return OK;
}//Push
```

### 判栈空

```c
Status StackEmpty(LinkStack S){
    return S.top==NULL;
}//LinkStack
```

### 取栈顶元素

```c
Status GetTop(LinkList S,SElemType &e){
    if(StackEmpty(S))
        return ERROR;
    e=S.top->data;
    return OK;
}//GetTop
```

### 出栈

```c
Status Pop(LinkStack &S.StackData &e){
    if(StackEmpty(S))
        return ERROR;
    e=S.top->data;
    temp=S.top;
    S.top=S.top->link;
    free(temp);
    return OK;
}//Pop
```

## 链队列

### 在内存中的表示

```c
typedef int QElemType;	//整数队列
typedef struct Qnode{
    QelemType data;		//队列结点数据
    struct Qnode *next;	//结点链指针
}Qnode,*QuenePtr;
typedef struct{
    QueuePtr rear,front;
}LinkQueue;
```

### 入队

```c
Status EnQueue(LinkQueue &Q,ElemType e){
    p=(QElemType*)malloc(sizeof(QElemType));
    if(!p)
        exit(OVERFLOW);
    p->data=e;
    p->next=NULL;
    Q.rear->next=p;
    Q.rear=p;
    return OK;
}//EnQueue
```

### 出队

```c
Status DeQueue(LinkQueue &Q,QElemType &e){
    if(Q.front==Q.rear)
        return ERROR;
    e=Q.front->next->next->dara;
    temp=Q.front->next->next;
    if(Q.rear==Q.front->next->next)
        Q.rear=Q.front->next;
    Q.front->next->next=Q.front->next->next->next;
    free(temp);
    return OK;
}//DeQueue
```

## 循环队列

### 在内存中的表示

```c
#define MAXSIZE 100
typedef struct{
    QElemType *base;
    int front;
    int rear;
}SqQueue;
```

### 初始化

```c
Status InitQueue(SqQueue &Q){
    Q.base=(QElemType*)malloc(MAXSIZE*sizeof(QElemType));
    if(!Q.base)
        exit(OVERFLOW);
    Q.rear=0;
    Q.front=0;
    return OK;
}//InitQueue
```

### 出队

```c
Status Dequeue(SqQueue &Q,QElemType &e){
    if(Q.rear==Q.front)
        return ERROR;
    e=Q.base[Q.front];
    Q.front=(Q.front+1)%MAXSIZE;
    return OK;
}//DeQueue
```

### 入队

```c
Status EnQueue(SqQueue &Q,QElemType e){
    if((Q.rear-Q.front)%MAXSIZE)==1)
        return ERROR;
    Q.base[Q.rear]=e;
    Q.rear=(Q.rear+1%MAXSIZE);
    return OK;
}//EnQueue
```

