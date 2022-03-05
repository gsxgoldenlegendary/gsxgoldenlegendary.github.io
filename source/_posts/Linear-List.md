---
title: Linear List
date: 2021-12-28 16:00:18
tags: Data Structure 
categories: Computer Science
mathjax: true
---

线性表ADT的逻辑结构、存储结构及基本操作：

<!--more-->

# 逻辑结构

ADT List{

数据对象：
$$
D=\{a_i|a_i\in ElemSet,i=1,2,\cdots,n,n\geqslant0\}
$$
数据关系：
$$
R1=\{<a_{i-1},a_i>|a_{i-1},a_i\in D,i=1,2,\cdots,n\}
$$
基本操作：

```c
InitList(&L);
DestroyList(&L);
ClearList(&L);
ListEmpty(L);
ListLength(L);
GetElem(L,i,&e);
LocateElem(L,e,compare());
PriorElem(L,cur_e,&pre_e);
NextElem(L,cur_e,&next_e);
ListInsert(&L,i,e);
ListDelete(&L,i,&e);
ListTraverse(L,visit());
```

}ADT List

# 存储结构

## 线性表的动态分配顺序存储结构

```c
#define LIST_INIT_SIZE 100
#define LISTINCREMENT 10
typedef struct{
    ElemType* elem;
    int length;
    int listsize;
}SqList;
```

## 线性表的单链表存储结构

```c
typedef struct LNode{
    ElemType data;
    struct LNode* next;
}LNode,*LinkList;
```

## 线性表的静态单链表存储结构

```c
#define MAXSIZE 1000
typedef struct{
    ElemType data;
    int cur;
}component,SLinkList[MAXSIZE];
```

## 线性表的双向链表存储结构

```c
typedef struct DuLNode{
    ElemType data;
    struct DuLNode* prior;
    struct DuLNode* next;
}DuLNode,*DuLinkList;
```

# 基本操作

## 顺序表

### 数据对象与数据关系的实现

```c
#define LIST_INIT_SIZE 100	//线性表存储空间的初始分配量
#define LISTINCREMENT 10	//存储空间分配增量
typedef struct {
    ElemType *elem;			//存储空间基址
    int length;			    //当前元素个数（表长）
    int listsize;			//当前分配存储容量
    					   //以sizeof(ElemType)为单位
} SqList;
```

### 初始化线性表

```c
void InitSqList(SqList&L){
    //从无到有，在内存中创造出一个线性表
    L=(ElemType*)malloc(LIST_INIT_SIZE*sizeof(ElemType));
    if(!L)
        exit(OVERFLOW);
    L.length=0;
    L.listsize=LIST_INIT_SIZE;
}//InitSqList
```

### 按值查找

```c
int LocateElem(SqList L,ElemType x,equal){
    //在顺序表中从头查找结点值等于给定值x的结点
    //返回结点的位置
    for(i=0;i<L.length&&*(L.elem+i-1)!=x;++i){}
    return i<L.length?i+1:0;
}//LocateElem
```

### 求表的长度

```c
int ListLength(SqList L){
    //返回表的长度
    return L.length;
}//ListLength
```

### 提取函数

```c
Status GetElem(SqList L,int i,ElemType &e){
    //在表中提取第i个元素的值
    if(i<=0||i>L.length)
        return ERROR;
    e=L.elem[i-1];
    return OK;
}//GetElem
```

### 插入元素

```c
Status ListInsert_Sq(SqList L,int i,ElemType e){
    //在表L中第i个位置前插入新元素e
    //时间复杂度O(n)
    if(i<1||i>L.length)
        return ERROR;
    if(L.length>=L.listsize){
        newbase=(ElemType*)realloc((L.listsize+LISTINCREMENT)*sizeof(ElemType));
        if(!newbase)
            return OVERFLOW;
        L.elem=newbase;
        L.listsize+=LISTINCREMENT;
    }//if
    q=L.elem+i-1;
    for(p=L.elem+L.length-1;p>=q;--p)
        *(p+1)=*p;
    *q=e;
    ++L.length;
    return OK;
}//ListInsert_Sq
```

### 删除元素

```c
Status ListDelete_Sq(SqList &L,int i,ElemType &e){
    //在表L中删除第i个元素，并用e返回其值
    //时间复杂度O(n)
    if(i<1||i>L.length)return ERROR;
    p=L.elem+i-1;
    e=*p;
    for(q=L.elem+L.length-1;p<=q;++p)
        *p=*(p+1);
    --L.length;
    return OK;
}//ListDelete_Sq
```

### 集合的并

```c
void Union(SqList &La,SqList Lb){
    //时间复杂度O(La.Length+Lb.length)
    //空间复杂度O(1)
    n=ListLength(La);
    m=ListLength(Lb);
    for(i=0;i<m;i++){
        GetElem(Lb,i,e);
        if(LocateElem(La,e,equal))
            ListInsert_Sq(La,++n,e);
    }//for
}//Union
```

### 集合相减

```c
void Intersection(SqList &La,SqList Lb){
    //时间复杂度O(La.Length+Lb.length)
    //空间复杂度O(1)
    n=ListLength(La);
    m=ListLength(Lb);
    for(i=0;i<m;++i){
        GetElem(Lb,i,e);
        if(x=LocateElem(La,e,equal))
            ListDelete_Sq(La,x,e);
    }//for
}//Intersection
```

### 有序表的归并

```c
void MergeList_Sq(SqList La,SqList,Lb,SqLIst &Lc){
    //两个有序表拼成更大的有序表
    //时间复杂度O(La.length+Lb.length)
    //空间复杂度O(La.length+Lb.length)
    pa=La.elem;
    pb=Lb.elem;
    pc=(ElemType*)malloc((La.length+Lb.length)*sizeof(ElemType));
    if(!pc)
        exit(OVERFLOW);
    Lc.elem=pc;
    Lc.listsize=La.length+Lb.length;
    Lc.length=Lc.listsize;
    pa_last=La.elem+La.length;
    pb_last=Lb.elem+Lb.length;
    for(;pa<pa_last&&pb<pb_last;)
        if(*pa<*pb)
            *pc++=*pa++;
    	else
        	*pc++=*pb++;
    for(;pa<pa_last;)
        *pc++=*pa++;
    for(;pb<pb_last;)
        *pc++=*pb++;
}//MergeList_Sq
```

## 单链表

### 单链表的数据对象和数据关系的实现

```c
typedef struct Lnode {	//链表结点
    ElemType data;	    //结点数据域
    struct Lnode *next;	//结点链域
} ListNode, *LinkList;
```

### 取第i个元素

```c
Status GetElem_L(LinkList L,int i, ElemType &e){
    //参数：链表L、位置i、取得的第i个元素e
    //算法：带头结点的单链表中取第i个元素
    p=L;
    for(j=1;j<i&&p;++j)
        p=p->next;
    if(!p)
        return ERROR;
    e=p->data;
    return OK;
}//GetElem_L
```

### 插入操作

```c
Status ListInsert(LinkList &L,int i,ElemType e){
    p=L;
    for(j=0;j<i-1&&p;++j)
        p=p->next;
    if(!p)
        return ERROR;
    s=(ElemType*)malloc()
}//ListInsert
```

## 循环链表

### 双向循环链表的数据对象和数据关系的实现

```c
typedef int ListData;
typedef struct dnode {
    ListData data;
    struct dnode *prior, *next;
}DblNode,*DblList;
```

